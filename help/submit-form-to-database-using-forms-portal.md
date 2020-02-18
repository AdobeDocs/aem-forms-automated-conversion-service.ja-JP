---
title: フォームポータルを使用したアダプティブフォームのデータベースへの送信
description: デフォルトのメタモデルを拡張して、組織に固有のパターン、検証、エンティティを追加し、自動フォームコンバージョンサービスの実行中にアダプティブフォームフィールドに設定を適用します。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: 040b0ddb489b5bdfd640a93b22cd7bc512a39aea

---


# フォームポータルを使用したアダプティブフォームとデータベースの統合 {#submit-forms-to-database-using-forms-portal}

自動フォーム変換サービスを使用すると、非インタラクティブPDFフォーム、AcroフォームまたはXFAベースのPDFフォームをアダプティブフォームに変換できます。 変換処理を開始する際に、データ連結の有無に関わらずアダプティブフォームを生成するオプションがあります。

データ連結なしでアダプティブフォームを生成する場合は、変換後のアダプティブフォームを、変換後のフォームデータモデル、XMLスキーマ、またはJSONスキーマと統合できます。 ただし、データ連結を含むアダプティブフォームを生成する場合、変換サービスはアダプティブフォームをJSONスキーマに自動的に関連付け、アダプティブフォームとJSONスキーマで使用可能なフィールド間にデータ連結を作成します。 その後、アダプティブフォームを選択したデータベースと統合し、フォームにデータを入力し、フォームポータルを使用してデータベースに送信できます。

次の図は、フォームポータルを使用して、変換されたアダプティブフォームをデータベースと統合する様々な段階を示しています。

![データベース統合](assets/database_integration.gif)

この記事では、これらすべての統合ステージを正常に実行するための手順を説明します。

この記事で説明するサンプルは、フォームポータルページをデータベースと統合するための、カスタマイズされたデータサービスとメタデータサービスのリファレンス実装です。 サンプル実装で使用されるデータベースはMySQL 5.6.24です。ただし、フォームポータルページを任意のデータベースと統合できます。

## 前提条件 {#pre-requisites}

* 最新のAEM 6.5 Service packを含むAEM 6.5作成者インスタンス
* AEM Formsアドオンパッケージの最新バージョン
* [Automated Forms Conversionサービス](configure-service.md)
* 統合するデータベース。 サンプル実装で使用されるデータベースはMySQL 5.6.24です。ただし、フォームポータルを任意のデータベースと統合できます。

## AEMインスタンスとデータベース間の接続の設定 {#set-up-connection-aem-instance-database}

AEMインスタンスとMYSQLデータベース間の接続の設定は、次の要素で構成されます。

* [MYSQLコネクタパッケージのインストール](#install-mysql-connector-java-file)

* [データベースでのスキーマとテーブルの作成](#create-schema-and-tables-in-database)

* [接続設定の指定](#configure-connection-between-aem-instance-and-database)

* [フォームポータル統合用のサンプルパッケージの設定と設定](#set-up-and-configure-sample)

### mysql-connector-java-5.1.39-bin.jar ファイルのインストール {#install-mysql-connector-java-file}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、mysql-connector-java-5.1.39-bin.jar ファイルをインストールします。

1. Navigate to http://[server]:[port]/system/console/depfinder and search for com.mysql.jdbc package.
1. 「次による書き出し」列で、パッケージがバンドルで書き出されているかどうかを確認します。パッケージがバンドルで書き出されていない場合は、先に進みます。
1. Navigate to http://[server]:[port]/system/console/bundles and click **[!UICONTROL Install/Update]**.
1. Click **[!UICONTROL Choose File]** and browse to select the mysql-connector-java-5.1.39-bin.jar file. また、とチェックボッ **[!UICONTROL Start Bundle]** クスを選 **[!UICONTROL Refresh Packages]** 択します。
1. またはをク **[!UICONTROL Install]** リックしま **[!UICONTROL Update]**&#x200B;す。 完了したら、サーバーを再起動します。
1. （Windowsのみ）ご使用のオペレーティングシステムのシステムファイアウォールをオフにします。

### データベースでのスキーマとテーブルの作成 {#create-schema-and-tables-in-database}

次の手順を実行して、データベースにスキーマとテーブルを作成します。

1. 次のSQL文を使用して、データベースにスキーマを作成します。

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   formsportalは **** 、スキーマの名前を指します。

1. 次のSQL文を使 **用して** 、データベーススキーマにデータテーブルを作成します。

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 次のSQL文を使 **用して** 、データベーススキーマにメタデータテーブルを作成します。

   ```sql
   CREATE TABLE `metadata` (
       `formPath` varchar(1000) DEFAULT NULL,
       `formType` varchar(100) DEFAULT NULL,
       `description` text,
       `formName` varchar(255) DEFAULT NULL,
       `owner` varchar(255) DEFAULT NULL,
       `enableAnonymousSave` varchar(45) DEFAULT NULL,
       `renderPath` varchar(1000) DEFAULT NULL,
       `nodeType` varchar(45) DEFAULT NULL,
       `charset` varchar(45) DEFAULT NULL,
       `userdataID` varchar(45) DEFAULT NULL,
       `status` varchar(45) DEFAULT NULL,
       `formmodel` varchar(45) DEFAULT NULL,
       `markedForDeletion` varchar(45) DEFAULT NULL,
       `showDorClass` varchar(255) DEFAULT NULL,
       `sling:resourceType` varchar(1000) DEFAULT NULL,
       `attachmentList` longtext,
       `draftID` varchar(45) DEFAULT NULL,
       `submitID` varchar(45) DEFAULT NULL,
       `id` varchar(60) NOT NULL,
       `profile` varchar(255) DEFAULT NULL,
       `submitUrl` varchar(1000) DEFAULT NULL,
       `xdpRef` varchar(1000) DEFAULT NULL,
       `agreementId` varchar(255) DEFAULT NULL,
       `nextSigners` varchar(255) DEFAULT NULL,
       `eSignStatus` varchar(45) DEFAULT NULL,
       `pendingSignID` varchar(45) DEFAULT NULL,
       `agreementDataId` varchar(255) DEFAULT NULL,
       `enablePortalSubmit` varchar(45) DEFAULT NULL,
       `submitType` varchar(45) DEFAULT NULL,
       `dataType` varchar(45) DEFAULT NULL,
       `jcr:lastModified` varchar(45) DEFAULT NULL,
       PRIMARY KEY (`id`),
       UNIQUE KEY `ID_UNIQUE` (`id`)
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 次のSQL文を使 **用して** 、データベーススキーマに追加のmetadatatableテーブルを作成します。

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 次のSQL文を使 **用して** 、データベーススキーマにコメントテーブルテーブルを作成します。

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### AEMインスタンスとデータベース間の接続の設定 {#configure-connection-between-aem-instance-and-database}

次の設定手順を実行して、AEMインスタンスとMYSQLデータベース間の接続を作成します。

1. Go to AEM Web Console Configuration page at *http://[host]:[port]/system/console/configMgr*.
1. Click to open **[!UICONTROL Forms Portal Draft and Submission Configuration]** in edit mode.
1. 次の表の説明に従って、プロパティの値を指定します。

   <table> 
    <tbody> 
    <tr> 
    <th><strong>プロパティ</strong></th> 
    <th><strong>説明</strong></th>
    <th><strong>値</strong></th> 
    </tr> 
    <tr> 
    <td><p>フォームポータル ドラフトデータサービス</p></td> 
    <td><p>ドラフトデータサービスの識別子</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル ドラフトメタデータサービス</p></td> 
    <td><p>ドラフトメタデータサービス の識別子</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル 送信データサービス</p></td> 
    <td><p>送信データサービス の識別子</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル 送信メタデータサービス</p></td> 
    <td><p>送信メタデータサービス の識別子</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル 保留中署名データサービス</p></td> 
    <td><p>保留中の署名データサービスの識別子</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル 保留中署名メタデータサービス</p></td> 
    <td><p>保留中の署名メタデータサービスの識別子</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. Leave other configurations as is and click **[!UICONTROL Save]**.
1. [Web Console Configuration]で編集モー **[!UICONTROL Apache Sling Connection Pooled DataSource]** ドで開くには、を探してクリックします。 次の表の説明に従って、プロパティの値を指定します。

   <table> 
    <tbody> 
    <tr> 
    <th><strong>プロパティ</strong></th> 
    <th><strong>値</strong></th> 
    </tr> 
    <tr> 
    <td><p>データソース名</p></td> 
    <td><p>データソースプールからドライバーをフィルターするためのデータソース名にあることで画像コンポーネントに問題が生じる。サンプルの実装では、データソース名としてFormsPortalを使用しています。</p></td>
    </tr>
    <tr> 
    <td><p>JDBC ドライバークラス</p></td> 
    <td><p>com.mysql.jdbc.Driver</p></td>
    </tr>
    <tr> 
    <td><p>JDBC 接続 URI</p></td> 
    <td><p>jdbc:mysql://[ホスト]:[ポート]/[スキーマ名]</p></td>
    </tr>
    <tr> 
    <td><p>ユーザー名</p></td> 
    <td><p>データベース表でのアクションを認証・実行するためのユーザー名</p></td>
    </tr>
    <tr> 
    <td><p>パスワード</p></td> 
    <td><p>ユーザー名に関連するパスワード</p></td>
    </tr>
    <tr> 
    <td><p>トランザクションの分離</p></td> 
    <td><p>READ_COMMITTED</p></td>
    </tr>
    <tr> 
    <td><p>最大アクティブ接続数</p></td> 
    <td><p>1000</p></td>
    </tr>
    <tr> 
    <td><p>最大アイドル接続数</p></td> 
    <td><p>100</p></td>
    </tr>
    <tr> 
    <td><p>最小アイドル接続数</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>初期サイズ</p></td> 
    <td><p>10</p></td>
    </tr>
    <tr> 
    <td><p>最大待機時間</p></td> 
    <td><p>100000</p></td>
    </tr>
     <tr> 
    <td><p>Test on Borrow</p></td> 
    <td><p>チェック</p></td>
    </tr>
     <tr> 
    <td><p>Test while Idle</p></td> 
    <td><p>チェック</p></td>
    </tr>
     <tr> 
    <td><p>検証クエリ</p></td> 
    <td><p>値の例：SELECT 1（mySQL）、select 1 from dual（Oracle）、SELECT 1（MS SQL Server）（validationQuery）</p></td>
    </tr>
     <tr> 
    <td><p>検証クエリタイムアウト</p></td> 
    <td><p>10000</p></td>
    </tr>
    </tbody> 
    </table>

### サンプルのセットアップおよび設定 {#set-up-and-configure-sample}

すべての作成者インスタンスと発行インスタンスで次の手順を実行し、サンプルをインストールして設定します。

1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** をファイルシステムにダウンロードします。

   [ファイルを入手](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Go to AEM package manager at *http://[host]:[port]/crx/packmgr/*.
1. 「**[!UICONTROL Upload Package]**」をクリックします。
1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** を参照して選択し、「**[!UICONTROL OK]**」をクリックします。
1. Click **[!UICONTROL Install]** next to the package to install the package.

## フォームポータル統合用の変換済みアダプティブフォームの設定 {#configure-converted-adaptive-form-for-forms-portal-integration}

フォームポータルページを使用してアダプティブフォームの送信を有効にするには、次の手順を実行します。
1. [変換を実行して](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) 、ソースフォームをアダプティブフォームに変換します。
1. アダプティブフォームを編集モードで開きます。
1. 「フォームコンテナ」をタップし、「アダプティブフォームを ![設定」を選択しま](assets/configure-adaptive-form.png)す。
1. セクション **[!UICONTROL Submission]** で、ドロップダ **[!UICONTROL Forms Portal Submit Action]** ウンリスト **[!UICONTROL Submit Action]** から選択します。
1. 「テンプレ ![ートポリシーの保存](assets/edit_template_done.png) 」をタップして設定を保存します。

## フォームポータルページの作成と設定 {#create-configure-forms-portal-page}

次の手順を実行して、フォームポータルページを作成し、このページを使用してアダプティブフォームを送信できるように設定します。

1. AEM作成者インスタンスにログオンし、/をタッ **[!UICONTROL Adobe Experience Manager]** プしま **[!UICONTROL Sites]**&#x200B;す。
1. 新しいフォームポータルページを保存する場所を選択し、/をタッ **[!UICONTROL Create]** プしま **[!UICONTROL Page]**&#x200B;す。
1. ページのテンプレートを選択し、をタップし **[!UICONTROL Next]**&#x200B;て、ページのタイトルを指定し、をタップしま **[!UICONTROL Create]**&#x200B;す。
1. をタップ **[!UICONTROL Edit]** して、ページを設定します。
1. ページヘッダーで、テンプレートの編集 ![/](assets/edit_template_sites.png) をタッ **[!UICONTROL Edit Template]** プして、ページのテンプレートを開きます。
1. 「レイアウトコンテナ」をタップし、「テンプレート ![ポリシーの編集」をタップしま](assets/edit_template_policy.png)す。 タブで、とオプシ **[!UICONTROL Allowed Components]** ョンを有効にし、「テンプレ **[!UICONTROL Document Services]** ート **[!UICONTROL Document Services Predicates]** ポリシーを保存」 ![をタップします](assets/edit_template_done.png)。
1. ページにコ **[!UICONTROL Search & Lister]** ンポーネントを挿入します。 その結果、AEMインスタンスで使用可能な既存のアダプティブフォームがすべてページに表示されます。
1. ページにコ **[!UICONTROL Drafts & Submissions]** ンポーネントを挿入します。 との2つのタブ **[!UICONTROL Draft Forms]** がフォ **[!UICONTROL Submitted Forms]**&#x200B;ームポータルページに表示されます。 このタブに **[!UICONTROL Draft Forms]** は、フォームポータル統合のための変換済みアダプティブフォームの設定で説明されてい [る手順を使用して生成された変換済みアダプティブフォームも表示されます](#configure-converted-adaptive-form-for-forms-portal-integration)

1. 変換さ **[!UICONTROL Preview]**&#x200B;れたアダプティブフォームをタップし、アダプティブフォームフィールドの値を指定して送信します。 アダプティブフォームのフィールドに指定した値が統合データベースに送信されます。

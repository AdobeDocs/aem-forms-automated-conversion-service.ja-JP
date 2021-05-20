---
title: フォームポータルを使用してアダプティブフォームをデータベースに送信する
description: デフォルトのメタモデルを拡張することにより、組織固有のパターン、検証設定、エンティティを追加し、自動フォーム変換サービスの実行時に、設定情報をアダプティブフォームの各フィールドに適用することができます。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
source-git-commit: ead1b4ee177029c60f095dc596b1f3db5878760e
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 100%

---


# フォームポータルを使用してアダプティブフォームをデータベースに統合する{#submit-forms-to-database-using-forms-portal}

自動フォーム変換サービスを使用すると、非対話型 PDF フォーム、AcroForms、XFA ベース PDF フォームをアダプティブフォームに変換することができます。 変換サービスを実行する際に、データバインディングを持つアダプティブフォームを生成するのか、データバインディングのないアダプティブフォームを生成するのかを指定することができます。

データバインディングがないアダプティブフォームを生成する場合は、変換処理の完了後に、フォームデータモデル、XML スキーマ、または JSON スキーマに、変換後のアダプティブフォームを統合することができます。 ただし、データバインディングを持つアダプティブフォームを生成すると、アダプティブフォームが自動的に JSON スキーマに関連付けられ、アダプティブフォームと JSON スキーマのフィールド間でデータバインディングが作成されます。その後、フォームポータルを使用して任意のデータベースにアダプティブフォームを統合し、フォーム内のフィールドに値を設定して、データベースにフォームを送信することができます。

以下の図は、フォームポータルを使用して変換後のアダプティブフォームをデータベースに統合する手順をステージ別に示しています。

![データベースとの統合手順](assets/database_integration.gif)

この記事では、これらの統合ステージを正しく実行するための手順について説明します。

この記事で使用するサンプルは、フォームポータルページをデータベースに統合するためにカスタマイズされたデータサービスとメタデータサービスの参照実装環境です。このサンプル実装環境で使用されるデータベースは MySQL 5.6.24 ですが、任意のデータベースをフォームポータルページに統合することができます。

## 前提条件 {#pre-requisites}

* バージョン 6.4 および 6.5 の AEM オーサーインスタンスのセットアップ
* AEM インスタンスの[最新のサービスパック](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html)をインストールする
* 最新バージョンの AEM Forms アドオンパッケージ
* [自動フォーム変換サービス](configure-service.md)の設定
* データベースを設定します。 サンプルの実装環境では MySQL 5.6.24 データベースを使用しますが、変換後のアダプティブフォームは任意のデータベースに統合することができます。

## AEM インスタンスとデータベース間の接続を設定する{#set-up-connection-aem-instance-database}

AEM インスタンスと MYSQL データベース間の接続を設定するには、以下の処理を行う必要があります。

* [MYSQL コネクターパッケージをインストールする](#install-mysql-connector-java-file)

* [データベース内にスキーマとテーブルを作成する](#create-schema-and-tables-in-database)

* [接続の設定を行う](#configure-connection-between-aem-instance-and-database)

* [フォームポータルを統合するためのサンプルパッケージを設定する](#set-up-and-configure-sample)

### mysql-connector-java-5.1.39-bin.jar ファイルをインストールする {#install-mysql-connector-java-file}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、mysql-connector-java-5.1.39-bin.jar ファイルをインストールします。

1. http://[server]:[port]/system/console/depfinder に移動して com.mysql.jdbc パッケージを検索します。
1. 「次による書き出し」列で、パッケージがバンドルで書き出されているかどうかを確認します。パッケージがバンドルで書き出されていない場合は、先に進みます。
1. http://[server]:[port]/system/console/bundles に移動して「**[!UICONTROL Install/Update]**」をクリックします。
1. 「**[!UICONTROL ファイルを選択]**」をクリックし、mysql-connector-java-5.1.39-bin.jar を探して選択します。また、「**[!UICONTROL Start Bundle]**」チェックボックスと「**[!UICONTROL Refresh Packages]**」チェックボックスを選択します。
1. 「**[!UICONTROL Install]**」または「**[!UICONTROL Update]**」をクリックします。完了したら、サーバーを再起動します。
1. （Windows のみ）オペレーティングシステムのシステムファイアウォールをオフにします。

### データベース内にスキーマとテーブルを作成する{#create-schema-and-tables-in-database}

データベース内にスキーマとテーブルを作成するには、以下の手順を実行します。

1. 以下の SQL ステートメントを使用して、データベース内にスキーマを作成します。

   ```sql
   CREATE SCHEMA `formsportal` ;
   ```

   **formsportal** は、スキーマの名前です。

1. 以下の SQL ステートメントを使用して、データベーススキーマ内に **data** というテーブルを作成します。

   ```sql
    CREATE TABLE `data` (
        `owner` varchar(255) DEFAULT NULL,
        `data` longblob,
        `metadataId` varchar(45) DEFAULT NULL,
        `id` varchar(45) NOT NULL,
        PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 以下の SQL ステートメントを使用して、データベーススキーマ内に **metadata** というテーブルを作成します。

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

1. 以下の SQL ステートメントを使用して、データベーススキーマ内に **additionalmetadatatable** というテーブルを作成します。

   ```sql
   CREATE TABLE `additionalmetadatatable` (
       `value` text,
       `key` varchar(255) NOT NULL,
       `id` varchar(60) NOT NULL,
       PRIMARY KEY (`id`,`key`),
       CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
       ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

1. 以下の SQL ステートメントを使用して、データベーススキーマ内に **commenttable** というテーブルを作成します。

   ```sql
   CREATE TABLE `commenttable` (
       `commentId` varchar(255) DEFAULT NULL,
       `comment` text DEFAULT NULL,
       `ID` varchar(255) DEFAULT NULL,
       `commentowner` varchar(255) DEFAULT NULL,
       `time` varchar(255) DEFAULT NULL);
   ```

### AEM インスタンスとデータベース間の接続を設定する{#configure-connection-between-aem-instance-and-database}

AEM インスタンスと MYSQL データベース間の接続を作成するには、以下の手順を実行します。

1. AEM Web コンソールの設定ページ（*http://[host]:[port]/system/console/configMgr*）に移動します。
1. **[!UICONTROL Forms Portal Draft and Submission Configuration]** をクリックし、編集モードで開きます。
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
    <td><p>ドラフトメタデータサービスの識別子</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル 送信データサービス</p></td> 
    <td><p>送信データサービスの識別子</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル 送信メタデータサービス</p></td> 
    <td><p>送信メタデータサービスの識別子</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル 保留中署名データサービス</p></td> 
    <td><p>保留中署名データサービスの識別子</p></td>
    <td><p>formsportal.sampledataservice</p></td> 
    </tr>
    <tr> 
    <td><p>フォームポータル 保留中署名メタデータサービス</p></td> 
    <td><p>保留中署名メタデータサービスの識別子</p></td>
    <td><p>formsportal.samplemetadataservice</p></td> 
    </tr>
    </tbody> 
    </table>
1. 他の設定はそのままにし、「**[!UICONTROL 保存]**」をクリックします。
1. Web コンソールの設定ページで、「**[!UICONTROL Apache Sling Connection Pooled DataSource]**」をクリックして編集モードで開きます。次の表の説明に従って、プロパティの値を指定します。

   <table> 
    <tbody> 
    <tr> 
    <th><strong>プロパティ</strong></th> 
    <th><strong>値</strong></th> 
    </tr> 
    <tr> 
    <td><p>データソース名</p></td> 
    <td><p>データソースプールからドライバーをフィルターするためのデータソース名 このサンプル実装環境では、データソース名として「FormsPortal」を使用しています。</p></td>
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

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、サンプルをインストールして設定します。

1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** をファイルシステムにダウンロードします。

[ファイルを入手](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. AEM パッケージマネージャー（*http://[host]:[port]/crx/packmgr/*）に移動します。
1. 「**[!UICONTROL パッケージをアップロード]**」をクリックします。
1. パッケージ **aem-fp-db-integration-sample-pkg-6.1.2.zip** を参照して選択し、「**[!UICONTROL OK]**」をクリックします。
1. パッケージの横に表示されている「**[!UICONTROL インストール]**」クリックしてパッケージをインストールします。

## 変換後のアダプティブフォームをフォームポータル統合用に設定する{#configure-converted-adaptive-form-for-forms-portal-integration}

フォームポータルページでアダプティブフォームを送信できるようにするには、以下の手順を実行します。
1. [変換サービスを実行](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process)して、ソースフォームをアダプティブフォームに変換します。
1. アダプティブフォームを編集モードで開きます。
1. フォームコンテナをタップして「![アダプティブフォームを設定](assets/configure-adaptive-form.png)」を選択します。
1. 「**[!UICONTROL 送信]**」セクションの「**[!UICONTROL 送信アクション]**」プルダウンリストで「**[!UICONTROL フォームポータル送信アクション]**」を選択します。
1. 「![テンプレートポリシーを保存](assets/edit_template_done.png)」をタップして設定を保存します。

## フォームポータルページの作成と設定を行う{#create-configure-forms-portal-page}

フォームポータルページを作成し、そのページでアダプティブフォームを送信できるように設定するには、以下の手順を実行します。

1. AEM オーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL サイト]**&#x200B;の順にタップします。  
1. 新しいフォームポータルページの保存場所を選択し、**[!UICONTROL 作成]**／**[!UICONTROL ページ]**&#x200B;をタップします。
1. ページのテンプレートを選択して「**[!UICONTROL 次へ]**」をタップし、ページのタイトルを入力して「**[!UICONTROL 作成]**」をタップします。
1. 「**[!UICONTROL 編集]**」をタップして、ページの設定を行います。
1. ページのヘッダーで、「![テンプレートの編集](assets/edit_template_sites.png)  ／**[!UICONTROL テンプレートを編集]**」の順にタップしてページのテンプレートを開きます。
1. レイアウトコンテナをタップして、「![テンプレートポリシーを編集](assets/edit_template_policy.png)」をタップします。 「**[!UICONTROL 許可されているコンポーネント]**」タブで「**[!UICONTROL Document Services]**」オプションと「**[!UICONTROL Document Services の述語]**」オプションを有効にして「![テンプレートポリシーを保存](assets/edit_template_done.png)」をタップします。
1. 「**[!UICONTROL 検索とリスター]**」コンポーネントをページ内に挿入します。 これにより、AEM インスタンス上のすべてのアダプティブフォームがページに一覧表示されます。
1. 「**[!UICONTROL ドラフトと送信]**」コンポーネントをページ内に挿入します。 「**[!UICONTROL ドラフトフォーム]**」と「**[!UICONTROL 送信済みのフォーム]**」という 2 つのタブがフォームポータルページに表示されます。 「**[!UICONTROL ドラフトフォーム]**」タブには、「[変換後のアダプティブフォームをフォームポータル統合用に設定する](#configure-converted-adaptive-form-for-forms-portal-integration)」セクションの手順に従って生成された変換後のアダプティブフォームも表示されます。

1. 「**[!UICONTROL プレビュー]**」をタップしてから変換後のアダプティブフォームをタップして、アダプティブフォームフィールドの値を指定してフォームを送信します。 アダプティブフォームフィールドで指定した値が、統合後のデータベースに送信されます。

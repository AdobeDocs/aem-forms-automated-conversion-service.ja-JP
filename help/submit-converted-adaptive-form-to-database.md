---
title: 変換されたアダプティブフォームをJSONスキーマと共にデータベースに送信する
description: フォームデータモデルを作成し、AEMワークフローで参照して、変換されたアダプティブフォームをJSONスキーマと共にデータベースに送信します。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: c552f4073ac88ca9016a746116a27a5898df7f7d

---


# AEMワークフローを使用したアダプティブフォームとデータベースの統合 {#submit-forms-to-database-using-forms-portal}

Automated Forms Conversionサービスを使用すると、非インタラクティブPDFフォーム、AcroフォームまたはXFAベースのPDFフォームをアダプティブフォームに変換できます。 変換処理を開始する際に、データ連結の有無に関わらず、アダプティブフォームを生成するオプションがあります。

データ連結なしでアダプティブフォームを生成する場合は、変換後のアダプティブフォームを、変換後のフォームデータモデル、XMLスキーマまたはJSONスキーマと統合できます。 フォームデータモデルの場合は、アダプティブフォームのフィールドをフォームデータモデルと手動で連結する必要があります。 ただし、データ連結を含むアダプティブフォームを生成する場合、変換サービスはアダプティブフォームをJSONスキーマに自動的に関連付け、アダプティブフォームで使用可能なフィールドとJSONスキーマの間にデータ連結を作成します。 その後、アダプティブフォームを選択したデータベースと統合し、フォームにデータを入力して、データベースに送信できます。 同様に、データベースとの統合が成功したら、変換後のアダプティブフォームのフィールドを設定して、データベースから値を取得し、アダプティブフォームのフィールドに事前入力することができます。

次の図は、変換されたアダプティブフォームをデータベースと統合する様々な段階を示しています。

![データベース統合](assets/integrate-adaptive-form-with-database.png)

この記事では、これらすべての統合ステージを正しく実行するための手順を説明します。

## 前提条件 {#pre-requisites}

* AEM 6.4または6.5の作成者インスタンスの設定
* AEMインスタ [ンスの最新のService](https://helpx.adobe.com/experience-manager/aem-releases-updates.html) Packをインストールします。
* AEM Formsアドオンパッケージの最新バージョン
* 自動フォ [ーム変換サービスの設定](configure-service.md)
* データベースを設定します。 サンプル実装で使用されるデータベースはMySQL 5.6.24です。ただし、変換されたアダプティブフォームは任意のデータベースと統合できます。

## アダプティブフォームのサンプル {#sample-adaptive-form}

AEMワークフローを使用して、変換されたアダプティブフォームをデータベースと統合するユースケースを実行するには、次のサンプルPDFファイルをダウンロードします。

サンプルのお問い合わせフォームは、次を使用してダウンロードできます。

[ファイルを入手](assets/sample_contact_us_form.pdf)

PDFファイルは、Automated Forms Conversionサービスへの入力として機能します。 このファイルはアダプティブフォームに変換されます。 次の画像は、PDF形式のサンプルの連絡先フォームを示しています。

![サンプルローン申込フォーム](assets/sample_contact_us_form.png)

## mysql-connector-java-5.1.39-bin.jar ファイルのインストール {#install-mysql-connector-java-file}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、mysql-connector-java-5.1.39-bin.jar ファイルをインストールします。

1. com.mysql.jdbc `http://server:port/system/console/depfinder` パッケージに移動し、検索します。
1. 「次による書き出し」列で、パッケージがバンドルで書き出されているかどうかを確認します。パッケージがバンドルで書き出されていない場合は、先に進みます。
1. に移動し、を `http://server:port/system/console/bundles` クリックしま **[!UICONTROL Install/Update]**&#x200B;す。
1. Click **[!UICONTROL Choose File]** and browse to select the mysql-connector-java-5.1.39-bin.jar file. また、とチェックボッ **[!UICONTROL Start Bundle]** クスを選 **[!UICONTROL Refresh Packages]** 択します。
1. またはをク **[!UICONTROL Install]** リックしま **[!UICONTROL Update]**&#x200B;す。 完了したら、サーバーを再起動します。
1. （Windowsのみ）お使いのオペレーティングシステムのシステムファイアウォールをオフにします。

## フォームモデルのデータを準備する {#prepare-data-for-form-model}

AEM Forms のデータ統合機能により、複数の異なるデータソースを設定して接続することができます。変換プロセスを使用してアダプティブフォームを生成した後、フォームデータモデル、XSD、またはJSONスキーマに基づいてフォームモデルを定義できます。 データベース、Microsoft Dynamicsまたはその他のサードパーティサービスを使用して、フォームデータモデルを作成できます。

このチュートリアルでは、MySQLデータベースをソースとして使用し、フォームデータモデルを作成します。 データベースにスキーマを作成し、アダプテ **ィブフォームで** 使用可能なフィールドに基づいて、スキーマに連絡先テーブルを追加します。

![サンプルデータmysql](assets/db_entries_sample_form.png)

次のDDL文を使用して、データベースに連絡先テーブ **ルを作** 成できます。

```sql
CREATE TABLE `contactus` (
   `name` varchar(45) NOT NULL,
   `email` varchar(45) NOT NULL,
   `phonenumber` varchar(10) DEFAULT NULL,
   `issuedesc` varchar(1000) DEFAULT NULL,
   PRIMARY KEY (`email`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## AEMインスタンスとデータベース間の接続の設定 {#configure-connection-between-aem-instance-and-database}

次の設定手順を実行して、AEMインスタンスとMYSQLデータベース間の接続を作成します。

1. Go to AEM Web Console Configuration page at `http://server:port/system/console/configMgr`.
1. [Web Console Configuration]で編集モ **[!UICONTROL Apache Sling Connection Pooled DataSource]** ードで開くには、をクリックします。 次の表の説明に従って、プロパティの値を指定します。

   <table> 
    <tbody> 
    <tr> 
    <th><strong>プロパティ</strong></th> 
    <th><strong>値</strong></th> 
    </tr> 
    <tr> 
    <td><p>データソース名</p></td> 
    <td><p>データソースプールからドライバーをフィルターするためのデータソース名。</p></td>
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

## フォームデータモデルの作成 {#create-form-data-model}

MYSQLをデータソースとして設定したら、次の手順を実行してフォームデータモデルを作成します。

1. AEMオーサーインスタンスで、/に移動 **[!UICONTROL Forms]** しま **[!UICONTROL Data Integrations]**&#x200B;す。

1. タップ **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.

1. ウィザード **[!UICONTROL Create Form Data Model]** で、フ **ォームデータモデルの名前としてworkflow_submit** を指定します。 タップ **[!UICONTROL Next]**.

1. 前の節で設定したMYSQLデータソースを選択し、をタップします **[!UICONTROL Create]**。

1. 左側の **[!UICONTROL Edit]** ウィンドウに表示されているデータソースをタップして展開し、 **連絡先** 、表、サービスを選択し **[!UICONTROL get]**、をタップしま **[!UICONTROL insert]****[!UICONTROL Add Selected]**&#x200B;す。

   ![サンプルデータmysql](assets/fdm_details_workfdlow_submit.png)

1. 右側のウィンドウでデータモデルオブジェクトを選択し、をタップしま **[!UICONTROL Edit Properties]**&#x200B;す。 およびド **[!UICONTROL get]** ロップダ **[!UICONTROL insert]** ウンリストか **[!UICONTROL Read Service]** ら、およびを **[!UICONTROL Write Service]** 選択します。 Readサービスの引数を指定し、をタップしま **[!UICONTROL Done]**&#x200B;す。

1. タブで、サ **[!UICONTROL Services]** ービスを選択 **[!UICONTROL get]** し、をタップしま **[!UICONTROL Edit Properties]**&#x200B;す。 を選択し、 **[!UICONTROL Output Model Object]**&#x200B;トグルを無効 **[!UICONTROL Return array]** にしてをタップしま **[!UICONTROL Done]**&#x200B;す。

1. Select the **[!UICONTROL Insert]** service and tap **[!UICONTROL Edit Properties]**. Select the **[!UICONTROL Input Model Object]** and tap **[!UICONTROL Done]**.

1. Tap **[!UICONTROL Save]** to save the form data model.

次を使用して、サンプルのフォームデータモデルをダウンロードできます。

[ファイルを入手](assets/DownloadedFormsPackage_1497728018502500.zip)

## JSONバインディングを使用したアダプティブフォームの生成 {#generate-adaptive-forms-with-json-binding}

Automated Forms Conversionサービ [スを使用して](convert-existing-forms-to-adaptive-forms.md) 、データ連結を [](#sample-adaptive-form) 含むアダプティブフォームにContact Usフォームを変換します。 アダプティブフォームの生成時に、チェックボッ **[!UICONTROL Generate adaptive form(s) without data bindings]** クスをオンにしないようにしてください。

![JSONバインディングを使用したアダプティブフォーム](assets/generate_af_with_data_bindings.png)

のフォルダーにあ **る変換済みの** 「お問い合わせ」フォ **[!UICONTROL output]** ームを選択し、を **[!UICONTROL Forms & Documents]** タップしま **[!UICONTROL Edit]**&#x200B;す。 をタップ **[!UICONTROL Preview]**&#x200B;し、アダプティブフォームのフィールドに値を入力してをタップしま **[!UICONTROL Submit]**&#x200B;す。

crx-repositoryにロ **グオンし** 、 ** /content/forms/fp/admin/submit/dataに移動して、送信された値をJSON形式で表示します。 変換された **Contact Usアダプティブフォームを送信する際のJSON形式のサンプルデータは** 、次のとおりです。

```json
{
  "afData": {
    "afUnboundData": {
      "data": {}
    },
    "afBoundData": {
      "data": {
        "name1": "Gloria",
        "email": "abc@xyz.com",
        "phone_number": "2346578965",
        "issue_description": "Test message"
      }
    },
    "afSubmissionInfo": {
      "computedMetaInfo": {},
      "stateOverrides": {},
      "signers": {},
      "afPath": "/content/dam/formsanddocuments/docs_conversion/output/sample_form_json",
      "afSubmissionTime": "20191204014007"
    }
  }
}
```

このデータを処理し、前の節で作成したフォームデータモデルを使用してMYSQLデータベースに送信できるように、ワークフローモデルを作成する必要があります。

## JSONデータを処理するワークフローモデルの作成 {#create-workflow-model}

次の手順を実行して、アダプティブフォームデータをデータベースに送信するワークフローモデルを作成します。

1. ワークフローモデルコンソールを開きます。The default URL is `https://server:port/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`.

1. を選択し **[!UICONTROL Create]**&#x200B;て、を選択しま **[!UICONTROL Create Model]**&#x200B;す。 The **[!UICONTROL Add Workflow Model]** dialog appears.

1. とを入力し **[!UICONTROL Title]** ます(オ **[!UICONTROL Name]** プション)。 例えば、 **workflow_json_submit**。 をタップ **[!UICONTROL Done]** して、モデルを作成します。

1. ワークフローモデルを選択し、をタッ **[!UICONTROL Edit]** プして、モデルを編集モードで開きます。 「+」をタップし、ワークフ **[!UICONTROL Invoke Form Data Model Service]** ローモデルに手順を追加します。

1. 手順をタッ **[!UICONTROL Invoke Form Data Model Service]** プし、「設定」をタ ![ップしま](assets/configure_icon.png)す。

1. タブで、 **[!UICONTROL Form Data Model]** フィールドで作成したフォームデータモデルを選択し、 **[!UICONTROL Form Data Model path]** ドロップダウンリ **[!UICONTROL insert]** ストから **[!UICONTROL Service]** 選択します。

1. タブで、ド **[!UICONTROL Input for Service]** ロップダ **[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]** ウンリストから選択し、チェッ **[!UICONTROL Map input fields from input JSON]** クボックスを選択し **[!UICONTROL Relative to payload]**&#x200B;て、 **data.xmlをフィールドの値として指定し****[!UICONTROL Select input JSON document using]** ます。

1. この節では、 **[!UICONTROL Service Arguments]** フォームデータモデルの引数に次の値を指定します。

   ![フォームデータモデルサービスを起動](assets/invoke_form_data_model_service.png)

   フォームデータモデルのフィールド（例えば、ドット名を含む）は、送信されたアダプティブフォームのJSONスキーマバインディングを参照する **afData.afBoundData.data.name1**&#x200B;にマッピングされます。

## アダプティブフォーム送信の設定 {#configure-adaptive-form-submission}

次の手順を実行して、前の節で作成したワークフローモデルにアダプティブフォームを送信します。

1. のフォルダーにある変換済みのお問い合わせフォームを **[!UICONTROL output]** 選択し、を **[!UICONTROL Forms & Documents]** タップしま **[!UICONTROL Edit]**&#x200B;す。

1. アダプティブフォームのプロパティを開くには、をタップし **[!UICONTROL Form Container]** てから「設定」をタッ ![プします](assets/configure_icon.png)。

1. セクション **[!UICONTROL Submission]** のドロップダ **[!UICONTROL Invoke an AEM workflow]** ウンリ **[!UICONTROL Submit Action]** ストから選択し、前のセクションで作成したワークフローモデルを選択し、フィールドに **data.xml** を指定し **[!UICONTROL Data File Path]** ます。

1. 「![保存](assets/save_icon.png)」をタップして、プロパティを保存します。

1. をタップ **[!UICONTROL Preview]**&#x200B;し、アダプティブフォームのフィールドに値を入力してをタップしま **[!UICONTROL Submit]**&#x200B;す。 現在は、送信された値が **crx-repositoryではなくMYSQLデータベーステーブルに表示されます**。

## データベースから値を事前入力するアダプティブフォームの設定

次の手順を実行して、表で定義されたプライマリキーに基づいてMYSQLデータベースの値を事前入力するようにアダプティブフォームを設定します（この場合は電子メールで送信）。

1. アダプティブフ **ォームの「電子メール** 」フィールドをタップし、「ルールを編集」を ![タップしま](assets/edit-rules.png)す。

1. をタッ **[!UICONTROL Create]** プし、セ **[!UICONTROL is changed]** クションのド **[!UICONTROL Select State]** ロップダウンリストから選択 **[!UICONTROL When]** します。

1. この節で **[!UICONTROL Then]** は、前の節 **[!UICONTROL Invoke Service]** で作成 **** したフォームデータモデルのサービスを選択し、取得します。

1. セクション **内の** 「電子メール」を選択し、フォームデータモデルの残りの3つのフィールド(「 **[!UICONTROL Input]** Name **」、「Name**」、「E-mail」、「E-mail」、「E-mail」、「 **E-mail」、「E-mail」、「E-mail」、「E-phone」の各セクション内********[!UICONTROL Output]** 」)を選択します。 Tap **[!UICONTROL Done]** to save the settings.

   ![電子メールの事前入力の設定](assets/email_prefill_settings.png)

   その結果、MYSQLデータベース内の既存の電子メールエントリに基づいて、アダプティブフォームのモードで残りの3つのフィールドの値を事前入 **[!UICONTROL Preview]** 力することができます。 例えば、 **E-mail** ( [Based existing data in](#prepare-data-for-form-model) Form data prepare **section of this article)とtab out to the field、残りの3つのフィールド、** Name、 **Name、** NameName、 **** Phone、Issue Desplaying forming Inurenute Desアダプティブフォームに、

次を使用して、変換されたアダプティブフォームのサンプルをダウンロードできます。

[ファイルを入手](assets/DownloadedFormsPackage_1498226829041200.zip)

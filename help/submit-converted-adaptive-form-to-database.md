---
title: JSONスキーマを含む変換済みアダプティブフォームをデータベースに送信する
description: フォームデータモデルを作成し、AEMワークフローで参照して、JSONスキーマを使用して変換済みのアダプティブフォームをデータベースに送信します。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: b879a0ddecd5370c754dfe9e1bf33121dd5ecc97

---


# AEMワークフローを使用したアダプティブフォームとデータベースの統合 {#submit-forms-to-database-using-forms-portal}

自動フォーム変換サービスを使用すると、非インタラクティブPDFフォーム、AcroフォームまたはXFAベースのPDFフォームをアダプティブフォームに変換できます。 変換処理を開始する際に、データ連結の有無に関わらずアダプティブフォームを生成するオプションがあります。

データ連結なしでアダプティブフォームを生成する場合は、変換後のアダプティブフォームを、変換後のフォームデータモデル、XMLスキーマ、またはJSONスキーマと統合できます。 フォームデータモデルの場合は、アダプティブフォームフィールドを手動でフォームデータモデルに連結する必要があります。 ただし、データ連結を含むアダプティブフォームを生成する場合、変換サービスはアダプティブフォームをJSONスキーマに自動的に関連付け、アダプティブフォームとJSONスキーマで使用可能なフィールド間にデータ連結を作成します。 その後、アダプティブフォームを選択したデータベースと統合し、フォームにデータを入力して、データベースに送信できます。 同様に、データベースとの統合が成功したら、変換されたアダプティブフォームのフィールドを設定して、データベースから値を取得し、アダプティブフォームのフィールドに事前入力することができます。

次の図は、変換されたアダプティブフォームをデータベースと統合する様々な段階を示しています。

![データベース統合](assets/integrate-adaptive-form-with-database.png)

この記事では、これらすべての統合ステージを正常に実行するための手順を説明します。

## 前提条件 {#pre-requisites}

* 最新のAEM 6.5 Service packを含むAEM 6.5作成者インスタンス
* AEM Formsアドオンパッケージの最新バージョン
* [Automated Forms Conversionサービス](configure-service.md)
* 統合するデータベース。 サンプル実装で使用されるデータベースはMySQL 5.6.24です。ただし、変換されたアダプティブフォームを任意のデータベースに統合することはできます。

## アダプティブフォームのサンプル {#sample-adaptive-form}

AEMワークフローを使用して、変換されたアダプティブフォームをデータベースと統合するユースケースを実行するには、次のサンプルPDFファイルをダウンロードします。

次を使用して、お問い合わせフォームのサンプルをダウンロードできます。

[ファイルを入手](assets/sample_contact_us_form.pdf)

PDFファイルは、Automated Forms Conversionサービスへの入力として機能します。 このファイルはアダプティブフォームに変換されます。 次の画像は、PDF形式のサンプルの連絡先フォームを示しています。

![申込書](assets/sample_contact_us_form.png)

## mysql-connector-java-5.1.39-bin.jar ファイルのインストール {#install-mysql-connector-java-file}

すべてのオーサーインスタンスとパブリッシュインスタンスで、次の手順を実行し、mysql-connector-java-5.1.39-bin.jar ファイルをインストールします。

1. com.mysql.jdbc `http://server:port/system/console/depfinder` パッケージに移動し、検索します。
1. 「次による書き出し」列で、パッケージがバンドルで書き出されているかどうかを確認します。パッケージがバンドルで書き出されていない場合は、先に進みます。
1. に移動し、をク `http://server:port/system/console/bundles` リックしま **[!UICONTROL Install/Update]**&#x200B;す。
1. Click **[!UICONTROL Choose File]** and browse to select the mysql-connector-java-5.1.39-bin.jar file. また、とチェックボッ **[!UICONTROL Start Bundle]** クスを選 **[!UICONTROL Refresh Packages]** 択します。
1. またはをク **[!UICONTROL Install]** リックしま **[!UICONTROL Update]**&#x200B;す。 完了したら、サーバーを再起動します。
1. （Windowsのみ）ご使用のオペレーティングシステムのシステムファイアウォールをオフにします。

## フォームモデルのデータを準備する {#prepare-data-for-form-model}

AEM Forms のデータ統合機能により、複数の異なるデータソースを設定して接続することができます。変換プロセスを使用してアダプティブフォームを生成した後、フォームデータモデル、XSD、またはJSONスキーマに基づいてフォームモデルを定義できます。 フォームデータモデルの作成には、データベース、Microsoft Dynamics、またはその他のサードパーティサービスを使用できます。

このチュートリアルでは、MySQLデータベースをソースとして使用し、フォームデータモデルを作成します。 データベースにスキーマを作成し、アダプ **ティブフォームで** 使用可能なフィールドに基づいてスキーマに連絡先テーブルを追加します。

![サンプルデータmysql](assets/db_entries_sample_form.png)

次のDDL文を使用して、データベースに連絡先表 **を作成で** きます。

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
1. [Web Console Configuration]で編集モー **[!UICONTROL Apache Sling Connection Pooled DataSource]** ドで開くには、を探してクリックします。 次の表の説明に従って、プロパティの値を指定します。

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

1. AEM作成者インスタンスで、/に移動 **[!UICONTROL Forms]** します **[!UICONTROL Data Integrations]**。

1. タップ **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.

1. ウィザード **[!UICONTROL Create Form Data Model]** で、フォ **ームデータモデルの名前としてworkflow_submit** を指定します。 タップ **[!UICONTROL Next]**.

1. 前の節で設定したMYSQLデータソースを選択し、をタップします **[!UICONTROL Create]**。

1. 左側の **[!UICONTROL Edit]** ウィンドウに表示されているデータソースをタップして展開し、 **連絡先** 、表、サービスを選 **[!UICONTROL get]**&#x200B;択して、をタップしま **[!UICONTROL insert]****[!UICONTROL Add Selected]**&#x200B;す。

   ![サンプルデータmysql](assets/fdm_details_workfdlow_submit.png)

1. 右側のウィンドウでデータモデルオブジェクトを選択し、をタップしま **[!UICONTROL Edit Properties]**&#x200B;す。 およびド **[!UICONTROL get]** ロップダ **[!UICONTROL insert]** ウンリスト **[!UICONTROL Read Service]** から、および **[!UICONTROL Write Service]** を選択します。 Readサービスの引数を指定し、をタップします **[!UICONTROL Done]**。

1. タブで、サ **[!UICONTROL Services]** ービスを選択し、を **[!UICONTROL get]** タップしま **[!UICONTROL Edit Properties]**&#x200B;す。 を選択し、 **[!UICONTROL Output Model Object]**&#x200B;トグルを無効 **[!UICONTROL Return array]** にしてをタップしま **[!UICONTROL Done]**&#x200B;す。

1. Select the **[!UICONTROL Insert]** service and tap **[!UICONTROL Edit Properties]**. Select the **[!UICONTROL Input Model Object]** and tap **[!UICONTROL Done]**.

1. Tap **[!UICONTROL Save]** to save the form data model.

サンプルのForm Data modelは、次を使用してダウンロードできます。

[ファイルを入手](assets/DownloadedFormsPackage_1497728018502500.zip)

## JSONバインディングを使用したアダプティブフォームの生成 {#generate-adaptive-forms-with-json-binding}

Automated Forms Conversionサービスを使 [用して、お問い合わせフォームを](convert-existing-forms-to-adaptive-forms.md) 、データ連結 [](#sample-adaptive-form) を含むアダプティブフォームに変換します。 アダプティブフォームの生成中は、チェックボ **[!UICONTROL Generate adaptive form(s) without data bindings]** ックスをオンにしないでください。

![JSONバインディングを使用したアダプティブフォーム](assets/generate_af_with_data_bindings.png)

のフォルダーにあ **る変換済みの「お問い合わせ** 」フォームを **[!UICONTROL output]** 選択し、を **[!UICONTROL Forms & Documents]** タップしま **[!UICONTROL Edit]**&#x200B;す。 をタップ **[!UICONTROL Preview]**&#x200B;し、アダプティブフォームのフィールドに値を入力してをタップしま **[!UICONTROL Submit]**&#x200B;す。

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

1. を選択 **[!UICONTROL Create]**&#x200B;し、次に **[!UICONTROL Create Model]**。 The **[!UICONTROL Add Workflow Model]** dialog appears.

1. とを入力し **[!UICONTROL Title]** ます(オ **[!UICONTROL Name]** プション)。 例えば、 **workflow_json_submit**。 をタップ **[!UICONTROL Done]** して、モデルを作成します。

1. ワークフローモデルを選択し、をタ **[!UICONTROL Edit]** ップして、モデルを編集モードで開きます。 「+」をタップし、ワークフ **[!UICONTROL Invoke Form Data Model Service]** ローモデルにステップを追加します。

1. 手順をタップし **[!UICONTROL Invoke Form Data Model Service]** 、「設定」をタ ![ップします](assets/configure_icon.png)。

1. タブで、 **[!UICONTROL Form Data Model]** フィールドに作成したフォームデータモデルを選択し、ド **[!UICONTROL Form Data Model path]** ロップダウンリ **[!UICONTROL insert]** ストか **[!UICONTROL Service]** ら選択します。

1. タブで、ド **[!UICONTROL Input for Service]** ロップダウン **[!UICONTROL Provide input data using literal, variable, or a workflow metadata, and a JSON file]** リストから選択し、チェックボッ **[!UICONTROL Map input fields from input JSON]** クスを選択し **[!UICONTROL Relative to payload]**&#x200B;て、フィールドの値として **data.xml** を指定し **[!UICONTROL Select input JSON document using]** ます。

1. この節で **[!UICONTROL Service Arguments]** は、フォームデータモデルの引数に次の値を指定します。

   ![フォームデータモデルサービスを起動](assets/invoke_form_data_model_service.png)

   フォームデータモデルのフィールド（例えば、ドット名に一致）は、送信されたアダプティブフォームのJSONスキーマバインディングを参照する **afData.afBoundData.data.name1**&#x200B;にマッピングされます。

## アダプティブフォーム送信の設定 {#configure-adaptive-form-submission}

次の手順を実行して、前の節で作成したワークフローモデルにアダプティブフォームを送信します。

1. のフォルダーにある変換済みのお問い合わせフォームを選択し、 **[!UICONTROL output]** をタ **[!UICONTROL Forms & Documents]** ップしま **[!UICONTROL Edit]**&#x200B;す。

1. アダプティブフォームのプロパティを開くには、「設 **[!UICONTROL Form Container]** 定」をタップ ![します](assets/configure_icon.png)。

1. セクション **[!UICONTROL Submission]** で、ドロッ **[!UICONTROL Invoke an AEM workflow]** プダウン **[!UICONTROL Submit Action]** リストから選択し、前のセクションで作成したワークフローモデルを選択し、フィールドに **data.xml** を指定し **[!UICONTROL Data File Path]** ます。

1. 「![保存](assets/save_icon.png)」をタップして、プロパティを保存します。

1. をタップ **[!UICONTROL Preview]**&#x200B;し、アダプティブフォームのフィールドに値を入力してをタップしま **[!UICONTROL Submit]**&#x200B;す。 送信された値は、 **crx-repositoryではなくMYSQLデータベーステーブルに表示されます**。

## データベースから値を事前入力するアダプティブフォームの設定

次の手順を実行して、表で定義されたプライマリキーに基づいてMYSQLデータベースの値を事前入力するようにアダプティブフォームを設定します（この場合は電子メールで送信）。

1. アダプティブ **フォームの「電子メール** 」フィールドをタップし、「ルールを編集」を ![タップしま](assets/edit-rules.png)す。

1. をタッ **[!UICONTROL Create]** プし、セ **[!UICONTROL is changed]** クション **[!UICONTROL Select State]** のドロップダウンリストから選択 **[!UICONTROL When]** します。

1. この節で **[!UICONTROL Then]** は、前の節 **[!UICONTROL Invoke Service]** で作 **** 成したフォームデータモデルのサービスを選択し、取得します。

1. セクシ **ョン内の** 「電子メール」を選択し、フォームデータモデルの残り3つのフィールド( **[!UICONTROL Input]** Name **、Name**、E-mail、E-mail Description In The Phone Section)を選択します **********[!UICONTROL Output]** 。 Tap **[!UICONTROL Done]** to save the settings.

   ![電子メールの事前入力の設定](assets/email_prefill_settings.png)

   その結果、MYSQLデータベース内の既存の電子メールエントリに基づいて、アダプティブフォームのモードで残りの3つのフィールドの値を事 **[!UICONTROL Preview]** 前入力できます。 例えば、「 **E-mail** 」フィールドにaya.tan@xyz.comを指定し(この記事の「 [Based existing data Prepare form data model](#prepare-data-for-form-model) 」セクションに「 **Based」と入力)、フィールドの外にタブを指定し、残りの3つの「** Name」、「 **Name Phone Form」、「Adaptive****** Phone Pone Form」と入力Dis Dis Displatine De Pone Pone Fore In

次を使用して、変換されたアダプティブフォームのサンプルをダウンロードできます。

[ファイルを入手](assets/DownloadedFormsPackage_1498226829041200.zip)

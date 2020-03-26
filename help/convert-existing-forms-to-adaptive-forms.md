---
title: 'PDFフォームからアダプティブフォームへの変換 '
seo-title: 'PDFフォームからアダプティブフォームへの変換 '
description: PDFフォームをアダプティブフォームに変換するには、Automated Forms Conversionサービスを実行します。
seo-description: PDFフォームをアダプティブフォームに変換するには、Automated Forms Conversionサービスを実行します。
uuid: 49fcd5c0-0e72-496d-9831-00f79d582f57
contentOwner: khsingh
topic-tags: forms
discoiquuid: 9358219c-6079-4552-92b9-b427a23811af
translation-type: tm+mt
source-git-commit: bcd55fa59f37b71b95b7cbfd80fcda368eaba408

---


# PDFフォームからアダプティブフォームへの変換 {#convert-print-forms-to-adaptive-forms}

Adobe Senseiが提供するAEM Forms Automated Forms Conversionサービスは、PDFフォームをデバイスに優しくレスポンシブなアダプティブフォームに自動的に変換します。 非インタラクティブPDFフォーム、Acro Forms、XFAベースのPDFフォームのどちらを使用している場合でも、Automated Forms Conversionサービスは、これらのフォームをアダプティブフォームに簡単に変換できます。 機能、コンバージョンワークフロー、およびオンボーディング情報について詳しくは、「自動フォームコンバ [ージョンサービス](introduction.md) 」を参照してください。

## 前提条件 {#pre-requisites}

* [**変換サービスの設定&#x200B;**](configure-service.md)

* **変換されたフォ[ームに適用する](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html)、テンプレートを準備します。** テンプレートを使用すると、すべてのアダプティブフォームに一貫したブランドを適用できます。 また、自動フォーム変換サービスでは、ソースPDFドキュメントのヘッダーとフッターを抽出して使用することはできません。 アダプティブフォームテンプレートを使用して、ヘッダーとフッターを指定できます。 テンプレートで指定されたヘッダーとフッターは、変換時にアダプティブフォームに適用されます。

* **変換されたフ[ォームに](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html)、適用するテーマを準備します。** テーマを使用すると、組織のすべてのアダプティブフォームに一貫したスタイルを適用できます。

## 変換プロセスの開始 {#start-the-conversion-process}

AEMインスタンスをAEM Forms Conversion Serviceに接続した後、PDFフォームをアダプティブフォームに変換できます。 フォームを変換するには、一覧の順序で次の手順を実行します。

* [PDFフォームのAEM Formsサーバーへのアップロード](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [変換の実行](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [変換されたフォームの確認と修正](review-correct-ui-edited.md)

### PDFフォームのAEM Formsサーバーへのアップロード {#upload-pdf-forms-to-your-aem-forms-server}

変換サービスを実行すると、AEM Forms インスタンス上の PDF フォームがアダプティブフォームに変換されます。 必要に応じて、すべての PDF フォームを一度にアップロードすることも、段階的にアップロードすることもできます。 フォームをアップロードする場合は、以下の点に注意してください。

* 1 つのフォルダーに保存するフォームの数は 15 個未満にしてください。また、1 つのフォルダーに保存する合計ページ数は 50 ページ未満にしてください。
* フォルダーのサイズは 10 MB 未満にしてください。 サブフォルダー内にフォームを保存しないでください。
* 各フォームのページ数は 15 ページ未満にしてください。
* 保護されたフォームをアップロードしないでください。 この変換サービスでは、パスワードで保護されたフォームを変換することはできません。
* ファイル名にスペースが含まれているソースファイルをアップロードしないでください。 こうしたファイルをアップロードする場合は、ファイル名に含まれているスペースを削除してからアップロードしてください。
* [PDFポートフォリオはアップロードしない](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 この変換サービスでは、PDF ポートフォリオをアダプティブフォームに変換することはできません。
* 「既知の問題 [」、「ベスト](known-issues.md) ・プラクティス [と考慮事項](styles-and-pattern-considerations-and-best-practices.md) 」の節を読み、フォームに推奨される変更を加えます。

次の手順を実行して、AEM Formsインスタンス上のフォルダーに変換するフォームをアップロードします。

1. AEM Forms フォームインスタンスにログインします。

1. Tap **[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. タップ **[!UICONTROL Create]**> **[!UICONTROL Folder]**. フォルダ **ーのタイ** トル **** と名前を指定します。 タップ **[!UICONTROL Create]**. フォルダが作成されます。
1. をタップして、新しく作成したフォルダーを開きます。
1. タップ **[!UICONTROL Create]**> **[!UICONTROL File Upload]**. アップロードするフォームを選択し、をクリッ **[!UICONTROL Open]**&#x200B;クしてをクリックしま **[!UICONTROL Upload]**&#x200B;す。 フォームがアップロードされます。

### 変換の実行 {#run-the-conversion}

フォームをアップロードし、サービスを設定した後、次の手順を実行して変換を開始します。

1. AEM Formsインスタンスで、変換設定ダイアログ **[!UICONTROL Adobe Experience Manager]** / ![/をタ](assets/adobeexperiencemanager.png) ップし **[!UICONTROL Navigation]** ます ![](assets/compass.png)**[!UICONTROL Forms]****[!UICONTROL Forms & Documents]**。
1. PDFフォーム（変換するフォーム）を含むフォームまたはフォルダーを選択し、をタップしま **[!UICONTROL Start Automated Conversion]**&#x200B;す。 The **[!UICONTROL Conversion Settings]** dialog appears.

   ![設定の指定](assets/conversion-settings-dialog.png)

1. [変換設定] **[!UICONTROL Basic]** ダイアログのタブで、次の操作を行います。

   * **[!UICONTROL Select a cloud configuration]** です。設定を選択すると、デフォルトのテンプレートとテーマが既に指定されています。 必要に応じて、別のテンプレートまたはテーマを指定できます。
   * 生成されたアダプティブフォームと対応するスキーマを保存する場所を指定します。 デフォルトのパスを使用するか、カスタムパスを指定できます。
   * 「データモ **デルの連結なしでアダプティブフォームを生成」オプションを使用して** 、データモデルの連結を使用してアダプティブフォームを生成するか、データモデルの連結を使用しないかを選択します。
このオプションを選択しない場合、変換サービスはアダプティブフォームをJSONスキーマに自動的に関連付け、アダプティブフォームで使用可能なフィールドとJSONスキーマの間にデータ連結を作成します。 このフィ **[!UICONTROL Save generated data model schema at]** ールドには、生成されたJSONスキーマを保存するデフォルトの場所が表示されます。 また、生成されたスキーマを保存する場所をカスタマイズすることもできます。
このオプションを選択すると、変換サービスはデータモデルの連結なしのアダプティブフォームを生成します。 変換が成功したら、アダプティブフォームをフォームデータモデル、XMLスキーマ、またはJSONスキーマに関連付けることができます。 For more information, see [Creating an adaptive form](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html).
   <!--
   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. 変換設定ダ **[!UICONTROL Additional]** イアログのタブで、
   * 変換サービスで、 **[!UICONTROL Extract fragment from adaptive forms]** 変換されたフォームのフォームフラグメントを識別、抽出、およびダウンロードできるようにするには、このオプションを選択します。 このオプションを選択する **[!UICONTROL Extract fragment from adaptive forms]** と、抽出したフォームフラグメントと対応するフォームフラグメントスキーマの保存パスを指定するオプションが有効になります。
   * 既存のJSONスキーマベースのフ **[!UICONTROL existing adaptive form fragments]**&#x200B;ラグメントとスキーマの少ないアダプティブフォームフラグメントが存在し、これらのフラグメントを自動生成されたアダプティブフォームで使用する場合は、の場所を指定します。 変換サービスは、使用可能なJSONスキーマベースおよびスキーマの少ないアダプティブフォームフラグメントを入力PDFフォーム（非インタラクティブPDFフォームのみ）と照合し、一致がある場合は、対応するアダプティブフォームで使用します。
   >[!NOTE]
   >
   >
   > * 一度に使用できるのは、 **[!UICONTROL  Extract Fragment]** または **[!UICONTROL Use existing adaptive form fragments]** オプションのみです。 両方のオプションを同時に使用することはできません。
   > * このオプションは、非イン **[!UICONTROL Use existing adaptive form fragments]** タラクティブPDFフォームでのみ使用できます。 その他のフォームタイプはまだサポートされていません。
   > * 自動変換サービスでは、連結されていないフラグメントまたはJSONスキーマに連結されたフラグメントのみを使用できます。 XFAフラグメントは使用しないでください。 XFAフラグメントはサポートされていません。


   * デスクトップ **[!UICONTROL Auto-detect multi-column layout of input forms]** やラップトップなどの大画面用にソースフォームのレイアウトを保持する場合は、このオプションを選択します。 このオプションは、ソースフォームの複数列レイアウトを保持する場合に役立ちます。 例えば、ソースPDFに2列レイアウトが含まれている場合、サービスは、大画面表示用に2列レイアウト、携帯電話などの小画面デバイス用に1列レイアウトを含む出力アダプティブフォームを生成します。 この機能には、データソースのスキーマ構造に関する既知の問題がいくつかあります。 詳しくは、既知の問題の記事 [を参照してください](known-issues.md) 。
   * デフォルトでは、PDFフォームの各ページに対して別々のトップレベルパネルが作成されます。 このオプションを使用して、ページレ **[!UICONTROL Auto-detect logical sections]** ベルのパネル（ページ番号ベースのパネル）をドロップし、論理パネルのみを作成できるようになりました。 また、前の論理セクションを持つセクションに属さないフィールドと、隣接する2つのページにまたがる論理セクションのフィールドを1つの論理セクションにクラブします。 例えば、論理セクションの一部のフィールドがページ1の最後にあり、一部がページ2の先頭にある場合、これらのフィールドはすべて1つの論理セクションに分類されます。

      >[!NOTE]
      > この機能を使用するには、コネクタパッケージ1.1.38以降が必要 **[!UICONTROL Auto-detect logical sections]** です。



1. タップ **[!UICONTROL Start Conversion]**. 変換が開始されます。 変換の進行状況は、変換が進行するまで、フォルダーまたはフォームに表示されます。 メッセージは、変換が完了した後、別のステータスメッセージ（変換済み、部分的に変換済み、または変換に失敗した）に置き換えられます。 コンバージョンの完了時に、設定済みの電子メールアドレスにステータスの電子メールも送信されます。

   * 変換が成功すると、変換されたアダプティブフォームと関連するスキーマが、変換ダイアログのタブで指定されたパ **[!UICONTROL Basic]** スにダウンロードされます。 変換を開始する前に「フラグメントを抽出」オプションが選択されている場合にのみ、フォームフラグメントと対応するスキーマがダウンロードされます。
   * 変換に失敗した場合、すべての入力フ **[!UICONTROL Conversion Failed]** ォームが変換に失敗した場合、または変換に失敗した入力フォームの一部のみが表示された場合に、メッセージが表示さ **[!UICONTROL Partially Failed]** れます。 設定した電子メールアドレスにステータス [電子メールが送信され](configure-service.md#configureemailnotification) 、エラーがerror.logファイルに記録されます。
   XFAベースのPDFフォームをアダプティブフォームに変換する場合、変換サービスは、PDFフォームをレコードのドキュメントテンプレートとして変換されたアダプティブフォームに自動的に関連付けます。 変換後は、アダプティブフォームのプロパティを開いて、タブのセクションにレコードのドキュメントテンプレートを表 **[!UICONTROL Document of Record Template Configuration]** 示することがで **[!UICONTROL Form Model]** きます。 </br>

   変換サービスは、////オプションを有効にした場合にのみ、PDFフォームをレコードのドキュメントテンプレートとして変換済みのアダプティブフォームに自動的にアップロード **[!UICONTROL Tools]** し **[!UICONTROL Cloud Services]****[!UICONTROL Automated Forms Conversion Configuration]****[!UICONTROL Properties of selected configuration]****[!UICONTROL Advanced]****[!UICONTROL Generate Document of Record]** ます。

   <!--
   Comment Type: draft

   <note type="note">
   <p>By default, the adaptive form produces a JSON schema instead of XML schema on submission. JSON schema of a converted adaptive form is complaint with XML schema of an XFA-based form. You can use the <a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString">org.apache.sling.commons.json.xml API</a> to convert a JSON schema to XML schema. You can also use the following sample code for conversion:</p>
   <p><code class="code">import org.apache.sling.commons.json.JSONException;
   <discoiqbr /> import org.apache.sling.commons.json.JSONObject;
   <discoiqbr /> import org.apache.sling.commons.json.xml.XML;
   <discoiqbr />
   <discoiqbr /> public class ConversionUtils {
   <discoiqbr />
   <discoiqbr /> public static String jsonToXML(String jsonString) throws JSONException {
   <discoiqbr /> //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
   <discoiqbr /> //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
   <discoiqbr /> //Note: Need to extract boundData part before converting to XML
   <discoiqbr /> return XML.toString(new JSONObject(jsonString));
   <discoiqbr /> }
   <discoiqbr /> }</code><br /> </p>
   </note>
   -->

   >[!NOTE]
   >
   >変換処理に60分以上かかり、PDFフォームがまだアダプティブフォームに変換されていない場合は、AEM Formsインスタンスで新しいフォルダーを作成し、新しく作成したフォルダーにPDFフォームをアップロードし、変換を再開します。

## 変換されたフォームの確認と修正 {#review-and-correct-the-converted-forms}

実世界のフォームには複雑なデータ取得要件があります。 自動変換が完了すると、顧客はフォームの変換の質を確認し、フォームを必要に応じて更新できます。 AEM Formsでは、必要な変更を行うた [めのレビューおよび修正](review-correct-ui-edited.md) (Review And Correct Editor)を提供しています。 これにより、フォームフィールドの自動識別を改善し、識別されたフィールドを別の種類に変換できます。 例えば、フォームの2列レイアウトを特定し、ラジオボタンとして自動的に識別されるフィールドを複数選択フィールドに変更する場合に役立ちます。

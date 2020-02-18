---
title: 'PDFフォームからアダプティブフォームへの変換 '
seo-title: 'PDFフォームからアダプティブフォームへの変換 '
description: Automated Forms Conversionサービスを実行してPDFフォームをアダプティブフォームに変換する
seo-description: Automated Forms Conversionサービスを実行してPDFフォームをアダプティブフォームに変換する
uuid: 49fcd5c0-0e72-496d-9831-00f79d582f57
contentOwner: khsingh
topic-tags: forms
discoiquuid: 9358219c-6079-4552-92b9-b427a23811af
translation-type: tm+mt
source-git-commit: bbf39e3bae55654f92a50f52a22cee5da938236d

---


# PDFフォームからアダプティブフォームへの変換 {#convert-print-forms-to-adaptive-forms}

Adobe SenseiによるAEM Forms自動フォーム変換サービスは、PDFフォームをデバイスに対応したレスポンシブなアダプティブフォームに自動的に変換します。 非インタラクティブPDFフォーム、Acro Forms、XFAベースのPDFフォームのどちらを使用している場合でも、自動フォーム変換サービスでは、これらのフォームをアダプティブフォームに簡単に変換できます。 機能、コンバージョンワークフロー、およびオンボーディング情報について詳しくは、「自動フォームコンバ [ージョンサービス](introduction.md) 」を参照してください。

## 前提条件 {#pre-requisites}

* [**コンバージョンサービスの設定&#x200B;**](configure-service.md)

* **[変換されたフォ](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html)ームに適用する** 、テンプレートを準備します。テンプレートを使用すると、すべてのアダプティブフォームに一貫したブランドを適用できます。 また、Automated Forms Conversionサービスでは、ソースPDFドキュメントのヘッダーとフッターを抽出して使用することはできません。 アダプティブフォームテンプレートを使用して、ヘッダーとフッターを指定できます。 テンプレートで指定されたヘッダーとフッターは、変換中にアダプティブフォームに適用されます。

* **[変換されたフ](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html)ォームに** 、適用するテーマを準備します。テーマを使用すると、組織のアダプティブフォームすべてに一貫したスタイルを適用できます。

## 変換プロセスの開始 {#start-the-conversion-process}

AEMインスタンスをAEM Forms Conversion Serviceに接続した後、PDFフォームをアダプティブフォームに変換できます。 フォームを変換するには、次の手順をリストの順序で実行します。

* [PDFフォームをAEM Formsサーバーにアップロードする](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [コンバージョンの実行](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [変換されたフォームの確認と修正](review-correct-ui-edited.md)

### PDFフォームをAEM Formsサーバーにアップロードする {#upload-pdf-forms-to-your-aem-forms-server}

変換サービスは、AEM Formsインスタンスで使用可能なPDFフォームをアダプティブフォームに変換します。 必要に応じて、すべてのPDFフォームを一度に、または段階的にアップロードできます。 フォームをアップロードする前に、次の点を考慮してください。

* フォルダー内のフォーム数は15未満にし、フォルダー内の合計ページ数は50未満にします。
* フォルダーのサイズを10 MB未満にします。 フォームをサブフォルダーに保持しないでください。
* フォームのページ数は15未満にします。
* 保護されたフォームはアップロードしないでください。 サービスは、パスワードで保護されたフォームと保護されたフォームを変換しません。
* ファイル名にスペースを含むソースフォームはアップロードしないでください。 フォームをアップロードする前に、ファイル名からスペースを削除します。
* [PDFポートフォリオはアップロードしない](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 このサービスは、PDFポートフォリオをアダプティブフォームに変換しません。
* 「既知の問題 [」、「ベストプラ](known-issues.md) クティスと考慮事項 [](styles-and-pattern-considerations-and-best-practices.md) 」の節を読み、推奨される変更をフォームに加えます。

変換するフォームをAEM Formsインスタンス上のフォルダーにアップロードするには、次の手順を実行します。

1. AEM Forms フォームインスタンスにログインします。

1. Tap **[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. タップ **[!UICONTROL Create]**> **[!UICONTROL Folder]**. フォルダ **ーのタイ** トルと名前 **(Name** )を指定します。 タップ **[!UICONTROL Create]**. フォルダが作成されます。
1. をタップして、新しく作成したフォルダーを開きます。
1. タップ **[!UICONTROL Create]**> **[!UICONTROL File Upload]**. アップロードするフォームを選択し、をクリッ **[!UICONTROL Open]**&#x200B;クして、をクリックしま **[!UICONTROL Upload]**&#x200B;す。 フォームがアップロードされます。

### コンバージョンの実行 {#run-the-conversion}

フォームをアップロードし、サービスを設定した後、次の手順を実行して変換を開始します。

1. AEM Formsインスタンスで、変換設定ダイアロ **[!UICONTROL Adobe Experience Manager]** グ ![/](assets/adobeexperiencemanager.png) / **[!UICONTROL Navigation]** をタ ![](assets/compass.png) ップしま **[!UICONTROL Forms]****[!UICONTROL Forms & Documents]**&#x200B;す。
1. PDFフォーム（変換するフォーム）を含むフォームまたはフォルダーを選択し、をタップしま **[!UICONTROL Start Automated Conversion]**&#x200B;す。 The **[!UICONTROL Conversion Settings]** dialog appears.

   ![設定の指定](assets/conversion-settings-dialog.png)

1. [変換設定] **[!UICONTROL Basic]** ダイアログのタブで、次の操作を行います。

   * **[!UICONTROL Select a cloud configuration]** です。設定を選択すると、デフォルトのテンプレートとテーマが既に指定されています。 必要に応じて、別のテンプレートまたはテーマを指定できます。
   * 生成されたアダプティブフォームと対応するスキーマを保存する場所を指定します。 デフォルトのパスを使用するか、カスタムパスを指定できます。
   * 「データモ **デルの連結なしでアダプティブフォームを生成する」オプションを使用して** 、データモデルの連結を使用してアダプティブフォームを生成するか、使用しないかを選択します。
このオプションを選択しない場合、変換サービスはアダプティブフォームをJSONスキーマに自動的に関連付け、アダプティブフォームで使用可能なフィールドとJSONスキーマの間にデータ連結を作成します。 このフィ **[!UICONTROL Save generated data model schema at]** ールドには、生成されたJSONスキーマを保存するデフォルトの場所が表示されます。 また、生成されたスキーマを保存する場所をカスタマイズすることもできます。
このオプションを選択すると、変換サービスはデータモデルの連結なしのアダプティブフォームを生成します。 変換が成功したら、アダプティブフォームをフォームデータモデル、XMLスキーマ、またはJSONスキーマに関連付けることができます。 For more information, see [Creating an adaptive form](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html).
   <!--
   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. [変換設 **[!UICONTROL Additional]** 定]ダイアログのタブで、
   * 変換サービスで **[!UICONTROL Extract fragment from adaptive forms]** 変換済みフォームのフラグメントを識別、抽出、ダウンロードできるようにするには、このオプションを選択します。 このオプションを選択する **[!UICONTROL Extract fragment from adaptive forms]** と、抽出したフォームフラグメントと対応するフォームフラグメントスキーマを保存するためのパスを指定するオプションが有効になります。
   * 既存のJSONスキーマベースのフ **[!UICONTROL existing adaptive form fragments]**&#x200B;ラグメントが存在し、スキーマの少ないアダプティブフォームフラグメントが存在し、これらのフラグメントを自動生成されたアダプティブフォームで使用する場合は、の場所を指定します。 コンバージョンサービスは、使用可能なJSONスキーマベースと、入力PDFフォーム（非インタラクティブPDFフォームのみ）を持つスキーマの少ないアダプティブフォームフラグメントを照合し、一致したアダプティブフォームフラグメントを対応するアダプティブフォームで使用します。
   >[!NOTE]
   >
   >
   > * 一度に使用できるのは、 **[!UICONTROL  Extract Fragment]** または **[!UICONTROL Use existing adaptive form fragments]** オプションのみです。 両方のオプションを同時に使用することはできません。
   > * このオプションは、非イン **[!UICONTROL Use existing adaptive form fragments]** タラクティブPDFフォームでのみ使用できます。 その他のフォームタイプはまだサポートされていません。
   > * 自動変換サービスでは、連結されていないフラグメントまたはJSONスキーマに連結されたフラグメントのみを使用できます。 XFAフラグメントは使用しないでください。 XFAフラグメントはサポートされていません。


   * デスクトップ **[!UICONTROL Auto-detect multi-column layout of input forms]** やラップトップなどの大画面用にソースフォームのレイアウトを維持する場合は、このオプションを選択します。 このオプションは、ソースフォームの複数列レイアウトを保持する場合に役立ちます。 例えば、ソースPDFに2列レイアウトが含まれる場合、サービスは、大画面表示用に2列レイアウト、携帯電話などの小画面デバイス用に1列レイアウトを含む出力アダプティブフォームを生成します。 この機能には、データソーススキーマ構造に関する既知の問題があります。 詳しくは、既知の問題に関する [記事を参照してください](known-issues.md) 。



1. タップ **[!UICONTROL Start Conversion]**. 変換が開始されます。 変換の進行状況は、変換が進行中になるまで、フォルダーまたはフォームに表示されます。 メッセージは、変換が完了した後、別のステータスメッセージ（変換済み、部分的に変換済み、または変換に失敗）に置き換えられます。 コンバージョンの完了時に、設定済みの電子メールアドレスにステータス電子メールも送信されます。

   * 変換に成功すると、変換されたアダプティブフォームと関連するスキーマが、変換ダイアログのタブで指定されたパ **[!UICONTROL Basic]** スにダウンロードされます。 フォームフラグメントと対応するスキーマは、変換を開始する前に「フラグメントを抽出」オプションが選択されている場合にのみダウンロードされます。
   * 変換に失敗した場合、すべての入力フォーム **[!UICONTROL Conversion Failed]** が変換に失敗した場合、またはすべての入力フォームの一部のみが変換に失敗した場合にメッセージが表示され **[!UICONTROL Partially Failed]** ます。 設定した電子メールアドレスにステータス [電子メールが送信され](configure-service.md#configureemailnotification) 、error.logファイルにエラーが記録されます。
   XFAベースのPDFフォームをアダプティブフォームに変換する場合、変換サービスは、PDFフォームをレコードのドキュメントテンプレートとして変換されたアダプティブフォームに自動的に関連付けます。 変換後は、アダプティブフォームのプロパティを開いて、タブのセクションにレコードのドキュメントテンプレートを表 **[!UICONTROL Document of Record Template Configuration]** 示することがで **[!UICONTROL Form Model]** きます。 </br>

   変換サービスは、////オプションを有効にした場合にのみ、PDFフォームをレコードのドキュメントテンプレートとして変換済みのアダプティブフォームに自動的にアップロ **[!UICONTROL Tools]** ード **[!UICONTROL Cloud Services]** し **[!UICONTROL Automated Forms Conversion Configuration]****[!UICONTROL Properties of selected configuration]****[!UICONTROL Advanced]****[!UICONTROL Generate Document of Record]** ます。

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
   >変換処理に60分以上かかり、PDFフォームがまだアダプティブフォームに変換されていない場合は、AEM formsインスタンスで新しいフォルダーを作成し、新しく作成したフォルダーにPDFフォームをアップロードして、変換を再開します。

## 変換されたフォームの確認と修正 {#review-and-correct-the-converted-forms}

実世界のフォームには複雑なデータ取得要件があります。 自動変換が完了すると、顧客はフォームの変換品質を確認し、フォームを必要に応じて更新できます。 AEM Formsは、必要な変更を行うた [めのレビューと修正](review-correct-ui-edited.md) のエディターを提供します。 これにより、フォームフィールドの自動識別を改善し、識別されたフィールドを別の型に変換することができます。 例えば、フォームの2列レイアウトを特定し、ラジオボタンとして自動的に識別されるフィールドを複数選択フィールドに変更する場合に役立ちます。

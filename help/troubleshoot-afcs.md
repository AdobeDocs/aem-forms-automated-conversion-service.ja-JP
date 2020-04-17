---
title: 'Automated Forms Conversion Serviceのトラブルシューティング '
seo-title: 'Automated Forms Conversion Service(AFCS)のトラブルシューティング '
description: '一般的なAFCSの問題とその解決策 '
seo-description: 一般的なAFCSの問題とその解決策
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 56e4696c0372223e0b27f1c313382a2a637b6db1

---


# Automated Forms Conversion Serviceのトラブルシューティング


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## 一般的なエラー {#commonerrors}

<!--
|Error|Example|
|--- |--- |
|**Error Message** <br> The access token header is not available. <br><br>**Reason** <br> An administrator has created multiple IMS configurations or IMS configuration is not able to reach AFCS service on Adobe Cloud. <br><br>**Resolution** <br> If there are multiple configurations, delete all the configurations and [create a new configuration](configure-service.md#obtainpubliccertificates). <br> If there is a single configuration, use **[!UICONTROL Health Check]** to [check connectivity](configure-service.md#createintegrationoption).|![The access token header is not available](assets/invalid-ims-configuration.png)|
|**Error Message** <br> Unable to connect to the service.  <br><br>**Reason** <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service cloud services. <br><br>**Resolution** <br> Correct [Service URL](configure-service.md#configure-the-cloud-service) in Automated Forms Conversion Service Cloud services.|![Unable to connect to the service.](assets/wrong-endpoint-configured.png)|
|**Error Message** <br> The service failed to convert the form.  <br><br>**Reason** <br> Network connectivity issues at your end, the service is down due to scheduled maintenance, or outage on Adobe Cloud. <br><br>**Resolution** <br> Resolve network connectivity issues at your end and check the status of the service on https://status.adobe.com/ for a planned or unplanned outage.|![Unable to connect to the service.](assets/service-failure.png)|
|**Error Message** <br> The number of pages is more than 15.  <br><br>**Reason** <br> The source form is more than 15 pages long.  <br><br>**Resolution** <br> Use Adobe Acrobat to split forms with more than 15 pages. Bring the number of pages in a form to less than 15. |![Unable to connect to the service.](assets/number-of-pages.png)|
|**Error Message** <br> The number of files is more than 15.  <br><br>**Reason** <br>  The folder contains more than 15 forms. <br><br>**Resolution** <br> Bring the number of forms in a folder to less than or equal to 15. Bring the total number of pages in a folder less than 50. Bring the size of the folder to less than 10 MB. Do not keep forms in a sub-folder. Organize source forms into a batch of 8-15 forms. |![Unable to connect to the service.](assets/number-of-pages.png)|
|**Error Message** <br> The source file format is not supported.  <br><br>**Reason** <br> The folder containing source forms have some unsupported files. <br><br>**Resolution** <br> The service supports only .xdp and .pdf files. Remove files with any other extension from the folder and run the conversion. |![Unable to connect to the service.](assets/unsupported-file-formats.png)|
|**Error Message** <br> Scanned forms are not supported.  <br><br>**Reason** <br> The PDF form contains only scanned images of the form and contains no content structure. <br><br>**Resolution** <br> The service does not support converting scanned forms or an image of a form to an adaptive out-of-the-box. However, you use Adobe Acrobat to convert the image of a form to a PDF Form. Then, use the service to convert the PDF Form to an adaptive form. Always use a high-quality image of the form for conversion in Acrobat. It improves the quality of the conversion. |![Unable to connect to the service.](assets/scanned-forms-error.png)|
|**Error Message** <br> Encrypted PDF form is not supported.  <br><br>**Reason** <br> The folder contains encrypted PDF forms. <br><br>**Resolution** <br> The service does not support converting an encrypted PDF form to an adaptive form. Remove the encryption, upload the non-encrypted form, and run the conversion. |![Unable to connect to the service.](assets/secured-pdf-form.png)|
|**Error Message** <br> Unable to parse meta-model JSON schema.  <br><br>**Reason** <br> The JSON schema supplied to the service is not properly formatted, contains invalid characters, or uses invalid syntax to map components.  <br><br>**Resolution** <br> Check the formatting of the JSON file. You can use any online JSON validator to check the formatting and structure of the schema. See, [Extend the default meta-model](extending-the-default-meta-model.md) article for information on meta-model syntax. |![Unable to connect to the service.](assets/invalid-meta-model-schema.png)| -->

<table>
<thead>
<tr>
<th>エラー</th>
<th>例</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>エラーメッセージ</strong> :アクセストークン <br> ・ヘッダーは使用できません。 <br><br><strong>理由</strong><br> 管理者が複数のIMS設定を作成したか、IMS設定がAdobe CloudのAFCSサービスに到達できない。 <br><br><strong>解決</strong> ：複数の設定がある場合は、すべての設定を削除し、 <br> 新しい設定を作成します <a href="configure-service.md#obtainpubliccertificates"></a>。 <br> 構成が1つだけの場合は、[!UICONTROL Health Check] <strong>を使用して接続を確認</strong> し <a href="configure-service.md#createintegrationoption">ます</a>。</td>
<td><img alt="アクセストークンヘッダーが使用できません" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>エラーメッセージ</strong><br> ：サービスに接続できません。  <br><br><strong>Reason</strong> Incorrect service URL <br> , or no service URL is montioned in Automated Forms Conversion Service cloud services. <br><br><strong>Automated</strong> Forms Conversion Service <br><a href="configure-service.md#configure-the-cloud-service"></a> Cloudサービスでの解決の正しいサービスURL。</td>
<td><img alt="サービスに接続できません。" src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>エラーメッセージ</strong><br> ：サービスはフォームを変換できませんでした。  <br><br><strong>Reason</strong><br> Network connectivity issubes to your end, the service is down buide to scheduled maintenance, or outame on Adobe Cloud. <br><br><strong>解決</strong> ：ネットワーク接続に関する問題を解決し、https://status.adobe.com/でサービスの状態を確認し <br> てください <a href="https://status.adobe.com/"></a> 。計画的または予期しない停止が発生した場合は、</td>
<td><img alt="サービスはフォームを変換できませんでした。" src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>エラーメッセージ</strong><br> ：ページ数が15を超えています。  <br><br><strong>理由</strong><br> ソースフォームの長さが15ページを超えています。  <br><br><strong>解決</strong><br> :Adobe Acrobatを使用して、15ページを超えるフォームを分割します。 フォームのページ数を15未満にします。</td>
<td><img alt="ページ数が15を超えています。" src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>エラーメッセージ</strong><br> ：ファイルの数が15を超えています。  <br><br><strong>Reason</strong> ：フォ <br> ルダーに15を超えるフォームが含まれています。 <br><br><strong>解決</strong><br> フォルダー内のフォーム数を15以下にします。 フォルダー内の合計ページ数を50未満にします。 フォルダーのサイズを10 MB未満にします。 サブフォルダー内にフォームを保存しないでください。ソースフォームを8 ～ 15個のフォームのバッチに整理します。</td>
<td><img alt="ファイルの数が15を超えています。" src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>エラーメッセージ</strong><br> ：ソースファイルの形式がサポートされていません。  <br><br><strong>理由</strong><br> ：ソースフォームを含むフォルダーに、サポートされていないファイルがいくつか含まれています。 <br><br><strong>解決</strong><br> ：サービスは.xdpファイルと.pdfファイルのみをサポートします。 その他の拡張子の付いたファイルをフォルダーから削除し、変換を実行します。</td>
<td><img alt="ソースファイルの形式がサポートされていません。" src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> Scanned forms <br> are not supported.  <br><br><strong>理由</strong><br> : PDFフォームには、スキャンされたフォームの画像のみが含まれ、コンテンツ構造が含まれていません。 <br><br><strong>解決</strong><br> ：サービスは、スキャンされたフォームやフォームの画像をアダプティブフォームに変換する機能をサポートしていません。 ただし、Adobe Acrobat を使用して、画像だけのフォームを PDF フォームに変換することはできます。 次に、変換サービスを使用して、この PDF フォームをアダプティブフォームに変換します。 Acrobat で変換を行う場合は、必ず品質の高い画像を使用するようにしてください。 これにより、変換後のフォームの品質が高くなります。</td>
<td><img alt="スキャンされたフォームはサポートされていません。" src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong><br> Encrypted PDFフォームはサポートされていません。  <br><br><strong>Reason</strong><br> ：フォルダーに暗号化されたPDFフォームが含まれています。 <br><br><strong>解決</strong><br> ：サービスは、暗号化されたPDFフォームからアダプティブフォームへの変換をサポートしていません。 暗号化を削除し、非暗号化フォームをアップロードし、変換を実行します。</td>
<td><img alt="暗号化されたPDFフォームはサポートされていません。" src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>エラーメッセージ</strong><br> ：メタモデルJSONスキーマを解析できません。  <br><br><strong>理由</strong><br> ：サービスに指定されたJSONスキーマが正しい形式ではないか、無効な文字が含まれているか、無効な構文を使用してコンポーネントをマッピングしています。  <br><br><strong>解決</strong><br> : JSONファイルの形式を確認します。 任意のオンラインJSONバリデーターを使用して、スキーマの形式と構造を確認できます。 メタモデルの <a href="extending-the-default-meta-model.md">構文について詳しくは、</a> Extend the default meta-modelの記事を参照してください。</td>
<td><img alt="メタモデルJSONスキーマ" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>

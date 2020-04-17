---
title: 'Automated Forms Conversion Serviceのトラブルシューティング '
seo-title: 'Automated Forms Conversion Service(AFCS)のトラブルシューティング '
description: '一般的なAFCSの問題とその解決策 '
seo-description: 一般的なAFCSの問題とその解決策
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 8d640b7d55a31bcdf425d7fd91f2465912da679b

---


# Automated Forms Conversion Serviceのトラブルシューティング


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## 一般的なエラー {#commonerrors}

| エラー | 例 |
|--- |--- |
| **エラーメッセージ** :アクセストークン <br> ・ヘッダーは使用できません。 <br><br>**理由&#x200B;**<br>管理者が複数のIMS設定を作成したか、IMS設定がAdobe CloudのAFCSサービスに到達できない。<br><br>**解決** ：複数の設定がある場合は、すべての設定を削除し、 <br> 新しい設定を作成します [](configure-service.md#obtainpubliccertificates)。 <br> 設定が1つだけの場合は、ヘルスチェック **を使用し** 、接続を [確認します](configure-service.md#createintegrationoption)。 | ![アクセストークンヘッダーが使用できません](assets/invalid-ims-configuration.png) |
| **エラーメッセージ**<br> ：サービスに接続できません。  <br><br>**Reason **Incorrect service URL<br>, or no service URL is montioned in Automated Forms Conversion Service cloud services.<br><br>**Automated** Forms Conversion Service <br>[](configure-service.md#configure-the-cloud-service) Cloudサービスでの解決の正しいサービスURL。 | ![サービスに接続できません。](assets/wrong-endpoint-configured.png) |
| **エラーメッセージ**<br> ：サービスはフォームを変換できませんでした。  <br><br>**Reason **<br>Network connectivity issubes to your end, the service is down buide to scheduled maintenance, or outame on Adobe Cloud.<br><br>**解決方法**<br> ：ネットワーク接続に関する問題を解決し、計画的または予期しない停止が発生した場合は、https://status.adobe.com/でサービスのステータスを確認します。 | ![サービスに接続できません。](assets/service-failure.png) |
| **エラーメッセージ**<br> ：ページ数が15を超えています。  <br><br>**理由&#x200B;**<br>ソースフォームの長さが15ページを超えています。<br><br>**解決**<br> :Adobe Acrobatを使用して、15ページを超えるフォームを分割します。 フォームのページ数を15未満にします。 | ![サービスに接続できません。](assets/number-of-pages.png) |
| **エラーメッセージ**<br> ：ファイルの数が15を超えています。  <br><br>**Reason **：フォ<br>ルダーに15を超えるフォームが含まれています。<br><br>**解決**<br> フォルダー内のフォーム数を15以下にします。 フォルダー内の合計ページ数を50未満にします。 フォルダーのサイズを10 MB未満にします。 サブフォルダー内にフォームを保存しないでください。ソースフォームを8 ～ 15個のフォームのバッチに整理します。 | ![サービスに接続できません。](assets/number-of-pages.png) |
| **エラーメッセージ**<br> ：ソースファイルの形式がサポートされていません。  <br><br>**理由&#x200B;**<br>：ソースフォームを含むフォルダーに、サポートされていないファイルがいくつか含まれています。<br><br>**解決**<br> ：サービスは.xdpファイルと.pdfファイルのみをサポートします。 その他の拡張子の付いたファイルをフォルダーから削除し、変換を実行します。 | ![サービスに接続できません。](assets/unsupported-file-formats.png) |
| **Error Message** Scanned forms <br> are not supported.  <br><br>**理由&#x200B;**<br>: PDFフォームには、スキャンされたフォームの画像のみが含まれ、コンテンツ構造が含まれていません。<br><br>**解決**<br> ：サービスは、スキャンされたフォームやフォームの画像をアダプティブフォームに変換する機能をサポートしていません。 ただし、Adobe Acrobat を使用して、画像だけのフォームを PDF フォームに変換することはできます。 次に、変換サービスを使用して、この PDF フォームをアダプティブフォームに変換します。 Acrobat で変換を行う場合は、必ず品質の高い画像を使用するようにしてください。 これにより、変換後のフォームの品質が高くなります。 | ![サービスに接続できません。](assets/scanned-forms-error.png) |
| **Error Message**<br> Encrypted PDFフォームはサポートされていません。  <br><br>**Reason **<br>：フォルダーに暗号化されたPDFフォームが含まれています。<br><br>**解決**<br> ：サービスは、暗号化されたPDFフォームからアダプティブフォームへの変換をサポートしていません。 暗号化を削除し、非暗号化フォームをアップロードし、変換を実行します。 | ![サービスに接続できません。](assets/secured-pdf-form.png) |
| **エラーメッセージ**<br> ：メタモデルJSONスキーマを解析できません。  <br><br>**理由&#x200B;**<br>：サービスに指定されたJSONスキーマが正しい形式ではないか、無効な文字が含まれているか、無効な構文を使用してコンポーネントをマッピングしています。<br><br>**解決**<br> : JSONファイルの形式を確認します。 任意のオンラインJSONバリデーターを使用して、スキーマの形式と構造を確認できます。 メタモデルの [構文について詳しくは、](extending-the-default-meta-model.md) Extend the default meta-modelの記事を参照してください。 | ![サービスに接続できません。](assets/invalid-meta-model-schema.png) |

<!--

<table>
<thead>
<tr>
<th>Error</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Error Message</strong> <p> The access token header is not available. </p><br><strong>Reason</strong> <br> An administrator has created multiple IMS configurations or IMS configuration is not able to reach AFCS service on Adobe Cloud. <br><br><strong>Resolution</strong> <br> If there are multiple configurations, delete all the configurations and <a href="configure-service.md#obtainpubliccertificates">create a new configuration</a>. <br> If there is a single configuration, use <strong> Health Check </strong> to <a href="configure-service.md#createintegrationoption">check connectivity</a>.</td>
<td><img alt="The access token header is not available" src="assets/invalid-ims-configuration.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to connect to the service.  <br><br><strong>Reason</strong> <br> Incorrect service URL or no service URL is mentioned in Automated Forms Conversion Service cloud services. <br><br><strong>Resolution</strong> <br> Correct <a href="configure-service.md#configure-the-cloud-service">Service URL</a> in Automated Forms Conversion Service Cloud services.</td>
<td><img alt="Unable to connect to the service." src="assets/wrong-endpoint-configured.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The service failed to convert the form.  <br><br><strong>Reason</strong> <br> Network connectivity issues at your end, the service is down due to scheduled maintenance, or outage on Adobe Cloud. <br><br><strong>Resolution</strong> <br> Resolve network connectivity issues at your end and check the status of the service on <a href="https://status.adobe.com/">https://status.adobe.com/</a> for a planned or unplanned outage.</td>
<td><img alt="The service failed to convert the form." src="assets/service-failure.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of pages is more than 15.  <br><br><strong>Reason</strong> <br> The source form is more than 15 pages long.  <br><br><strong>Resolution</strong> <br> Use Adobe Acrobat to split forms with more than 15 pages. Bring the number of pages in a form to less than 15.</td>
<td><img alt="The number of pages is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The number of files is more than 15.  <br><br><strong>Reason</strong> <br>  The folder contains more than 15 forms. <br><br><strong>Resolution</strong> <br> Bring the number of forms in a folder to less than or equal to 15. Bring the total number of pages in a folder less than 50. Bring the size of the folder to less than 10 MB. Do not keep forms in a sub-folder. Organize source forms into a batch of 8-15 forms.</td>
<td><img alt="The number of files is more than 15." src="assets/number-of-pages.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> The source file format is not supported.  <br><br><strong>Reason</strong> <br> The folder containing source forms have some unsupported files. <br><br><strong>Resolution</strong> <br> The service supports only .xdp and .pdf files. Remove files with any other extension from the folder and run the conversion.</td>
<td><img alt="The source file format is not supported." src="assets/unsupported-file-formats.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Scanned forms are not supported.  <br><br><strong>Reason</strong> <br> The PDF form contains only scanned images of the form and contains no content structure. <br><br><strong>Resolution</strong> <br> The service does not support converting scanned forms or an image of a form to an adaptive out-of-the-box. However, you use Adobe Acrobat to convert the image of a form to a PDF Form. Then, use the service to convert the PDF Form to an adaptive form. Always use a high-quality image of the form for conversion in Acrobat. It improves the quality of the conversion.</td>
<td><img alt="Scanned forms are not supported." src="assets/scanned-forms-error.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Encrypted PDF form is not supported.  <br><br><strong>Reason</strong> <br> The folder contains encrypted PDF forms. <br><br><strong>Resolution</strong> <br> The service does not support converting an encrypted PDF form to an adaptive form. Remove the encryption, upload the non-encrypted form, and run the conversion.</td>
<td><img alt="Encrypted PDF form is not supported." src="assets/secured-pdf-form.png" /></td>
</tr>
<tr>
<td><strong>Error Message</strong> <br> Unable to parse meta-model JSON schema.  <br><br><strong>Reason</strong> <br> The JSON schema supplied to the service is not properly formatted, contains invalid characters, or uses invalid syntax to map components.  <br><br><strong>Resolution</strong> <br> Check the formatting of the JSON file. You can use any online JSON validator to check the formatting and structure of the schema. See, <a href="extending-the-default-meta-model.md">Extend the default meta-model</a> article for information on meta-model syntax.</td>
<td><img alt="Unable to parse meta-model JSON schema" src="assets/invalid-meta-model-schema.png" /></td>
</tr>
</tbody>
</table>
-->
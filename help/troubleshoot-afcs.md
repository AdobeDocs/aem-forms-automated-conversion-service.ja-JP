---
title: '自動フォーム変換サービスのトラブルシューティング '
seo-title: '自動フォーム変換サービス（AFCS）のトラブルシューティング '
description: 'AFCS の一般的な問題とその解決方法 '
seo-description: AFCS の一般的な問題とその解決方法
contentOwner: khsingh
topic-tags: forms
exl-id: e8406ed9-37f5-4f26-be97-ad042f9ca57c
source-git-commit: 5353a071f8633b36fc73c34c5d7629228659e2ba
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 89%

---

# 自動フォーム変換サービスのトラブルシューティング

ここでは、一般的なエラーの基本的なトラブルシューティング手順について説明します。

<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. -->

## 一般的なエラー {#commonerrors}

| エラー | 例 |
|--- |--- |
| **エラーメッセージ** <br> アクセストークンヘッダーを使用できません。 <br><br> **原因** <br> 管理者が複数の IMS 設定を作成しているか、IMS 設定を使用して Adobe Cloud 上 の AFCS サービスにアクセスできません。 <br><br>**解決方法** <br> 設定が複数存在する場合は、すべての設定を削除して、[新しい設定を作成](configure-service.md#obtainpubliccertificates)してください。 <br> 設定が 1 つのみの場合は、 **ヘルスチェック** を使用して、[接続状態を確認](configure-service.md#createintegrationoption)してください。 | ![アクセストークンヘッダーを使用できません](assets/invalid-ims-configurations.png) |
| **エラーメッセージ** <br> サービスに接続できません。  <br><br>**原因** <br> サービス URL が正しくないか、自動フォーム変換サービスのクラウドサービスでサービス URL が指定されていません。 <br><br>**解決方法** <br> 自動フォーム変換サービスのクラウドサービスで[サービス URL](configure-service.md#configure-the-cloud-service) を修正してください。 | ![サービスに接続できません。](assets/wrong-service-url-configured.png) |
| **エラーメッセージ** <br> フォームの変換が失敗しました。  <br><br>**原因** <br> ユーザー側にネットワーク接続の問題が発生しているか、定期メンテナンスのためサービスが停止されているか、Adobe Cloud が停止しています。 <br><br>**解決方法** <br> ユーザー側でネットワーク接続の問題を解決し、https://status.adobe.com/ でサービスが（計画的または計画外に）停止されていないか確認してください。 | ![サービスに接続できません。](assets/conversion-failure.png) |
| **エラーメッセージ** <br> ページ数が 15 ページを超えています。  <br><br>**原因** <br> ソースフォームのページ数が 15 ページを超えています。  <br><br>**解決方法** <br> Adobe Acrobat を使用して、15 ページを超えているフォームを分割してください。 各フォームのページ数は 15 ページ未満にしてください。 | ![サービスに接続できません。](assets/number-of-pages.png) |
| **エラーメッセージ** <br> ファイル数が 15 個を超えています。  <br><br>**原因** <br>  フォルダーに 15 個を超えるフォームが含まれています。 <br><br>**解決方法** <br> フォルダー内のフォーム数を 15 個以内にしてください。 1 つのフォルダーに保存する合計ページ数は 50 ページ未満にしてください。 フォルダーのサイズは 10 MB 未満にしてください。 サブフォルダー内にフォームを保存しないでください。ソースフォームは 8 ～ 15 個のフォームに編成してください。 | ![サービスに接続できません。](assets/number-of-pages.png) |
| **エラーメッセージ** <br> ソースファイル形式がサポートされていません。  <br><br>**原因** <br> ソースフォームが含まれているフォルダーには、サポートされていないファイルがいくつか存在します。 <br><br>**解決方法** <br> このサービスでは .xdp ファイルと .pdf ファイルのみがサポートされます。 その他の拡張子を持つファイルをフォルダーから削除した後、変換を実行してください。 | ![サービスに接続できません。](assets/unsupported-file-formats.png) |
| **エラーメッセージ** <br> スキャンされたフォームはサポートされていません。  <br><br>**原因** <br> PDF フォームにスキャンされたフォームの画像のみが含まれており、コンテンツ構造が存在しません。 <br><br>**解決方法** <br> スキャンされたフォームや画像だけのフォームを、すぐに使用できる形式のアダプティブフォームに変換することはできません。ただし、Adobe Acrobat を使用して、画像だけのフォームを PDF フォームに変換することはできます。 次に、変換サービスを使用して、この PDF フォームをアダプティブフォームに変換します。 Acrobat で変換を行う場合は、必ず品質の高い画像を使用するようにしてください。 これにより、変換後のフォームの品質が高くなります。 | ![サービスに接続できません。](assets/scanned-forms-error.png) |
| **エラーメッセージ**<br> 暗号化された PDF フォームはサポートされていません。  <br><br>**原因**<br> フォルダーに暗号化された PDF フォームが含まれています。 <br><br>**解決方法** <br> 暗号化された PDF フォームをアダプティブフォームに変換することはできません。 暗号を解除し、暗号化されていないフォームをアップロードして、変換を実行してください。 | ![サービスに接続できません。](assets/secured-pdf-form.png) |
| **エラーメッセージ** <br> メタモデル JSON スキーマを解析できません。  <br><br>**原因** <br> サービスに使用されている JSON スキーマが正しい形式ではないか、無効な文字が含まれているか、無効な構文を使用してコンポーネントをマッピングしています。  <br><br>**解決方法** <br> JSON ファイルの形式を確認してください。 任意のオンライン JSON バリデーターを使用して、スキーマの形式と構造を確認できます。 メタモデル構文の詳細については、「[デフォルトメタモデルの拡張](extending-the-default-meta-model.md)」の記事を参照してください。 | ![サービスに接続できません。](assets/invalid-meta-model-schema.png) |
| **エラー（オンプレミス環境のみ）** <br> 「ソー **[!UICONTROL ス言語」オ]** プションにアダプティブフォームの正しい言語がリストされない。<br><br>**** <br> 原因アダプティブフォームのjcr:languageプロパティが正しく設定されていません。<br><br>**** <br> 解決方法CRX-DE liteを開き、に移動し `/content/forms/af/`てノードを開 `jcr:content` き、ノードの値を正しい言語に設定します。サポートされる言語の一覧については、[サポートされていないロケールのローカライゼーションサポートの追加](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html#add-localization-support-for-non-supported-locales)を参照してください。 | ![サービスに接続できません。](assets/aem-forms-translation-project-language-unavailable.png) |

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

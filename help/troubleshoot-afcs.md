---
title: 'Automated Forms Conversion Serviceのトラブルシューティング '
seo-title: 'Automated Forms Conversion Service(AFCS)のトラブルシューティング '
description: '一般的なAFCSの問題とその解決策 '
seo-description: 一般的なAFCSの問題とその解決策
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 0af626e21a0c3d6a7d3c339c0b87179b048092d3

---


# Automated Forms Conversion Serviceのトラブルシューティング


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## 一般的なエラー {#commonerrors}

<table>
<thead>
<tr>
<th>エラー</th>
<th>例</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>エラーメッセージ</strong> :アクセストークン <br> ・ヘッダーは使用できません。 <br><br><strong>理由</strong><br> 管理者が複数のIMS設定を作成したか、IMS設定がAdobe CloudのAFCSサービスに到達できない。 <br><br><strong>解決</strong> ：複数の設定がある場合は、すべての設定を削除し、 <br> 新しい設定を作成します <a href="configure-service.md#obtainpubliccertificates"></a>。 <br> 設定が1つだけの場合は、ヘルスチェックを使 <strong> 用して接 </strong> 続を確 <a href="configure-service.md#createintegrationoption">認します</a>。</td>
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

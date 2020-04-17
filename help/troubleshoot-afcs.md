---
title: 'Automated Forms Conversion Serviceのトラブルシューティング '
seo-title: 'Automated Forms Conversion Service(AFCS)のトラブルシューティング '
description: '一般的なAFCSの問題とその解決策 '
seo-description: 一般的なAFCSの問題とその解決策
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: 535267e20fb8e583e1c01f4160be378ffd31a4a4

---


# Automated Forms Conversion Serviceのトラブルシューティング


<!--The article provides information on installation, configuration and administration issues that may arise in an Automated Forms Conversion Service production environment. --> The document  provides basic troubleshooting steps for common errors.

## 一般的なエラー {#commonerrors}

| エラー | 例 |
|--- |--- |
| **エラーメッセージ** :アクセストークン <br> ・ヘッダーは使用できません。 <br><br>**理由&#x200B;**<br>管理者が複数のIMS設定を作成したか、IMS設定がAdobe CloudのAFCSサービスに到達できない。<br><br>**解決** ：複数の設定がある場合は、すべての設定を削除し、 <br> 新しい設定を作成します [](configure-service.md#obtainpubliccertificates)。 <br> 設定が1つだけの場合は、を使用して接続 **[!UICONTROL Health Check]** を確 [認します](configure-service.md#createintegrationoption)。 | ![アクセストークンヘッダーが使用できません](assets/invalid-ims-configuration.png) |
| **エラーメッセージ**<br> ：サービスに接続できません。  <br><br>**Reason **Incorrect service URL<br>, or no service URL is montioned in Automated Forms Conversion Service cloud services.<br><br>**Automated** Forms Conversion Service <br>[](configure-service.md#configure-the-cloud-service) Cloudサービスでの解決の正しいサービスURL。 | ![サービスに接続できません。](assets/wrong-endpoint-configured.png) |
| **エラーメッセージ**<br> ：サービスはフォームを変換できませんでした。  <br><br>**Reason **<br>Network connectivity issubes to your end, the service is down buide to scheduled maintenance, or outame on Adobe Cloud.<br><br>**解決方法**<br> ：ネットワーク接続に関する問題を解決し、計画的または予期しない停止が発生した場合は、https://status.adobe.com/でサービスのステータスを確認します。 | ![サービスに接続できません。](assets/service-failure.png) |
| **エラーメッセージ**<br> ：ページ数が15を超えています。  <br><br>**理由&#x200B;**<br>ソースフォームの長さが15ページを超えています。<br><br>**解決**<br> :Adobe Acrobatを使用して、15ページを超えるフォームを分割します。 フォームのページ数を15未満にします。 | ![サービスに接続できません。](assets/number-of-pages.png) |
| **エラーメッセージ**<br> ：ファイルの数が15を超えています。  <br><br>**Reason **：フォ<br>ルダーに15を超えるフォームが含まれています。<br><br>**解決**<br> フォルダー内のフォーム数を15以下にします。 フォルダー内の合計ページ数を50未満にします。 フォルダーのサイズを10 MB未満にします。 サブフォルダー内にフォームを保存しないでください。ソースフォームを8 ～ 15個のフォームのバッチに整理します。 | ![サービスに接続できません。](assets/number-of-pages.png) |
| **エラーメッセージ**<br> ：ソースファイルの形式がサポートされていません。  <br><br>**理由&#x200B;**<br>：ソースフォームを含むフォルダーに、サポートされていないファイルがいくつか含まれています。<br><br>**解決**<br> ：サービスは.xdpファイルと.pdfファイルのみをサポートします。 その他の拡張子の付いたファイルをフォルダーから削除し、変換を実行します。 | ![サービスに接続できません。](assets/unsupported-file-formats.png) |
| **Error Message** Scanned forms <br> are not supported.  <br><br>**理由&#x200B;**<br>: PDFフォームには、スキャンされたフォームの画像のみが含まれ、コンテンツ構造が含まれていません。<br><br>**解決**<br> ：サービスは、スキャンされたフォームやフォームの画像をアダプティブフォームに変換する機能をサポートしていません。 ただし、Adobe Acrobat を使用して、画像だけのフォームを PDF フォームに変換することはできます。 次に、変換サービスを使用して、この PDF フォームをアダプティブフォームに変換します。 Acrobat で変換を行う場合は、必ず品質の高い画像を使用するようにしてください。 これにより、変換後のフォームの品質が高くなります。 | ![サービスに接続できません。](assets/scanned-forms-error.png) |
| **Error Message**<br> Encrypted PDFフォームはサポートされていません。  <br><br>**Reason **<br>：フォルダーに暗号化されたPDFフォームが含まれています。<br><br>**解決**<br> ：サービスは、暗号化されたPDFフォームからアダプティブフォームへの変換をサポートしていません。 暗号化を削除し、非暗号化フォームをアップロードし、変換を実行します。 | ![サービスに接続できません。](assets/secured-pdf-form.png) |
| **エラーメッセージ**<br> ：メタモデルJSONスキーマを解析できません。  <br><br>**理由&#x200B;**<br>：サービスに指定されたJSONスキーマが正しい形式ではないか、無効な文字が含まれているか、無効な構文を使用してコンポーネントをマッピングしています。<br><br>**解決**<br> : JSONファイルの形式を確認します。 任意のオンラインJSONバリデーターを使用して、スキーマの形式と構造を確認できます。 メタモデルの [構文について詳しくは、](extending-the-default-meta-model.md) Extend the default meta-modelの記事を参照してください。 | ![サービスに接続できません。](assets/invalid-meta-model-schema.png) |

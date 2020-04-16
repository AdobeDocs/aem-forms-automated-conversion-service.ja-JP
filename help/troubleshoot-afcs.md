---
title: 'Automated Forms Conversion Serviceのトラブルシューティング '
seo-title: 'Automated Forms Conversion Service(AFCS)のトラブルシューティング '
description: '一般的なAFCSの問題とその解決策 '
seo-description: 一般的なAFCSの問題とその解決策
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: ccf30bc990c1a7cdb261332403668af6f35aeb9e

---


# Automated Forms Conversion Serviceのトラブルシューティング


この記事では、Automated Forms Conversion Serviceの実稼働環境で発生する可能性のある、インストール、設定、管理に関する問題について説明しています。環境 また、このドキュメントでは、基本的なトラブルシューティング手順と、一般的なエラーメッセージの説明も提供されています。

## 一般的なエラー {#commonerrors}

| エラー | 例 |
|--- |--- |
| **エラーメッセージ** :アクセストークン <br> ・ヘッダーは使用できません。 <br><br>**理由&#x200B;**<br>管理者が複数のIMS設定を作成したか、IMS設定がAdobe CloudのAFCSサービスに到達できない。<br><br>**解決** ：複数の設定がある場合は、すべての設定を削除し、 <br> 新しい設定を作成します [](configure-service.md#obtainpubliccertificates)。 <br> 設定が1つだけの場合は、を使用して接 **[!UICONTROL Health Check]** 続を確 [認します](configure-service.md#createintegrationoption)。 | ![アクセストークンヘッダーが使用できません](assets/invalid-ims-configuration.png) |
| **エラーメッセージ**<br> ：サービスに接続できません。  <br><br>**Reason **Incorrect service URL<br>, or no service URL is montioned in Automated Forms Conversion Service cloud services.<br><br>**Automated** Forms Conversion Service <br>[](configure-service.md#configure-the-cloud-service) Cloudサービスでの解決の正しいサービスURL。 | ![サービスに接続できません。](assets/wrong-endpoint-configured.png) |
| **エラーメッセージ**<br> ：サービスはフォームを変換できませんでした。  <br><br>**Reason **<br>Network connectivity issues to your end or the service is down duen ed decured maintenance or outable on Adobe Cloud.<br><br>**解決方法**<br> ：ネットワーク接続に関する問題を解決し、https://status.adobe.com/#のサービスの状態を確認して、計画的または予期しない停止を確認します。 | ![サービスに接続できません。](assets/service-failure.png) |

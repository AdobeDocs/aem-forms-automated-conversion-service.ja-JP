---
title: 'Automated Forms Conversion Serviceのトラブルシューティング '
seo-title: 'Automated Forms Conversion Service(AFCS)のトラブルシューティング '
description: '一般的なAFCSの問題とその解決策 '
seo-description: 一般的なAFCSの問題とその解決策
contentOwner: khsingh
topic-tags: forms
translation-type: tm+mt
source-git-commit: aebfde420d02bd4184022ecb42496a379d66a3b5

---


# Automated Forms Conversion Serviceのトラブルシューティング


この記事では、Automated Forms Conversion Serviceの実稼働環境で発生する可能性のある、インストール、設定、管理に関する問題について説明しています。環境 また、このドキュメントでは、基本的なトラブルシューティング手順と、一般的なエラーメッセージの説明も提供されています。

### 一般的なエラー {#commonerrors}

| エラー | 例 |
|--- |--- |
| **エラーメッセージ** :アクセストークン <br> ・ヘッダーは使用できません。 <br><br>**理由&#x200B;**<br>管理者が複数のIMS設定を作成したか、IMS設定がAdobe CloudのAFCSサービスに到達できない。<br><br>**解決** ：複数の設定がある場合は、すべての設定を削除し、 <br> 新しい設定を作成します [](configure-service.md#obtainpubliccertificates)。 <br> 設定が1つだけの場合は、を使用して接 **[!UICONTROL Health Check]** 続を確 [認します](configure-service.md#createintegrationoption)。 | ![カラーのフォーム](assets/invalid-ims-configuration.png) |
| **エラーメッセージ**<br> ：サービスに接続できません。  <br><br>**Reason **Incorrect service URL<br>, or no service URL is montioned in Automated Forms Conversion Service cloud services.<br><br>**Automated** Forms Conversion Service <br>[](configure-service.md#configure-the-cloud-service) Cloudサービスでの解決の正しいサービスURL。 | ![カラーのフォーム](assets/wrong-endpoint-configured.png) |

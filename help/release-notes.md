---
title: 新機能? リリースノート — Automated Forms Conversion Service
description: 'Automated Forms Conversion Serviceの最新の機能とバグ修正について説明します。 '
translation-type: tm+mt
source-git-commit: dc17dfcb331df6144b8a7ce3c9c9d840b1182a95

---


# Automated Forms Conversion Service:リリースノート

自動フォームコンバージョンサービスは、継続的に改善を受けます。 最新の開発状況を常に把握するには、このページを定期的にご覧ください。 このページには、次の情報が表示されます。

* 早期アクセス
* 最新リリース
* 新機能
* 改善
* バグの修正
* 廃止された機能
* 特別な手順
* 今後の変更計画

## 2020年3月20日(AFC-2020.03.1)

### 早期アクセス

**フォーム内の論理セクションを自動的に検出する**

AFC-2020.03.1リリースでは、この機能に早期にアクセスでき **[!UICONTROL Auto-detect logical sections]** ます。

デフォルトでは、PDFフォームの各ページに対して別々のトップレベルパネルが作成されます。 このオプションを使用して、ページレ **[!UICONTROL Auto-detect logical sections]** ベルのパネル（ページ番号ベースのパネル）をドロップし、論理パネルのみを作成できるようになりました。  また、前の論理セクションを持つセクションに属さないフィールドと、隣接する2つのページにまたがる論理セクションのフィールドを1つの論理セクションにクラブします。 例えば、論理セクションの一部のフィールドがページ1の最後にあり、一部がページ2の先頭にある場合、これらのフィールドはすべて1つの論理セクションに分類されます。

この機能を使用するには、コネクタパッケージ1.1.38以降が必要 **[!UICONTROL Auto-detect logical sections]** です。 You can download the connector package from [AEM Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1).

### 改善点

**リスト検出の改善**

このサービスは、箇条書きリストと番号付きリストの検出をより効率的に行えるようになりました。
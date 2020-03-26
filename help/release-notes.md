---
title: 新機能? リリースノート — Automated Forms Conversion Service
description: 'Automated Forms Conversion Serviceの最新の機能とバグ修正について説明します。 '
translation-type: tm+mt
source-git-commit: c0ca850a0a1e82e34364766601011d6367b218ac

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

デフォルトでは、PDFフォームの各ページに対して別々のトップレベルパネルが作成されます。 このオプションを使用して、ペー **[!UICONTROL Auto-detect logical sections]** ジレベルのパネル（ページ番号ベースのパネル）をドロップし、論理パネルのみを作成できるようになりました。 また、前の論理セクションを持つどのセクションにも属さないフィールドと、隣接する2つのページにまたがる論理セクションのフィールドを1つの論理セクションにクラブします。 例えば、論理セクションの一部のフィールドがページ1の最後にあり、一部がページ2の先頭にある場合、これらのフィールドはすべて1つの論理セクションに分類されます。

### 改善点

**リスト検出の改善**

このサービスは、箇条書きリストと番号付きリストの検出をより効率的に行えるようになりました。

### 特別な手順

**Automated Forms Conversion Service Connectorパッケージのインストール**

リリースAFC-2020.03.1で提供される最新の機能と改善を使用するには、コネクタパッケージ1.1.38以降が必要です。コネクタパッケージは [AEM Package Shareからダウンロードできます](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/AFCS-Connector-2020.03.1)。

既にAutomated Forms Conversionサービス環境を使用している場合は、コンバージョンサービスの最新の機能を使用するには、最新のサービスパック、最新のAEM Formsアドオンパッケージ、最新のコネクタパッケージを上記の順序でインストールします。 手順について詳しくは、「Automated Forms Conversion [サービスの設定」を参照してください](configure-service.md) 。
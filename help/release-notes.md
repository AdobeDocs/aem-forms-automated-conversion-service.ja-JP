---
title: 新機能? リリースノート — Automated Forms Conversion Service
description: 'Automated Forms Conversion Serviceの最新の機能とバグ修正について説明します。 '
translation-type: tm+mt
source-git-commit: 01dfd20951314017d47713bfb1a2a5f2d563f434

---


# Automated Forms Conversion Service:リリースノート

自動フォームコンバージョンサービスは、継続的に改善を受けます。 最新の開発状況を常に把握するには、このページを定期的にご覧ください。 このページには、次の情報が表示されます。

* 最新リリース
* 新機能
* バグの修正
* 廃止された機能
* 特別な手順
* 今後の変更計画

このページは毎月更新されているので、定期的に再訪してください。

## 2020年3月20日(AFC-2020.03.1)

### 最新情報

**フォーム内の論理セクションを自動的に検出する**

デフォルトでは、入力PDFフォームの各ページに対して別々のトップレベルパネルが作成されます。 このオプションを選択すると、各PDF **[!UICONTROL Auto-detect logical sections]** ページに対して別々のトップレベルパネルを作成する概念を削除し、論理セクションを自動的に検出できます。 サービスクラブは、フォームのフィールドを論理セクションに関連付けます。 例えば、請求先住所に関連するすべてのフィールドは1つのセクションに分類され、配送先住所に関連するすべてのフィールドは別のセクションに分類されます。 また、自動的に検出された論理セクションごとに別々のトップレベルパネルを作成します。

### 改善点

**リスト検出の改善**

このサービスは、箇条書きリストと番号付きリストの検出をより効率的に行えるようになりました。 複数レベルのリストを簡単に検出できるようになりました。

### 特別な手順

**Automated Forms Conversion Service Connectorパッケージのインストール**

リリースAFC-2020.03.1で提供される最新の機能と改善を使用するには、コネクタパッケージ1.1.38以降が必要です。コネクタパッケージは [AEM Package Shareからダウンロードできます](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/fd/AEM-Forms-6.5.4.0-WIN)。

既にAutomated Forms Conversionサービス環境を使用している場合は、コンバージョンサービスの最新の機能を使用するには、最新のサービスパック、最新のAEM Formsアドオンパッケージ、最新のコネクタパッケージを上記の順序でインストールします。 手順について詳しくは、「Automated Forms Conversion [サービスの設定」を参照してください](configure-service.md) 。

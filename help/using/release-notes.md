---
title: 新機能 リリースノート - 自動 Forms コンバージョンサービス
description: 自動 Forms コンバージョンサービスの最新機能と修正済みのバグについて説明します。
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: fccafbc9-28c1-4736-922c-24d675b25213
TQID: 'https://experienceleague.adobe.com/5c2zcJqsjOyH--SIp-DbEyQtflWnBy67-ja0BZY8aC8'
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
    internal-label: Administration
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: e40aeabffdc79dbf5d42a89b8e37c298e016cb90
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 85%
---
# リリースノート

自動フォーム変換サービスは継続的に改善されます。 最新の開発情報を入手するには、このページを定期的に参照してください。 このページでは、次の情報が確認できます。

* 早期アクセス
* 最新リリース
* 新機能
* 改善
* バグの修正
* 非推奨の機能
* 特別な手順
* 将来の変更プラン

## 2022 年 2 月 24 日（PT）（AFC-2022.02.0） {#feb-2022}

* [セクションをフラグメントに自動変換する](convert-existing-forms-to-adaptive-forms.md)機能を追加し、変換されたフォームのレンダリング速度を改善し、アダプティブフォームエディターで大きなフォームをより簡単に読み込めるようにしました。

## 2021 年 8 月 29 日（PT）（AFC-2021.08.0） {#aug-2021}

* イタリア語およびポルトガル語の PDF フォームをアダプティブフォームに変換する機能が追加されました。

## 2021 年 7 月 29 日（PT）（AFC-2021.07.2） {#july-2021}

* フランス語、ドイツ語、スペイン語の PDF フォームをアダプティブフォームに変換する機能が追加されました。

## 2021 年 6 月 24 日（PT）（AFC-2021.06.2） {#june-2021}

### 改善された点 {#june-2021-improvements}

ソースフォーム内の論理セクションを自動的に検出し、対応するアダプティブフォームパネルに変換する際の精度が向上しました。

## 2021 年 3 月 3 日（PT）（AFC-2021.02.2） {#mar-2021}

### 改善された点 {#march-2021-improvements}

ソースフォームをアダプティブフォームに変換する際に、フォームコンテンツを選択肢グループやフィールドに整理する処理が改善されました。

## 2021 年 2 月 2 日（PT）（AFC-2021.01.2） {#feb-2021}

### 改善された点 {#feb-2021-improvements}

ソースフォームをアダプティブフォームに変換する際に、フォームコンテンツをパネルに整理する処理と、パネルタイトルを生成する処理が改善されました。

## 2020 年 7 月 16 日（PT）（AFC-2020.07.2） {#jul-2020}

### 新機能 {#whats-new-jul-2020-}

カラーの PDF フォームからアダプティブフォームへの変換がサポートされるようになりました。

### 改善された点 {#jul-2020-improvements}

テキストフィールド、フォームフィールド、選択グループフィールドを対応するアダプティブフォームコンポーネントに自動変換する機能が改善されました。

## 2020 年 3 月 20 日（PT）（AFC-2020.03.1） {#mar-2020}

### 早期アクセス {#early-access}

**フォーム内の論理セクションの自動検出**

デフォルトでは、このサービスは PDF フォームの各ページに個別のトップレベルパネルを作成します。 これで、**[!UICONTROL 自動検出論理セクション]**&#x200B;オプションを使用して、ページレベルのパネル（ページ番号ベースのパネル）を破棄して、論理パネルのみを作成できるようになりました。 また、いずれのセクションにも属さないフィールドを直前の論理セクションにまとめ、さらに、隣接する 2 ページにまたがっている論理セクションのフィールドも 1 つの論理セクションとしてまとめます。 例えば、論理セクションの一部のフィールドが 1 ページ目の終わりにあり、一部が 2 ページ目の最初にある場合、そのようなフィールドはすべて 1 つの論理セクションにまとめられます。

### 改善された点 {#mar-2020-improvements}

**リスト検出の改善**

このサービスでは、箇条書きリストと番号付きリストの検出がより効率的になりました。

### 特別な手順 {#special-instructions}

**自動フォーム変換サービスコネクターパッケージのインストール**

リリース AFC-2020.03.1 で提供される最新の機能と改善を使用するには、コネクタパッケージ 1.1.38 以降が必要です。

Automated Forms Conversion Service環境（AEM 6.5またはAEM 6.5 LTS）を既に導入している場合は、コンバージョンサービスの最新機能を使用するには、最新のサービスパック、最新のAEM Forms アドオンパッケージ、および最新のコネクタパッケージを上記の順序でインストールします。 AEM Forms as a Cloud Serviceの場合、更新は自動的に配信されます。 詳しい手順については、「[自動フォーム変換サービスの設定](configure-service.md)」の記事を参照してください。


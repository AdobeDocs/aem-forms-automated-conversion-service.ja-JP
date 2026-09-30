---
title: 自動フォーム変換サービス（AFCS）の概要
description: 印刷用フォームからアダプティブフォームへの変換を高速化
solution: Experience Manager Forms
feature: Adaptive Forms, Foundation Components
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: edabeac8-cd66-48ca-a99f-9643a1c184cf
TQID: 'https://experienceleague.adobe.com/stoZAgMJGYjT1IKCcXBAe2JxWAvPJfwq0znNs757b0U'
product_v2:
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
    internal-label: Administration
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
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
source-wordcount: '769'
ht-degree: 89%
---
# 自動フォーム変換サービス（AFCS） {#introduction-to-automated-forms-conversion-service}

フォーム自動変換サービス（AFCS）は、PDF formsをアダプティブフォームに自動変換することで、データキャプチャ体験のデジタル化と近代化を加速させるのに役立ちます。 Adobe Sensei をベースとして開発されたこの変換サービスにより、使用しているデバイスに合わせて、PDF フォームが自動的に HTML5 ベースのアダプティブフォームに変換されます。 PDF forms と XFA への既存投資を活用しながら、このサービスはコンバージョン時にアダプティブフォームのフィールドに対して適切な検証、スタイル、レイアウトを適用します。 この変換サービスの特長を以下に示します。

* 印刷フォームをアダプティブフォームにコンバージョンする際に必要な手動作業を削減します。
* コンバージョン時に各種パターンを適用し、適切な検証処理を実行します。
* コンバージョン時に DoR を生成します。
* 使用頻度の高いフィールドが再利用可能な「フォームフラグメント」としてグループ化される
* コンバージョン時に Adobe Analytics を有効化します。

![操作は非常に簡単です。 変換するソースフォームを準備して、自動フォーム変換サービスを実行します。 美しいアダプティブフォームが生成されます。 出力はいつでも満足いくまで修正できます。](assets/pdf-to-adaptive-form-gitx50.gif)

## オンボーディング {#onboarding}

このサービスは、AEM 6.5 FormsおよびAEM 6.5 LTS Forms オンプレミス期間のお客様とAdobe Managed Service エンタープライズ版のお客様が無料で利用できます。 変換サービスを使用する場合は、アドビのセールスチームまたはアドビの営業担当者に問い合わせてください。 また、AEM Forms as a Cloud Service のお客様は無料でご利用いただけ、事前に有効化されています。

お客様の組織で変換サービスを使用できるように設定し、組織の管理者に対して必要な権限を設定します。 必要な権限を設定された管理者は、変換サービスに接続するためのアクセス権限を、組織内の AEM Forms 開発ユーザーに付与することができます。 詳しくは、「[自動フォーム変換サービスの設定](configure-service.md)」を参照してください。

## サポート対象の PDF フォームと言語 {#supported-languages-and-pdf-forms}

このサービスで変換できるフォームは、非対話型 PDF フォーム、Adobe Acrobat で作成されたフォーム（AcroForms といいます）、AEM Forms または Adobe LiveCycle で作成された XFA ベースフォームです。

このサービスは、Adobe Sign が有効になっている PDF forms もサポートしています。 ソースの PDF フォームに Adobe Sign のテキストタグが付いている場合、サービスはコンバージョン時に Adobe Sign に関するすべての情報を保持し、ソース PDF の署名者情報を対応するアダプティブフォームのフィールドに関連付けます。 この機能は、AcroForms でのみ使用できます。

サービスを実行すると、英語、フランス語、ドイツ語、スペイン語、イタリア語、ポルトガル語のフォームをアダプティブフォームに変換することができます。 また、[AEM 翻訳ワークフロー](https://helpx.adobe.com/jp/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)を使用して変換後のアダプティブフォームを別の言語に翻訳することもできます。

## 変換ワークフロー  {#conversion-workflow}

自動フォーム変換サービス（AFCS）は、Adobe Cloud 上で稼働します。 AEM インスタンスをコンバージョンサービスに接続し、コンバージョンするフォームを AEM インスタンスにアップロードして、コンバージョンを開始します。 コンバージョンプロセス全体の流れは、次のとおりです。

![ワークフロー](assets/conversion-workflow.png)

### &#x200B;1. 環境を設定する {#set-up-the-environment}

自動フォーム変換サービス（AFCS）は、Adobe Cloud 上で稼働します。 [組織の Adobe I/O アカウントを設定し、ローカルの AEM インスタンスを Adobe Cloud 上で稼働している変換サービスに接続](configure-service.md)します。 AEM 6.5およびAEM 6.5 LTSの場合、コアコンポーネントベースのテンプレートとテーマを使用する場合は、アダプティブフォームのコアコンポーネントを有効にする必要があります。[ サービスの設定](configure-service.md#referencepackage)を参照してください。

### &#x200B;2. アダプティブフォームへの PDF フォームの変換 {#use-the-conversion-service}

AEM Forms の環境を設定したら、[PDF フォームを AEM インスタンスにアップロード](convert-existing-forms-to-adaptive-forms.md)して[変換処理を開始](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)します。 フォームをアップロードする場合は、以下の点に注意してください。

* 保護されたフォームをアップロードしないでください。 この変換サービスでは、パスワードで保護されたフォームや暗号化されたフォームを変換することはできません。
* スキャンされたフォーム、色付きのフォーム、入力済みのフォーム、英語、フランス語、ドイツ語、スペイン語、イタリア語、ポルトガル語以外の言語のフォームをアップロードしないでください。 こうしたフォームはサポートされていません。
* ファイル名にスペースが含まれている PDF フォームをアップロードしないでください。
* [PDF ポートフォリオ](https://helpx.adobe.com/jp/acrobat/using/overview-pdf-portfolios.html)をアップロードしないでください。 この変換サービスでは、PDF ポートフォリオをアダプティブフォームに変換することはできません。
* PDF フォームで推奨される変更内容については、「[ベストプラクティスと考慮事項](styles-and-pattern-considerations-and-best-practices.md)」を参照してください。
* 変換サービスに関する問題点については、「[既知の問題](known-issues.md)」を参照してください。

### &#x200B;3. 変換されたフォームの確認 {#review-converted-forms}

実際のフォームには、フィールドのレイアウトや名前などについて、人工知能や機械学習ベースの検出ロジックでは正確に認識できない複雑なデータキャプチャ要件が含まれている場合があります。 自動変換処理が完了したら、[「レビューと修正」エディター](review-correct-ui-edited.md)を使用して変換後のフォームを確認し、必要な更新を行って、質の高いフォームを作成することができます。 必要な変更を加えたら、そのフォームをもう一度コンバージョンに送信します。

自動コンバージョンにかかる時間は、入力フォームのサイズ、フォームの複雑さ、サービスの処理キューの負荷など、様々な要因によって異なります。 ユーザーには、フォルダーやファイル上のステータスインジケーターを通じて、進行状況が定期的に通知されます。 コンバージョンが完了すると、設定済みのメールアドレス宛てにメール通知が送信されます。


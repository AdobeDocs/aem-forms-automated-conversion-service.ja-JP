---
title: 概要
description: '印刷フォームからアダプティブフォームへの変換の高速化 '
translation-type: tm+mt
source-git-commit: ceff5cb56aa9896a28004628c5e26c262b7918bd

---


# 概要 {#introduction-to-automated-forms-conversion-service}

Automated Forms Conversionサービスは、PDFフォームからアダプティブフォームへの自動変換を通じて、データ取得エクスペリエンスのデジタル化と最新化を促進します。 Adobe Senseiが提供するサービスは、PDFフォームをデバイスに優しく、レスポンシブで、HTML5ベースのアダプティブフォームに自動的に変換します。 PDFフォームとXFAに対する既存の投資を活用する一方で、変換時にアダプティブフォームのフィールドに適切な検証、スタイル設定、レイアウトを適用します。 このサービスは、次の点に役立ちます。

* 印刷フォームをアダプティブフォームに変換する手作業を省く
* 変換中にパターンと適切な検証を適用します。
* 変換中にレコードのドキュメントを生成
* 一般的なフィールドを再利用可能なフォームフラグメントにグループ化する
* 変換中にAdobe Analyticsを有効にします。

![簡単だ ソースフォームを提供し、すべてを私たちに任せるだけです。 美しいアダプティブフォームを提供します。 もちろん、出力を十分に調べてみましょう。 ](assets/pdf-to-adaptive-form-gitx50.gif)

## オンボーディング {#onboarding}

このサービスは、AEM 6.4 FormsおよびAEM 6.5 Formsのオンプレミスのお客様およびAdobe Managed Serviceのエンタープライズのお客様が無料で利用できます。 アドビの販売チームまたはアドビの担当者に連絡して、サービスへのアクセスをリクエストできます。

アドビは、組織へのアクセスを許可し、組織の管理者として指定されたユーザーに必要な権限を与えます。 管理者は、組織のAEM Forms開発者（ユーザー）に対するアクセス権を付与して、サービスに接続できます。 詳しくは [、「Automated Forms Conversionサービスの設定](configure-service.md) 」を参照してください。

## サポートされるPDFフォームと言語 {#supported-languages-and-pdf-forms}

このサービスは、非インタラクティブPDFフォーム、AcroFormsと呼ばれるAdobe Acrobatで作成されたフォーム、AEM FormsまたはAdobe LiveCycleを使用して作成されたXFAベースのフォームをサポートします。

このサービスで変換できるのは、英語のフォームのみです。 生成されたアダプティブフォームは、 [AEM翻訳ワークフローを使用して別の言語に翻訳できます](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)。

## 変換ワークフロー {#conversion-workflow}

自動フォームコンバージョンサービスは、Adobe Cloud上で実行されます。 AEMインスタンスをサービスに接続し、フォームをAEMインスタンスにアップロードして、変換を開始します。 完全なコンバージョンプロセスは次のとおりです。

![ワークフロー](assets/conversion-workflow.png)

### 1.環境の設定 {#set-up-the-environment}

自動フォームコンバージョンサービスは、Adobe Cloud上で実行されます。 [組織のAdobe I/Oアカウントを設定し、ローカルAEMインスタンスを](configure-service.md) 、Adobe Cloudで実行している変換サービスに接続します。

### 2.PDFフォームからアダプティブフォームへの変換 {#use-the-conversion-service}

AEM Forms環境の設定後、PDFフォームをアダプティブフォームに変換するには、PDFフォームをAEM [インスタンスに](convert-existing-forms-to-adaptive-forms.md) アップロードし、変換 [を開始します](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)。 フォームをアップロードする場合は、以下の点に注意してください。

* 保護されたフォームはアップロードしないでください。 サービスは、パスワードで保護され、暗号化されたフォームを変換しません。
* スキャンされたフォーム、色付きのフォーム、英語以外の言語で作成されたフォーム、フィールドに値が設定されているフォームをアップロードしないでください。 こうしたフォームを変換することはできません。
* ファイル名にスペースを含むPDFフォームはアップロードしないでください。
* [PDFポートフォリオはアップロードしない](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 この変換サービスでは、PDF ポートフォリオをアダプティブフォームに変換することはできません。
* 「ベストプラクティスと考慮事項」の記事で説明されているPDFフ [ォームに推奨される変更を加え](styles-and-pattern-considerations-and-best-practices.md) ます。
* 問題を回避する [には](known-issues.md) 、「既知の問題」を参照してください。

### 3.変換されたフォームの確認 {#review-converted-forms}

実世界のフォームは、フィールドレイアウト、命名、暗黙的な提案の観点から、複雑なデータ取得要件を持つ場合があり、AI/MLベースの検出ロジックでは正確に取り込めない可能性があります。 自動変換が完了したら、 [Review and Correctエディターを使用して](review-correct-ui-edited.md) 、変換されたフォームを確認し、必要な更新を行い、目的のエクスペリエンスに近い拡張出力を生成できます。 必要な変更を加えた後、変換用にフォームを再度送信します。

自動変換に要する時間は、入力フォームのサイズ、フォームの複雑さ、サービスの処理キューへのローンなど、様々な要因によって異なります。 フォルダ/ファイルのステータスインジケータを通じて、ユーザに進行状況を定期的に通知する。 変換が完了すると、設定済みの電子メールアドレスにも電子メール通知が送信されます。

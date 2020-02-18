---
title: 'ベストプラクティスと考慮事項 '
seo-title: 'ベストプラクティスと考慮事項 '
description: 自動フォームコンバージョンサービスのベストプラクティスと考慮事項
seo-description: Automated Forms Conversionサービスで識別が困難なソースPDFフォームのスタイルとパターンのリスト
uuid: e24773a2-be14-4184-a168-48aa976d459a
topic-tags: introduction
discoiquuid: 79f2026e-73a5-4bd1-b041-d1399b4ad23e
translation-type: tm+mt
source-git-commit: 0f413a8bc0bb444b6faaddaf32f84f36e38438a5

---


# ベストプラクティスと既知の複雑なパターン {#Best-practices-and-considerations2}

このドキュメントでは、フォーム管理者、作成者、開発者がAutomated Forms Conversionサービスを使用する際にメリットを得られるガイドラインと推奨事項を示します。 ソースフォームの準備から、自動変換のために多少の労力を要する複雑なパターンの修正まで、ベストプラクティスを説明します。 これらのベストプラクティスは、まとめて、自動フォームコンバージョンサービスの全体的なパフォーマンスと出力に貢献します。

## ベストプラクティス

変換サービスは、AEM Formsインスタンスで使用可能なPDFフォームをアダプティブフォームに変換します。 必要に応じて、すべてのPDFフォームを一度に、または段階的にアップロードできます。 フォームをアップロードする前に、次の点を考慮してください。

* フォルダー内のフォーム数は15未満にし、フォルダー内の合計ページ数は50未満にします。
* フォルダーのサイズを10 MB未満にします。 フォームをサブフォルダーに保持しないでください。
* フォームのページ数は15未満にします。
* 保護されたフォームはアップロードしないでください。 サービスは、パスワードで保護されたフォームと保護されたフォームを変換しません。
* [PDFポートフォリオはアップロードしないでください](https://helpx.adobe.com/acrobat/using/overview-pdf-portfolios.html)。 このサービスは、PDFポートフォリオをアダプティブフォームに変換しません。
* スキャン、色付き、英語以外の言語、入力済みのフォームはアップロードしないでください。 このようなフォームはサポートされていません。
* ファイル名にスペースを含むソースフォームはアップロードしないでください。 フォームをアップロードする前に、ファイル名からスペースを削除します。
* アダプティブフォームテンプレートを使用して、出力アダプティブフォームのヘッダーとフッターを指定します。 このサービスは、ソースPDFドキュメントのヘッダーとフッターを無視し、アダプティブフォームテンプレートで指定されたヘッダーとフッターを使用します。

## 複雑なパターンの把握

AEM Forms自動コンバージョンサービスでは、人工知能と機械学習アルゴリズムを使用して、ソースフォームのレイアウトとフィールドを把握します。 各機械学習サービスは、ソースデータから継続的に学習し、各チャーンでの出力を改善します。 これらのサービスは人間のような体験から学びます。

自動フォームコンバージョンサービスは、大規模なフォームセットに関するトレーニングを受けています。 ソースフォーム内のフィールドを簡単に識別し、アダプティブフォームを作成できます。 ただし、PDFフォームには、人間の目に見えやすいが、サービスにとって理解しにくいフィールドやスタイルがいくつかあります。 このサービスでは、一部のフィールドやスタイルに、該当するフィールドの種類やパネルとは異なる種類を割り当てることができます。 このようなフィールドパターンとスタイルパターンはすべて次のとおりです。

ソースデータから学習を続けるため、サービスでは、正しいフィールドやパネルを識別し、これらのパターンに割り当て始めます。 当面は、「レビューと修正」エディターを使用 [して](review-correct-ui-edited.md) 、このような問題を修正できます。 問題の修正を始める前に、または詳しく読む前に、アダプティブフォームのコンポ [ーネントについて理解しま](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)す。

### 一般的なパターン {#general}

| パターン | 解像度 |
|--- |--- |
| **パターンサービスは**<br> 、色付きのPDFフォームをアダプティブフォームに変換しません。 <br><br>**解像度&#x200B;**<br>：白黒またはグレースケールのPDFフォームを使用します。 | ![色付きフォーム](assets/best-practice-coloured-forms.png) |
| **パターンサ**<br>ービスは、入力済みPDFフォームをアダプティブフォームに変換しません。 <br><br>**解決：空のアダ&#x200B;**<br>プティブフォームを使用します。 | ![記入済みフォーム](assets/best-practice-filled-forms.png) |
| **パターンサ**<br>ービスは、密なフォーム内のテキストとフィールドを認識できない場合があります。 <br><br>**解像度&#x200B;**<br>：変換を開始する前に、密なフォームのテキストとフィールドの間の幅を広げます。 |  |
| **パターンサービ**<br>スは、スキャンされたフォームをサポートしません。 <br><br>**解決スキャン&#x200B;**<br>されたフォームは使用しません。 | ![スキャン済みフォーム](assets/scanned-forms.png) |
| **パターンサ**<br>ービスでは、画像および画像内のテキストは抽出されません。 <br><br>**解像度&#x200B;**<br>：変換したフォームに画像またはテキストを手動で追加します。 | ![テキストフォーム付き画像](assets/best-practice-image-with-text.png) |
| **点線また**<br>は非明確な境界線と境界線を含むパターンテーブルは変換されません。 <br><br>**解像度&#x200B;**：明確<br>な境界と境界線を持つテーブルを使用します。 サポートされます。 | ![非クリアテーブルフォーム](assets/best-practice-table-dotted-non-clear.png) |
| **パターン**<br> ・アダプティブ・フォームは標準テキストをサポートしておらず、すぐに使用できます。 したがって、縦書きテキストは対応するアダプティブフォームのテキストに変換されません。 <br><br>**解像度&#x200B;**：必要に応じて<br>、アダプティブフォームエディターを使用して縦書きのテキストを追加します。 | ![非クリアテーブルフォーム](assets/vertical-text.png) |



### 選択グループ {#choice-group}

| パターン | 解像度 |
|--- |--- |
| **ボックス**<br> や円以外の図形を持つパターン選択グループオプションは、対応するアダプティブフォームコンポーネントに変換されません。 <br><br>**[解像度&#x200B;**<br>] [選択オプション]図形をボックスまたは円に変更するか、[レビューと修正]エディタを使用して図形を識別します。 | ![選択フィールド ](assets/best-practice-choice-group-options.png) |

### Form fields {#form-fields}

| パターン | 解像度 |
|--- |--- |
| **パターンサービスは**<br> 、明確な境界線を持たないフィールドを識別しません。 <br><br>**解決レビュー&#x200B;**<br>&amp;正解エディターを使用して、このようなフィールドを特定します。 | ![境界が不明なフィールド](assets/best-practice-fields-without-clear-borders.png) |
| **パターンサービスは**<br> 、フォームの下部または右側にキャプションが付いた選択グループフォームフィールドを識別できない場合があります。 <br><br>**Resolution **<br>Review and Correct editorを使用してこのようなフィールドを識別する | ![選択フィールド](assets/best-practice-caption-bottom-right.png) |
| **Pattern**<br> Serviceは、互いに非常に近くに配置されているフォームフィールドや、明確な境界線を持たない一部のフォームフィールドに誤った型を結合または割り当てます。 <br><br>**解決レビュー&#x200B;**<br>&amp;正解エディターを使用して、このようなフィールドを特定します。 | ![選択フィールド](assets/best-practice-placed-very-near.png) |
| **パターンサービスは**<br> 、キャプションが遠くにあるフィールドや、キャプションと入力フィールドの間に点線が引かれているフィールドを認識できない場合があります。 <br><br>**解決方法&#x200B;**<br>：フォームのフィールドを明確な境界で使用するか、レビューおよび修正エディターを使用してこのような問題を修正します。 | ![遠く離れたフィールドまたはキャプションのフィールド間の点線](assets/best-practice-far-away-captions-or-a-dotted-line.png) |

### リスト {#lists}

| パターン | 解像度 |
|--- |--- |
| **フォームフ** ィールドを含むパターンリストは、マージされるか、対応するアダプティブフォームコンポーネント <br>Resolution <br><br>**Use forms **<br>fields with clear boundaries（明確な境界を持つフォームを使用）に変換されないか、レビューおよび修正エディターを使用してこのような問題を修正します。 | ![選択グループを含むリスト](assets/best-practice-lists-containing-form-fields.png) |
| **パターンサ** ービスでは、ネストされたリストの中に、「 <br>Resolution <br><br>**Use **<br>Review and Correct」エディターが表示されないままにして、このような問題を修正できます。 | ![選択グループを含むリスト](assets/best-practice-nested-lists.png) |
| **パターンサービスは** 、選択グループを含む一部のリストを、互いに <br> Resolution <br><br>****<br>Review and Correctエディターを使用して結合し、このような問題を修正します。 | ![選択グループを含むリスト](assets/best-practice-check-box-in-table-cells.png) |

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fields without borders are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->

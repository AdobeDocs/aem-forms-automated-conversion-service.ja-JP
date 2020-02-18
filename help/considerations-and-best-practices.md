---
title: '[公開しない]ベストプラクティスと考慮事項 '
seo-title: '[公開しない]ベストプラクティスと考慮事項 '
description: 'null'
seo-description: 'null'
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
translation-type: tm+mt
source-git-commit: afe461baa5bcfc1106c16aae2d6a9c839ea675e8

---


# [ベストプラクティスと考慮事項を公開しない] （英語のみ） {#do-not-publish-best-practices-and-considerations}

AEM Forms自動変換サービスは、PDFフォームをアダプティブフォームに変換します。 このサービスでは、人工知能と機械学習アルゴリズムを使用して、ソースフォームのレイアウトとフィールドを把握します。 各機械学習サービスは、ソースデータから継続的に学習し、各チャーンでの出力を改善します。 これらのサービスは人間のような体験から学びます。

自動フォームコンバージョンサービスは、大規模なフォームセットに関するトレーニングを受けています。 ソースフォーム内のフィールドを簡単に識別し、アダプティブフォームを作成できます。 ただし、PDFフォームには、人間の目に見えやすいが、サービスにとって理解しにくいフィールドやスタイルがいくつかあります。 このサービスでは、一部のフィールドやスタイルに、該当するフィールドの種類やパネルとは異なる種類を割り当てることができます。 このようなフィールドパターンとスタイルパターンはすべて次のとおりです。

ソースデータから学習を続けるため、サービスでは、正しいフィールドやパネルを識別し、これらのパターンに割り当て始めます。 当面は、「レビューと修正」エディターを使用 [して](review-correct-ui-edited.md) 、このような問題を修正できます。 問題の修正を始める前に、または詳しく読む前に、アダプティブフォームのコンポ [ーネントについて理解しま](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html)す。

## 一般 {#general}

<!--
Comment Type: draft

<ul>
<li>Service does not convert filled PDF forms to adaptive form. Use empty adaptive forms.Service does not convert colored PDF forms to adaptive form. Use black and white or grayscale adaptive forms. <br /> </li>
<li>Service does not convert filled PDF forms to adaptive form. Use empty adaptive forms.</li>
<li>Service does not support scanned forms. Do not use scanned forms. </li>
<li>Service can fail to recognize text and fields in a dense form. Increase the width between text and fields of a dense form before starting the conversion.</li>
<li>Service does not extract images. Manually add images to converted forms.</li>
<li>Service does not extract text present within an image. Manually add text to the adaptive form.</li>
</ul>
-->

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">既知のパターンと解像度</td> 
   <td width="70%">例</td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスは色付きPDFフォームをアダプティブフォームに変換しません。</p> <p> </p> <p><strong>解像度</strong></p> <p>白黒またはグレースケールのPDFフォームを使用します。 </p> </td> 
   <td style="text-align: left;"> <img src="assets/coloured-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスは入力済みPDFフォームをアダプティブフォームに変換しません。</p> <p> </p> <p><strong>解像度</strong></p> <p>空のアダプティブフォームを使用します。</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスが密なフォーム内のテキストとフィールドを認識できない場合があります。</p> <p> </p> <p><strong>解像度</strong></p> <p>濃密なフォームのテキストとフィールドの間の幅を広げてから変換を開始します。</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスはスキャンされたフォームをサポートしていません。</p> <p> </p> <p><strong>解像度</strong></p> <p>スキャンされたフォームは使用しないでください。 </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>画像と画像内のテキストは抽出されません。 </p> <p> </p> <p><strong>解像度</strong></p> <p>変換後のフォームに画像またはテキストを手動で追加します。</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>点線または非明確な境界と境界を持つテーブルは変換されません。</p> <p><strong>解像度</strong></p> <p>明確な境界と境界線を持つテーブルを使用します。 サポートされます。</p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## 選択グループ {#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">パターン</td> 
   <td width="70%">例</td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>ボックスや円以外の形状を持つ選択グループオプションは、対応するアダプティブフォームコンポーネントに変換されません。 </p> <p> </p> <p><strong>解像度</strong></p> <p>選択オプション図形をボックスまたは円に変更するか、[レビューと修正]エディタを使用して図形を識別します。</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## Form fields {#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">パターン</td> 
   <td width="70%">例</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>パターン</strong></p> <p>サービスは、明確な境界線を持たないフィールドを識別しません。</p> <p> </p> <p><strong>解像度</strong></p> <p>レビューおよび修正エディターを使用して、このようなフィールドを特定します。</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスでは、下部または右側に不明なキャプションが付いたフォームフィールドが一部残ります。</p> <p> </p> <p><strong>解像度</strong></p> <p>「レビューと修正」エディタを使用してこのようなフィールドを特定する</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスは、互いに非常に近くに配置されたフォームフィールドや、明確な境界線がない一部のフォームフィールドに誤った型を結合または割り当てます。 </p> <p> </p> <p><strong>解像度</strong></p> <p>レビューおよび修正エディターを使用して、このようなフィールドを特定します。</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスは、キャプションが遠くにあるフィールドや、キャプションと入力フィールドの間に点線が引かれているフィールドを認識できない場合があります。</p> <p> </p> <p><strong>解像度</strong></p> <p>フォームフィールドを明確な境界で使用するか、レビューおよび修正エディターを使用してこのような問題を修正します。</p> </td> 
   <td><img src="assets/form-fields-with-far-away-captions.png" /></td> 
  </tr>
 </tbody>
</table>

## リスト {#lists}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">パターン</td> 
   <td width="70%">例</td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>フォームフィールドを含むリストが結合されるか、対応するアダプティブフォームコンポーネントに変換されない</p> <p><strong>解像度</strong></p> <p>フォームフィールドを明確な境界で使用するか、レビューおよび修正エディターを使用してこのような問題を修正します。</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスでは、ネストされたリストを識別できないままにすることが可能</p> <p> </p> <p><strong>解像度</strong></p> <p>このような問題を修正するには、レビューおよび修正エディターを使用します。</p> </td> 
   <td><img src="assets/nested-lists.png" /> </td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>サービスは、選択グループを含む一部のリストを相互に結合します</p> <p><strong>解像度</strong></p> <p>このような問題を修正するには、レビューおよび修正エディターを使用します。</p> </td> 
   <td><img src="assets/lists-containing-choice-groups.png" /> </td> 
  </tr>
 </tbody>
</table>

<!--
Comment Type: draft

<h3>Choice groups</h3>
-->

<!--
Comment Type: draft

<ul>
<li>Lists with form fields, nested lists, and nested choice groups are not supported.</li>
<li>Form fields with captions at bottom or right are not supported.</li>
<li>Form fiields without bordes are not supported.</li>
<li>Hidden form fields are not supported.</li>
<li>Button in PDF forms are not converted to adaptive form buttons.<br /> </li>
<li>Tables with clear explicit boundaries and borders are supported.</li>
<li>Fields with far away captions are not supported.<br /> </li>
<li>Choice groups with only box or circle shaped selectors are supported. </li>
</ul>
-->


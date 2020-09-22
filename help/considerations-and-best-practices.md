---
title: 'ベストプラクティスと考慮事項 '
description: 'null'
seo-description: 'null'
page-status-flag: never-activated
uuid: c2821264-39e2-44f8-b234-835c46f33fd5
topic-tags: introduction
discoiquuid: b786e40a-202e-4e17-a2f5-1f77c46538c2
privatebeta: true
index: false
translation-type: tm+mt
source-git-commit: bc7a0a86a211214d6e43e7c95809f6f40fe267f8
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 100%

---


# ベストプラクティスと考慮事項 {#do-not-publish-best-practices-and-considerations}

<!--
[DO NOT PUBLISH]
-->

AEM Forms 自動変換サービスは、PDF フォームをアダプティブフォームに変換します。 このサービスは、人工知能と機械学習アルゴリズムを使用して、ソースフォームのレイアウトとフィールドを理解します。 すべての機械学習サービスは、ソースデータを使用して継続的に学習を行い、すべてのチャーンで改善された出力を生成します。 これらのサービスは、人間と同様に、これまでの経験を基にして学習していきます。

自動フォーム変換サービスは、大量のフォームに基づいて学習していきます。 このサービスにより、ソースフォーム内のフィールドを関単に特定して、アダプティブフォームを生成することができます。 ただし、PDF フォームのフィールドとスタイルには、人間にとっては簡単に区別できても、変換サービスでは認識するのが難しいものもあります。 変換サービスは、正しくないフィールドタイプやパネルを、特定のフィールドやスタイルに割り当てる場合があります。 以下に、こうしたフィールドやスタイルのパターンを示します。

変換サービスは、ソースデータを使用して継続的に学習していくため、ある程度学習が進むと、正しいフィールドやパネルを特定して割り当て、これらのパターンに対応できるようになります。 変換サービスがある程度の学習レベルに到達するまでは、「[レビューと修正](review-correct-ui-edited.md)」エディターを使用して、これらのパターンに対応してください。 以下の説明を読む前に、[アダプティブフォームのコンポーネント](https://helpx.adobe.com/jp/experience-manager/6-5/forms/using/introduction-forms-authoring.html)について理解してください。

## 一般 {#general}

<table border="1" cellpadding="1" cellspacing="0" style="border-collapse: separate; border-spacing: 0px;" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">既知のパターンとその解決方法</td> 
   <td width="70%">例</td> 
  </tr>
   <td><p><strong>パターン</strong></p> <p>入力済みの PDF フォームがアダプティブフォームに変換されない。</p> <p> </p> <p><strong>解決方法</strong></p> <p>空のアダプティブフォームを使用してください。</p> </td> 
   <td style="text-align: left;"><img src="assets/pre-filled-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>複雑なフォーム内のテキストやフィールドが認識されない。</p> <p> </p> <p><strong>解決方法</strong></p> <p>複雑なフォームのテキストとフィールドの幅を広げてから、変換処理を実行してください。</p> </td> 
   <td style="text-align: left;"><img src="assets/dense%20form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>スキャンされたフォームを使用できない。</p> <p> </p> <p><strong>解決方法</strong></p> <p>スキャンされたフォームは使用しないでください。 </p> </td> 
   <td><img src="assets/scanned-form.jpg" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>画像とその画像内のテキストが抽出されない。 </p> <p> </p> <p><strong>解決方法</strong></p> <p>変換後のフォームに画像とテキストを手動で追加してください。</p> </td> 
   <td><img src="assets/image-in-adaptive-form.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>点線や不明瞭な境界線（または不明瞭な枠線）が含まれているテーブルが変換されない。</p> <p><strong>解決方法</strong></p> <p>境界線や枠線が明確に設定されているテーブルを使用してください。  </p> </td> 
   <td><img src="assets/border-less-tables.png" /></td> 
  </tr>
 </tbody>
</table>

## 選択グループ  {#choice-group}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">パターン</td> 
   <td width="70%">例</td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>四角形と円以外の形状を持つ選択グループのオプションが、対応するアダプティブフォームのコンポーネントに変換されない。 </p> <p> </p> <p><strong>解決方法</strong></p> <p>選択グループオプションの形状を四角形または円に変更するか、「レビューと修正」エディターを使用して、選択グループオプションの形状を特定してください。</p> </td> 
   <td><img src="assets/shaded-box-patterns.png" /> </td> 
  </tr>
 </tbody>
</table>

## フォームフィールド {#form-fields}

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody>
  <tr>
   <td width="30%">パターン</td> 
   <td width="70%">例</td> 
  </tr>
  <tr>
   <td width="25%"><p><strong>パターン</strong></p> <p>境界線が不明瞭なフィールドが認識されない。</p> <p> </p> <p><strong>解決方法</strong></p> <p>「レビューと修正」エディターを使用して、こうしたフィールドを特定してください。</p> <p> </p> <p> </p> </td> 
   <td width="50%"><br /> <img src="assets/fields-without-clear-borders.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>下部または右側にキャプションが付いている一部のフォームフィールドが識別されない。</p> <p> </p> <p><strong>解決方法</strong></p> <p>「レビューと修正」エディターを使用して、こうしたフィールドを特定してください。</p> </td> 
   <td><br /> <img src="assets/forms-with-clear-borders-scale.png" /><br /> </td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>互いに非常に近い位置に配置されているフォームフィールドや、境界線が不明瞭なフォームフィールドに、正しくないタイプが結合されたり割り当てられたりする。 </p> <p> </p> <p><strong>解決方法</strong></p> <p>「レビューと修正」エディターを使用して、こうしたフィールドを特定してください。</p> </td> 
   <td><img src="assets/forms-with-fields-placed-nearby.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>離れた位置にキャプションが付いているフィールドや、キャプションと入力フィールドの間に点線が存在するフィールドが認識されない。</p> <p> </p> <p><strong>解決方法</strong></p> <p>境界線が明確に設定されているフォームフィールドを使用するか、「レビューと修正」エディターを使用して、問題のあるフィールドを修正してください。</p> </td> 
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
   <td><p><strong>パターン</strong></p> <p>フォームフィールドが含まれているリストが結合される、または対応するアダプティブフォームのコンポーネントに変換されない。</p> <p><strong>解決方法</strong></p> <p>境界線が明確に設定されているフォームフィールドを使用するか、「レビューと修正」エディターを使用して、問題のあるリストを修正してください。</p> </td> 
   <td><img src="assets/lists-with-fields.png" /></td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>ネストされた一部のリストが識別されない。</p> <p> </p> <p><strong>解決方法</strong></p> <p>「レビューと修正」エディターを使用して、問題のあるリストを修正してください。</p> </td> 
   <td><img src="assets/nested-lists.png" /> </td> 
  </tr>
  <tr>
   <td><p><strong>パターン</strong></p> <p>選択グループが含まれているリスト同士が結合される。</p> <p><strong>解決方法</strong></p> <p>「レビューと修正」エディターを使用して、問題のあるリストを修正してください。</p> </td> 
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


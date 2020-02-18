---
title: 変換中のレコードのドキュメントの生成
seo-title: 変換中のレコードのドキュメントの生成
description: 変換に使用するソースフォームのタイプに基づいてDoRを生成するための推奨パス。
seo-description: 変換に使用するソースフォームのタイプに基づいてDoRを生成するための推奨パス。
page-status-flag: never-activated
uuid: 7f0f5bf3-21be-449a-b23e-5946a9fd7ed4
contentOwner: khsingh
discoiquuid: 75f6e6bc-7636-4b40-919c-8b20a6ccbb1f
translation-type: tm+mt
source-git-commit: 640d72d7961ef0c2393bf0ae6745d918e388a056

---


# アダプティブフォームのレコードのドキュメント生成を有効にするための推奨ワークフロー {#recommended-workflows-dor-generation}

レコードのドキュメント(DoR)を使用すると、アダプティブフォームで提供および送信した情報を記録しておき、後で参照できるようにすることができます。
DoRは、基本テンプレートを使用してレイアウトを定義します。 DoRは、デフォルトのテンプレートを使用して生成するか、アダプティブフォームに他のテンプレートを関連付けることができます。

![レコードの生成ドキュメント](assets/document_of_record.gif)

DoRの生成について詳しくは、「アダプティブフォームのレコ [ードのドキュメントの生成」を参照してください](https://helpx.adobe.com/experience-manager/6-5/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.html)。

Automated Forms Conversionサー [ビスは](../help/introduction.md) 、次のソースフォームをアダプティブフォームに変換します。

* 非インタラクティブPDFフォーム
* Acroフォーム
* XFAベースのPDFフォーム

変換に使用するソースフォームに基づいて、次を使用してDoRを生成できます。

* デフォルトのテンプレート
* ソースフォームをテンプレートとして使用 — このオプションを選択すると、変換サービスは変換元フォームを変換後のアダプティブフォームにDoRテンプレートとして自動的に関連付けます。
* 変換されたアダプティブフォームに他のテンプレートを関連付ける

次の表に、使用するDoRテンプレートが生成されたDoRのレイアウトに与える影響の例を示します。

<table> 
 <tbody>
 <tr>
  <td><p><strong>ソースフォーム</strong></p></td>
  <td><p><strong>生成されたDoR</strong></p></td> 
   </tr>
  <tr>
   <td><img src="assets/source_xdp_updated.png"/></td>
   <td><p>DoRの生成にデフォルトのテンプレートを使用する場合：</br><img src="assets/source_form_default_updated.png"/></td>
   </tr>
   <tr>
   <td></td>
   <td><p>DoRを生成する際にソースフォームをテンプレートとして使用する場合：</br></p><img src="assets/source_form_dor_updated.png"/></td>
   </tr>
  </tbody>
</table>

表に示すように、ソースフォームをテンプレートとして使用する場合、DoRはソースフォームのレイアウトを保持します。
この記事では、3種類のソースフォームに基づいてDoRを生成するための推奨パスについて説明します。

<table> 
 <tbody> 
  <tr> 
   <th><strong>ソースフォーム</strong></th> 
   <th><strong>DoRを生成する方法</strong></th> 
  </tr> 
  <tr> 
   <td><p>非インタラクティブPDFフォーム</p></td> 
   <td> 
    <ul> 
     <li><a href="#generate-document-of-record-using-cloud-configuration">アダプティブフォーム変換前のDoR生成を有効にして、デフォルトのテンプレートを使用してDoRを生成する</a></li> 
     <li><a href="#edit-adaptive-form-properties-generate-document-of-record">アダプティブフォームの変換後にアダプティブフォームのプロパティを編集し、デフォルトまたは他のフォームテンプレートを使用したDoRの生成を有効にします。</a></li> 
    </ul> </td> 
  </tr>
  <tr> 
   <td><p>AcroフォームまたはXFAベースのPDFフォーム</p></td> 
   <td> 
    <ul> 
     <li><a href="#use-input-form-as-template-to-generate-document-of-record">アダプティブフォーム変換前のDoR生成を有効にし、ソースフォームをテンプレートとして使用してDoRを生成する</a></li> 
     <li><a href="#edit-adaptive-form-properties-to-generate-document-of-record">アダプティブフォームの変換後にアダプティブフォームのプロパティを編集し、デフォルトのテンプレート、ソースフォームをテンプレートまたはその他のフォームテンプレートを使用したDoRの生成を有効にします</a></li> 
    </ul> </td> 
  </tr>    
 </tbody> 
</table>

## 非インタラクティブPDFフォームのレコードのドキュメントを生成 {#generate-document-of-record-non-interactive-pdf}

自動フォーム変換サービスのソースフォームとして非インタラクティブPDFフォームを使用している場合は、次のことができます。

* アダプティブフォーム変換前のDoR生成を有効にして、デフォルトテンプレートを使用してDoRを生成する
* またはアダプティブフォーム変換後にアダプティブフォームのプロパティを編集して、デフォルトまたは他のフォームテンプレートを使用したDoRの生成を有効にします。

### 変換前のDoR生成を有効にして、デフォルトのテンプレートを使用してDoRを生成する {#generate-document-of-record-using-cloud-configuration}

1. // **[!UICONTROL Tools]** /変 **[!UICONTROL Cloud Services]** 換に使 **[!UICONTROL Automated Forms Conversion Configuration]** 用するクラウド設定のプロパティ/オプションを選 **[!UICONTROL Advanced]** 択し **[!UICONTROL Generate Document of Record]** ます。

   ![クラウド設定を使用したレコードのドキュメントの生成](assets/generate_dor_cloud_config.gif)

1. Tap **[!UICONTROL Save & Close]** to save the settings.

1. [変換を実行します](../help/convert-existing-forms-to-adaptive-forms.md)。 手順1で編集したクラウド設定を使用していることを確認します。
変換されたアダプティブフォームを送信すると、DoRはデフォルトのテンプレートを使用して自動的に生成されます。

### 変換後にアダプティブフォームのプロパティを編集し、DoR生成を有効にする {#edit-adaptive-form-properties-generate-document-of-record}

ソースフォームをアダプティブフォームに変換する前にDoR生成を有効にしない場合でも、変換後にDoR生成を有効にすることができます。

1. [非インタラクティブ](../help/convert-existing-forms-to-adaptive-forms.md) PDFフォームで変換を実行し、アダプティブフォームを生成します。

1. フォルダー内のアダプティブフォームを選 **[!UICONTROL output]** 択し、をタップしま **[!UICONTROL Properties]**&#x200B;す。

1. タブで、 **[!UICONTROL Form Model]** セクションを展 **[!UICONTROL Document of Record Template Configuration]** 開し、を選択しま **[!UICONTROL Generate Document of Record]**&#x200B;す。

   ![レコードのドキュメントを生成](assets/generate_dor_af_properties.png)

1. Tap **[!UICONTROL Save & Close]** to save the settings.

変換されたアダプティブフォームを送信すると、DoRはデフォルトのテンプレートを使用して自動的に生成されます。 その他のDoRテンプレートを変換されたアダプティブフォームに関連付ける場合は、オプションを選択で **[!UICONTROL Associate form template as the Document of Record template]** きます。

## AcroフォームまたはXFAベースのPDFフォームのレコードのドキュメントの生成 {#generate-document-of-record-acroform-xfaform}

Acro FormまたはXFAベースのPDFフォームを自動フォーム変換サービスのソースフォームとして使用している場合、次のことができます。

* アダプティブフォーム変換前のDoR生成を有効にして、ソースフォームをテンプレートとして使用してDoRを生成する

* アダプティブフォーム変換後にアダプティブフォームのプロパティを編集して、デフォルトのテンプレート、ソースフォームをテンプレートまたはその他のフォームテンプレートを使用したDoRの生成を有効にします。

### 変換前のDoR生成を有効にして、ソースフォームテンプレートを使用してDoRを生成する {#use-input-form-as-template-to-generate-document-of-record}

1. // **[!UICONTROL Tools]** /変 **[!UICONTROL Cloud Services]** 換に使 **[!UICONTROL Automated Forms Conversion Configuration]** 用するクラウド設定のプロパティ/オプションを選 **[!UICONTROL Advanced]** 択し **[!UICONTROL Generate Document of Record]** ます。

1. Tap **[!UICONTROL Save & Close]** to save the settings.

1. [変換を実行します](../help/convert-existing-forms-to-adaptive-forms.md)。 手順1で編集したクラウド設定を使用していることを確認します。
変換サービスは、Acro formまたはXFAベースのPDFフォームを、変換済みのアダプティブフォームにDoRテンプレートとして自動的に関連付けます。
アダプティブフォームのプロパティを開いて、タブのセクションにDoRテンプレートを表 **[!UICONTROL Document of Record Template Configuration]** 示することがで **[!UICONTROL Form Model]** きます。

   ![アダプティブフォームのプロパティを編集してレコードのドキュメントを生成](assets/generate_dor_af_properties_xdp_acro.png)

   変換されたアダプティブフォームを送信すると、DoRはソースフォームテンプレートを使用して自動的に生成されます。

### 変換後にアダプティブフォームのプロパティを編集し、DoR生成を有効にする {#edit-adaptive-form-properties-to-generate-document-of-record}

1. [非インタラクティブ](../help/convert-existing-forms-to-adaptive-forms.md) PDFフォームで変換を実行し、アダプティブフォームを生成します。

1. フォルダー内のアダプティブフォームを選 **[!UICONTROL output]** 択し、をタップしま **[!UICONTROL Properties]**&#x200B;す。

1. タブで、セク **[!UICONTROL Form Model]** ションを展開し、デフォ **[!UICONTROL Document of Record Template Configuration]** ルトのテンプ **[!UICONTROL Generate Document of Record]** レートを使用したDoRの生成を有効にします。
また、このオプションを選択し、テ **[!UICONTROL Associate form template as the Document of Record template]** ンプレートを選択して、ソースフォームテンプレートまたはその他のフォームテンプレートを使用したDoR生成を有効にすることもできます。

1. Tap **[!UICONTROL Save & Close]** to save the settings.

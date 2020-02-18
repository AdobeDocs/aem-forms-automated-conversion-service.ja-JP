---
title: デフォルトのメタモデルの拡張
seo-title: デフォルトのメタモデルの拡張
description: デフォルトのメタモデルを拡張して、組織に固有のパターン、検証、エンティティを追加し、自動フォームコンバージョンサービスの実行中にアダプティブフォームフィールドに設定を適用します。
seo-description: デフォルトのメタモデルを拡張して、組織に固有のパターン、検証、エンティティを追加し、自動フォームコンバージョンサービスの実行中にアダプティブフォームフィールドに設定を適用します。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: tm+mt
source-git-commit: 5d4dba8fea7439b991a7a15872e6f4ed48156ac9

---


# デフォルトのメタモデルの拡張 {#extend-the-default-meta-model}

自動フォーム変換サービスは、ソースフォームからフォームオブジェクトを識別して抽出します。 セマンティックマッパーを使用すると、抽出したオブジェクトをアダプティブフォームでどのように表すかを判断できます。 例えば、ソースフォームには、日付の様々なタイプの表現を含めることができます。 セマンティックマッパーは、ソースフォームの日付フォームオブジェクトのすべての表現をアダプティブフォームの日付コンポーネントにマッピングするのに役立ちます。 また、セマンティックマッパーを使用すると、変換中に検証、ルール、データパターン、ヘルプテキスト、アクセシビリティプロパティをアダプティブフォームコンポーネントに事前設定し、適用することもできます。

![](assets/meta-model.gif)

メタモデルはJSONスキーマです。 メタモデルを使用する前に、JSONに精通していることを確認します。 JSON形式で保存したデータの作成、編集、読み取りの経験が必要です。

## デフォルトのメタモデル {#default-meta-model}

自動フォームコンバージョンサービスには、デフォルトのメタモデルがあります。 これはJSONスキーマで、Adobe cloud上にあり、Automated Forms Conversionサービスの他のコンポーネントと共に存在します。 メタモデルのコピーは、ローカルのAEMサーバー上の次の場所にあります。

http://&lt;サーバー>:&lt;ポート>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json.

メタモデルのスキーマは、https://schema.org/docs/schemas.htmlにあるスキーマエンティティから派生します。 https://schema.orgで定義されているPerson、PostalAddress、LocalBusiness、およびその他のエンティティが含まれます。 メタモデルのすべてのエンティティは、JSONスキーマオブジェクトタイプに従います。 次のコードは、メタモデル構造の例を表しています。

```
   "Entity": {
      "id": "Entity",
      "properties": {
        "name": {
          "type": "string"
        },

        "description": {
          "type": "string",
          "description": "Description of the item"
        }
      }
    }
```

## デフォルトのメタモデルのダウンロード {#download-the-default-meta-model}

次の手順を実行して、デフォルトのメタモデルをローカルファイルシステムにダウンロードします。

1. AEM Formsインスタンスにログインします。
1. >>フォルダ **[!UICONTROL Forms]** ーに **[!UICONTROL Forms & Documents]****移動し****[!UICONTROL Meta Model]** ます。
1. ファイルを選択 **[!UICONTROL global.schema.json]** し、をタップしま **[!UICONTROL Download]**&#x200B;す。 ダウンロードダイアログボックスが表示されます。 オプションを選 **[!UICONTROL Download asset(s) as binary files]** 択します。 タップ **[!UICONTROL Download]**. アーカイブがダウンロードされます。

   <!--
   Comment Type: draft

   <li><p>Extract the archive and open the global.schema.json file for editing. </p> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

## メタモデルについて {#understanding-the-meta-model}

メタモデルは、エンティティを含むJSONスキーマファイルを参照します。 JSONスキーマファイル内のすべてのエンティティには、名前とIDが含まれます。 各エンティティには複数のプロパティを含めることができます。 エンティティとそのプロパティは、ドメインによって異なる場合があります。 スキーマファイルにキーワードとフィールド設定を追加して、スキーマプロパティをアダプティブフォームコンポーネントにマップすることができます。

```
"Event": {
      "id": "Eventid",
      "allOf": [
        {
          "$ref": "#Entity"
        },
        {
          "properties": {
            "startDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the start date and time of the event in ISO 8601 date format."
            },
            "endDate": {
              "type": "string",
              "format": "date",
              "description": "Specify the end date and time of the event in ISO 8601 date format."
            },
            "location": {
              "$ref": "#PostalAddress",
              "description": "Specify the location of the event."
            }
          }
        }
      ]
    }
```

この例では、 **Event** は、idの値がEventidであるエンティティの名前を表 **し** ます ****。 Eventエンティティには、複数のプロパティが含まれます。

* startDate
* endDate
* location

メタモ **デルのallOf** 構文は、エンティティ間の継承を有効にします。

各プロパティには、さらに次のものを含めることができます。

* [JSONスキーマプロパティ](#jsonschemaproperties)
* [生成されたアダプティブフォームフィールドにプロパティを適用するためのキーワードベースの検索](#keywordsearch)
* [その他のプロパティ](#additionalproperties)

![メタモデルのプロパティ](assets/meta_model_elements.gif)

変換サービスは、aem:affKeywordを使用して参照さ **れたキーワードに基づいて**、ソースフォームフィールドに対して検索操作を実行します。 変換サービスは、検索条件を満たすフィールドにJSONスキーマプロパティと追加のプロパティを適用します。

この例では、コンバージョンサービスは、ソースフォーム内の電話、電話、携帯電話、勤務先電話、自宅電話、電話番号、電話番号、電話番号、電話番号の各キーワードを検索します。 変換サービスは、これらのキーワードを含むフィールドに基づいて、変換後のアダプティブフォームフィールドにタイプ、パターン、aem:afPropertiesを適用します。

### 生成されたアダプティブフォームフィールドのJSONスキーマプロパティ {#jsonschemaproperties}

メタモデルは、Automated Forms Conversionサービスを使用して生成されたアダプティブフォームフィールドに対して、次のJSONスキーマの共通プロパティをサポートします。

<table> 
 <tbody> 
  <tr> 
   <th><strong>プロパティ名</strong></th> 
   <th><strong>説明</strong></th> 
  </tr> 
  <tr> 
   <td><p>ページのタイトルではなく、</p></td> 
   <td> 
    <p>メタモデルのtitleプロパティ内に記述されたテキストは、生成されたアダプティブフォームフィールドに対してアクションを実行する検索キーワードとして機能します。 例えば、アダプティブフォームフィールドのラベルを変更する場合などです。 詳しくは、「カスタムメタモ <strong>デルの例」の「フォームフィールド</strong> のラベ <a href="#custommetamodelexamples">ルを変更する」を参照してください。</a></p> </td> 
  </tr>
  <td><p>description</p></td> 
   <td> 
    <p>descriptionプロパティは、生成されたアダプティブフォームフィールドのヘルプテキストを設定します。 詳しくは、カスタムメタモデル <strong>の例の「フォームフィールドへのヘルプテキストの追加</strong><a href="#custommetamodelexamples">」を参照してください。</a></p> </td> 
  </tr>
  <td><p>type</p></td> 
   <td> 
    <p>typeプロパティは、生成されたアダプティブフォームフィールドのデータタイプを定義します。 titleプロパティに指定できる値は次のとおりです。</p>
    <ul> 
     <li>文字列：テキストデータ型のアダプティブフォームフィールドを生成します。</li> 
     <li>number:数値データ型のアダプティブフォームフィールドを生成します。</li>
     <li>整数：サブタイプが整数に設定された数値データ型のアダプティブフォームフィールドを生成します。</li>
     <li>boolean:切り替えアダプティブフォームコンポーネントを生成します。</li>
     </ul><p>メタモデルでのtypeプロパティの使用について詳しくは、「カスタムメタモデルの例 <strong>」の「フォームフィールドの種類</strong><a href="#custommetamodelexamples">の変更」を参照してください。</a></p></td> 
  </tr>
  <td><p>pattern</p></td> 
   <td> 
    <p>patternプロパティは、生成されるアダプティブフォームフィールドの値を正規表現に基づいて制限します。 例えば、メタモデルの次のコードは、生成されるアダプティブフォームフィールドの値を10桁の数字に制限し<br>ます。「pattern」:"/\\d{10}/"同様に、メタモ<br>デルの次のコードはフィールドの値を特定の日付形式に制限します。<br> "pattern":"date{DD MMMM, YYYY}",</p> </td> 
  </tr>
  <td><p>形式</p></td> 
   <td> 
    <p>formatプロパティは、正規表現の代わりに名前付きのパターンに基づいて、生成されるアダプティブフォームフィールドの値を制限します。 formatプロパティに指定できる値は次のとおりです。<ul><li>email:電子メールアダプティブフォームコンポーネントを生成します。</li><li>ホスト名：テキストボックスアダプティブフォームコンポーネントを生成します。</li></ul>メタモデルでのformatプロパティの使用について詳しくは、「カスタムメタモデルの例」の <strong>Modify the form</strong> field <a href="#custommetamodelexamples">of a format of a meta modelを参照してください。</a></p> </td> 
  </tr>
  <td><p>enumとenumNames</p></td> 
   <td> 
    <p>enumプロパティとenumNamesプロパティは、コンボボックス、チェックボックス、またはラジオボタンフィールドの値を固定セットに制限します。 enumNamesに示す値は、ユーザーインターフェイスに表示されます。 enumプロパティを使用して一覧表示される値は、計算に使用されます。<br>詳しくは、「アダプティブフォームの <strong>Convert a form field to multiple-choice check boxes</strong>」、「 <strong>Convert a text field to drop-down list in the adaptive form</strong>to drop-down list」、「 <strong></strong><a href="#custommetamodelexamples">Custom meta-model examples」を参照してください。</a></p> </td> 
  </tr>
 </tbody> 
</table>

### 生成されたアダプティブフォームフィールドにプロパティを適用するためのキーワードベースの検索 {#keywordsearch}

自動フォームコンバージョンサービスは、コンバージョン中にソースフォームに対してキーワード検索を実行します。 検索条件を満たすフィールドをフィルタリングした後、変換サービスは、メタモデル内のこれらのフィールドに対して定義されたプロパティを、生成されたアダプティブフォームフィールドに適用します。

キーワードは、aem:affKeywordプロパ **ティを使用して参照し** ます。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

この例では、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の **Bank account number** textを取得した後、変換サービスは **typeプロパティを使用してフィールドを** number **typeに変換** します。

### 生成されたアダプティブフォームフィールドの追加プロパティ {#additionalproperties}

メタモデルで **aem:afPropertiesプロパティを使用して** 、Automated Forms Conversionサービスを使用して生成されたアダプティブフォームフィールドに対して次の追加プロパティを定義できます。

<table> 
 <tbody> 
  <tr> 
   <th><strong>プロパティ名</strong></th> 
   <th><strong>説明</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiline</p></td> 
   <td> 
    <p>multilineプロパティは、変換後にアダプティブフォームのソースフォームフィールドを複数行フィールドに変換します。 詳しくは、カスタムメタモデ <strong>ルの例の「文字列フィールドを複数行フィールドに変換</strong> 」を <a href="#custommetamodelexamples">参照してください。</a></p> </td> 
  </tr>
  <td><p>mandatory</p></td> 
   <td> 
    <p>mandatoryプロパティは、変換後のアダプティブフォームフィールドの入力を必須として設定します。<br>詳しくは、「カスタムメタモデルの例 <strong>」の「アダプティブフォームフィールドへの検証の追加</strong><a href="#custommetamodelexamples">」を参照してください。</a></p>
    </td> 
  </tr>
  <td><p>jcr:title</p></td> 
   <td> 
    <p>jcr:titleプロパティとtitle JSONスキーマプロパティを使用すると、変換後にアダプティブフォームフィールドのラベルを変更できます。<br>詳しくは、「カスタムメタモ <strong>デルの例」の「フォームフィールド</strong> のラベ <a href="#custommetamodelexamples">ルを変更する」を参照してください。</a><br>JSONスキーマを <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank"></a> 使用してアダプティブフォームフィールドに適用できるその他のプロパティについて詳しくは、「JSONスキーマを使用したアダプティブフォームの作成」を参照してください。</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceTypeおよびguideNodeClass</p></td> 
   <td> 
    <p>sling:resourceTypeプロパティとguideNodeClassプロパティを使用すると、フォームフィールドを対応するアダプティブフォームコンポーネントにマップできます。<br>詳しくは、「アダプティブフォームの <strong>Convert a form field to multiple-choice check boxes</strong> 」および「 <strong>Convert a text field to drop-down list in</strong><a href="#custommetamodelexamples">Custom meta-model examples」を参照してください。</a></p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>validatePictureClauseプロパティは、変換後のアダプティブフォームフィールドで許可される形式に対する検証を設定します。<br>詳しくは、「カスタムメタモデルの例 <strong>」の「アダプティブフォームフィールドへの検証の追加</strong><a href="#custommetamodelexamples">」を参照してください。</p> </td> 
  </tr>
 </tbody> 
</table>

## カスタムメタモデルを使用したアダプティブフォームフィールドの変更 {#modify-adaptive-form-fields-using-custom-meta-model}

組織では、デフォルトのメタモデルに一覧表示されているパターンと検証に加えて、パターンと検証を使用できます。 デフォルトのメタモデルを拡張して、組織に固有のパターン、検証およびエンティティを追加できます。 自動フォームコンバージョンサービスは、変換中にカスタムメタモデルをフォームフィールドに適用します。 メタモデルは、新しいパターン、検証、および組織に固有のエンティティが検出された場合に更新を続けることができます。

自動フォームコンバージョンサービスは、次の場所に保存されたデフォルトのメタモデルを使用して、変換中にソースフォームフィールドをアダプティブフォームフィールドにマッピングします。

http://&lt;サーバー>:&lt;ポート>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

ただし、カスタムメタモデルをフォルダーに保存し、変換サービスのプロパティを変更して、変換中にカスタムメタモデルを使用することはできます。

### 変換中にカスタムメタモデルを使用する {#use-custom-meta-model-during-conversion}

変換中にカスタムメタモデルを使用するには、次の手順を実行します。

1. >でフォルダーを作 **[!UICONTROL Forms]** 成し、カ **[!UICONTROL Forms & Documents]** スタムメタモデルJSONスキーマファイルをフォルダーにアップロードします。
1. 次を使用して、コンバージョンサービスのプロパティを開きます。

   **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]**> **&lt;選択した**&#x200B;設定のプロパティ&#x200B;**>**

1. タブで、 **[!UICONTROL Basic]** フィールド内のカスタムメタモデルの場所を指定し、を **[!UICONTROL Custom Meta-model]** タップします **[!UICONTROL Save & Close]**。
1. [変換を実行し](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process) 、カスタムメタモデルを変換プロセスに適用します。

### カスタムメタモデルの例 {#custommetamodelexamples}

カスタムメタモデルを使用してアダプティブフォームフィールドのプロパティを変更する一般的な例を次に示します。

* フォームフィールドのラベルの変更
* フォームフィールドの種類の変更
* フォームフィールドへのヘルプテキストの追加
* フォームフィールドをアダプティブフォームの複数選択ラジオボタンに変換する
* フォームフィールドの形式の変更
* アダプティブフォームフィールドへの検証の追加
* アダプティブフォームのフォームフィールドをコンボボックスオプションに変換する
* ドロップダウンリストにオプションを追加する
* 文字列フィールドを複数行フィールドに変換する

#### フォームフィールドのラベルの変更 {#modify-the-label-of-a-form-field}

**** 例：変換後に、フォームの銀行口座番号のラベルをアダプティブフォームのカスタム口座番号に変更します。

このカスタムメタモデルでは、コンバージョンサービスは **title** プロパティを検索キーワードとして使用します。 フォーム内の **Bank account number** textを取得した後、変換サービスは、テキストを、aafPropertiesセクションの **jcr:title** プロパティで指定されたCustomer account number **文字列に置き換え****** ます。

```
{
  "numberfields": {
      "type": "number",
   "title": "Bank account number",
   "aem:afProperties" : {
    "jcr:title" : "Customer account number"
   }
   }
}
```

#### フォームフィールドの種類の変更 {#modify-the-type-of-a-form-field}

**例**:変換前のフォ **ーム内のテキストタイプの「銀行口座番号** 」フィールドを、変換後のアダプティブフォーム内の番号タイプフィールドに変更します。

このカスタムメタモデルでは、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の **Bank account number** textを取得した後、変換サービスはtypeプロパティを使用してフィールドを数値型に変換 **します** 。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### フォームフィールドへのヘルプテキストの追加 {#add-help-text-to-a-form-field}

**例**:アダプティブフォームの「銀行口 **座番号** 」フィールドにヘルプテキストを追加します。

このカスタムメタモデルでは、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の銀 **行口座番号のテキストを取得した後** 、コンバージョンサービスは **descriptionプロパティを使用してアダプティブフォームフィールドにヘルプテキストを追加します** 。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "description": "Specify your bank account number."
 }
}
```

#### フォームフィールドをアダプティブフォームの複数選択チェックボックスに変換する {#convert-a-form-field-to-multiple-choice-check-boxes-in-the-adaptive-form}

**例**:変換前のフォ **ーム内の文字列タイプの「国** 」フィールドを、変換後のアダプティブフォーム内のチェックボックスに変換します。

このカスタムメタモデルでは、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の **Country** （国）テキストを取得した後、変換サービスは、 **enum** プロパティを使用して、フィールドを次のチェックボックスに変換します。

* インド
* 英国
* オーストラリア
* ニュージーランド

**sling:resourceTypeおよびguideNodeClassプロパティは****** 、フォームフィールドをチェックボックスアダプティブフォームコンポーネントにマップします。

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### フォームフィールドの形式の変更 {#modify-the-format-of-a-form-field}

**例**:「電子メールアドレス」フィ **ールドの形式を** 、電子メール形式に変更します。

このカスタムメタモデルでは、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の「 **Email Address** 」テキストを取得した後、変換サービスは、 **formatプロパティを使用してフィールドを電子メール形式に変換します** 。

```
{
   "additionalDetails" : {
      "aem:affKeyword": ["E-mail Address"],
       "type" : "string",
       "format" : "email"
  } 
}
```

#### アダプティブフォームフィールドへの検証の追加 {#add-validations-to-adaptive-form-fields}

**** 例1:アダプティブフォームの「 **郵便番号** 」フィールドに検証を追加します。

このカスタムメタモデルでは、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の **郵便番号** ( **Postal Code** )テキストを取得した後、変換サービスは、aem:afPropertiesセクションで定義された **validatePictureClause** プロパティを使用して、フィールドに検証を追加します。 検証に基づき、変換後のアダプティブフォームの「 **郵便番号** 」フィールドに指定する入力には、6文字を含める必要があります。

```
{
   "postalCode" : {
      "aem:affKeyword": ["Postal Code"],
      "type" : "string",
      "aem:afProperties" : {
        "validatePictureClause" : "\\d{6}"
      } 
   }
}
```

**** 例2:アダプティブフォームの「 **銀行口座番号** 」フィールドに検証を追加します。

このカスタムメタモデルでは、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の **Bankアカウント番号** ( **Bank account number** )のテキストを取得した後、変換サービスは、aem:afPropertiesセクションで定義された **mandatory** プロパティを使用して、フィールドに検証を追加します。 検証に基づき、変換後にフォームを送信する前に、「銀行口座番 **号** 」フィールドの値を指定する必要があります。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "aem:afProperties" : {
        "mandatory": "true"
      }   
   }
}
```

#### テキストフィールドをアダプティブフォームのコンボボックスに変換する {#convert-a-text-field-to-drop-down-list-in-the-adaptive-form}

**例**:変換前のフォ **ーム内の文字列タイプの「国** 」フィールドを、変換後のアダプティブフォーム内のドロップダウンオプションに変換します。

このカスタムメタモデルでは、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の **Country** （国）テキストを取得した後、変換サービスは、 **enum** プロパティを使用して、フィールドを次のコンボボックスオプションに変換します。

* インド
* 英国
* オーストラリア
* ニュージーランド

**sling:resourceTypeおよびguideNodeClass** プロパティは **** 、フォームフィールドをドロップダウンアダプティブフォームコンポーネントにマップします。

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidedropdownlist",
      "guideNodeClass": "guideDropDownlist"
    }
  }
}
```

#### ドロップダウンリストにオプションを追加する {#add-additional-options-to-the-drop-down-list}

**** 例：カスタム **メタモデルを使用して** 、既存のコンボボックスにスリランカを追加するオプションを追加します。

オプションを追加するには、新しいオプションで **enum** プロパティを更新します。 この例では、スリランカを追加のオプ **ションとして** 、 **enumプロパティを更新します** 。 enumプロパティにリ **ストされた値は** 、ドロップダウンリストに表示されます。

```
{
"title": {
    "aem:affKeyword": [
      "country"
    ],
    "type" : "string",
    "enum": [
      "India",
      "England",
      "Australia",
      "New Zealand",
   "Sri Lanka"
    ],
    "aem:afProperties": {
      "sling:resourceType": "fd/af/components/guidecheckbox",
      "guideNodeClass": "guidecheckbox"
    }
  }
}
```

#### 文字列フィールドを複数行フィールドに変換する {#convert-a-string-field-to-a-multi-line-field}

**** 例：変換後に、 **文字列型の** 「住所」フィールドをフォーム内の複数行フィールドに変換します。

このカスタムメタモデルでは、コンバージョンサービスは **aem:affKeyword内のテキストを検索キーワ** ードとして使用します。 フォーム内の **Address** （住所）テキストを取得した後、サービスは、 **aem:afPropertiesセクションで定義された** multiline **** （複数行）プロパティを使用して、テキストフィールドを複数行フィールドに変換します。

```
{
 "multiline" : {
   "aem:affKeyword": [
      "Address"
    ],
    "type" : "string",
    "aem:afProperties": {
      "multiline": "true"
    }
  }
}
```

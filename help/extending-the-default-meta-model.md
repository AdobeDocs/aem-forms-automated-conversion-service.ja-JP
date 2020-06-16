---
title: デフォルトメタモデルの拡張
seo-title: デフォルトメタモデルの拡張
description: デフォルトのメタモデルを拡張することにより、組織固有のパターン、検証設定、エンティティを追加し、自動フォーム変換サービスの実行時に、設定情報をアダプティブフォームの各フィールドに適用することができます。
seo-description: デフォルトのメタモデルを拡張することにより、組織固有のパターン、検証設定、エンティティを追加し、自動フォーム変換サービスの実行時に、設定情報をアダプティブフォームの各フィールドに適用することができます。
uuid: f98b4cca-f0a3-4db8-aef2-39b8ae462628
topic-tags: forms
discoiquuid: cad72699-4a4b-4c52-88a5-217298490a7c
translation-type: ht
source-git-commit: 77bdb4e88194bd634dea125852ff2a897bc24678
workflow-type: ht
source-wordcount: '2401'
ht-degree: 100%

---


# デフォルトメタモデルの拡張{#extend-the-default-meta-model}

自動フォーム変換サービスにより、ソースフォーム内でフォームオブジェクトを特定して抽出することができます。 自動フォーム変換サービスでセマンティックマッパーを使用すると、抽出したオブジェクトがアダプティブフォーム内でどのように表示されるのかを確認することができます。 例えば、ソースフォームには、表示形式の異なる様々な日付オブジェクトが含まれている場合があります。 こうした場合にセマンティックマッパーを使用すると、ソースフォーム内の日付オブジェクトのすべての表示形式を、アダプティブフォームの日付コンポーネントにマップすることができます。 また、変換処理の実行中にセマンティックマッパーを使用して、検証設定、ルール、データパターン、ヘルプテキスト、アクセシビリティのプロパティをアダプティブフォームコンポーネントに対して事前に設定して適用することもできます。

![](assets/meta-model.gif)

メタモデルとは、JSON スキーマのことです。 メタモデルを使用するには、JSON について理解する必要があります。 具体的には、JSON 形式で保存されたデータの作成、編集、読み取りに関する知識と経験が必要になります。

## デフォルトのメタモデル{#default-meta-model}

自動フォーム変換サービスには、デフォルトのメタモデルが付属しています。 このメタモデルは JSON スキーマで、自動フォーム変換サービスの他のコンポーネントとともに、Adobe Cloud 上に存在しています。 メタモデルのコピーは、ローカル AEM サーバー上の以下のフォルダーに保管されています。 http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json. デフォルトのスキーマにアクセスする、またはダウンロードするには、[ここ](assets/global.schema.json)をクリックします。

メタモデルのスキーマは、https://schema.org/docs/schemas.html のスキーマエンティティから継承されます。 このスキーマエンティティには、https://schema.org で定義された各種エンティティ（Person、PostalAddress、LocalBusiness など）が含まれています。 メタモデルのすべてのエンティティは、JSON スキーマオブジェクトに従属します。 以下のコードは、サンプルのメタモデル構造を示しています。

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

## デフォルトメタモデルのダウンロード{#download-the-default-meta-model}

デフォルトのメタモデルをローカルファイルシステムにダウンロードするには、以下の手順を実行します。

1. AEM Forms インスタンスにログインします。
1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]****／****[!UICONTROL メタモデル]**&#x200B;フォルダーに移動します。
1. **[!UICONTROL global.schema.json]** ファイルを選択して「**[!UICONTROL ダウンロード]**」をタップします。 ダウンロード用のダイアログボックスが表示されます。「**[!UICONTROL アセットをバイナリファイルとしてダウンロード]**」オプションを選択します。 「**[!UICONTROL ダウンロード]**」をタップします。アーカイブファイルがダウンロードされます。

   <!--
   Comment Type: draft

   <li><p>Extract the archive and open the global.schema.json file for editing. </p> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

## メタモデルについて{#understanding-the-meta-model}

メタモデルとは、各種エンティティが保管された JSON スキーマファイルのことです。 JSON スキーマファイル内のすべてのエンティティに、名前と ID が設定されています。 各エンティティに複数のプロパティを設定することができます。 エンティティとそのプロパティは、ドメインによって異なる場合があります。 キーワードとフィールド設定を使用してスキーマファイルを拡張することにより、スキーマのプロパティをアダプティブフォームのコンポーネントにマップすることができます。

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

このサンプルコードでは、**Event** がエンティティ名を表し、**id** の値が **Eventid** に設定されています。 Event エンティティには、以下に示す複数のプロパティが含まれています。

* startDate
* endDate
* location

メタモデル内の **allOf** コンストラクターにより、エンティティ間での継承が可能になります。

各プロパティには、さらに以下のものを含めることができます。

* [JSON スキーマのプロパティ](#jsonschemaproperties)
* [生成後のアダプティブフォームフィールドにプロパティを適用するためのキーワードベース検索](#keywordsearch)
* [追加のプロパティ](#additionalproperties)

![メタモデルのプロパティ](assets/meta_model_elements.gif)

変換サービスは、**aem:affKeyword** を使用して参照されるキーワードに基づいて、ソースフォームフィールドに対して検索操作を実行します。 変換サービスにより、JSON スキーマのプロパティと追加のプロパティが、検索条件に一致するフィールドに適用されます。

上記のサンプルコードでは、変換サービスを使用して、ソースフォーム内のキーワード（phone、telephone、mobile phone、work phone、home phone、telephone number、telephone no、phone number）を検索しています。 変換サービスは、これらのキーワードが含まれているフィールドに基づき、変換処理の完了後に、各種プロパティ（type、pattern、aem:afProperties）をアダプティブフォームのフィールドに適用します。

### 生成後のアダプティブフォームフィールドに対する JSON スキーマプロパティ{#jsonschemaproperties}

メタモデルでは、自動フォーム変換サービスによって生成されたアダプティブフォームフィールドに対して、以下の JSON スキーマ共通プロパティを使用することができます。

<table> 
 <tbody> 
  <tr> 
   <th><strong>プロパティ名</strong></th> 
   <th><strong>説明</strong></th> 
  </tr> 
  <tr> 
   <td><p>title</p></td> 
   <td> 
    <p>メタモデルの title プロパティ内で指定されたテキストは、生成後のアダプティブフォームフィールドで操作を実行するためのキーワードとして機能します。 例えば、アダプティブフォームフィールドのラベルを変更する場合などに、その変更操作のキーワードとして機能します。 詳しくは、「<a href="#custommetamodelexamples">カスタムメタモデルの例</a>」の「<strong>フォームフィールドのラベルを変更する</strong>」セクションを参照してください。</p> </td> 
  </tr>
  <td><p>description</p></td> 
   <td> 
    <p>description プロパティにより、生成後のアダプティブフォームフィールドのヘルプテキストが設定されます。 詳しくは、「<a href="#custommetamodelexamples">カスタムメタモデルの例</a>」の「<strong>フォームフィールドにヘルプテキストを追加する</strong>」セクションを参照してください。</p> </td> 
  </tr>
  <td><p>type</p></td> 
   <td> 
    <p>type プロパティにより、生成後のアダプティブフォームフィールドのデータタイプが定義されます。 type プロパティで指定できる値は以下のとおりです。</p>
    <ul> 
     <li>string：アダプティブフォームフィールドがテキストデータタイプとして生成されます。</li> 
     <li>number：アダプティブフォームフィールドが数値データタイプとして生成されます。</li>
     <li>integer：アダプティブフォームフィールドが数値データタイプとして生成され、サブタイプとして整数データタイプが設定されます。</li>
     <li>boolean：切り替え式アダプティブフォームコンポーネントが生成されます。</li>
     </ul><p>メタモデルで type プロパティを使用する方法については、「<a href="#custommetamodelexamples">カスタムメタモデルの例</a>」の「<strong>フォームフィールドのタイプを変更する</strong>」セクションを参照してください。</p></td> 
  </tr>
  <td><p>pattern</p></td> 
   <td> 
    <p>pattern プロパティでは、正規表現に基づいて、生成後のアダプティブフォームフィールドの値が制限されます。 例えば、メタモデル内で「<br>"pattern": "/\\d{10}/"<br>」というコードを記述すると、生成後のアダプティブフォームフィールドの値が 10 桁に制限されます。同様に、メタモデル内で次のコードを記述して特定の日付形式を指定すると、生成後のアダプティブフォームフィールドの値がその日付形式に制限されます：<br> "pattern": "date{DD MMMM, YYYY}",</p> </td> 
  </tr>
  <td><p>format</p></td> 
   <td> 
    <p>format プロパティでは、正規表現ではなく指定されたパターンに基づいて、生成後のアダプティブフォームフィールドの値が制限されます。 format プロパティで指定できる値は以下のとおりです。<ul><li>email：アダプティブフォームの電子メールコンポーネントが生成されます。</li><li>hostname：アダプティブフォームフィールドのテキストボックスコンポーネントが生成されます。</li></ul>メタモデルで format プロパティを使用する方法については、「<a href="#custommetamodelexamples">カスタムメタモデルの例</a>」の「<strong>フォームフィールドの形式を変更する</strong>」セクションを参照してください。</p> </td> 
  </tr>
  <td><p>enum と enumNames</p></td> 
   <td> 
    <p>enum プロパティと enumNames プロパティでは、ドロップダウンフィールド、チェックボックスフィールド、ラジオボタンフィールドの値が、事前に設定した値に制限されます。 enumNames プロパティで指定した値は、ユーザーインターフェイスに表示されます。 enum プロパティで指定した値は、計算処理で使用されます。<br>詳しくは、「<a href="#custommetamodelexamples">カスタムメタモデルの例</a>」の「<strong>フォームフィールドをアダプティブフォーム内の複数選択チェックボックスに変換する</strong>」セクション、「<strong>テキストフィールドをアダプティブフォーム内のドロップダウンリストに変換する</strong>」セクション、「<strong>ドロップダウンリストにその他のオプションを追加する</strong>」セクションを参照してください。</p> </td> 
  </tr>
 </tbody> 
</table>

### 生成後のアダプティブフォームフィールドにプロパティを適用するためのキーワードベース検索{#keywordsearch}

自動フォーム変換サービスは、変換処理の実行時に、ソースフォームに対してキーワード検索を実行します。 変換サービスは、検索条件に一致するフィールドをフィルタリングしてから、メタモデル内のそれらのフィールドに対して定義されているプロパティを、生成後のアダプティブフォームフィールドに適用します。

キーワードは、**aem:affKeyword** プロパティを使用して参照されます。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

この例では、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 検索サービスは、フォーム内の「**Bank account number**」テキストフィールドを取得し、**type** プロパティを使用して、このテキストフィールドを&#x200B;**数値**&#x200B;タイプに変換します。

### 生成後のアダプティブフォームフィールドに対する追加のプロパティ{#additionalproperties}

メタモデル内の **aem:afProperties** プロパティを使用して、自動フォーム変換サービスによって生成されたアダプティブフォームフィールドに対して、以下の追加のプロパティを定義することができます。

<table> 
 <tbody> 
  <tr> 
   <th><strong>プロパティ名</strong></th> 
   <th><strong>説明</strong></th> 
  </tr> 
  <tr> 
   <td><p>multiLine</p></td> 
   <td> 
    <p>multiLine プロパティにより、変換処理の完了後に、ソースフォームフィールドがアダプティブフォーム内の複数行フィールドに変換されます。詳しくは、「<a href="#custommetamodelexamples">カスタムメタモデルの例</a>」の「<strong>文字列フィールドを複数行フィールドに変換する</strong>」セクションを参照してください。</p> </td> 
  </tr>
  <td><p>mandatory</p></td> 
   <td> 
    <p>mandatory プロパティにより、変換処理の完了後に、アダプティブフォームフィールドの入力が必須入力として設定されます。<br>詳しくは、「<a href="#custommetamodelexamples">カスタムメタモデルの例</a>」の「<strong>アダプティブフォームフィールドに検証機能を追加する</strong>」セクションを参照してください。</p>
    </td> 
  </tr>
  <td><p>jcr:title</p></td> 
   <td> 
    <p>jcr:title プロパティを JSON スキーマの title プロパティとともに指定すると、変換処理の完了後に、アダプティブフォームフィールドのラベルを変更することができます。<br>詳しくは、「<a href="#custommetamodelexamples">カスタムメタモデルの例」の「<strong>フォームフィールドのラベルを変更する</strong>」セクションを参照してください。</a><br>JSON スキーマを使用してアダプティブフォームフィールドに適用できる追加のプロパティについては、「<a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html" target="_blank">JSON スキーマを使ったアダプティブフォームの作成</a>」を参照してください。</p>
    <p></p></td> 
  </tr>
  <td><p>sling:resourceType と guideNodeClass</p></td> 
   <td> 
    <p>sling:resourceType プロパティと guideNodeClass プロパティを使用して、対応するアダプティブフォームコンポーネントにフォームフィールドをマップすることができます。<br>詳しくは、「<a href="#custommetamodelexamples">カスタムメタモデルの例</a>」の「<strong>フォームフィールドをアダプティブフォーム内の複数選択チェックボックスに変換する</strong>」セクションと「<strong>テキストフィールドをアダプティブフォーム内のドロップダウンリストに変換する</strong>」セクションを参照してください。</p> </td> 
  </tr>
  <td><p>validatePictureClause</p></td> 
   <td> 
    <p>validatePictureClause プロパティにより、変換処理の完了後に、アダプティブフォームフィールドで許可されている形式に対する検証処理が設定されます。<br>詳しくは、「<a href="#custommetamodelexamples">カスタムメタモデルの例」の「<strong>アダプティブフォームフィールドに検証機能を追加する</strong>」セクションを参照してください。</p> </td> 
  </tr>
 </tbody> 
</table>

## カスタムメタモデルを使用してアダプティブフォームフィールドを変更する{#modify-adaptive-form-fields-using-custom-meta-model}

デフォルトのメタモデルで登録されているパターンと検証機能のほかに、組織内でパターンと検証機能を設定することができます。 デフォルトのメタモデルを拡張することにより組織固有のパターン、検証機能、エンティティを追加することができます。 自動フォーム変換サービスにより、変換処理の実行時に、カスタムメタモデルがフォームフィールドに適用されます。 組織固有の新しいパターン、検証機能、エンティティが検出されるたびに、メタモデルを継続的に更新することができます。

自動フォーム変換サービスは、変換処理の実行時に、以下の場所に保存されているデフォルトのメタモデルを使用して、ソースフォームフィールドをアダプティブフォームフィールドにマップします。

http://&lt;server>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/metamodel/global.schema.json

ただし、カスタムメタモデルを特定のフォルダーに保存して変換サービスのプロパティを変更することにより、変換処理の実行時にカスタムメタモデルを使用することができます。

### 変換処理の実行時にカスタムメタモデルを使用する{#use-custom-meta-model-during-conversion}

変換処理の実行時にカスタムメタモデルを使用するには、以下の手順を実行します。

1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;でフォルダーを作成し、このフォルダーにカスタムメタモデルの JSON スキーマファイルをアップロードします。
1. 以下のオプションを使用して、変換サービスを起動します。

   **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 自動フォーム変換の設定]**／**&lt;**&#x200B;選択した設定のプロパティ&#x200B;**>**

1. 「**[!UICONTROL 基本]**」タブの「**[!UICONTROL カスタムメタモデル]**」フィールドでカスタムメタモデルの場所を指定し、「**[!UICONTROL 保存して閉じる]**」をタップします。
1. [変換処理を実行](convert-existing-forms-to-adaptive-forms.md#start-the-conversion-process)し、カスタムメタモデルを変換処理に適用します。

### カスタムメタモデルの例{#custommetamodelexamples}

ここでは、カスタムメタモデルを使用してアダプティブフォームフィールドを変更する場合の一般的な例について説明します。以下のようなケースが考えられます。

* フォームフィールドのラベルを変更する
* フォームフィールドのタイプを変更する
* フォームフィールドにヘルプテキストを追加する
* フォームフィールドをアダプティブフォーム内の複数選択チェックボックスに変換する
* フォームフィールドの形式を変更する
* アダプティブフォームフィールドに検証機能を追加する
* フォームフィールドをアダプティブフォーム内のドロップダウンリストオプションに変換する
* ドロップダウンリストにその他のオプションを追加する
* 文字列フィールドを複数行フィールドに変換する

#### フォームフィールドのラベルを変更する{#modify-the-label-of-a-form-field}

**例：**&#x200B;変換処理の完了後に、アダプティブフォーム内の「Bank account number」というラベルを「Customer account number」に変更する

このカスタムメタモデルの場合、変換サービスは **title** プロパティを検索キーワードとして使用します。 検索サービスは、フォーム内の「**Bank account number**」というテキストを取得し、**aem:afProperties** セクションの **jcr:title** プロパティで指定された「**Customer account number**」というテキストに置き換えます。

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

#### フォームフィールドのタイプを変更する{#modify-the-type-of-a-form-field}

**例**：変換処理の完了後に、アダプティブフォーム内の「**Bank account number**」というテキストタイプフィールドを変更してから数値タイプフィールドに変換する

このカスタムメタモデルでは、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 検索サービスは、フォーム内の「**Bank account number**」テキストフィールドを取得し、**type** プロパティを使用して、このテキストフィールドを数値タイプに変換します。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"]
 }
}
```

#### フォームフィールドにヘルプテキストを追加する{#add-help-text-to-a-form-field}

**例**：アダプティブフォーム内の「**Bank account number**」フィールドにヘルプテキストを追加する

このカスタムメタモデルでは、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 変換サービスは、フォーム内の「**Bank account number**」テキストフィールドを取得し、**description** プロパティを使用して、このテキストフィールドにヘルプテキストを追加します。

```
{
  "numberfields": {
      "type": "number",
      "aem:affKeyword": ["Bank account number"],
   "description": "Specify your bank account number."
 }
}
```

#### フォームフィールドをアダプティブフォーム内の複数選択チェックボックスに変換する{#convert-a-form-field-to-multiple-choice-check-boxes-in-the-adaptive-form}

**例**：変換処理の完了後に、アダプティブフォーム内の「**Country**」文字列タイプフィールドをチェックボックスに変換する

このカスタムメタモデルでは、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 変換サービスは、変換処理の完了後、フォーム内の「**Country**」テキストフィールドを取得し、**enum** プロパティを使用して、このテキストフィールドを以下のチェックボックスに変換します。

* India
* England
* Australia
* New Zealand

**sling:resourceType** プロパティと **guideNodeClass** プロパティにより、フォームフィールドがアダプティブフォームのチェックボックスコンポーネントにマップされます。

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

#### フォームフィールドの形式を変更する{#modify-the-format-of-a-form-field}

**例**：「**Email Address**」フィールドの形式を電子メール形式に変換する

このカスタムメタモデルでは、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 変換サービスは、フォーム内の「**Email Address**」テキストフィールドを取得し、**format** プロパティを使用して、このテキストフィールドを電子メール形式に変換します。

```
{
   "additionalDetails" : {
      "aem:affKeyword": ["E-mail Address"],
       "type" : "string",
       "format" : "email"
  } 
}
```

#### アダプティブフォームフィールドに検証機能を追加する{#add-validations-to-adaptive-form-fields}

**例 1**：アダプティブフォームの「**Postal Code**」フィールドに検証機能を追加する

このカスタムメタモデルでは、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 変換サービスは、フォーム内の「**Postal Code**」テキストフィールドを取得し、**aem:afProperties** セクションで定義された **validatePictureClause** プロパティを使用して、このテキストフィールドに検証機能を追加します。 追加された検証機能に従い、変換後のアダプティブフォーム内の「**Postal Code**」フィールドに値を指定する場合は、6 文字の値を指定する必要があります。

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

**例 2**：アダプティブフォームの「**Bank account number**」フィールドに検証機能を追加する

このカスタムメタモデルでは、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 変換サービスは、フォーム内の「**Bank account number**」テキストフィールドを取得し、**aem:afProperties** セクションで定義された **mandatory** プロパティを使用して、このテキストフィールドに検証機能を追加します。 追加された検証機能に従い、変換後のフォームを送信する前に、「**Bank account number**」フィールドに値を指定する必要があります。

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

#### テキストフィールドをアダプティブフォーム内のドロップダウンリストに変換する{#convert-a-text-field-to-drop-down-list-in-the-adaptive-form}

**例**：変換処理の完了後に、アダプティブフォーム内の「**Country**」文字列タイプフィールドをドロップダウンオプションに変換する

このカスタムメタモデルでは、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 変換サービスは、フォーム内の「**Country**」テキストフィールドを取得し、**enum** プロパティを使用して、このテキストフィールドを以下のドロップダウンリストに変換します。

* India
* England
* Australia
* New Zealand

**sling:resourceType** プロパティと **guideNodeClass** プロパティにより、フォームフィールドがアダプティブフォームのドロップダウンコンポーネントにマップされます。

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

#### ドロップダウンリストにその他のオプションを追加する{#add-additional-options-to-the-drop-down-list}

**例**：カスタムメタモデルを使用して、追加のオプションとして「**Sri Lanka**」を既存のドロップダウンリストに追加する

オプションをさらに追加するには、そのオプションを使用して **enum** プロパティを更新します。 以下のサンプルコードでは、**Sri Lanka** を追加のオプションとして使用して **enum** プロパティを更新しています。 **enum** プロパティに登録された値は、ドロップダウンリスト内の項目として表示されます。

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

#### 文字列フィールドを複数行フィールドに変換する{#convert-a-string-field-to-a-multi-line-field}

**例**：変換処理の完了後に、「**Address**」文字列タイプフィールドをフォーム内の複数行フィールドに変換する

このカスタムメタモデルでは、**aem:affKeyword** プロパティ内のテキストが、変換サービスの検索キーワードとして使用されます。 変換サービスは、フォーム内の「**Address**」テキストフィールドを取得し、**aem:afProperties** セクションで定義された **multiLine** プロパティを使用して、このテキストフィールドを複数行フィールドに変換します。

```
{
 "multiLine" : {
   "aem:affKeyword": [
      "Address"
    ],
    "type" : "string",
    "aem:afProperties": {
      "multiLine": "true"
    }
  }
}
```

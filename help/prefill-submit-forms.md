---
title: アダプティブフォームの推奨データソースベースの事前入力および送信ワークフロー
seo-title: アダプティブフォームの事前入力および送信オプション
description: Automated Forms Conversion Serviceを使用して生成されたアダプティブフォームのデータソースベースの事前入力および送信ワークフロー。
seo-description: Automated Forms Conversion Serviceを使用して生成されたアダプティブフォームのデータソースベースの事前入力および送信ワークフロー。
uuid: 91409a82-141c-4233-82b1-1539a0b250f8
contentOwner: khsingh
topic-tags: forms
discoiquuid: cad34fff-7f9f-4a27-8b5c-d0a523903eec
privatebeta: true
translation-type: tm+mt
source-git-commit: caccb547a5741eb0e70ddf75630a661f8fe75cb3

---


# アダプティブフォームの推奨データソースベースの事前入力および送信ワークフロー {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

Automated Forms Conversionサービスを使用して変換されたアダプティブフォームでは、次のデータソースを使用できます。

* フォームデータモデル、OData、またはその他のサードパーティサービス
* JSONスキーマ
* XSDスキーマ

データソースに基づいて、データモデルの有無に関わらずアダプティブフォームを生成するように選択できます。

この記事では、データソースを選択し、変換サービスを使用してアダプティブフォームを生成した後に、フィールドの値と送信オプションを事前入力するための推奨ワークフローについて説明します。

<table> 
 <tbody> 
  <tr> 
   <th><strong>データソース</strong></th> 
   <th><strong>推奨ワークフロー</strong></th> 
  </tr> 
  <tr> 
   <td><p>フォームデータモデル、OData、またはその他のサードパーティサービス</p></td> 
   <td> 
    <p><strong>オプション1</strong>:フォームデータモデル、OData、または他のサードパーティサービスをデータソースとして選択します。 Automated Forms Conversion <a href="#generate-adaptive-forms-with-no-data-binding">サービスを使用して、データ連結のない</a> 、アダプティブフォームを生成します。 アダプティブフォームフィールドをフォームデータモデルのエンティティに手動で連結し、「Form Data Model Prefill Service」オプションを使用してフィールドの値を事前入力します。 アダプティブフォームを送信するには、「Submit using Form Data Model」オプションを使用します。</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>オプション2</strong>:フォームデータモデル、OData、または他のサードパーティサービスをデータソースとして選択します。 Automated Forms Conversion <a href="#generate-adaptive-forms-with-no-data-binding">サービスを使用して、データ連結のない</a> 、アダプティブフォームを生成します。 アダプティブフォームのフィールドを連結するには、ルールエディターを使用してフィールドの値を事前入力します。 必要に応じてフィールド値を変更し、crx-repositoryにデータを送信します。</p>
    </td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
    <p>これらのワークフローを実行する手順については、データベース、ODataまたは任意のサ <a href="#sqldatasource">ードパーティサービスをデータソースとして使用するを参照してください。</a></p> </td> 
  </tr>
  <tr>
  <td><p>JSON スキーマ</p></td> 
   <td> 
    <p>データソースとしてJSONスキーマを選択します。 選択したデータソースに基づいて：</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>オプション1</strong>:Automated Forms Conversion <a href="#generate-adaptive-forms-with-no-data-binding">サービスを使用して</a> 、データ連結のないアダプティブフォームを生成し、JSONスキーマをデータソースとして設定します。 アダプティブフォームのフィールドをJSONスキーマに手動で連結し、サポートさ <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">れている任意のプロトコルを使用して</a> 、フィールドの値を事前入力します。 必要に応じてフィールド値を変更し、crx-repositoryにデータを送信します。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>ワークフローを実行する手順については、JSONスキーマをデータソースと <a href="#jsondatasource">して使用するを参照してください。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>オプション2</strong>:JSONデータ <a href="#generate-adaptive-forms-with-json-binding">連結を使用してアダプティブフォームを生成するには</a> 、Automated Forms Conversionサービスを使用します。 事前入力サービスとフォーム送信機能はシームレスに機能します。 設定手順は不要です。</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>ワークフローを実行する手順については、JSONスキーマをデータソースと <a href="#jsonwithdatabinding">して使用するを参照してください。</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSDスキーマ</p></td> 
   <td> 
    <p>データソースとしてXSDスキーマを選択します。 選択したデータソースに基づいて、Automated Forms Conversion <a href="#generate-adaptive-forms-with-no-data-binding">サービスを使用してデータ連結のないアダプティブフォームを</a> 、データソースとしてXSDスキーマを設定します。 アダプティブフォームのフィールドをXSDスキーマに手動で連結し、サポー <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">トされているプロトコルを使用して</a> 、フィールドの値を事前入力します。 必要に応じてフィールド値を変更し、crx-repositoryにデータを送信します。</p>
    </td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>ワークフローを実行する手順については、「XSDスキーマをデータソースと <a href="#xsddatasource">して使用する」を参照してください。</a></p>
    </td> 
  </tr>
 </tbody> 
</table>


Automated Forms Conversionサービスについて詳しくは、次の記事を参照してください。

* [Automated Forms Conversionサービスの概要](introduction.md)
* [自動フォーム変換サービスの設定](configure-service.md)
* [印刷フォームのアダプティブフォームへの変換](convert-existing-forms-to-adaptive-forms.md)
* [変換されたフォームの確認と修正](review-correct-ui-edited.md)

この記事に記載されている情報は、読者がアダプティブフォームの概念に関する基本的な知識を持つことを前提としています。

## 前提条件 {#pre-requisites}

* Configure an [AEM author instance](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html)
* AEMオーサ [ーインスタンスでの自動フォーム変換サービスの設定](configure-service.md)

## アダプティブフォームのサンプル {#sample-adaptive-form}

使用事例を実行してアダプティブフォームのフィールド値を事前入力し、データソースに送信するには、以下のサンプルPDFファイルをダウンロードします。

ローン申し込みフォームの例

[ファイルを入手](assets/sample_loan_application_form.pdf)

PDFファイルは、Automated Forms Conversionサービスへの入力として機能します。 このファイルはアダプティブフォームに変換されます。 次の画像は、PDF形式のローン申し込みの例を示しています。

![サンプルローン申込フォーム](assets/sample_form_new.png)

## フォームモデルのデータを準備する {#prepare-data-for-form-model}

AEM Forms のデータ統合機能により、複数の異なるデータソースを設定して接続することができます。変換プロセスを使用してアダプティブフォームを生成した後、フォームデータモデル、XSD、またはJSONスキーマに基づいてフォームモデルを定義できます。 データベース、Microsoft Dynamicsまたはその他のサードパーティサービスを使用して、フォームデータモデルを作成できます。

このチュートリアルでは、MySQLデータベースをソースとして使用し、フォームデータモデルを作成します。 データベース **内にローンアプリ** ・スキーマを作成し、アダプティブ・フォームで使用可能 **なフィールドに基づいて** 、申込者テーブルをスキーマに追加します。

![サンプルデータmysql](assets/sample_data_mysql.png)

次のDDL文を使用して、申込者テーブルをデータベ **ース** に作成できます。

```sql
CREATE TABLE `applicant` (
   `name` varchar(45) DEFAULT NULL,
   `address` varchar(45) DEFAULT NULL,
   `phonenumber` int(11) NOT NULL,
   `email` varchar(45) DEFAULT NULL,
   `occupation` varchar(45) DEFAULT NULL,
   `annualsalary` varchar(45) DEFAULT NULL,
   `familymembers` int(11) DEFAULT NULL,
   PRIMARY KEY (`phonenumber`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

XSDスキーマをフォームモデルとして使用して使用事例を実行する場合は、次のテキストを含むXSDファイルを作成します。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="http://adobe.com/sample.xsd"
                    xmlns="http://adobe.com/sample.xsd"
                    xmlns:xs="http://www.w3.org/2001/XMLSchema">

<xs:element name="sample" type="SampleType"/>

  <xs:complexType name="SampleType">
    <xs:sequence>
      <xs:element name="name" type="xs:string"/>
   <xs:element name="address" type="xs:string"/>
   <xs:element name="phonenumber" type="xs:int"/>
   <xs:element name="email" type="xs:string"/>
   <xs:element name="occupation" type="xs:string"/>
   <xs:element name="annualsalary" type="xs:string"/>
   <xs:element name="familymembers" type="xs:string"/>
 </xs:sequence>
  </xs:complexType>

  </xs:schema>
```

または、XSDスキーマをローカルファイルシステムにダウンロードします。

ローン申し込みのXSDスキーマの例

[ファイルを入手](assets/loanapplication.xsd)

XSDスキーマをアダプティブフォームのフォームモデルとして使用する方法について詳しくは、「XMLスキーマを使用したアダプテ [ィブフォームの作成」を参照してくださ](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html)い。

JSONスキーマをフォームモデルとして使用して使用例を実行する場合は、次のテキストを含むJSONファイルを作成します。

```JSON
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "definitions": {
        "loanapplication": {
            "type": "object",
            "properties": {
                "name": {
                    "type": "string"
                },
                "address": {
                    "type": "string"
                },
    "phonenumber": {
                    "type": "number"
                },
    "email": {
                    "type": "string"
                },
    "occupation": {
                    "type": "string"
                },
    "annualsalary": {
                    "type": "string"
                },
    "familymembers": {
                    "type": "number"
                }
            }
        }
 },
 "type": "object",
    "properties": {
        "employee": {
            "$ref": "#/definitions/loanapplication"
        }
    }
}
```

または、JSONスキーマをローカルファイルシステムにダウンロードします。

ローン申し込みJSONスキーマの例

[ファイルを入手](assets/demo_schema.json)

JSONスキーマをアダプティブフォームのフォームモデルとして使用する方法について詳しくは、「JSONスキーマを使用したアダプテ [ィブフォームの作成」を参照してくださ](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html)い。

## データ連結のないアダプティブフォームの生成 {#generate-adaptive-forms-with-no-data-binding}

Automated Forms Conversionサービスを使用 [して](convert-existing-forms-to-adaptive-forms.md) 、サンプルのローン申し込 [みフォームをデータ連結のないアダプティブフォーム](#sample-adaptive-form) に変換します。 データ連結のないアダプティブフォームを生 **[!UICONTROL Generate adaptive form(s) without data bindings]** 成する場合は、必ずチェックボックスをオンにしてください。

![データ連結のないアダプティブフォーム](assets/generate_af_without_binding.png)

データ連結のないアダプティブフォームを生成した後、アダプティブフォームのデータソースを選択します。

* [データベース、OData、または任意のサードパーティサービス](#sqldatasource)
* [JSONスキーマ](#jsondatasource)
* [XSDスキーマ](#xsddatasource)

>[!NOTE]
> Automated Forms Conversionサービスを使用して変換するアダプティブフォームに、同じ名前の複数のフィールドが含まれる場合は、送信時にデータが失われるのを防ぐために、これらのフィールドがデータソースエンティティに連結されていることを確認します。


### データベース、ODataまたは任意のサードパーティサービスをデータソースとして使用する {#sqldatasource}

使用例：Automated Forms Conversionサービスを使用して、データ連結のないアダプティブフォームを生成し、MYSQLデータベースをデータソースとして設定します。 アダプティブフォームフィールドをフォームデータモデルのエンティティに手動で連結し、このオプションを使用し **[!UICONTROL Form Data Model Prefill Service]** てフィールドの値を事前入力します。 このオプションを使 **[!UICONTROL Submit using Form Data Model]** 用して、アダプティブフォームを送信します。

使用事例を実行する前に：

* [MySQLデータベースをデータソースとして設定する](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [フォームデータモデルの作成](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

使用例に基づいて、loanapplication **form data modelを作成し、読み取りサービスの引数を値に連結し****[!UICONTROL Literal]** ます。 電話番号リテラル値は、MySQLデータベースの申込者スキーマで設定されたレコ **ードの** 1つである必要があります。 この値は、データソースから詳細を取得するための引数として使用されます。 また、ドロップダウンリ [ストから「ユーザープロファイル属性](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument) 」または「属性を **[!UICONTROL Binding To]** 要求」を選択できます

![フォームデータモデルを設定する](assets/configure_model_object.png)

>[!NOTE]
>
>使用事例を実行する前に **、必ず** get **and** insert servicesをフォームデータモデルに追加し、設定し、サービスをテストしてください。

次の手順を実行します。

1. フォルダー内の変換 **済みサンプルローン申込** フォームを選択 **[!UICONTROL output]** し、をタップしま **[!UICONTROL Properties]**&#x200B;す。
1. タブをタッ **[!UICONTROL Form Model]** プし、ド **[!UICONTROL Form Data Model]** ロップダウンリ **[!UICONTROL Select From]** ストから選択し、をタップして、アプリケ **[!UICONTROL Select Form Data Model]** ーションフ **** ォームデータモデルを選択します。 Tap **[!UICONTROL Save & Close]** to save the form.
1. サンプルのロ **ーン申し込みフォームを選択し** 、をタップしま **[!UICONTROL Edit]**&#x200B;す。
1. タブで、設 **[!UICONTROL Content]** 定アイコンをタップします。

   ![フォームコンテナの設定](assets/configure_form_container.png)

   1. セクション **[!UICONTROL Basic]** で、ドロップダ **[!UICONTROL Form Data Model Prefill service]** ウンリスト **[!UICONTROL Prefill Service]** からを選択します。

   1. セクション **[!UICONTROL Submission]** で、ドロップダ **[!UICONTROL Submit using Form Data Model]** ウンリスト **[!UICONTROL Submit Action]** からを選択します。

   1. フィールドを使用してデータモデルを選 **[!UICONTROL Data Model to submit]** 択します。
   1. Tap ![done icon](assets/save_icon.svg) to save the properties.

1. 「Applicant Name」テキストボックスをタップし、設定アイコ ![ン](assets/configure_icon.svg) （設定）を選択します。

   1. 「参照を連結」フィールドで、 **Applicant** / **Nameを選択し**、完了ア ![イコンをタ](assets/save_icon.svg) ップしてプロパティを保存します。 同様に、 **Address**, Phone Number, **E-mail**, E-mail **,** Orcupation Annual Salary, Occupation Annual Salary, Occuppation Annual Salury, **********No Data Bindingを作成します。 フォームデータモデルエンティティを持つ** 、従属ファミリメンバフィールドの
   ![バインド参照](assets/bind_references.png)

1. をタップし **[!UICONTROL Preview]** て、事前入力されたアダプティブフォームフィールドの値を表示します。
1. 必要に応じてフィールドの値を変更し、アダプティブフォームを送信します。 フィールド値がMySQLデータベースに送信されます。 データベース内のapplicant **テーブル** を更新して、テーブル内の更新された値を表示できます。

**使用例：** Automated Forms Conversionサービスを使用して、データ連結のないアダプティブフォームを生成し、MYSQLデータベースをデータソースとして設定します。 アダプティブフォームのフィールドを連結するには、ルールエディターを使用してフィールドの値を事前入力します。 必要に応じてフィールド値を変更し、crx-repositoryにデータを送信します。

ルールエディターを使用してフォームデ [ータモデル](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html) ・サービスを呼び出し、アダプティブフォームのフィールドと事前入力値を連結するには、次の手順を実行します。

1. フォルダー内 **のサンプルのローン申し込みフォーム** を選択 **[!UICONTROL output]** し、をタップしま **[!UICONTROL Edit]**&#x200B;す。
1. タブで、設 **[!UICONTROL Content]** 定アイコンをタップします。

   ![フォームコンテナの設定](assets/configure_form_container.png)

   セクション **[!UICONTROL Basic]** で、ドロップダ **[!UICONTROL Form Data Model Prefill service]** ウンリスト **[!UICONTROL Prefill Service]** からを選択します。

1. テキストボッ **[!UICONTROL Applicant Name]** クスをタップし、をタップしま **[!UICONTROL Edit Rules]**&#x200B;す。

   ![ルールを編集してデータ連結を作成する](assets/edit_rules_bind_reference.png)

1. ルールエデ **[!UICONTROL Create]** ィターページでをタップします。
1. On the **[!UICONTROL Rule Editor]** page:

   1. 「申込者名」テキストボックスの州を選択します。 例えば、モ **[!UICONTROL is initialized]**&#x200B;ードでフォームをレンダリ **[!UICONTROL Then]** ングする場合に条件が実行され **[!UICONTROL Preview]** ます。

   1. セクション **[!UICONTROL Then]** で、ドロップダ **[!UICONTROL Invoke Service]** ウンリスト **[!UICONTROL Select Action]** からを選択します。 Formsインスタンス上のすべてのサービスがドロップダウンリストに表示されます。

   1. フォームデー **[!UICONTROL Get]** タモデルの一覧表示のセクションからサービスを選択します。 「Input」フィールドに **は**、応募者データモデル用に定義された主キーであるPhoneNumber **が表示されます** 。 このフィールドに基づいて、「出力」セクションのフィールドのアダプティブフォーム内の値が取得され、事前入力されます。

   1. 「出力」セクションを使用して、フォームデータモデルエンティティを含むアダプティブフォームフィールドの連結を作成します。 例えば、アダプティブフォ **[!UICONTROL Applicant Name]** ームフィールドを名前エンティティと連 **結し** ます。

   1. タップ **[!UICONTROL Done]**. ルールエデ **[!UICONTROL Done]** ィターページでを再度タップします。
   ![参照を連結するルールエディタ](assets/rule_editor_bind_references.png)

1. をタップし **[!UICONTROL Preview]** て、事前入力されたアダプティブフォームフィールドの値を表示します。

   >[!NOTE]
   >
   >アダプティブフォ **[!UICONTROL Return Array]** ームに関連付けられたフォームデータモデルの **get** serviceプロパティに対して、PropertyがOFFに設定されていることを確認します。

1. 必要に応じてフィールドの値を変更し、アダプティブフォームを送信します。 送信されたデータは、crx-repository内の次の場所で利用できます。

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### JSONスキーマをデータソースとして使用する {#jsondatasource}

**使用例：** Automated Forms Conversionサービスを使用して、データ連結のないアダプティブフォームを生成し、JSONスキーマをデータソースとして設定します。 アダプティブフォームのフィールドをJSONスキーマに手動で連結し、「データと共にプレビ **ュー」オプションを使用して** 、フィールドの値を事前入力します。 必要に応じてフィールド値を変更し、crx-repositoryにデータを送信します。

使用事例を実行する前に、次の事項を確認します。

* [JSONスキーマ構造に準拠した有効なJSONスキーマ](#prepare-data-for-form-model)
* [データ連結のないアダプティブフォーム](#generate-adaptive-forms-with-no-data-binding)

次の手順を実行します。

1. 出力フォルダーで **使用可能な変換済みサンプルローン申し込みフォーム** を選択し **、** 「」をタップしま **[!UICONTROL Properties]**&#x200B;す。
1. タブをタッ **[!UICONTROL Form Model]** プし、ドロ **[!UICONTROL Schema]** ップダウンリ **[!UICONTROL Select From]** ストから選択し、をタップして、ローカルファイルシステムに保存され **[!UICONTROL Select Schema]** たdemo.schema JSON **** schemaをアップロードします。 Tap **[!UICONTROL Save & Close]** to save the form.
1. サンプルのロ **ーン申し込みフォームを選択し** 、をタップしま **[!UICONTROL Edit]**&#x200B;す。
1. 「Applicant Name」テキストボックスをタップし、設定アイコ ![ン](assets/configure_icon.svg) （設定）を選択します。

   「参照を連結」フィールドで、 **Applicant** / **Nameを選択し**、完了ア ![イコンをタ](assets/save_icon.svg) ップしてプロパティを保存します。 同様に、 **Address**, Phone Number, **E-mail**, E-mail **,** Orcupation Annual Salary, Occupation Annual Salary, Occuppation Annual Salury, **********No Data Bindingを作成します。 JSONスキーマエンティティを持つ** 、従属ファミリメンバーフィールドの

1. フォルダーで再び使 **用可能な変換済みのサンプル** ・ローンの申し込 **[!UICONTROL output]** みフォームを選択し、「/」を **[!UICONTROL Preview]** 選択しま **[!UICONTROL Preview with Data]**&#x200B;す。</br>

   サンプルデータファイルのダウンロード</br>

   [ファイルを入手](assets/json_data_file.txt)</br>

1. 必要に応じてフィールドの値を変更し、アダプティブフォームを送信します。 送信されたデータは、crx-repository内の次の場所で利用できます。

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### XSDスキーマをデータソースとして使用する {#xsddatasource}

**使用例：** Automated Forms Conversionサービスを使用して、データ連結のないアダプティブフォームを生成し、XSDスキーマをデータソースとして設定します。 アダプティブフォームフィールドをXSDスキーマに手動で連結し、「データと共にプレビュ **ー」を使用して** 、フィールドの値を事前入力します。 必要に応じてフィールド値を変更し、crx-repositoryにデータを送信します。

使用事例を実行する前に、次の事項を確認します。

* [xmlスキーマ構造に準拠した有効なXSDスキーマ](#prepare-data-for-form-model)
* [データ連結のないアダプティブフォーム](#generate-adaptive-forms-with-no-data-binding)

次の手順を実行します。

1. フォルダー内の変換 **済みサンプルローン申込** フォームを選択 **[!UICONTROL output]** し、をタップしま **[!UICONTROL Properties]**&#x200B;す。
1. タブをタッ **[!UICONTROL Form Model]** プし、ドロッ **[!UICONTROL Schema]** プダウンリ **[!UICONTROL Select From]** ストから選択し、をタップして、ローカルファイルシステムに保存され **[!UICONTROL Select Schema]** ているローンアプリ **** XSDスキーマをアップロードします。 XSDスキーマのルート要素を選択し、をタップして **[!UICONTROL Save & Close]** フォームを保存します。
1. サンプルのロ **ーン申し込みフォームを選択し** 、をタップしま **[!UICONTROL Edit]**&#x200B;す。
1. 「Applicant Name」テキストボックスをタップし、設定アイコ ![ン](assets/configure_icon.svg) （設定）を選択します。
「参照を連結」フィールドで、 **Applicant** / **Nameを選択し、**「完了」ア ![イコンをタップして](assets/save_icon.svg) 、プロパティを保存します。 同様に、 **Address**, Phone Number, **E-mail**, E-mail **,** Orcupation Annual Salary, Occupation Annual Salary, Occuppation Annual Salury, **********No Data Bindingを作成します。 XSDスキーマエンティティを持つ依存ファミリ** ・メンバー・フィールドの

1. 出力フォルダーで **使用可能な変換済みサンプルローン申し込みフォーム** を再度選択 **し、** /を選択 **[!UICONTROL Preview]** してくださ **[!UICONTROL Preview with Data]**&#x200B;い。</br>

   サンプルデータファイルのダウンロード</br>

   [ファイルを入手](assets/loan-application-data-xml-data.zip)</br>


1. 必要に応じてフィールドの値を変更し、アダプティブフォームを送信します。 送信されたデータは、crx-repository内の次の場所で利用できます。

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## JSONバインディングを使用したアダプティブフォームの生成 {#generate-adaptive-forms-with-json-binding}

Automated Forms Conversionサービスを使用 [して](convert-existing-forms-to-adaptive-forms.md) 、サンプルのローン申し込 [みフォームをデータ連結のあるアダプティブフォーム](#sample-adaptive-form) に変換します。 アダプティブフォームの生成時に、チェックボッ **[!UICONTROL Generate adaptive form(s) without data bindings]** クスをオンにしないようにしてください。

![JSONバインディングを使用したアダプティブフォーム](assets/generate_af_with_data_bindings.png)

### JSONスキーマをデータソースとして使用する {#jsonwithdatabinding}

**使用例：** Automated Forms Conversionサービスを使用して、JSONデータ連結を使用してアダプティブフォームを生成します。 事前入力サービスとフォーム送信機能はシームレスに機能します。 設定手順は不要です。

使用事例を実行する前に、データ連結を含むアダプテ [ィブフォームがあることを確認します](#generate-adaptive-forms-with-json-binding)。

次の手順を実行します。

1. フォルダーで再び使 **用可能な変換済みのサンプル** ・ローンの申し込 **[!UICONTROL output]** みフォームを選択し、「/」を **[!UICONTROL Preview]** 選択しま **[!UICONTROL Preview with Data]**&#x200B;す。</br>

   サンプルデータファイルのダウンロード</br>

   [ファイルを入手](assets/loan_application_data_source_json_data_binding.txt)</br>

1. 必要に応じてフィールドの値を変更し、アダプティブフォームを送信します。 送信されたデータは、crx-repository内の次の場所で利用できます。

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 送信されたアダプティブフォームのJSONデータをXML形式に変換 {#convert-submitted-adaptive-form-data-to-xml}

アダプティブフォームのフィールドに値を入力して送信すると、データはJSON形式でcrx-repositoryで使用できます。 JSONデータの形式は、 [org.apache.sling.commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) APIまたは次のサンプルコードを使用してXMLに変換できます。

```
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;
import org.apache.sling.commons.json.xml.XML;
 
public class ConversionUtils {
 
    public static String jsonToXML(String jsonString) throws JSONException {
        //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
        //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
        //Note: Need to extract boundData part before converting to XML
        return XML.toString(new JSONObject(jsonString));
    }
}
```

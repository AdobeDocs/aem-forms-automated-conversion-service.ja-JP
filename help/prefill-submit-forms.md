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
source-git-commit: f598871fd41c402f98d94d7b2174ab8b2e487075

---


# アダプティブフォームの推奨データソースベースの事前入力および送信ワークフロー {#recommended-data-source-btased-prefill-and-submit-workflows-for-adaptive-forms}

Automated Forms Conversionサービスを使用して変換されたアダプティブフォームでは、次のデータソースを使用できます。

* フォームデータモデル、OData、またはその他のサードパーティサービス
* JSONスキーマ
* XSDスキーマ

データソースに基づいて、データモデルの有無に関係なくアダプティブフォームを生成するよう選択できます。

この記事では、データソースを選択し、コンバージョンサービスを使用してアダプティブフォームを生成した後に、フィールドの値と送信オプションを事前入力するための推奨ワークフローについて説明します。

<table> 
 <tbody> 
  <tr> 
   <th><strong>データソース</strong></th> 
   <th><strong>推奨ワークフロー</strong></th> 
  </tr> 
  <tr> 
   <td><p>フォームデータモデル、OData、またはその他のサードパーティサービス</p></td> 
   <td> 
    <p><strong>オプション1</strong>:フォームデータモデル、OData、または他のサードパーティサービスをデータソースとして選択します。 Automated Forms Conversion <a href="#generate-adaptive-forms-with-no-data-binding">サービスを使用して、データ連結のないアダプティブ</a> ・フォームを生成します。 アダプティブフォームフィールドをフォームデータモデルエンティティに手動で連結し、「Form Data Model Prefill Service」オプションを使用してフィールドの値を事前入力します。 「フォームデータモデルを使用して送信」オプションを使用して、アダプティブフォームを送信します。</p></td> 
  </tr>
  <tr> 
   <td></td> 
   <td> 
   <p><strong>オプション2</strong>:フォームデータモデル、OData、または他のサードパーティサービスをデータソースとして選択します。 Automated Forms Conversion <a href="#generate-adaptive-forms-with-no-data-binding">サービスを使用して、データ連結のないアダプティブ</a> ・フォームを生成します。 アダプティブフォームのフィールドを連結するには、ルールエディターを使用してフィールドの値を事前入力します。 必要に応じてフィールドの値を変更し、crx-repositoryにデータを送信します。</p>
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
    <p>データソースとしてJSONスキーマを選択します。 選択したデータソースに基づいて、次の操作を行います。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>オプション1</strong>:Automated Forms Conversion <a href="#generate-adaptive-forms-with-no-data-binding">サービスを使用して、データ連結のないアダプティブフォームを生成し</a> 、データソースとしてJSONスキーマを設定します。 アダプティブフォームのフィールドをJSONスキーマに手動で連結し、サポートさ <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">れている任意のプロトコルを使用して</a> 、フィールドの値を事前入力します。 必要に応じてフィールドの値を変更し、crx-repositoryにデータを送信します。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p>ワークフローを実行する手順については、「JSONスキーマをデータソースと <a href="#jsondatasource">して使用する」を参照してください。</p></td> 
  </tr>
  <tr>
  <td></td> 
   <td> 
    <p><strong>オプション2</strong>:Automated Forms Conversion <a href="#generate-adaptive-forms-with-json-binding">サービスを使用して、JSONデータ連結を使用し</a> 、アダプティブフォームを生成します。 事前入力サービスとフォーム送信機能はシームレスに動作します。 設定手順は不要です。</p> </td> 
  </tr>
   <tr>
  <td></td> 
   <td> 
    <p>ワークフローを実行する手順については、「JSONスキーマをデータソースと <a href="#jsonwithdatabinding">して使用する」を参照してください。</a></p> </td> 
  </tr>
  <tr>
  <td><p>XSDスキーマ</p></td> 
   <td> 
    <p>データソースとしてXSDスキーマを選択します。 選択したデータソースに基づいて、Automated Forms Conversion <a href="#generate-adaptive-forms-with-no-data-binding">サービスを使用してデータ連結のないアダプティブフォームを生成し</a> 、XSDスキーマをデータソースとして設定します。 アダプティブフォームフィールドをXSDスキーマに手動で連結し、サポートさ <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#Supportedprotocolsforprefillinguserdata" target="_blank">れているプロトコルを使用して</a> 、フィールド値を事前入力します。 必要に応じてフィールドの値を変更し、crx-repositoryにデータを送信します。</p>
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
* [Automated Forms Conversionサービスの設定](configure-service.md)
* [印刷フォームをアダプティブフォームに変換する](convert-existing-forms-to-adaptive-forms.md)
* [変換済みフォームの確認と修正](review-correct-ui-edited.md)

この記事に記載されている情報は、読者がアダプティブフォームの概念に関する基本的な知識を持つことを前提としています。

## 前提条件 {#pre-requisites}

* Configure an [AEM author instance](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html)
* AEMオーサ [ーインスタンスでのAutomated Forms Conversionサービスの設定](configure-service.md)

## アダプティブフォームのサンプル {#sample-adaptive-form}

アダプティブフォームのフィールド値を事前入力し、データソースに送信するための使用例を実行するには、次のサンプルPDFファイルをダウンロードします。

ローン申し込みフォームの例

[ファイルを入手](assets/sample_loan_application_form.pdf)

PDFファイルは、Automated Forms Conversionサービスへの入力として機能します。 このファイルはアダプティブフォームに変換されます。 次の画像は、PDF形式のローン申し込みの例を示しています。

![申込書](assets/sample_form_new.png)

## フォームモデルのデータを準備する {#prepare-data-for-form-model}

AEM Forms のデータ統合機能により、複数の異なるデータソースを設定して接続することができます。変換プロセスを使用してアダプティブフォームを生成した後、フォームデータモデル、XSD、またはJSONスキーマに基づいてフォームモデルを定義できます。 フォームデータモデルの作成には、データベース、Microsoft Dynamics、またはその他のサードパーティサービスを使用できます。

このチュートリアルでは、MySQLデータベースをソースとして使用し、フォームデータモデルを作成します。 データベース **にローンアプリ** ・スキーマを作成し、アダプティブ・フォームで使用可能 **なフィールドに基づいて** 、スキーマにapplicantテーブルを追加します。

![サンプルデータmysql](assets/sample_data_mysql.png)

次のDDL文を使用して、申込者テーブルをデータベースに **作成でき** ます。

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

フォームモデルとしてXSDスキーマを使用して使用事例を実行する場合は、次のテキストを含むXSDファイルを作成します。

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

ローン申し込みXSDスキーマのサンプル

[ファイルを入手](assets/loanapplication.xsd)

XSDスキーマをアダプティブフォームのフォームモデルとして使用する方法について詳しくは、「XMLスキーマを使用したアダプ [ティブフォームの作成」を参照してくださ](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-xml-schema-form-model.html)い。

フォームモデルとしてJSONスキーマを使用して使用事例を実行する場合は、次のテキストを含むJSONファイルを作成します。

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

アダプティブフォームでのフォームモデルとしてのJSONスキーマの使用に関する詳細は、「JSONスキーマを使用したアダプ [ティブフォームの作成」を参照してくださ](https://helpx.adobe.com/experience-manager/6-5/forms/using/adaptive-form-json-schema-form-model.html)い。

## データ連結のないアダプティブフォームの生成 {#generate-adaptive-forms-with-no-data-binding}

Automated Forms Conversionサービスを使用 [して](convert-existing-forms-to-adaptive-forms.md) 、サンプルローン申し込 [みフォームをデータ連結のないアダプティブフォームに](#sample-adaptive-form) 変換します。 データ連結のないアダプティブフ **[!UICONTROL Generate adaptive form(s) without data bindings]** ォームを生成する場合は、このチェックボックスを必ずオンにしてください。

![データ連結のないアダプティブフォーム](assets/generate_af_without_binding.png)

データ連結のないアダプティブフォームを生成した後、アダプティブフォームのデータソースを選択します。

* [データベース、ODataまたはサードパーティのサービス](#sqldatasource)
* [JSONスキーマ](#jsondatasource)
* [XSDスキーマ](#xsddatasource)

>[!NOTE]
> 自動フォーム変換サービスを使用して変換するアダプティブフォームに、同じ名前の複数のフィールドが含まれている場合は、送信中にデータが失われるのを防ぐために、それらのフィールドがデータソースエンティティに連結されていることを確認します。


### データベース、ODataまたはサードパーティのサービスをデータソースとして使用する {#sqldatasource}

使用例：Automated Forms Conversionサービスを使用して、データ連結のないアダプティブフォームを生成し、MYSQLデータベースをデータソースとして設定します。 アダプティブフォームフィールドをフォームデータモデルのエンティティに手動で連結し、このオプションを使用 **[!UICONTROL Form Data Model Prefill Service]** してフィールドの値を事前入力します。 このオプションを使 **[!UICONTROL Submit using Form Data Model]** 用して、アダプティブフォームを送信します。

使用事例を実行する前に、次の手順を実行します。

* [MySQLデータベースをデータソースとして設定する](https://helpx.adobe.com/experience-manager/6-5/forms/using/configure-data-sources.html#configurerelationaldatabase)
* [フォームデータモデルの作成](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html)

使用例に基づいて、loanapplication **form data modelを作成し、読み取りサービスの引数を値に連結****[!UICONTROL Literal]** します。 電話番号リテラル値は、MySQLデータベースの申込者スキーマで設定されたレコ **ードの** 1つである必要があります。 この値は、データソースから詳細を取得するための引数として使用されます。 また、ドロップダウンリ [ストから「ユーザープロファイル属性」または](https://helpx.adobe.com/experience-manager/6-5/forms/using/work-with-form-data-model.html#bindargument) 「要求属性」 **[!UICONTROL Binding To]** を選択することもできます

![フォームデータモデルを設定する](assets/configure_model_object.png)

>[!NOTE]
>
>使用例を実行する前に、 **get** and **insert** servicesをフォームデータモデルに追加し、設定し、サービスをテストしてください。

次の手順を実行します。

1. フォルダー内の変換済 **みサンプルローン申込フォーム** を選択し、 **[!UICONTROL output]** をタップしま **[!UICONTROL Properties]**&#x200B;す。
1. タブをタッ **[!UICONTROL Form Model]** プし、ドロッ **[!UICONTROL Form Data Model]** プダウンリ **[!UICONTROL Select From]** ストから選択し、をタップして **[!UICONTROL Select Form Data Model]** アプリケーシ **ョンフォーム** データモデルを選択します。 Tap **[!UICONTROL Save & Close]** to save the form.
1. サンプルのロ **ーン申込フォームを選択し** 、をタップしま **[!UICONTROL Edit]**&#x200B;す。
1. タブで、設 **[!UICONTROL Content]** 定アイコンをタップします。

   ![フォームコンテナの設定](assets/configure_form_container.png)

   1. セクション **[!UICONTROL Basic]** で、ドロップダ **[!UICONTROL Form Data Model Prefill service]** ウンリスト **[!UICONTROL Prefill Service]** から選択します。

   1. セクション **[!UICONTROL Submission]** で、ドロップダ **[!UICONTROL Submit using Form Data Model]** ウンリスト **[!UICONTROL Submit Action]** から選択します。

   1. フィールドを使用してデータモデルを選択 **[!UICONTROL Data Model to submit]** します。
   1. Tap ![done icon](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) to save the properties.

1. 「Applicant Name」テキストボックスをタップし、「 ![configure」アイコン](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) （設定）を選択します。

   1. 「参照を連結」フィールドで、 **Applicant** / **Nameを選択し**、完了アイコン ![をタップして](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 、プロパティを保存します。 同様に、 **Address**, Phone Number, **E-mail**-E-mail **,************Salary (Dollars Andulary), Occupation Annual Salary (Occupation Nocupation Phone Number), No Adeのデータ連結を作成します。 フォームデータモデルエンティティを持つ依存ファミリーメンバー** （従属ファミリーメンバー）フィールドの
   ![バインド参照](assets/bind_references.png)

1. をタップし **[!UICONTROL Preview]** て、事前入力されたアダプティブフォームフィールドの値を表示します。
1. 必要に応じてフィールド値を変更し、アダプティブフォームを送信します。 フィールドの値がMySQLデータベースに送信されます。 データベース内のapplicantテーブル **を更新し** 、更新された値をテーブルに表示することができます。

**** 使用例：Automated Forms Conversionサービスを使用して、データ連結のないアダプティブフォームを生成し、MYSQLデータベースをデータソースとして設定します。 アダプティブフォームのフィールドを連結するには、ルールエディターを使用してフィールドの値を事前入力します。 必要に応じてフィールドの値を変更し、crx-repositoryにデータを送信します。

ルールエディターを使用してフォームデ [ータモデル](https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html) ・サービスを呼び出し、アダプティブフォーム内のフィールドと事前入力値を連結するには、次の手順を実行します。

1. フォルダー内 **のサンプルローン申込フォーム** を選択 **[!UICONTROL output]** し、をタップしま **[!UICONTROL Edit]**&#x200B;す。
1. タブで、設 **[!UICONTROL Content]** 定アイコンをタップします。

   ![フォームコンテナの設定](assets/configure_form_container.png)

   セクション **[!UICONTROL Basic]** で、ドロップダ **[!UICONTROL Form Data Model Prefill service]** ウンリスト **[!UICONTROL Prefill Service]** から選択します。

1. テキストボックス **[!UICONTROL Applicant Name]** をタップし、をタップしま **[!UICONTROL Edit Rules]**&#x200B;す。

   ![ルールを編集してデータ連結を作成する](assets/edit_rules_bind_reference.png)

1. ルールエ **[!UICONTROL Create]** ディターページでをタップします。
1. On the **[!UICONTROL Rule Editor]** page:

   1. 「申込者名」テキストボックスの州を選択します。 例えば、モ **[!UICONTROL is initialized]**&#x200B;ードでフォームをレンダリングす **[!UICONTROL Then]** るときに条件が実行され **[!UICONTROL Preview]** ます。

   1. セクション **[!UICONTROL Then]** で、ドロップダ **[!UICONTROL Invoke Service]** ウンリスト **[!UICONTROL Select Action]** から選択します。 Formsインスタンス上のすべてのサービスがドロップダウンリストに表示されます。

   1. フォームデー **[!UICONTROL Get]** タモデルの一覧を示すセクションからサービスを選択します。 「Input」フィールドには、 **phonenumber**（応募者データモデル用に定義された主キー） **が表示されます** 。 「出力」セクションのフィールドのアダプティブフォーム内の値が、このフィールドに基づいて取得され、事前入力されます。

   1. 「出力」セクションを使用して、フォームデータモデルエンティティを含むアダプティブフォームフィールドの連結を作成します。 例えば、アダプティブフォ **[!UICONTROL Applicant Name]** ームフィールドに名前エンティティ **を連結** します。

   1. タップ **[!UICONTROL Done]**. ルールエ **[!UICONTROL Done]** ディターページでを再度タップします。
   ![参照を連結するルールエディター](assets/rule_editor_bind_references.png)

1. をタップし **[!UICONTROL Preview]** て、事前入力されたアダプティブフォームフィールドの値を表示します。

   >[!NOTE]
   >
   >アダプティブフォ **[!UICONTROL Return Array]** ームに関連付けられたフォームデータモデルの **get** serviceプロパティに対して、PropertyがOFFに設定されていることを確認します。

1. 必要に応じてフィールド値を変更し、アダプティブフォームを送信します。 送信されたデータは、crx-repositoryの次の場所で入手できます。

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### JSONスキーマをデータソースとして使用 {#jsondatasource}

**** 使用例：Automated Forms Conversionサービスを使用して、データ連結のないアダプティブフォームを生成し、JSONスキーマをデータソースとして設定します。 アダプティブフォームフィールドをJSONスキーマに手動で連結し、「データと共にプレビ **ュー」オプションを使用して** 、フィールドの値を事前入力します。 必要に応じてフィールドの値を変更し、crx-repositoryにデータを送信します。

使用事例を実行する前に、次の事項を確認してください。

* [JSONスキーマ構造に準拠した有効なJSONスキーマ](#prepare-data-for-form-model)
* [データ連結のないアダプティブフォーム](#generate-adaptive-forms-with-no-data-binding)

次の手順を実行します。

1. 出力フォルダーで **使用可能な変換済みサンプルローン申し込みフォーム** を選択 **し、** 「」をタ **[!UICONTROL Properties]**&#x200B;ップします。
1. タブをタッ **[!UICONTROL Form Model]** プし、ドロップダ **[!UICONTROL Schema]** ウンリ **[!UICONTROL Select From]** ストから選択し、をタップして、ローカルファイルシステムに保存され **[!UICONTROL Select Schema]** たdemo.schema JSON **** schemaをアップロードします。 Tap **[!UICONTROL Save & Close]** to save the form.
1. サンプルのロ **ーン申込フォームを選択し** 、をタップしま **[!UICONTROL Edit]**&#x200B;す。
1. 「Applicant Name」テキストボックスをタップし、「 ![configure」アイコン](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) （設定）を選択します。

   「参照を連結」フィールドで、 **Applicant** / **Nameを選択し**、完了アイコン ![をタップして](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 、プロパティを保存します。 同様に、 **Address**, Phone Number, **E-mail**-E-mail **,************Salary (Dollars Andulary), Occupation Annual Salary (Occupation Nocupation Phone Number), No Adeのデータ連結を作成します。 JSONスキーマエンティティを持つ依存ファミリ** ・メンバー・フィールドの

1. フォルダーで再び使 **用可能な変換済みサンプルローン** 申し込みフォームを **[!UICONTROL output]** 選択し、「/」を **[!UICONTROL Preview]** 選択しま **[!UICONTROL Preview with Data]**&#x200B;す。</br>

   サンプルデータファイルのダウンロード</br>

   [ファイルを入手](assets/json_data_file.txt)</br>

1. 必要に応じてフィールド値を変更し、アダプティブフォームを送信します。 送信されたデータは、crx-repositoryの次の場所で入手できます。

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

### XSDスキーマをデータソースとして使用する {#xsddatasource}

**** 使用例：Automated Forms Conversionサービスを使用して、データ連結のないアダプティブフォームを生成し、XSDスキーマをデータソースとして設定します。 アダプティブフォームフィールドをXSDスキーマに手動で連結し、「データと共にプレビ **ュー」を使用して** 、フィールドの値を事前入力します。 必要に応じてフィールドの値を変更し、crx-repositoryにデータを送信します。

使用事例を実行する前に、次の事項を確認してください。

* [xmlスキーマ構造に準拠した有効なXSDスキーマ](#prepare-data-for-form-model)
* [データ連結のないアダプティブフォーム](#generate-adaptive-forms-with-no-data-binding)

次の手順を実行します。

1. フォルダー内の変換済 **みサンプルローン申込フォーム** を選択し、 **[!UICONTROL output]** をタップしま **[!UICONTROL Properties]**&#x200B;す。
1. タブをタップ **[!UICONTROL Form Model]** し、ドロッ **[!UICONTROL Schema]** プダウンリスト **[!UICONTROL Select From]** から選択し、をタップして、ローカルファイルシステムに保存され **[!UICONTROL Select Schema]** たアプリ **** XSDスキーマをアップロードします。 XSDスキーマのルート要素を選択し、をタップしてフ **[!UICONTROL Save & Close]** ォームを保存します。
1. サンプルのロ **ーン申込フォームを選択し** 、をタップしま **[!UICONTROL Edit]**&#x200B;す。
1. 「Applicant Name」テキストボックスをタップし、「 ![configure」アイコン](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) （設定）を選択します。
「Bind Reference」フィールドで、 **Applicant** / **Nameを選択し、**「 ![Done Icon](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 」をタップしてプロパティを保存します。 同様に、 **Address**, Phone Number, **E-mail**-E-mail **,************Salary (Dollars Andulary), Occupation Annual Salary (Occupation Nocupation Phone Number), No Adeのデータ連結を作成します。 のXSDスキーマエンティティを持つ依存ファミリ** ・メンバー・フィールドの

1. もう一度出力フォ **ルダーで使用可能な変換済みサンプルロー** ン申し込みフォーム **を選択し、** / **[!UICONTROL Preview]** を選択しま **[!UICONTROL Preview with Data]**&#x200B;す。</br>

   サンプルデータファイルのダウンロード</br>

   [ファイルを入手](assets/loan-application-data-xml-data.zip)</br>


1. 必要に応じてフィールド値を変更し、アダプティブフォームを送信します。 送信されたデータは、crx-repositoryの次の場所で入手できます。

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## JSONバインディングを使用したアダプティブフォームの生成 {#generate-adaptive-forms-with-json-binding}

Automated Forms Conversionサービスを使用 [して](convert-existing-forms-to-adaptive-forms.md) 、サンプルローン申し込 [みフォームをデータ連結付きのアダプティブフォーム](#sample-adaptive-form) に変換します。 アダプティブフォームの生成中は、チェックボ **[!UICONTROL Generate adaptive form(s) without data bindings]** ックスをオンにしないでください。

![JSONバインディングを使用したアダプティブフォーム](assets/generate_af_with_data_bindings.png)

### JSONスキーマをデータソースとして使用 {#jsonwithdatabinding}

**** 使用例：Automated Forms Conversionサービスを使用して、JSONデータ連結を使用したアダプティブフォームを生成します。 事前入力サービスとフォーム送信機能はシームレスに動作します。 設定手順は不要です。

使用例を実行する前に、データ連結を含むアダプティブフ [ォームがあることを確認します](#generate-adaptive-forms-with-json-binding)。

次の手順を実行します。

1. フォルダーで再び使 **用可能な変換済みサンプルローン** 申し込みフォームを **[!UICONTROL output]** 選択し、「/」を **[!UICONTROL Preview]** 選択しま **[!UICONTROL Preview with Data]**&#x200B;す。</br>

   サンプルデータファイルのダウンロード</br>

   [ファイルを入手](assets/loan_application_data_source_json_data_binding.txt)</br>

1. 必要に応じてフィールド値を変更し、アダプティブフォームを送信します。 送信されたデータは、crx-repositoryの次の場所で入手できます。

   `http://host name:port/crx/de/index.jsp#/content/forms/fp/admin/submit/data/latest file available in the folder`

## 送信済みのアダプティブフォームJSONデータをXML形式に変換 {#convert-submitted-adaptive-form-data-to-xml}

アダプティブフォームのフィールドに値を入力して送信すると、データはcrx-repositoryでJSON形式で使用できます。 JSONデータの形式は、 [org.apache.sling.commons.json.xml](https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString) APIまたは次のサンプルコードを使用してXMLに変換できます。

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

---
title: 変換済みフォームの確認と修正
seo-title: 変換済みフォームの確認と修正
description: Automated Forms Conversionサービスによって変換されたアダプティブフォームを確認し、修正します。
seo-description: Automated Forms Conversionサービスによって変換されたアダプティブフォームの確認と修正
uuid: 5a0a6d24-dff6-4732-b607-24848b07b26d
topic-tags: forms
discoiquuid: f45ab2d7-5234-42d6-aeb6-b2cb1a7ce3c2
translation-type: tm+mt
source-git-commit: 3303c72b7d644dd183c036ba3cc48e629a9a503e

---


# 変換済みフォームの確認と修正{#review-and-correct-converted-forms}

AEM Forms自動フォーム変換サービスは、入力PDFドキュメントのフィールド、コンテンツ、レイアウトを識別し、PDFドキュメントをアダプティブフォームに変換します。 出力されたアダプティブフォームに、いくつかの見つからないフィールドや不適切に変換されたフィールドが含まれる場合があります。 「レビューと修正」エディターを使用して、特定したフィールドに改善を加え、アダプティブフォームを再生成して、目的のエクスペリエンスに近い出力を得ることができます。 最初の変換後、入力PDFドキュメントをエディターで開くと、次の操作を行うことができます。

* 変換中に特定されたすべてのフィールドとコンテンツを表示します
* 変換中に失われたフィールドとコンテンツの特定
* 必要に応じて、フィールドの種類を確認し、その種類を変更します
* 識別されたテーブルの検証、列のサイズ変更、セルの内容の変更
* 誤って識別されたフィールドの削除

必要な変更を行った後、PDFフォームを変換サービスに再送信します。 変換が成功すると、アダプティブフォームやスキーマを含む更新済みのアセットがAEM Formsインスタンスにダウンロードされます。 目的のエクスペリエンスが達成されるまで、このプロセスを繰り返すことができます。 ![](assets/stages-of-form-2.gif)

レビューおよび修正エディターを使用するには、Google Chrome、Mozilla fireFoxまたはMicrosoft edgeブラウザーが必要です。 エディターはInternet Explorerをサポートしていません。

## レビューと修正エディターへようこそ {#welcome-to-review-and-correct-editor}

レビューと修正のエディターは、使いやすいインターフェイスです。 次のコンポーネントがあります。

* コンテンツブラウザー：コンテンツブラウザーを使用して、要素の位置を変更できます。 コンテンツブラウザーを使用すると、フォームオブジェクトをドラッグ&amp;ドロップして位置を変更できます。 例えば、テキストボックスの前にテーブルを移動するなどです。 これに応じて、出力アダプティブフォームのタブ順序が変更されます。
* プロパティブラウザー：選択したフィールドのプロパティが表示されます。 また、プロパティを変更することもできます。
* ツールバー：ツールバーはエディターの上部に表示されます。 フィールドの追加、変更、グループ化、グループ化解除、削除を行うツールが表示されます。
* プロパティを開く：アイコンをタップすると、「プロパティを開く」オプションが表示 ![](assets/properties.png) されます。 「プロパティを開く」をクリックしてフォームのプロパティを開き、追加のオプションを表示できます。
* フィルタボタン：フィルターボタ ![](assets/toggle_eye.png) ンはエディターの上部にあります。 これにより、フィールドをフィルタして、テキスト、フィールド、選択グループ、パネル、またはすべてのコンポーネントのみを表示できます。
* 保存ボタン：ボ **[!UICONTROL Save]** タンはエディターの右上隅にあります。 「保存」ボタンの横の矢印を使用して、変換用にフォームを送信するオプションを表示することもできます。

* PDFフォーム：エディターにソースPDFドキュメントが表示され、識別されたフィールドと共にオーバーレイされます。 ツールバーのツールを使用して、フィールドを変更できます。
* ページ：1つのソースフォームに複数のページを含めることができます。 エディターの右上隅には、ページ間を移動するためのボタンが表示されます。

![UIの確認と修正](assets/reviewcorrectui.png)

**************A.コンテンツブラ**&#x200B;ウザBプロパティブ **ラウザC.** Toolbar **D.「プロパティ」ボ**&#x200B;タンE.フィルターボ **タンF。「保存」ボ**&#x200B;タンG識別されたフィールドでオーバーレイされたPDFフォーム

最初の変換が成功した後、変換サービスは、特定されたフィールドとコンポーネントを含むソースPDFドキュメントをオーバーレイします。 次のフィールドまたはコンポーネントの種類があります。テキスト、フィールド、パネル、選択グループおよびテーブル：

* テキスト：ソースPDFドキュメントのプレーンテキスト。 例えば、上に示した画像の「Loan Application」テキストなどです。
* フィールド：値または入力ボックスに関連付けられたテキストまたはアイコンラベルの組み合わせ。 例えば、上の画像の「名」フィールド名などです。 テキストラベルと入力ボックスがあります。 フィールドは、テキスト、数値、ドロップダウン、日付、電子メール、電話番号、署名、通貨、パスワードの各データタイプをサポートしています。
* パネル：コンテンツとコンポーネントの論理的なコレクション。 例えば、上の画像の人物1パネルと人物2パネルの個人情報。
* 選択グループ：複数選択オプションに関連付けられたテキストの組み合わせ：チェックボックスとラジオボタン 例えば、上の画像の「Marital status（婚姻状況）」や「Existing customer（既存の顧客）」などです。\
   変換サービスは、選択グループのキャプションとその複数選択オプションに基づいて、選択グループを単一選択ラジオボタンまたは複数選択チェックボックスに自動変換します。 例えば、「 **Select any** one as the choice group caption」または「 **Yes** 」または「 **No**」の選択肢を1つだけ選択できる場合、変換サービスは選択肢グループを自動的に単一選択ラジオボタンに変換します。 同様に、「 **Select all that apply** or **Select multiple** 」が選択グループキャプションまたは複数選択オプションとして指定されている場合、変換サービスは選択グループを自動的に複数選択チェックボックスに変換します。

* 表：列と行に情報が表示された2次元テーブル。 行や列をテーブルに追加したり、テーブルから削除したりできます。

## コンバージョンの確認を開始する {#start-reviewing-a-conversion}

最初の変換が成功した後、変換サービスは、特定されたフィールドとコンポーネントを含むソースPDFドキュメントをオーバーレイします。 識別されたフィールドに改善を加え、アダプティブフォームを再生成して、目的のエクスペリエンスに近い出力を得ることができます。 最初にコンバージョンが成功した後でのみ、コンバージョンの確認を開始できます。

### 事前準備 {#before-you-start}

* レビューおよび修正エディターはフラグメントをサポートしていません。 変換中に「フラグメントの抽出」オプションが有効になっていた変換は、エディター **を使用して** 、確認しないでください。 このような変換には、アダプ [ティブフォームエディタ](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html) を使用できます。

* 「Review and Correct」エディタには、元に戻す操作はありません。 「保存」ボタンは、変更を永続的に保存する場合にのみ使用します。

### レビューの開始 {#start-the-review}

変換の確認を開始するには、変換に使用するソースPDFドキュメントを選択し、「変換を確認」を選択し **てタップします**。 レビューと修正のエディターが新しいタブで開きます。 コンバージョンの確認を開始できます。 他の問題の修正を開始する前に、次の基本的なチェックを実行します。

![](assets/usingreviewandcorrecteditor.png)

1. **すべてのフィールドのタイプを確認**:コンバージョンサービスは、間違った型をフィールドに割り当てる可能性があります。 例えば、「text」と入力すると、「telephone」の代わりに「text」と入力すると、「mobile phone」フィールドに割り当てられます。 フィールド上にマウスポインターを置くと、フィールドの種類を確認できます。

   フィールドのタイプを変更するには、フィールドを選択し、プロパティブラウザーを開き、ドロップダウンから値 **[!UICONTROL Type]** を選択して、をタップしま **[!UICONTROL Save]**&#x200B;す。 タイプが変更されます。

   ![](assets/check-typex75.gif)

1. **余分なパネルを削除**:コンバージョンサービスは、追加のパネルを生成できます。 例えば、親パネルに追加のサブパネルが含まれ、空きスペースがパネルに変換され、チェックボックスがパネルに変換されます。 すべてのパネルの境界を確認し、余分なパネルを削除します。 フィルターボタンまたはコンテンツ ![](assets/toggle_eye.png) ブラウザーを使用して、すべてのパネルを表示できます。

   パネルを削除するには、パネルを削除するか、グループ化を解除します。 削除オプションを使用すると、パネルの子フィールドまたはコンポーネントも削除されます。

   * パネルを削除するには、パネルを選択し、ツールバーの削除アイコ ![](assets/delete-icon.png) ンをタップします。 確認ダイアログで、をタップしま **[!UICONTROL Confirm]**&#x200B;す。 Tap **[!UICONTROL Save]** to save the changes.

   * パネルのグループ化を解除するには、パネルを選択し、ツールバーのグループ化解除アイコンをタップします。 パネルがグループ解除され、グループ解除されたパネルの子フィールドが親フィールドに調整されます。 Tap **[!UICONTROL Save]**to save the changes.

1. **テキストの論理グループの作成**:識別されたテキストの完全性と正確性を検証します。 また、テキストが正しいパネルまたはグループに論理的に配置されていることを確認します。 例えば、複数列レイアウトでは、ある論理グループのテキストを別のグループに配置します。

   * テキストの完全性と正確性を確認するには、フィルタボタンを使用し ![](assets/toggle_eye.png) てテキストのみを表示し、各テキストをクリックして検証します。 スペル、入力ミス、文法上の問題があれば修正します。

   * フォームにテキストを追加するには、「+」ボタンをタップし、をタップしま **[!UICONTROL Text]**&#x200B;す。 ボックスを描画し、プロパティブラウザーを開き、「コンテンツ」ボックスに追加するテキストを入力します。

1. **** 表の確認：テーブルのすべての境界線が識別されていることを確認します。 また、セルの内容が正しく識別されていることを確認します。

   * 見つからない境界線を識別するには、またはを **[!UICONTROL Add Column]** 使用 **[!UICONTROL Add Row]** します。

   * 余分な境界線を削除するには、またはを **[!UICONTROL Delete Column]** 使用 **[!UICONTROL Delete Row]** します。

必要な変更を行った後、ボタンをタップし **[!UICONTROL Save & Convert]** て、PDFフォームを変換サービスに再送信します。 各フィールドは、対応するアダプティブフィールドコンポーネントに変換されます。 変換後、アダプティブフォームやスキーマを含む更新済みアセットがAEM Formsインスタンスにダウンロードされます。 フォームの複雑さによっては、サービスが変換を完了するのに時間がかかる場合があります。

![保存して変換](assets/save-and-convert.png)

基本チェックを実行した後、フォームを確認して、組織に特有の問題を修正できます。 これらの問題は、見つからないフィールドの追加などに関連する場合があります。 「レビューと修正のエ [ディタツールを使用する」セクションを表示して](review-correct-ui-edited.md#use-the-review-and-correct-editor-tools) 、このような問題を修正するためにエディターが提供するすべてのツールについて確認できます。

また、ほとんどすべてのフォームで発生する同一の問題を認識し、そのようなパターンをアドビに報告することもできます。 目的のエクスペリエンスが得られるまで、レビューと修正エディターを使用します。

## レビューおよび修正エディターツールの使用 {#use-the-review-and-correct-editor-tools}

レビューと修正のエディターを使用すると、次のことができます。

* [フォームへのコンポーネントの追加](review-correct-ui-edited.md#add-a-component-to-the-form)
* [テーブルの追加または編集](review-correct-ui-edited.md)
* [コンポーネントのタイプを変更する](review-correct-ui-edited.md#change-type-a-component)

* [パネルの作成または削除](review-correct-ui-edited.md#create-or-remove-a-panel)
* [パネルまたはコンポーネントの削除](review-correct-ui-edited.md#delete-a-panel-or-component)
* [コンポーネントのプロパティの設定](review-correct-ui-edited.md#set-properties-of-a-component)
* [変換用のフォームの送信](review-correct-ui-edited.md#send-a-form-for-conversion)

### フォームへのコンポーネントの追加 {#add-a-component-to-the-form}

変換サービスは、印刷フォームの一部のコンポーネントを識別しない場合があります。 例えば、フォームの **生年月日コンポーネント** (Date of birth)は、変換中に識別されません。 +ツールを使用して、そ **のようなコ** ンポーネントを特定できます。 このツールを使用して、テキスト、フィールド、選択グループ、テーブル、パネルの各コンポーネントを追加できます。

![](assets/add-component.gif)

コンポーネントをフォームに追加するには、をタップし **[!UICONTROL +]** 、をタップしま **[!UICONTROL Field]**&#x200B;す。 フィールドのラベルと入力ボックスを覆うボックスを描画します。 例えば、上の例の画像では、フィールドコンポーネントを使用して、「 **Date of Birth** 」ラベルと「value」ボックスをフォームに追加しています。 ボックスを描画すると、変換サービスによってフィールドのタイプが識別されます。 必要に応じて、プロパティブラウザーからフィールドのタイプを変更できます。 コンポーネントの作成後、プロパティブラウザを開き、コンポーネントのプロパティを設定します。

ボタンを **[!UICONTROL Save]** タップして変更を保存するか、ボタンを使用し **[!UICONTROL Save & Convert]** てPDFフォームを変換サービスに再送信します。

### テーブルの追加または編集 {#addedittable}

変換によって、表のセルの一部、境界、または内容が不明になる場合があります。 例えば、テーブルの行が識別されません。 このような項目は、レビューと修正エディターを使用して識別できます。 テーブルに対しては、次の操作を実行できます。

* テーブルを選択するには、テーブルの任意のセルをクリックします。
* 名前、タイトル、種類など、セルのプロパティを変更するには、セルをダブルクリックします。 また、セルをダブルクリックして、コンテンツを変更したり、必要なフィールドをマークしたり、他のプロパティを選択したりすることもできます。
* 完全に不明なテーブルまたは新しいテーブルをフォームに追加/識別するには、このツールを使用 **[!UICONTROL +]** します。
* テーブルのセルまたは行のサイズを変更するには、テーブルの空の領域をシングルクリックし、行または列の境界線にカーソルを合わせます。カーソルポインタが変わったら、境界線を選択して移動します。 サイズ変更後、をクリック **[!UICONTROL Done]** して変更を確定します。 このキーを押すと、サ **[!UICONTROL ESC]** イズ変更を破棄できます。

* 行または列を追加または削除するには、テーブルの行のセルを選択し、メニューから「、」、「、」、「 **[!UICONTROL Add Row]**」、「 **[!UICONTROL Add Column]**」、「 **[!UICONTROL Delete Row]**」または「 **[!UICONTROL Delete Column]** 」オプ ![](assets/table_18x18.png) ションを選択します。

* セルをテーブルで分割するには、メニューから「または」 **[!UICONTROL Spilt Vertical]** オプ **[!UICONTROL Split Horizontal]** ションを選択 ![](assets/table_18x18.png) します。

* テーブルのセルを結合するには、結合するセルを選択し、テーブルメニューからオ **[!UICONTROL Merge Cells]** プションを ![](assets/table_18x18.png) 選択します。

### コンポーネントのタイプを変更する {#change-type-a-component}

コンバージョンサービスで、不正なタイプのフィールドが作成される場合があります。 例えば、次の画像では、「性別」フィールドが誤っ **て** 「テキスト」フィールドとして識別さ **れています** 。 また、ラベルの内容が正しくありません。 フィールドは選択フィールドタイプ、ラベルは性別にする必要があります。 コンポーネントのタイプを変更し、ラベルを修正するには：

変換するフィールドを選択し、フィールドの種 ![](assets/smock_shuffle_18_n.svg) 類をタップしてタップします。 フィールドは選択したフィールドタイプに変換されます。 フィールドは、次の表に示す型にのみ変換できます。 パネルコンポーネントは、グループ化を解除するだけで、変形することはできません。

| **コンポーネント** | **変換先** |
|---|---|
| テキスト | フィールドまたは選択グループ |
| フィールド | テキストまたは選択グループ |
| 選択グループ | テキストまたはパネル |

変換後は、プロパティブラウザーを開き、ラベルを指定し、その他の必要なプロパティを指定します。 変更を保 **[!UICONTROL Save]** 存するにはボタンをタップし、PDFフォームを変換サービスに再送信するには「保存して変換」ボタンを使用します。

### パネルの作成または削除 {#create-or-remove-a-panel}

変換サービスは、印刷フォームの関連するコンポーネントとコンテンツをパネルに集約します。 例えば、フォームに住所パネルが含まれ、そのフィールドには、名前、プロット番号、エリア、市区町村、都道府県、郵便番号、国などのフィールドを含めることができます。 これらのフィールドはパネルにグループ化されます。 フォームには複数のパネルを含めることができます。

コンバージョンサービスは、他のコンポーネントと関係のないコンポーネントを含むパネルを作成したり、相対コンポーネントをパネルの外に残したりすることができます。 グループ化ツールまたはグループ化解除ツールを使用して、このようなパネルを修正できます。

* パネルを削除するには、パネルを選択し、「グループ解除」をタップ ![します](assets/ungroupX18.png)。 パネルが削除され、パネルの子コンポーネントが親コンポーネントに移動されます。 また、コンポーネントの削除オ [プションを使用して](review-correct-ui-edited.md#delete-a-panel-or-component) 、パネルとその子を削除することもできます。

* パネルを作成するには、Ctrlキー（WindowsまたはLinux）またはControlキー(Mac)を使用して関連するコンポーネントを選択し、 ![group](assets/group.jpg) をタップしてパネルを作成します。 プロパティブラウザを開いて、パネルのプロパティを指定します。

ボタンを **[!UICONTROL Save]** タップして変更を保存するか、ボタンを使用し **[!UICONTROL Save & Convert]** てPDFフォームを変換サービスに再送信します。

### パネルまたはコンポーネントの削除 {#delete-a-panel-or-component}

コンバージョンサービスは、不正なパネルやコンポーネントを識別する可能性があります。 これらのパネルのコンポーネントのほとんどは非関連です。 このようなパネルやコンポーネントは削除できます。

パネルまたはコンポーネントを削除するには、パネルまたはコンポーネントを選択し、削除アイコンをタップ ![](assets/delete-icon.png) します。 確認ダイアログボックスで、をタップしま **[!UICONTROL Confirm]**&#x200B;す。 選択したパネルまたはコンポーネントが削除されます。 パネルを削除すると、パネルのすべての子も削除されます。 Ctrlキー（WindowsまたはLinux）またはControlキー(Mac)を使用して、複数のコンポーネントまたはパネルを選択できます。

### コンポーネントのプロパティの設定 {#set-properties-of-a-component}

フォームの各コンポーネントには、名前、タイトル、タイプなどのプロパティのセットがあります。 コンポーネントのプロパティを設定するには、コンポーネントを選択し、プロパティブラウザーをタップします。 選択したコンポーネントのプロパティが表示されます。 プロパティを変更または設定します。

ボタンを **[!UICONTROL Save]** タップして変更を保存するか、ボタンを使用し **[!UICONTROL Save & Convert]** てPDFフォームを変換サービスに再送信します。

### 変換用のフォームの送信 {#send-a-form-for-conversion}

レビューおよび修正エディターで必要な変更をすべて行ったら、フォームを変換用に再送信できます。 フォームを変換用に送信するには、をタップしま **[!UICONTROL Save & Convert]**&#x200B;す。 がソー **[!UICONTROL Sent for conversion label]** スドキュメントを含むフォルダーに適用され、更新されたソースフォームがAdobe I/Oで実行されている変換サービスにアップロードされます。

フォームの複雑さに応じて、変換サービスでフォームを変換するのに時間がかかる場合があります。 変換が完了すると、変換されたアダプティブフォームと関連アセットがマシンにダウンロードされます。 変換が完了した後にエディターでフォームを確認し、必要に応じてアダプティブフォームエディターでアダプテ [ィブフォーム](https://helpx.adobe.com/experience-manager/6-5/forms/using/introduction-forms-authoring.html) を開いて、最終的な修正を行うことができます。

アダプティブフォームエディターでフォームを更新した後にフォームを変換用に再送信すると、アダプティブフォームで行った変更がすべて失われます。 フォームをレビューで開き、正しいエディターを使用できるのは、変換が成功した後だけです。

<!--
Comment Type: draft

<h3>Open adaptive forms editor</h3>
-->

<!--
Comment Type: draft

<p>There can be instances where you require adaptive forms editor to make the changes like, applying a different theme to the form or fixing tables. Once you have made all the required changes in Review and Correct editor and converted the form, you can open your form in adaptive forms editor to make the final set of changes.</p>
<p>To open the form with adaptive forms editor, tap the <img src="assets/properties.png" /> icon, and tap <strong>Open Adaptive Form Editor</strong>. The form opens in adaptive form editor. </p>


## Previous {#previous}

[Use Automated Forms Conversion service](convert-existing-forms-to-adaptive-forms.md)
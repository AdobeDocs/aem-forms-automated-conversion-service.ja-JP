---
title: よくある質問
seo-title: よくある質問
description: よくある質問やよくある質問
seo-description: 自動フォームコンバージョンサービスに関するよくある質問(FAQ)
uuid: 0f6dc39c-99b7-49a4-8e9e-ecc4a35110c0
topic-tags: introduction
discoiquuid: e17c2d2c-8300-4467-aa01-57365697939f
translation-type: tm+mt
source-git-commit: 022b86b77c4a524f320cbcbcd6bad4403ddf57d8

---


# よくある質問{#frequently-asked-questions}

1. **Automated Forms ConversionサービスがサポートするAEM Formsのバージョンを教えてください。**
   <p>自動フォーム変換サービスは、AEM 6.4 FormsおよびAEM 6.5 Formsをサポートします。 OSGi上のAEM FormsとJEE上のAEM Formsの両方で機能します。 サービスを使用するには、AEM作成者インスタンスの上に最新のAEM Formsアドオンパッケージが必要です。 手順について詳しくは、「自動フォ <a href="configure-service.md">ーム変換サービスの設定</a> 」を参照してください。</p> 
    <br>

1. **サービスをオンプレミスでインストールできますか？**
   <p>アドビでは、Automated Forms ConversionサービスのAIおよびMLアルゴリズムを定期的にトレーニングし、変換の精度を向上させる新しいデータセットを提供しています。 更新されたアルゴリズムは、定期的にAdobe Cloud上で実行されるコンバージョンサービスに展開されます。 サービスのすべてのお客様に、更新されたアルゴリズムの利点があります。 したがって、クラウドホスト型の中央デプロイメントは、すべての顧客に対して継続的に学習と改善を提供する自動フォームコンバージョンサービスに最適です。</p> 
    <p>サービスは、空のフォームをアダプティブフォームに変換します。 このサービスは、入力済みのフォームおよび入力済みのフォームからのデータの抽出をサポートしていません。 フォームを変換用にサービスに送信する前に、入力済みのフォームからデータを削除し、フォームから固有の情報を削除またはホワイトリストに登録します。</p> <br>

1. **このサービスは、すべての形式のPDFフォームをサポートしていますか？ どの言語がサポートされていますか。**
   <p>このサービスでは、非インタラクティブPDFフォーム、XFAベースのXDPおよびPDFフォーム、AcroFormsをアダプティブフォームに変換できます。 このサービスは、スキャンまたは入力されたフォームをサポートしていません。 その他の制限については、既知の問題の記事を <a href="known-issues.md">参照してくださ</a> い。<br /> </p> 
    <p>他のソースタイプのサポートを定期的に追加しています。 新しく追加され <a href="introduction.md">た機能を定期的に更新する場合は</a> 、ウォッチリストの「supportedPDF forms」セクションをそのままにしておきます。</p>

   このサービスで変換できるのは、英語のフォームのみです。 生成されたアダプティブフォームは、 [AEM翻訳ワークフローを使用して別の言語に翻訳できます。](https://helpx.adobe.com/experience-manager/6-5/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.html)</br> </br>

1. **サービスは、アダプティブフォームの代わりにXDPを生成できますか。**
   <p>サービスはXDP出力を生成しません。 定期的に機能を追加し、サービスを提供しています。 新しく追加さ <a href="introduction.md">れた機能を定期的に更新するために</a> 、サポートされる言語とPDFフォームのセクションをウォッチリストに保持します。</p> <br>

1. **生成されたスキーマのタイプは何ですか。**
   <p>このサービスを使用して、次の情報を生成できます。 </p>

   * JSONスキーマに連結されたアダプティブフォームおよび
   * どのスキーマにも連結されていないアダプティブフォーム <br><br>

1. **サービスはMicrosoft Wordフォームをアダプティブフォームに変換できますか。**
   <p>いいえ。Microsoft Wordフォームはアダプティブフォームに変換されません。 Microsoft WordフォームをPDFフォームに保存し、PDFフォームをアダプティブフォームに変換することができます。 完了プロセスは </p> <br>

   1. Adobe Acrobatを使用して、Word [ドキュメントを非インタラクティブPDFに変換します](https://helpx.adobe.com/acrobat/how-to/create-pdf-files-word-excel-website.html)。
   1. Adobe Acrobatを使用して、生成さ [れたPDFフォームを入力可能なPDFフォームに変換します](https://helpx.adobe.com/acrobat/how-to/convert-word-excel-paper-pdf-forms.html)。
   1. Adobe Acrobatを使用して、フォームフィールドを手動で更新し、修正します。
   1. PDFフォームを保存します。 これで、フォームを変換サービスと共に使用してアダプティブフォームを生成できます。 フォームをレコードのドキュメントテンプレートとして使用することもできます。


1. **サービスは、スキャンされた紙のフォームと色付きのフォームをアダプティブフォームに変換できますか。**
   <p>このサービスでは、PDFフォームをアダプティブフォームに変換できます。 このサービスは、スキャンまたは入力されたフォームをサポートしていません。 その他の制限については、既知の問題の記事を <a href="known-issues.md">参照してくださ</a> い。</p> <br>

1. **サービスは、スキャンしたフォームまたはフォームの画像のみをアダプティブフォームに変換できますか。**
   <p>このサービスでは、スキャンされたフォームやフォームの画像のアダプティブフォームへの変換はサポートされていません。 ただし、Adobe Acrobatを使用して、フォームの画像をPDFフォームに変換します。 次に、サービスを使用してPDFフォームをアダプティブフォームに変換します。 Acrobatでの変換には、常に高品質なフォーム画像を使用します。 これにより、コンバージョンの質が向上します。</p> <br>

1. **一部のXDPベースのフォームはフォームフラグメントを使用します。これらのフォームフラグメントはどこでアップロードする必要がありますか。**
   <p class="MsoNormal">フォームフラグメントを変換フォルダーにアップロードし、元のフォルダー構造を保持します。 XDPベースのフォームやフォームフラグメントで使用される相対パスを保持するのに役立ちます。</p> <br>

1. **このサービスは、スキーマバインドXDPフォームをサポートしていますか？ スキーマに連結されたXDPがある場合、XDPにスキーマを埋め込む必要がありますか。**
   <p>はい。サービスはスキーマバインドXDPフォームをサポートし、スキーマをソースXDPフォームに埋め込む必要があります。 スキーマバインドXDPフォームを変換すると、サービスはJSONスキーマを生成します。 JSONスキーマは、ソースXDPフォームのXSDスキーマと構造的に似ています。</p> <br>

1. **サービスはフォームを変換できませんでした。 問題を解決する理由と方法を教えてください。**
変換が失敗する最も一般的な理由は、次のとおりです。</p>
   * 変換用に保護されたPDFフォームが提供されます。 パスワードで保護されたPDFフォームや保護されたPDFフォームは変換に使用しないでください。
   * インターネット接続が中断されました。 変換中にインターネットに接続していることを確認します。
   * ソースPDFには、実際のフォームではなく、フォームの画像が含まれます。
   * サービスが正しく設定されていないか、サービスURLが指定されていないか、指定されたサービスURLが正しくありません。 > > >でサ [ービス設定を](configure-service.md#configure-the-cloud-service) 確認 **[!UICONTROL AEM]** し **[!UICONTROL Tools]** ます **[!UICONTROL Cloud Services]****[!UICONTROL Automated Forms Conversion configuration]**。
   * IMS設定が正しく設定されていません。 IMS設定のヘルスチェックを実行し、正しく機能していることを確認します。 IMS設定が正しいかどうかを確認するには：
      1. 移動 :`http://[servername]:[port]/libs/cq/adobeims-configuration/content/configurations.html`
      2. 設定を選択します。 ヘッダーのを **[!UICONTROL Check Health]** クリックし、をクリックしま **[!UICONTROL Check]**&#x200B;す。 成功した場合は、メッセージが表示 **[!UICONTROL Token retrieved successfully!]** されます。 <br> <br>

1. **カスタムフォントを使用すると、変換に影響が出ますか？**
   <p>非インタラクティブPDFフォームをアダプティブフォームに変換する場合、変換の質を向上させるために、フォントがPDFフォームに埋め込まれます。 フォントの埋め込みのサポートは、非インタラクティブPDFフォームに制限されています。 AcroFormおよびXFAベースのPDFフォームの変換を最適化するために、代替フォントが使用されます。</p> 
    <p>非インタラクティブPDFフォームには、 <strong>CQ-DAM-Handler</strong> -Gibson Font Manager Service設定の <strong></strong> Customer fonts directoryフィールドに一覧表示されているカスタムフォントディレクトリで使用できるフォームのみが埋め込まれます。</p> 
    <p> </p> <br>

1. **出力されたアダプティブフォームでソースPDFのフォントを識別し、使用するか。**
   <p>レスポンシブHTMLフォームのスタイルとレイアウトは、通常、PDFまたは紙ベースのフォームとは異なります。 組織全体で一貫したレイアウトとスタイル設定をサポートするために、アダプティブフォームではテ <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html">ーマを使用してフォームのスタイルを設定し</a>ます。 変換サービスは、変換時に適用されたテーマで指定されたフォントとフォントスタイルを使用します。 テーマのフォントとフォントスタイルを変更して、アダプティブフォームのコンポーネントに対して明確なルック&amp;フィールを提供できます。</p> <br>

1. **このサービスは、XDPベースのフォームからJavaScriptを自動的に抽出し、対応するアダプティブフォームに適用しますか。**
   <p>サービスは、XFAベースのフォームまたはAcro Formsのスクリプトを、対応するアダプティブフォームルールに自動的に変換しません。 フォーム作成者は、ルールエディターを使用して <a href="https://helpx.adobe.com/experience-manager/6-5/forms/using/rule-editor.html"></a> 、アダプティブフォームにインタラクティブ機能を追加できます。</p> <br>

1. **一部のフォームオブジェクトは、アダプティブフォームのコンポーネントに正しく変換されません。 How to resolve the issue?**
   <p>自動フォーム変換サービスは、大量のフォームに基づいて学習していきます。 ただし、AI/MLベースのアプリケーションは、トレーニングデータとパターンによって制限されます。 人間の認識には複数のフィールドタイプ、レイアウト、パターン、コンテキストが認識される場合がありますが、自動認識は難しくなります。 サービスがそのようなオブジェクトを識別できないか、正しく認識されない可能性があります。 「レビューと修 <a href="review-correct-ui-edited.md" target="_blank">正」エディタを使用して</a> 、入力フォームの見慣れた紙のフォームベースのレイアウトに必要な変更を加えることができます。</p> <br/>

1. **一部の修正は、フォーム間で繰り返されます。 サービスは、将来のコンバージョンでこのようなすべてのインスタンスを識別して修正できますか。**

   このサービスは、フォームとパターンに関するトレーニングを一貫して受けています。 新しいパターンを日々学習します フォーム全体で繰り返される修正の自動適用は、まだ開始されていません。 プレリリースフォームの機能を利用できるかどうかは、常に確認してください。 <br/><br/>

   メタモデルを使用して、フォームオブジェクトをアダプティブフォームコンポーネントにマッピングし、コンポーネントの検証、ルール、データパターン、ヘルプテキスト、アクセシビリティプロパティを事前設定できます。 指定したすべてのプロパティが変換時に適用されます。 メタモデルを使用して、共通のプロパティをフィールドに適用できます。 フォーム間で繰り返し発生する問題を減らすのに役立ちます。<br/><br/>

1. **個人を特定できる情報(PII)情報などの機密データを含むフォームのオプションは何ですか。**
このサービスは、空白または未入力のフォームのみをサポートします。 入力済みのフォームや個人を特定できる情報(PII)を含むフォームはアップロードしないでください。 また、ソースフォーム内の事前入力済みのデータと、ホワイトラベルのPII、社外秘、および専有情報を削除します。 <br/>

1. **ヘッダーとフッターをどこに配置しますか？**
   <p>ヘッダーとフッターをアダプティブフォームのテンプレートに配置します。 ソースPDFフォームにヘッダーとフッターが含まれている場合、変換中に、検出されたヘッダーとフッターを検出し、アダプティブフォームテンプレートで使用可能なヘッダーとフッターで置き換えます。 アダプティブフォームに余分なヘッダーまたはフッターが含まれている場合は、レビューおよび修正エディターを使用して <a href="review-correct-ui-edited.md"></a> 、そのようなヘッダーまたはフッターを修正または削除できます。</p> <br />

1. **手動のアセットの計画、作成（テーマ、テンプレート）、アダプティブフォームの作成、発行のプロセスと比較して、サービスの節約に要する時間はどれくらいですか。**
   <p>時間は、入力フォームのサイズと複雑さ、および要求数によって異なります。 このサービスでは、PDFフォームをアダプティブフォームに変換することで、フォームを手動で変換するプロセスと比較して、はるかに高速なペースで時間を大幅に削減する予定です。 </p> <br />

1. **RSAライブラリに関連するエラーが発生した場合は、どうしますか。 エラーメッセージは、次に示すメッセージに似ています。** <br/>
   `*ERROR* [0:0:0:0:0:0:0:1 [1565757652491] POST /content/dam/formsanddocuments/demo004.affBatchProcessor.html HTTP/1.1] org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.NoClassDefFoundError: Could not initialize class com.rsa.cryptoj.o.dl at com.rsa.jsafe.JSAFE_SecureRandom.getInstance(Unknown Source) at com.adobe.internal.pdfm.util.Util.appendRandomNumberToPrefix(Util.java: 169) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34] at com.adobe.internal.pdfm.logging.JobLog.&amp;lt;init&amp;gt;(JobLog.java:126) [com.adobe.aemfd.adobe-aemfd-assembler:6.0.34]` 前述のエ <br>ラーは、RSA/BouncyCastleライブラリに対してブート委任が設定されていない場合に発生します。 次の手順を実行して、問題を解決します。
   <p> </p>

   1. AEM インスタンスを停止します。Navigate to the `[AEM installation directory]\crx-quickstart\conf\` folder. sling.propertiesファイルを開いて編集します。 If you use `[AEM installation directory]\crx-quickstart\bin\start.bat` to start an AEM instance, edit the sling.properties located at `[AEM_root]\crx-quickstart\`.
   1. 以下のプロパティを sling.properties ファイルに追加します。<br/> `sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*`<br />  `sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*`<br /> `sling.bootdelegation.xerces=org.apache.xerces.*`
   1. ファイルを保存して閉じます。<br/>
   1. AEM インスタンスを起動します。<br/>
   <br/>

1. **アダプティブフォームテキストの大文字と小文字の自動変更方法**
   <p>テーマやスタイルエディターからアダプティブフォームを使用して、アダプティブフォームのフィールドの大文字と小文字を変更できます。 例えば、テーマエディターを開き、フォームのすべてのテキストのCaseプロパティの値を大文字、小文字またはcamelCaseに設定できます。 テーマエディターの「CSSの上書き」オプションを使用して、異なるタイプのスタイルを作成することもできます。</p>
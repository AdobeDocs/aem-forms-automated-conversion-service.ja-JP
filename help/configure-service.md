---
title: Automated Forms Conversionサービスの設定
description: AEMインスタンスで自動フォームコンバージョンサービスを使用する準備が整いました
translation-type: tm+mt
source-git-commit: ef5789dabccc65dcf988b9424b435aa036017691

---


# Automated Forms Conversionサービスの設定 {#about-this-help}

このヘルプでは、AEM管理者がAutomated Forms Conversionサービスを設定して、PDFフォームからアダプティブフォームへの変換を自動化する方法を説明します。 このヘルプは、組織のIT管理者およびAEM管理者を対象としています。 このヘルプで扱う内容は、次のテクノロジーに関する十分な知識がある読者を想定しています。

* Adobe Experience ManagerおよびAEMパッケージのインストール、設定、管理、

* LinuxおよびMicrosoft Windowsオペレーティングシステムの使用、

* SMTPメールサーバーの設定

>[!VIDEO](https://video.tv.adobe.com/v/29267/)

**ビデオを見るか、記事を読んで自動フォームコンバージョンサービスを設定します**

## 使用開始{#onboarding}

このサービスは、AEM 6.5 FormsおよびAEM 6.4 Formsオンプレミスのお客様およびAdobe Managed Serviceのエンタープライズユーザーが無料で利用できます。 アドビのセールスチームまたはアドビの担当者に連絡して、サービスへのアクセスをリクエストできます。

アドビは、組織へのアクセスを許可し、組織の管理者として指定されたユーザーに必要な権限を与えます。 管理者は、組織のAEM Forms開発者（ユーザー）にサービスへの接続を許可できます。

## 前提条件 {#prerequisites}

Automated Forms Conversion Serviceを使用するには、次が必要です。

* 自動フォームコンバージョンサービスが組織で有効になっている
* コンバージョンサービスの管理者権限を持つAdobe IDアカウント
* 最新のAEM Service packを含むAEM 6.5またはAEM 6.4の作成者インスタンスの起動および実行
* forms-userグループのメンバーであるAEMユーザー（AEMインスタンス上）

## 環境の設定 {#setuptheservice}

サービスを使用する前に、AEM作成者インスタンスを準備して、Adobe cloud上で実行されているサービスに接続します。 リストに表示された順序で次の手順を実行し、サービスのインスタンスを準備します。

1. [AEM 6.5またはAEM 6.4のダウンロードとインストール](#aemquickstart)
1. [最新のAEM Service packをダウンロードしてインストールする](#servicepack)
1. [最新のAEM Formsアドオンパッケージのダウンロードとインストール](#downloadaemformsaddon)
1. [カスタムテーマとテンプレートの作成](#referencepackage)

### AEM 6.5またはAEM 6.4のダウンロードとインストール {#aemquickstart}


自動フォームコンバージョンサービスは、AEMオーサーインスタンス上で実行されます。 AEM作成者インスタンスを設定するには、AEM 6.5またはAEM 6.4が必要です。 AEMを起動および実行していない場合は、次の場所からダウンロードします。

* AEMをご利用のお客様は、 [Adobe Licensing webサイトからAEM 6.5またはAEM 6.4をダウンロードします](http://licensing.adobe.com)。

* アドビパートナーの場合は、 [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) （アドビパートナートレーニングプログラム）を使用してAEM 6.5またはAEM 6.4をリクエストします。

AEMのダウンロード後、AEMオーサーインスタンスを設定する手順については、デプロイと管理を [参照してください](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)。

### Download and install AEM latest Service Pack {#servicepack}

最新のAEM Service packをダウンロードしてインストールします。 詳しい手順については、「 [AEM 6.5 Service packリリースノート](https://helpx.adobe.com/experience-manager/6-5/release-notes/sp-release-notes.html) 」または「 [AEM 6.4 Service packリリースノート」を参照してください](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html)。

### Download and install AEM Forms add-on package  {#downloadaemformsaddon}

AEMインスタンスには、基本的なフォーム機能が含まれます。 変換サービスには、AEM formsの全機能が必要です。 AEM Formsのすべての機能を利用するには、AEM formsアドオンパッケージをダウンロードしてインストールします。 変換サービスを設定して実行するには、パッケージが必要です。 詳しい手順については、「データ取得 [機能のインストールと設定」を参照してください。](https://helpx.adobe.com/experience-manager/6-5/forms/using/installing-configuring-aem-forms-osgi.html)

>[!NOTE]
> Automated Forms Conversionサービスの既存のユーザーは、最新のAEM Formsアドオンをインストールしてサービスの使用を続行します。 コネクタパッケージがAEM Formsアドオンパッケージに結合されます。 追加のコネクタパッケージは不要になりました。
> アドオンパッケージをインストールした後は、必ず必須のインストール後の設定を行ってください。


### カスタムテーマとテンプレートの作成 {#referencepackage}

AEMを実稼働モードで起動する [と](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/production-ready.html) (nosamplecontent runmode)、参照パッケージはインストールされません。 リファレンスパッケージには、サンプルテーマとテンプレートが含まれています。 自動フォーム変換サービスでは、PDFフォームをアダプティブフォームに変換するために、少なくとも1つのテーマと1つのテンプレートが必要です。 独自のポイントサービス設定のカスタムテーマとテンプレートを作成し [て、サービスを使用する前に](#configure-the-cloud-service) 、カスタムテンプレートとテーマを使用します。

## Configure the service {#configure-the-service}

サービスの設定に進み、ローカルインスタンスをAdobe cloud上で実行しているサービスに接続する前に、サービスへの接続に必要な個人と権限について説明します。 このサービスでは、管理者と開発者の2種類の人物を使用します。

* **管理者**:管理者は、組織のアドビソフトウェアとサービスを管理する責任を負います。 管理者は、組織の開発者に、Adobe cloud上で実行されているAutomated Forms Conversionサービスへの接続権限を付与します。 組織の管理者がプロビジョニングされると、管理者はタイトルの電子メールを受け取りま **[!UICONTROL 'You now have administrator rights to manage Adobe software and services for your organization']**&#x200B;す。 管理者の場合は、メールボックスに前述のタイトルの電子メールが含まれていないか確認し、組織の開 [発者にアクセス権を付与します](#adduseranddevs)。

![管理者アクセス許可電子メール](assets/admin-console-adobe-io-access-grantedx75.png)

* **開発者**:開発者は、ローカルのAEM Forms作成者インスタンスをAdobe cloud上で実行されているAutomated Forms Conversionサービスに接続します。 管理者がAutomated Forms Conversionサービスに接続する権限を開発者に付与すると、組織のAdobe API統合を管理する開発者アクセス権を持つ、というタイトルの電子メールが開発者に送信されます。 開発者の場合は、メールボックスに前述のタイトルの電子メールが含まれているかどうかを確認し、「ローカルAEMインスタンスをAdobe cloud上のAutomated Forms Conversionサービスに接続する」に進みます。 [](#connectafcadobeio)

![開発者アクセス許可電子メール](assets/email-developer-accessx94.png)

### （管理者のみ）組織の開発者にアクセス権を付与します {#adduseranddevs}

アドビが組織へのアクセスを有効にし、管理者に必要な権限を与えたら、管理者は管理コンソールにログインし（以下の詳細な手順）、プロファイルを作成し、プロファイルに開発者を追加できます。 開発者は、AEM FormsのローカルインスタンスをAdobe cloudのAutomated Forms Conversionサービスに接続できます。

開発者は、コンバージョンサービスを実行するように指定された組織のメンバーです。 Adobe Automated Forms Conversionサービスプロファイルに追加された開発者のみが、Automated Forms Conversionサービスを使用できます。 次の手順を実行して、プロファイルを作成し、それに開発者を追加します。

1. 管理コンソールに [ログインします](https://adminconsole.adobe.com/)。 自動フォ **** ーム変換サービスを使用してログインするためにプロビジョニングされた管理者のAdobe IDを使用します。 他のIDやFederated IDを使用してログインしないでください。
1. オプションをクリ **[!UICONTROL Automated Forms Conversion]** ックします。
1. タブ内 **[!UICONTROL New Profile]** をクリック **[!UICONTROL Products]** します。
1. プロフ **[!UICONTROL Name]**&#x200B;ァイル **[!UICONTROL Display Name]**&#x200B;の、、お **[!UICONTROL Description]** よびを指定します。 「**[!UICONTROL Done]**」をクリックします。プロファイルが作成されます。

   ![新しいプロファイルの詳細を指定します。](assets/create-new-profile-details.png)

1. プロファイルに開発者を追加します。 開発者を追加するには：
   1. 管理コンソ [ールで](https://adminconsole.adobe.com/enterprise)、「概要」タブに移動します。
   1. 必要な製 **[!UICONTROL Assign Developers]** 品カードをクリックします。
   1. 開発者の電子メールアドレスと、（オプションで）姓と名を入力します。
   1. 製品プロファイルを選択します。 タップ **[!UICONTROL Save]**.

すべてのユーザーに対して上記の手順を繰り返します。  開発者の追加について詳しくは、開発者の管理を参 [照してください](https://helpx.adobe.com/enterprise/using/manage-developers.html)。

管理者がAdobe I/Oプロファイルに開発者を追加すると、開発者に電子メールで通知されます。 電子メールを受け取った後、開発者は、ローカルのAEM Forms [インスタンスをAdobe cloud上の自動フォーム変換サービスに接続できます](#connectafcadobeio)。

### （開発者のみ）ローカルAEM FormsインスタンスをAdobe cloud上のAutomated Forms Conversionサービスに接続します。 {#connectafcadobeio}

管理者から開発者アクセス権が与えられたら、ローカルのAEM FormsインスタンスをAdobe cloud上で実行されているAutomated Forms変換サービスに接続できます。 AEM Formsインスタンスをサービスに接続するには、一覧に示された順序で次の手順を実行します。

* [電子メール通知の設定](configure-service.md#configureemailnotification)
* [forms-usersグループへのユーザーの追加](#adduserstousergroup)
* [公開証明書の取得](#obtainpubliccertificates)
* [Adobe I/O 統合の作成](#createintegration)
* [クラウドサービスの設定](configure-service.md#configure-the-cloud-service)

#### 電子メール通知の設定 {#configureemailnotification}

自動フォームコンバージョンサービスは、Day CQメールサービスを使用して電子メール通知を送信します。 これらの電子メール通知には、変換の成功または失敗に関する情報が含まれます。 通知を受信しない場合は、これらの手順をスキップします。 Day CQ mailサービスを設定するには、次の手順を実行します。

1. AEM Configuration Manager( `http://localhost:4502/system/console/configMgr`
1. Day CQ 電子メールサービスの設定を開きます。、、およびの各フィー **[!UICONTROL SMTP server host name]**&#x200B;ルドの値 **[!UICONTROL SMTP server port]**&#x200B;を指定し **[!UICONTROL From address]** ます。 「**[!UICONTROL Save]**」をクリックします。

   SMTPサーバーのホスト名とポートについては、電子メールサービスプロバイダーまたはIT管理者に問い合わせてください。 [差出人]フィールドには、任意の有効な電子メールアドレスを入力できます。 例えば、notification@example.comやdonotreply@example.comのように指定します。

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual host name or IP address and port number for local, author, and publish instances. 「**[!UICONTROL Save]**」をクリックします。

#### forms-usersグループへのユーザーの追加 {#adduserstousergroup}

サービスを実行するように指定されたAEMユーザーのプロファイルに電子メールアドレスを指定します。 ユーザーが [formsユーザーグループのメンバーであることを確](https://helpx.adobe.com/experience-manager/6-4/forms/using/forms-groups-privileges-tasks.html) 認します。 電子メールは、変換を実行しているユーザーの電子メールアドレスに送信されます。 ユーザーの電子メールアドレスを指定し、formsユーザーグループにユーザーを追加するには：

1. AEM管理者としてAEM Forms作成者インスタンスにログインします。 ローカルのAEM資格情報を使用してログインします。 ログインにAdobe IDを使用しないでください。 Tap **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. 変換サービスを実行するユーザーを選択し、をタップしま **[!UICONTROL Properties]**&#x200B;す。 「ユーザー設定を編集」ページが開きます。
1. フィールドに電子メールアドレスを指定し **[!UICONTROL Email]** 、をタップしま **[!UICONTROL Save]**&#x200B;す。 変換が正常に完了したか失敗した場合は、指定した電子メールアドレスに電子メールが送信されます。
1. Tap the **Groups** tab. 「グループを選択」タブで、 **forms-usersグループを入力し** 、選択します。 Tap **Save &amp; Close**. これで、ユーザーはforms-usersグループのメンバーになります。

#### 公開証明書の取得 {#obtainpubliccertificates}

公開証明書により、Adobe I/O でプロファイルを認証できます。

1. AEM Forms作成者インスタンスにログインします。 Navigate to **[!UICONTROL Tools]**> **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. タップ **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** page appears.

   ![Adobe IMSテクニカルアカウント設定ページ](assets/adobe-ims-technical-account-configuration.png)

1. 「Cloud Solution」 **[!UICONTROL Automated Forms Conversion Service]** でを選択します。

1. チェックボッ **[!UICONTROL Create new certificate]** クスを選択し、エイリアスを指定します。 エイリアスは、ダイアログの名前として機能します。 タップ **[!UICONTROL Create certificate]**. ダイアログが表示されます。「**[!UICONTROL OK]**」をクリックします。証明書が作成されます。

1. をタップ **[!UICONTROL Download Public Key]** し、 *AEM-Adobe-IMS.crt証明書ファイルをコンピューターに保存します* 。 証明書ファイルは、Adobe I/Oコ [ンソールでの統合の作成に使用されます](#createintegration)。 タップ **[!UICONTROL Next]**.

1. 以下を指定します。

   * タイトル：タイトルを指定します。
   * Authorization Server: [https://ims-na1.adobelogin.com](https://ims-na1.adobelogin.com)
   その他のフィールドは現時点では空白のままにします（後で指定します）。ページを開いたままにします。

   <!--
   Comment Type: draft

   <li> </li>
   -->

   <!--
   Comment Type: draft

   <li>Step text</li>
   -->

#### Adobe I/O 統合の作成 {#createintegration}

Automated Forms Conversionサービスを使用するには、Adobe I/Oで統合を作成します。統合により、APIキー、クライアントシークレット、ペイロード(JWT)が生成されます。

1. https://console.adobe.io/にログイン [します](https://console.adobe.io/)。 管理者がAdobe I/OコンソールにログインするためにプロビジョニングしたAdobe ID、開発者アカウントを使用します。

1. タップ **[!UICONTROL View Integrations]**. 使用可能なすべての統合を含む画面が表示されます。
1. ドロップダウンリストから組織を選択しま **[!UICONTROL Integrations]**&#x200B;す。 をタッ **[!UICONTROL New Integration]**&#x200B;プし、選択 **[!UICONTROL Access an API]**&#x200B;して、をタップしま **[!UICONTROL Continue]**&#x200B;す。
1. /を選 **[!UICONTROL Experience Cloud]** 択し、を **[!UICONTROL Automated Forms Conversion]** タップしま **[!UICONTROL Continue]**&#x200B;す。 「自動フォームコンバージョン」オプションが無効になっている場合は、オプションの上のドロップダウンボックスで正しい組織を選択していることを確認し **[!UICONTROL Adobe Services]** ます。 組織が不明な場合は、管理者に問い合わせてください。

   ![自動フォームコンバージョンの選択](assets/create-new-integration.png)

1. 統合の名前と説明を指定します。 「公 **[!UICONTROL Select a File from your computer]** 開証明書を取得」セクションでダウンロードしたAEM-Adobe-IMS.crtファイルをタップし [てアップロードします](#obtainpubliccertificates) 。
1. 組織の開発者にアクセス権を付与 [する際に作成したプロファイルを選択し](#adduseranddevs) 、をタップしま **[!UICONTROL Create Integration]**&#x200B;す。 統合が作成されます。
1. をタップ **[!UICONTROL Continue to integration details]** して、統合情報を表示します。 このページには、APIキー、クライアントシークレット、およびローカルAEMインスタンスを自動フォームコンバージョンサービスに接続するために必要なその他の情報が含まれています。 ページ上の情報は、ローカルマシン上にIMS設定を作成するために使用されます。

   ![統合のAPIキー、クライアントシークレット、ペイロード情報](assets/integration-details.png)

1. ローカルインスタンスでIMS設定ページを開きます。 セクションの最後でページを開いたまま、「公開証明書を取 [得」をクリックします](#obtainpubliccertificates)。

   ![タイトル、APIキー、クライアントシークレットおよびペイロードの指定 ](assets/ims-configuration-details.png)

1. Adobe IMS技術ページで、APIキーとクライアントシークレットを指定します。 統合ページで指定した値を使用します。

   **ペイロードの場合は、統合ページの「JWT」タブに指定されたコードを使用します。** タップ  **[!UICONTROL Save]**. IMS設定が作成されます。 統合ページを閉じます。

   ![ペイロードフィールドにJWTフィールドの値を使用](assets/jwt.png)

   >[!CAUTION]
   >
   >IMS設定を1つだけ作成します。 複数のIMS設定を作成しないでください。

1. IMS設定を選択し、をタップしま **[!UICONTROL Check Health]**&#x200B;す。 ダイアログボックスが表示されます。タップ **[!UICONTROL Check]**. 接続に成功すると、「 *Token retrieved successfully* 」メッセージが表示されます。

   ![接続に成功すると、トークンが正常に取得されましたというメッセージが表示されます。 ](assets/health-check.png)

   <br/> <br/>

#### Configure the cloud service {#configure-the-cloud-service}

AEMインスタンスを変換サービスに接続するクラウドサービス設定を作成します。 また、変換するテンプレート、テーマ、フォームフラグメントを指定することもできます。 複数のクラウドサービス設定をフォームのセットごとに個別に作成できます。 例えば、販売部門のフォーム用に個別の設定を用意し、顧客サポートフォーム用に個別の設定を用意することができます。 次の手順を実行して、クラウドサービス設定を作成します。

1. AEM Formsインスタンスで、///をタ **[!UICONTROL Adobe Experience Manager]** ップ **[!UICONTROL Tools]**&#x200B;し **[!UICONTROL Cloud Services]** ます **[!UICONTROL Automate Forms Conversion Configuration]**。
1. フォルダーをタ **[!UICONTROL Global]** ップし、をタップしま **[!UICONTROL Create]**&#x200B;す。 自動フォームコンバージョン設定を作成するページが表示されます。 設定がグローバルフォルダーに作成されます。 既に存在する別のフォルダーに設定を作成したり、設定用の新しいフォルダーを作成したりすることもできます。

1. ページで、 **[!UICONTROL Create Automated Forms Conversion Configuration]** 次のフィールドの値を指定し、をタップしま **[!UICONTROL Next]**&#x200B;す。

   | フィールド | 説明 |
   |--- |--- |
   | タイトル | 設定の一意のタイトル。 タイトルは、変換を開始する際に使用するUIに表示されます。 |
   | 名前 | 設定の一意の名前。 設定は、指定した名前でCRX-Repositoryに保存されます。 名前はタイトルと同じにすることができます。 |
   | サムネールの位置 | 設定のサムネールの場所。 |
   | サービス URL | Adobe cloud上の自動フォームコンバージョンサービスのURL。 URLを使用し `https://aemformsconversion.adobe.io/` ます。 |
   | テンプレート | 変換されたフォームに適用されるデフォルトのテンプレート。 変換を開始する前に、いつでも別のテンプレートを指定できます。 テンプレートには、アダプティブフォームの基本構造と初期コンテンツが含まれます。 標準搭載のテンプレートからテンプレートを選択できます。 また、カスタムテンプレートを作成することもできます。 |
   | テーマ | 変換されたフォームに適用されるデフォルトのテーマ。 変換を開始する前に、常に別のテーマを指定できます。  アイコンをクリックして、あらかじめ用意されているテーマを選択できます。 また、カスタムテーマを作成することもできます。 |
   | 既存のフラグメント | 既存のフラグメントが存在する場合はその場所。 |
   | カスタムメタモデル | カスタムメタモデルの.schema.jsonファイルのパス。 |



1. ページの **[!UICONTROL Advanced]** タブで、 **[!UICONTROL Create Automated Forms Conversion Configuration]** 次のフィールドの値を指定します。

   <table>
   <thead>
   <tr>
   <th>フィールド</th>
   <th>説明</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td >レコードのドキュメントを生成</td>
   <td>変換されたフォームに対してレコードのドキュメントを自動的に生成する場合は、このオプションを選択します。 このオプションは、XFAベースのフォーム（XDPおよびPDFフォーム）に対してのみ有効です。 このオプションを有効にすると、顧客はフォームを送信した後、フォームに入力した情報を印刷またはドキュメント形式で記録し、将来の参照用に保持することができます。 これを、レコードのドキュメントといいます。</td>
   </tr>
   <tr>
   <td>Analytics を有効にする</td>
   <td>変換されたすべてのフォームでAdobe Analyticsを有効にする場合は、このオプションを選択します。 このオプションを使用する前に、AEM FormsインスタンスでAdobe Analyticsが有効になっていることを確認します。</td>
   </tr>
   </tbody>
   </table>

   * ソースが拡張子.XDPのXFAベースのフォームの場合、出力DORはXFAレイアウトを保持します。そうでない場合、コンバージョンサービスは標準搭載のテンプレートを使用して他のXFAベースのフォームのDORを生成します。
   * XFAフォームが送信されると、フォームの送信データはXML要素または属性として保存されます。 For example, `<Amount currency="USD"> 10.00 </Amount>`. 通貨は属性と通貨額として保存され、10.00は要素として保存されます。 アダプティブフォームの送信データには属性がなく、要素のみが含まれます。 したがって、XFAベースのフォームがアダプティブフォームに変換されると、アダプティブフォームの送信データには、このような属性ごとに1つの要素が含まれます。 例：

   ```css
      {
         "Type": "Principal",
   
         "Amount": "10.00",
   
         "currency": "USD"
      }
   ```

1. タップ **[!UICONTROL Create]**.  クラウド設定が作成されます。 AEM Formsインスタンスで、既存のフォームからアダプティブフォームへの変換を開始する準備が整いました。
---

copyright:
years: 2017
lastupdated: "2017-11-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
 

# SOAP サービスを REST API として公開する
**所要時間**: 20 分  
**スキル・レベル**: ビギナー  

---
## 目標
API Manager で、既存の SOAP サービスにアクセスしてそのサービスを REST API として公開するための REST API を作成します。

## 前提条件
1. 始める前に、[{{site.data.keyword.apiconnect_full}} インスタンスのセットアップ](tut_prereq_set_up_apic_instance.html)が必要です。
2. 始める前に、[weatherprovider.wsdl テスト ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](https://raw.githubusercontent.com/IBM-Bluemix-Docs/apiconnect/master/tutorials/weatherprovider.wsdl){:new_window} ファイルをローカル・ファイル・システムにコピーしてください。
	>![images/info.png]
	>**「未加工 (Raw)」**をクリックし、結果のページを `.wsdl` ファイルとしてローカル・システムに保存することもできます。

---
## REST API 定義のセットアップ
1. {{site.data.keyword.Bluemix_short}} にログインします ([https://new-console.ng.bluemix.net/login) ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](https://new-console.ng.bluemix.net/login){:new_window}。
2. {{site.data.keyword.Bluemix_notm}} **ダッシュボード**で、スクロールダウンして {{site.data.keyword.apiconnect_short}} を選択します。 あるいは、メニュー・アイコンから**「サービス」**を選択し、**「API」**を選択して**「API での作業」**ウィンドウを表示し、**「API Connect」**を選択することもできます。 **「API Connect」**ページでそのまま`「作成」`を押すことも、デフォルト設定を調整することもできます。 この演習では、インスタンスをバインドしないでおき、サービス名を後で見分けやすい名前に調整します。 一例として、`API Connect-weather-exercise` などの名前が考えられます。
`「作成」`ボタンを押して {{site.data.keyword.apiconnect_short}} サービスを起動します。  
新着情報を記述したアラートや**「ドラフト API」**通知スプラッシュ・ページが表示されることもあります。 情報を確認したら、**「OK」**アイコンをクリックして API Manager を表示します。
3. 以前に UI ナビゲーション・ペインをピン留めしていなかった場合は、{{site.data.keyword.apiconnect_short}} で**「ナビゲート」**アイコン ![](images/navigate-to.png) をクリックします。 API Manager UI ナビゲーション・ペインが開きます。 UI ナビゲーション・ペインをピン留めするには、**「メニューのピン留め」**アイコン ![](images/pinned.png) をクリックします。
4. UI ナビゲーション・ペインで**「ドラフト」**を選択し、**「API」**タブをクリックします。 **「API」**タブが開きます。![](images/drafts-api-1.png)
5. **「追加 +」**>**「新規 API」**を選択します。
6. API に関する基本情報を指定します。
	- **「タイトル」**フィールドに `Weather Data` と入力します。
	- タイトルを入力すると、**「名前」**フィールドに `weather-data` という名前が取り込まれます。この名前はそのままにしておきます。	
	- **「基本パス」**フィールドは `/weather-data` のままにします。
	- **「バージョン」**フィールドは `1.0.0` のままにします。
7. **「追加プロパティー」**を展開して、API の追加プロパティーを指定します。
	- API 定義を作成するためにデフォルトのテンプレートを使用する場合は、**「API テンプレート」**フィールドから**「デフォルト」**を選択します。
	- 残りのフィールドは変更しません。
![](images/new-api-1.png)
8. API を新規製品に追加してから、API 定義を作成します。
	- **「製品の追加」**を選択します。
	- **「タイトル」**フィールドで `Weather Data product` をデフォルトのまま使用します。
	- **「名前」**フィールドと**「バージョン」**フィールドは、そのままにしておきます。
	- **「この製品をカタログに公開」**チェック・ボックスを選択し、ターゲット・カタログとして**「サンドボックス」**を選択します。
![](images/new-api-2.png)
	- **「API の作成」**をクリックします。 API 定義のドラフト用の**「設計」**タブが開きます。
9. API が作成されます。 「設計」ページが表示されます。 ナビゲーション・バーで**「セキュリティー」**をクリックします。
![](images/api-security-1.png)
10. **「クライアント ID」**オプションのチェック・マークを外します。
![](images/api-security-2.png)
	>![](images/info.png)
	>ディスク保存アイコンの横に黄色の三角形のアイコンが表示されることもあります。  これは、まだ使用されていない定義があるかもしれないという意味の警告です。 (API 定義には影響ありません。)
11. **「定義」**セクションで**「定義の追加」**アイコン ![](images/add-icon.png) をクリックし、新しい定義をクリックして展開します。
12. その定義の名前を `Weather Data Output` にします。
13. その定義には 5 つのプロパティーがあります。 **「プロパティーの追加」**を 4 回クリックして、さらにプロパティーを追加します。 以下の説明を参考にして`「プロパティー名」`を名前変更し、`「説明」`、`「タイプ」`、`「例」`でデフォルトを使用します。
![](images/definition-new-1.png)
14. **「パス」**セクションで**「パスの追加」**アイコン ![](images/add-icon.png) をクリックします。
15. 新しく作成したパスの**「パス」**フィールドの内容を `/getweatherdata` に置き換えます。
16. **GET /getweatherdata** 操作をクリックして展開します。
![](images/path-new-1.png)
17. **GET /getweatherdata** 操作で**「パラメーターの追加」**をクリックし、**「新規パラメーターの追加」**をクリックします。
18. 新しいパラメーターの名前を `zip_code` にして、残りをデフォルトのままにします。
19. **「応答」**セクションの**「200 OK」**応答の**「スキーマ」**列で **Weather Data Output** 定義を選択します。 API 呼び出しの応答では、**Weather Data Output** で定義されているオブジェクトが応答オブジェクトになります。
![](images/path-new-2.png)
20. 「保存」アイコン ![](images/save-icon.png) をクリックして、変更内容を保存します。

---
## Web サービス呼び出しの追加および構成
Web サービスを API 定義に統合する invoke ポリシーと map ポリシーを追加して構成するには、以下の手順を実行します。
1. **「サービス」**セクションで**「サービスの追加」**アイコン ![](images/add-icon.png) をクリックします。 `「WSDL による Web サービスのインポート」`ウィンドウが開きます。
![](images/upload-file-1.png)
2. **「ファイルのアップロード」**を選択します。
3. **「ファイルのアップロード」**ウィンドウで、**「前提条件」**セクションの`手順 2` でダウンロードした `weatherprovider.wsdl` ファイルの場所を指定し、**「開く」**をクリックして作業を続けます。
4. **weatherService** SOAP サービスを選択して、**「完了」**をクリックします。 **「サービス」**セクションで、**WeatherService** Web サービスに **weatherRequest** 操作が 1 つだけ表示されます。
![](images/upload-file-2.png)

	![](images/services-add-1.png)	
5. **「アセンブル」**タブに移動して、**「DataPower Gateway ポリシー」**が選択されていることを確認します。
6. キャンバスで既存の **invoke** ポリシーを削除します。そのポリシーにカーソルを移動し、**「ポリシーの削除」**アイコン ![](images/delete-icon.png) をクリックしてください。
![](images/delete-invoke-1.png)	
7. パレットにある **weatherRequest** Web サービスを、キャンバスに表示されている破線のボックスにドラッグします。 invoke ポリシーと 2 つの map ポリシーがアセンブリーに配置されます。 最初の map ポリシーは、変数を Web サービス呼び出しの入力に割り当てます。2 番目のポリシーは、Web サービス呼び出しの出力を変数に割り当てます。 最初の map の出力と 2 番目の map の入力は、手順 4 で指定した WSDL から生成されます。
![](images/services-add-2.png)	
8. **「weatherRequest: input」**という map ポリシーをクリックした後、プロパティー・シートの「入力」列にある**「入力の編集」**アイコン ![](images/edit-icon.png) をクリックします。
![](images/services-add-3.png)	
9. **「+ 操作用パラメーター」**をクリックし、`get /getweatherdata` を選択します。
10. **「完了」**をクリックして `zip_code` パラメーターを追加します。
![](images/webservice-input-1.png)
11. 入力側の **zip_code string** に対応する円をクリックし、出力側の **zipcode string** に対応する円をクリックします。  
	![](images/webservice-input-2.png)
12. プロパティー・シートを閉じます。
13. パレットにある**「weatherRequest: output」**という map ポリシーをクリックした後、プロパティー・シートの「出力」列にある**「出力の編集」**アイコン ![](images/edit-icon.png) をクリックします。
14. **「+ 操作用出力」**を選択し、`get /getweatherdata` を選択します。
15. **「完了」**を選択して `Weather Data Output` 出力定義を追加します。
![](images/webservice-output-1.png)
16. 入力側の **zip string** に対応する円をクリックし、出力側の **zip string** に対応する円をクリックします。 以下の説明を参考にして残りのパラメーターをマップします。
![](images/webservice-output-2.png)
17. **「保存」**アイコン ![](images/save-icon.png) をクリックして、変更内容を保存します。

Web サービス呼び出しをアセンブリーに組み込み、入力パラメーターを SOAP 要求の該当部分にマップし、SOAP 応答の該当部分を JSON 出力にマップしました。

---
## API 定義のテスト
API Manager テスト・ツールを使用して API 定義をテストするには、以下の手順を実行します。
1. **「アセンブリー」**タブにある**「テスト」**アイコン ![](images/test-icon.png) をクリックして、テスト・ペインを表示します。
![](images/test-pane-1.png)
2. 以前にテスト・ツールを使用した場合は、**「セットアップの変更」**をクリックします。
3. 製品のリストから `Weather Data product 1.0.0` を選択します。
![](images/choose-product-1.png)
4. **「製品の再公開」**をクリックします。
5. **「次へ」**をクリックします。
6. 操作のリストから `get /getweatherdata` を選択します。  
	![](images/select-operation-1.png)
7. **zip_code** フィールドまでスクロールダウンして、`90210` と入力します。  
	![](images/test-api-1.png)
8. **「呼び出し」**をクリックします。 API から現在の天候が返されます。  
	![](images/test-api-2.png)

---
## このチュートリアルで学習した内容
このチュートリアルでは、以下のアクティビティーを実行しました。
1. REST API 定義をセットアップしました
2. 既存の Web サービスを呼び出して出力を返すように API を構成しました
3. API 定義をテストしました

---

## 次のステップ

[レート制限](tut_rate_limit.html)、[クライアント ID と秘密鍵](tut_secure_landing.html)、[OAuth 2.0 を使用した保護](tut_secure_oauth_2.html)のいずれかを使用して API を保護します。

作成 > **管理** > 保護 > ソーシャル化 > 分析

[important]: ./images/important.png "重要!"
[info]: ./images/info.png "情報"
[troubleshooting]: ./images/troubleshooting.png "トラブルシューティング" 

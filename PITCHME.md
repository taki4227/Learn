### エンジニアが学ばないとこうなります@Android
<br>

<br>
<br>
　　　　　　　　　　　　　Naoki Takimoto
---
今日話すこと
<br>

* 学ばなくて起きた障害
  * Android開発をやってきての経験
* 実際に自分が行っていること
  * （できれば）皆さんのも教えてほしい

---
### まずはじめに

---
### このブログ見たことありますか？

---

エンジニアは業務時間外でも勉強するべきなのか
<br>
<img src="assets/a.png" />

---

DevFest Tokyo 2017
<br>

<span>日時：2017/10/9(月) 10:00〜17:00</span><br>
<span>場所：東京国際交流館</span><br>
<span>主催：[東京で活躍している 14 のコミュニティ](https://tokyo.gdgjapan.org/team)</span><br>
<span>人数：約1,000人</span><br>
<span>内容：[タイムテーブル](https://tokyo.gdgjapan.org/schedule/day1)</span><br>
<span>URL：https://tokyo.gdgjapan.org/</span><br>
<img src="assets/logo_devfest2017.png" style="float: right;" height="100px" />

---
### レポート

---
個人スケジュール
<br>

<div style="padding-right: 75px; padding-left: 75px;">
  <div>10:00　オープニング</div>
  <div>10:40　クラウドってなんだろ？クラウドを活かすアプリケーション設計とは？</div>
  <div>11:30　大半のウェブサービス/アプリは、Firebaseなら簡単で安いですよ</div>
  <div>12:10　昼休憩</div>
  <div>13:20　ナビゲーションのUIベストプラクティス</div>
  <div>14:10　React Nativeアプリをリリースし続けるために、最初に行う8つの取り組み</div>
  <div>15:00　FirebaseAnalytics + BigQuery + DataStudio</div>
  <div>15:50　FlutterでAndroid/iOS両対応のアプリ開発</div>
</div>

---
オープニング
<br>
<img src="assets/dev_fest_opening.jpg" />

---
オープニング
<br>
<img src="assets/opening_me.jpg" />

---
クラウドってなんだろ？クラウドを活かすアプリケーション設計とは？
　[sinmetal](https://qiita.com/sinmetal)
<br>

* クラウドのメリット
  * H/Wのイニシャルコストが不要
  * H/Wのリプレースも不要
  * H/Wの構成を容易に変更可能
* クラウドでもH/Wがデータセンターに存在し、日々壊れている
  * H/Wが壊れたとしても、すぐ別のH/Wが生成され蘇る
  * クラウドが壊れることを前提に設計を行う必要あり

---
クラウドってなんだろ？クラウドを活かすアプリケーション設計とは？
<br>

* クラウドを活かすには？
  * 可用性(Availability)をあげる
    * リトライ
    * リクリエイト
  * パフォーマンスを上げる
    * 非同期処理(Queue)
    * 分散処理
* [発表資料](https://goo.gl/X54o2S)

Note:
リトライ
* 様々なレイヤー
  * クライアント・アプリケーションサーバ間
　* アプリケーションサーバ・DBサーバ間
* 適切なタイムアウト設定
* リトライを何回しても、複数のデータが作成されないようにする(冪等性(べきとう))

リクリエイト
* 複数インスタンスを用意
* 起動までにかかる時間を短くする

非同期処理
* 同期的に処理をする必要ないのは、非同期処理にする
* Queueサービスを使って、Taskのリトライ・割当などすると楽

---
大半のウェブサービス/アプリは、Firebaseなら簡単で安いですよ
　[神楽坂やちま](https://qiita.com/Yatima)
<br>

* Firebaseは真のサーバレス
* 使い方は少し独特
* 値段が高いがその分開発人数が減るので、トータルでは安くなる
* 無料枠も多い
* [Cloud Firestore](https://qiita.com/Yatima/items/54ea22d0cea1acc6cbcb)
* [発表資料](https://speakerdeck.com/yatima/apuriha-firebasenarajian-dan-dean-idesuyo)

Note:
様々なサービス
* 開発系
  * realtime database: DB
  * Hosting: HTML
  * Cloud Storage: 画像、動画
  * Cloud Function: API
* 便利系
  * Authentication
  * Cloud Messaging
  * Dynamic Links
* 監視系
  * Analytics
  * Crash Reporing
* 広告系

独特な例
* realtime database: NoSQL、JSONオブジェクトでデータ格納する

---
昼休憩
<br>
<img src="assets/lunch_time.png" height="440px" />


---
ナビゲーションのUIベストプラクティス<br>
　鈴木拓生
<br>

* 画面のヒエラルキーを考えることが大切
  * 親子関係
  * 並列関係
  * 無関係
  * コレクション
* そのヒエラルキーに基づいたナビゲーションを行う
  * 画面遷移の方法
    * ボタン、タブ、サイドメニュー...
  * 画面を戻る方法
    * 戻るボタン、☓ボタン...

Note:
例）ニュースアプリ
  * 親子関係: 一覧画面と詳細ページ
  * 並列関係: 一覧画面でのカテゴリー切り替え
  * 無関係: 設定、ヘルプ
  * コレクション: ポップアップ

画面のナビゲーション
  * Button
    * 下の階層に遷移するとき使う
  * Tab
    * 関連した項目を並べる
  * Bottom Navigation
    * 関連しない項目を並べる
    * ユーザがよく使う画面を置く
  * Navigation Drawer
    * どの画面からもアクセスができる
    * ユーザがたまにしか使わないが不可欠な画面を置く
  * Contents Navigation
    * 画面とコンテンツを分ける
    * 戻る以外のナビゲーションを置かない

---
React Nativeアプリをリリースし続けるために、最初に行う8つの取り組み
　[中川幸哉](https://qiita.com/Nkzn)
<br>

* React Nativeとは
* JSエンジニアはアプリエンジニアの"当たり前"で躓く
  * Gradle、XCode
  * Google Play Stpre、iTunes Connect
* 知っておきたいTips
  * applicationId / Bundle Identifier
  * バージョン番号
  * Fablic
  * Fastlane
* [発表資料](https://www.slideshare.net/Nkzn/react-native8-80596018?ref=http://ja.algonote.com/entry/devfest17)

Note:
applicationId / Bundle Identifier
 * アプリが持つ一意のID
 * 会社のドメインの逆順がいいよ
 * Android: ハイフンNG、アンダーバーOK
 * iOS: ハイフンOK、アンダーバーNG
バージョン番号
 * ストアに表示される番号
 * 内部バージョン（これしか使わない）

---
FirebaseAnalytics + BigQuery + DataStudio<br>
　[なかむらさとる](https://qiita.com/satoru_mag)
<br>

* FirebaseAnalyticsって？
  * SDK導入するだけで、ある程度データ収集してくれる
  * 自分でアクション設定してデータ収集も可能
* BigQueryって？
  * 完全なサーバレスモデル
  * Dremelというクエリエンジン
  * クエリ課金、ストレージ課金
* DataStudioって？
  * スライドにBigQuery連携してグラフを表示できる
  * GUIで操作(SQL不要)
* [発表資料](https://www.slideshare.net/ssuser8463f8/firebaseanalyticsbigquerydatastudio?ref=https://www.slideshare.net/ssuser8463f8/slideshelf)

Note:
完全なサーバレスモデル
* H/Wや機能アップデート不要
* VMやCPU、メモリ、ディスクサイズの設定も不要

Dremelというクエリエンジン
* いつでも元気にフルスキャン

---
FlutterでAndroid/iOS両対応のアプリ開発<br>
　[najeira](https://qiita.com/najeira)
<br>

* Flutterとは？
  * クロスプラットフォーム
  * 開発言語はDart
  * 自前でUI作成
  * ホットリロード
  * まだアルファ版
* [発表資料](https://www.slideshare.net/najeira/flutterandroidios)

Note:
Dart
* Googleによって開発されたウェブ向けのプログラミング言語
* JavaScriptの代替
* 競合するTypeScriptがGoogle社内の標準プログラミング言語として承認された

---
終わり
<br>
<img src="assets/dev_fest_place.jpg" height="500px" />

---
### Android Bazaar and <br>Conference 2017 Autumn

---
Android Bazaar and Conference 2017 Autumn
<br>

<span>日時：2017/10/14(土) 10:00〜18:00</span><br>
<span>場所：川崎市産業振興会館</span><br>
<span>主催：日本Androidの会</span><br>
<span>人数：約500人</span><br>
<span>内容：[タイムテーブル](http://abc.android-group.jp/2017a/timetables/)</span><br>
<span>　　　[バザール](http://abc.android-group.jp/2017a/bazaar/)</span><br>
<span>URL：http://abc.android-group.jp/2017a/</span><br>
<img src="assets/logo_abc2017a.png" style="float: right;" height="100px" />

---
### レポート〜セッション編〜

---
個人スケジュール
<br>

<div style="padding-right: 75px; padding-left: 75px;">
  <div>10:00　オープニング</div>
  <div>10:10　はじめてのボイス・アシスタント<br>　　　---Amazon Echo/Alexa と Google Assistant---</div>
  <div>11:10　Android登場10年目～Androidのイマを魅る～</div>
  <div>12:00　昼休憩</div>
  <div>13:00　Google AR101（TangoからARCore、WebAR）</div>
  <div>14:00　はじめてのActions on Google</div>
  <div>15:00　はじめてのMonaca ～中学校でもできる本格スマホアプリ開発</div>
  <div>16:00　アプリカンではじめるハイブリッドアプリ開発</div>
</div>

---
はじめてのボイス・アシスタント<br>
---Amazon Echo/AlexaとGoogle Assistant---
　丸山不二夫
<br>

* Amazon Echo/Alexa
  * ハードウェアやアプリの機能を呼び出す
  * 機能は限られる
* Google Assistant
  * 情報や知識をボイスを通じて提供する(音声検索)
  * 検索エンジンあって成り立つ
* Google Now
  * Google AssistantとのAIを使っているかどうか
  * Google Assistantと音声検索はほぼ同じ
    * 検索方法が異なる(Knowledge Graph検索)
* [発表動画](https://youtu.be/7yyJUv5iQ9c?t=4m27s)


Note:
Alexa
* あー言えば、こう言う
* 音声再生、電話、注文、Eメール

Knowledge Graph検索に問題あり
* 本来、Googleが収集したデータから検索してデータを返す
* Entity / Propertyモデルで構成されたグラフデータからデータを返す
* Entity: ○○ / Property: 誕生日 => 値を返す
* Propertyがなかったらデータを返さない

---
Android登場10年目<br>～Androidのイマを魅る～
　嶋是一
<br>

* 10年周期のイノベーション
  * 1990年代：インターネット
  * 2000年代：モバイルコンテンツ
  * 2010年代：スマホアプリ
  * 2020年代：スマホでWebアプリ？
* 今後のAndroid
  * IoT市場へ(Android Things)
  * AI市場へ(Tensor Flow Lite)
  * XR市場へ(Daydream, ARCore)
* [発表資料](https://www.slideshare.net/shimayo/android10-androidabc2017a)、[発表動画](https://youtu.be/7yyJUv5iQ9c?t=1h9m53s)

Note:
Android Things
* 小型マイコンボードなど組み込み向けOS
* ラズパイに入れられる

Tensor Flow Lite
* 端末上に用いるニューラルネット
* Google I/O 2017で発表

Daydream
* モバイルVR
ARCore
* モバイルAR
* Tangoの空間認識機能の一部をスマホで実現

---
Google AR101<br>
（TangoからARCore、WebAR）eegozilla
<br>

* ARCoreの特徴
  * モーショントラッキング
  * 水平面の検出
  * 光源の推測
* Tangoの特徴
  * モーショントラッキング
  * 深度認識
  * 領域学習

---
Google AR101<br>
（TangoからARCore、WebAR）

* ARCoreはTangoより機能としては劣るが普及しやすい
  * Tangoには追加ハードが必要
  * ARCoreは内蔵カメラのみ
* Web AR
  * ブラウザ上でAR体験ができる
  * ARCore, ARKitの入った専用のブラウザでthree.ar.js使う
* [発表動画](https://youtu.be/QVCvRgmMGt8?t=14m41s)

Note:
モーショントラッキング
* カメラを使い、スマートフォンの位置や向きや姿勢を計測して、オブジェクトの位置を正確に配置
水平面の検出
* 水平面にしかオブジェクトを置けない
光源の推測
* 周囲の環境光を推測して影をつける
* すべて画像解析

深度認識
* Time of Flight技術で赤外センサーで光線の照射と反射で距離を測定
* 水平だけでなく、壁でも可能
領域学習
* 自分がいる空間と場所を認識
* GPSの信号が途切れても、自分の位置を追跡可能

---
はじめてのActions on Google
　里山南人
<br>

* Actions on Googleとは
  * Google Assistantを使ったアプリの開発ができるツール
* [発表動画](https://youtu.be/7yyJUv5iQ9c?t=3h49m37s)

---
* アプリ作成に必要なもの

<img src="assets/action_on_google1.png" height="500px" />

---
* 会話フロー(静的)

<img src="assets/action_on_google2.png" height="500px" />

---
* 会話フロー(動的)

<img src="assets/action_on_google3.png" height="500px" />

---
* 会話設計

<img src="assets/action_on_google4.png" height="500px" />

---
はじめてのMonaca ～中学校でもできる本格スマホアプリ開発
　岡本雄樹
<br>

* Monacaとは？
  * Cordovaを内包したハイブリッドアプリ開発プラットフォーム
  * HTML5, CSS, JSでアプリ作成が可能
  * 月額課金(無料枠も少しある)
* Apache Cordovaとは？
  * モバイルアプリケーション開発フレームワーク
  * WebViewブラウザ上で動く
  * モバイルデバイスのカメラやGPSも使用可能

---
アプリカンではじめるハイブリッドアプリ開発
　畠田喜丈
<br>

* アプリカンとは？
  * 純国産のハイブリッドアプリフレームワーク
  * HTML5, CSS, JSでアプリ作成が可能
  * アプリ単位の固定額課金
* Monacaとの違い
  * アプリの中身だけを差し替えることが可能
  * Apple/Googleの審査なしにリリース可能
  * 各種SDKがJSで利用可能

Note:
各種SDK
* Replo, popinfo
* GA
* Felica

---
### レポート〜バザール編〜

---
バザール
<br>
<img src="assets/bazaar.png" height="500px" />

---
バザール全体
<br>
<img src="assets/bazaar1.JPG" height="500px" />

---
#### 企業ブース

---
みどりクラウド
<br>
<img src="assets/bazaar2.JPG" height="500px" />

Note:
* IoT
* 自動的に圃場の環境を計測、記録し、そのデータを離れた所からいつでも確認することができる圃場モニタリングシステム

---
富士通
<br>
<img src="assets/bazaar3.JPG" height="500px" />

---
PRISM
<br>
<img src="assets/bazaar4.png" height="500px" />

Note:
* 超小型IoTセンサー(5.2mm ☓ 9.0mm)
* 低消費電力なので、ボタン電池で1年以上稼働
* 加速度/地磁気/温度/湿度/気圧/照度/UVの7種類のデータを計測

---
RemoteRelay Solutions
<br>
<img src="assets/bazaar5.png" height="500px" />

Note:
* スマートグラスで通話やカメラ映像を共有する
* 遠隔での作業指示をサポート

---
#### コミュニティ団体

---
日本Androidの会 島原支部
<br>
<img src="assets/bazaar6.JPG" height="500px" />

---
そうめんもらいました
<br>
<img src="assets/bazaar7.JPG" height="500px" />

---
#### 体験・ワークショップ

---
ARのワークショップ
<br>
<img src="assets/bazaar8.png" height="500px" />

---
VR体験
<br>
<img src="assets/bazaar9.JPG" height="500px" />

Note:
* ヘッドマウンドディスプレイ(Oculus Rift)
* SteamVR ゲームプラットフォーム (台湾 Valve)
* MR
* ACWDEEPという会社 映像は映画やCMのCGなど(銀魂、進撃の巨人など)

---
ドローン体験
<br>
<img src="assets/bazaar10.JPG" height="500px" />

---
ドローン体験
<br>
<img src="assets/bazaar11.JPG" height="500px" />

---
ドローン体験
<br>
<img src="assets/bazaar12.png" height="500px" />

---
視覚障害者体験
<br>
<img src="assets/bazaar13.png" height="500px" />

Note:
* 色盲、視野狭窄などをAR体験

---
#### 子供向けプログラミング

---
教育版レゴ
<br>
<img src="assets/bazaar14.JPG" height="500px" />

Note:
* レゴで組み立てたロボットをプログラミングして動かす
* アイコンを使って、ドラック＆ドロップで、簡単にプログラミング
* 3〜6年生向け

---
プログラミング教育×ドローン、ロボット
<br>
<img src="assets/bazaar15.JPG" height="500px" />

---
ブロックでプログラミング
<br>
<img src="assets/bazaar16.JPG" height="500px" />

---
ブロックでプログラミング
<br>
<img src="assets/bazaar17.png" height="500px" />

---
IoT ブロック
<br>
<img src="assets/bazaar18.png" height="500px" />

Note:
* MESHというIoTブロック
* IoTブロックとスマホを無線で繋げてセンサーが使える

---
IoT ブロック　[活用例](https://recipe.meshprj.com/recipe)
<br>
<img src="assets/bazaar19.png" height="500px" />

Note:
* 左上：GPIO
* 右上：ボタン
* 左下：温度・湿度
* 右下：明るさ
* 他にも、人感・LED・動きなどある

---
### 今後行く予定

---
Droid Kaigi 2018
<br>

<span>日時：2018/2/8(木)、9(金)</span><br>
<span>場所：ベルサール新宿グランド<br>
　　　コンファレンスセンター</span><br>

---
#### ありがとうございました



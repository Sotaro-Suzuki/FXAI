[JP]
# FXAI 
こんにちは、AIエンジニア兼起業家の鈴木爽太郎です。<br>
この度着想から1日平均8時間、そして4年の歳月をかけて「自動で稼ぐAI」を開発いたしました。<br>
現時点のプログラムはβ版ですので、まだ販売等は行っていません。<br>
サブスクリプションによる販売は2022年6月ごろGogoJungleにて予定しています。<br>

## 「自動で稼ぐAI」とは？
このプログラムは端的に表すとAIを搭載した自動売買プログラムです。<br>
では普通のアルゴリズム取引とは何が違うかというと、一般的なアルゴリズム取引は決まったルール（例えば最も簡単なルールだとゴールデンクロスとデッドクロス）に従って売買取引を行いますが、このプログラムは「自動で情報を収集し、自動で学習し、自動で売買するプログラム」だということです。<br>
具体的には以下のような手順になります。<br>

<img src="https://user-images.githubusercontent.com/95641926/146052912-6321bc7a-fe88-4e75-b7d6-b1529010c87d.png" width="330">

<br>
①まずクラウド上で毎週末に自動で過去の株価、為替レート、商品先物、経済指標、SNS(twitter, reddit)の情報を収集しデータとして蓄積します。<br>
②次に、そのデータをクラウドで自動でAIに学習させます。ここでの重要なポイントは決められたパターンで学習をするのではなく、アンサンブル学習、つまり様々なモデルを試し、どの情報がその時代に最も影響するかを数値化し、複数の最適なモデルを組み合わせて選べるという点です。モデルは主にSVM、MLP、RNN、LSTM、GRUから選び、さらにその中でパラメータの調整を行います。<br>
③最適なモデルが選ばれたら、平日の取引時間帯にリアルタイムで売買判断を予測し、クラウドからクライアントへ判断結果を送ります。<br>
④各証券会社の自動売買プラットフォームで、送られてきた売買判断をもとに自動売買をします。<br>
このように、毎週AIを時代に沿ってどんな情報が重要か最適化できるので、何も手を加えずとも半永久的に成長し続けることのできることが可能なのです。<br>
ちなみに個人的には「自動で稼ぐAI」という呼び名は好きでは無いのですが、万人に刺さる言葉として、あえてこのような呼び名にしました。

## シミュレーション結果
過去4ヶ月間売買したシミュレーションの結果が以下の画像になります。<br>
![4096-64-1e-06-0 001-glorot_normal-LSTM-2 0-0 0-1 0-1 0-30分割](https://user-images.githubusercontent.com/95641926/147685891-28501ed7-1290-4642-857c-627b2848916f.png)

青の線が買いの判断をした時の利益になります。つまり右肩あがりになればなるほど利益が出ていることになります。<br>
逆に赤の線が売りの判断をした時の利益になります。この場合は右肩下がりになればなるほど利益が出ていることになります。<br>
そして緑の線は買いの判断をした場合の利益と売りの判断をした場合の利益の合計値になります。<br>
左の目盛りは通貨、つまりEUR_USDの価格推移を示し、右の目盛りは1通貨での取引をした際の利益(ドル)になります。過去4ヶ月の取引の結果、合計の利益が0.067まで伸びていますので、例えば資産額を13万ドルとして、全て10万通貨の取引をしたとすると6691ドルの利益が出たことになります。しかし取引回数が502回あり、1回の取引に0.00005ドルの取引手数料がかかりますので、純粋な利益は4181ドルになります。<br>
よって過去4ヶ月の利率は3.70%になります。最大ドローダウンを考慮するとレバレッジ25倍までは破産リスクはありませんが、念の為レバレッジを10倍に設定した場合、利率は37.0%になります。<br>





## プログラムの導入方法
このAIは為替証拠金取引(FX)のEUR/USDの15分足で最もパフォーマンスが良かったので、自動売買ができるのはEUR/USDの15分足のみとなります。その他通貨、株、債権、コモディティ、暗号資産取引用のAIも開発中ですので、良いパフォーマンスが出れば追加でアップロードしていきます。<br>
そして現在、このレポジリトリにはEX4ファイルが一つアップロードされています。なので、売買ができるプラットフォームはMetaTrader4上のみとなります(推奨はOandaJapan)。近々、どの証券会社のプラットフォームでも対応できるようなソフトウェアの開発を計画中です。<br>
そしてMetaTrader4は常時インターネットに接続してないといけないので、クラウド上で以下の手順を踏むことをお勧めします。<br>
では具体的な導入方法です。<br>
①まずこのレポジリトリ内の「FXAI.ex4」ファイルをローカルPCにダウンロードします。<br>
②次に証券会社のMetaTrader4を立ち上げ、「FXAI.ex4」ファイルをMetaTrader4上の「Experts」フォルダ内に加えます。(<br>
③次にライブラリファイル「Mylib.ex4」を「Library」フォルダ内に加え、「Mylib.mqh」ファイルを「Include」フォルダ内に加えます。<br>
④「Options」から「Expert Adviser」を選択し、以下の写真のように囲んだ場所をチェックし、urlに<br>"http://ss-cloud.net"<br>を追加します。これにより、クラウドに売買判断をリアルタイムにリクエストすると同時に実際の売買の取引ができます。<br>
⑤「Expert」フォルダ内の「FXAI.ex4」をEUR_USDの15分足のチャートにドラッグ&ドロップをする際、以下のようなウィンドウが立ち上がります。ここでは外部変数として名前と生年月日を入力する欄がありますので、TaroYamadaのようにアルフファベットのフルネームを挿入してください。生年月日は20010101のように空白を開けずに入力してください。名前と生年月日をクラウド上で照合し、売買判断をMQL4ファイルに送り、MT4上で売買することができます。<br>
<img width="330" alt="スクリーンショット 2021-12-15 0 12 00" src="https://user-images.githubusercontent.com/95641926/146094305-e216becb-5ce6-4816-9490-f8d798b7c02f.png">





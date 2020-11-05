# ConvCalcOCR


# 概要
G検定で出ると噂の、畳み込み計算をなんとか自働化できないかとチャレンジしました。
こんなの人間ががんばる計算じゃないかと思います。
でもこれ作っている時間を試験勉強に費やした方が良かった気がします。

内部的には
- PySimpleGUI (本当はKivyを使いたかった)
- OpenCVを使用したマウスドラッグによる領域指定
- TesseractOCRによる文字認識
を使用していますので、これら個別にも参考になれたらなと思います。
win32apiを使用しているのでそのままではUNIXでは動かないです。
Kivyの方がかっこいいし慣れているのでそっちを使いたかったのですが、勉強のためにPySimpleGUIを使ってみました。
でもKivyはモダンでかっこいいのでお勧めです。


# 必要モジュール
- PySimpleGUI
- numpy
- opencv
- scipy
- pywin32
- pyocr  
バージョン依存はないと思います。  
あとTesseractOCRを別途インストールして環境変数に追加する必要があります。

# 使い方
1. 読み取りたい対象のウィンドウ名を上の欄に入力し、右のボタンを押すと画面が右下に表示される。Chrome内のタブ名を入力しても黒い画面が出るので、Firefox内のタブ名を入力した方がいいです。(ChromeDriverが無いとアクセスできない？)
2. filterボタンを押すとポップアップが出るので、グリッドが合うように畳み込みフィルター部分を選択する。
3. targetボタンで畳み込みしたい対象を選択する。
4. 各テキストボックスの読み取った数値が間違っていたら修正する。 (割と誤判定する)
5. calculateボタンを押すと畳み込み計算結果が表示される。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/855265/8b16f4bc-5c79-fc07-b925-e279b6eda5d9.png" width=80%　alt="概要">

テスト用画像(Firefoxで開いてください)
<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/855265/a4307418-f6c8-f26d-e312-5e2bfc290b9a.jpeg" width=50%　alt="概要">

# 外観部分
PySimpleGUIでGUI部分を作ってます。
redefine_rectangle関数とdraw_shape関数はマウスドラッグで座標を取得する際の参考になるかもしれません。

実行結果

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/855265/e86ed4ee-91f9-47d9-88ec-67b4747f9b35.png" width=80%　alt="GUIフレーム">

# グリッド型の矩形描画
マウスドラッグした範囲を合わせやすいようにグリッド付きで描画する

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/855265/e096c9d0-fc66-9677-e957-4aa015c0d10b.png" width=80%　alt="マウスドラッグ">

# マウスドラッグによる範囲指定の補正

マウスドラッグで範囲を指定する際には、描画し始めに画像サイズが0になり発生するエラーや座標計算時の足し引きでマイナスにならないようにする (参考にしたページメモしてませんでした。すみません。)

# 画像分割
画像を任意の数分割し、ついでにeroderatio割合だけ周囲を削ることで問題文中の表の枠線を画像から削除する


# 読み取った数値の修正
「.」や「-」などが正常に読み取れないことが多いため、これらは一旦無視しG検定では整数部は1桁のみと仮定して整形する


# 読み取った数値の画面表示
OCRで読み取った数値のListには改行がなくそのままでは表示が崩れるため、分解して改行コードを挿し込む。


# 畳み込み計算
OCRで読み取った数値は、画面表示用にListの括弧を消してあるので戻してからscipyで計算する



# コード全体
OCRで読み取った数値は、画面表示用にListの括弧を消してあるので戻してからscipyで計算する


# 参考
- https://qiita.com/dario_okazaki/items/656de21cab5c81cabe59
- https://pystyle.info/opencv-split-and-concat-images/
- https://pystyle.info/opencv-resize/#outline__3_5
- https://stackoverflow.com/questions/48097941/strided-convolution-of-2d-in-numpy/48098534
- https://qiita.com/danupo/items/e196e0e07e704796cd42


# 最後に
- 至らない所が多いと思いますので気軽にご指摘ください
- G検定で畳み込み計算は何問出るのでしょうか
- これ作っている時間勉強した方が良かった気が

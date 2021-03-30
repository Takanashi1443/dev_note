[3D技術の目次へ](./../)

### マテリアル未設定の「スザンヌ」をUnityに持っていく

#### とりあえず何も考えずにUnityに持っていってみる

初期状態から、箱を消して、「Add」→「Mesh」→「Monkey」すると、スザンヌが出現しました。

![add_suzanne](./media/nakid_suzanne/add_suzanne.png)

これをさっきと同じようにライトとカメラを除いてエクスポートして、Unityへ。

![import_suzanne](./media/nakid_suzanne/import_suzanne.png)

ん。とりあえず配置できた。

けど……後ろ向いちゃってるな。なんかRotationが-89.98とかなってるし。

あと、なんかBlenderで見た時よりテカってるような。

Rotationを0にすると……

![import_suzanne2](./media/nakid_suzanne/import_suzanne2.png)

分かりにくいけど、下を向いてしまった。

あとScaleも100だな。これを通常の1.0にすると……まぁ米粒みたいなサイズになるよね。（省略）

なんか回転とスケールがよくない。

#### 回転とスケールを何とかする

結論から言うと、これはBlenderの設定で何とかなる。

改めてよく見ると、スザンヌはBlender上ではY軸の負の方向を向いている。

そして、Unity上でも、Rotationを0にすると下方向、つまりY軸の負の方向を向いていた。UnityとBlenderでは画面に対する軸の取り方が違うけどモデルの軸は変わっていないということだな。

BlenderではY軸マイナス方向が正っぽいけど、Unityでは、通常、Z軸の正方向が正となる。

さらに、Z軸を中指、Y軸を人差し指、X軸を親指となるようにすると、
Blenderでは右手、Unityでは左手になる。

画面上の軸の取り方も違うし、座標の「左手系」「右手系」も違う。

まあ違うのは分かったけど結局どうすればいいのかと言うと、エクスポート設定をこうすればよい。

![export_suzanne](./media/nakid_suzanne/export_suzanne.png)

- Scaleを「1.00」にしてApply Scalingsにチェックをつける
- Forwardを「-Z」、Upを「+Y」つまりUnityの設定に合わせる
- Apply UnitとApply Transformationのどっちにもチェックをつける

すると、ちゃんとZ軸の奥を向くし、回転もないし、スケールも1になる。ハッピー！

![import_suzanne3](./media/nakid_suzanne/import_suzanne3.png)

……当面そんなに困ることはなさそうだけど、実はこの「Apply Transformation」は実験的機能で、
オブジェクトを階層構造にしすぎたりするとうまく動作してくれないらしい。

奥の手としてはモデル全体を回転させて、Z軸正方向に向かせて、さらに左右反転させること。めんどくさそう。

#### ちゃんと読み込めたSuzanneを見てみる





# アセット備忘録 - MESHTINT STUDIO - Chibiシリーズ

## 関連リンク

[パブリッシャー公式](https://www.meshtint.com/)

### 雑記

2018年8月のリリース以降アップデートされていないので、それほど手厚いサポートは期待できないか。
2021年3月で最もアクティブなのは[Twitter](https://twitter.com/MeshTint)。

### デモシーンを動くようにするまで(2019.4.9f)

[Standard Assets (for Unity 2018.4)](https://assetstore.unity.com/packages/essentials/asset-packs/standard-assets-for-unity-2018-4-32351)のトゥーンシェーダや、First Person Controllerというスクリプトを利用している。
Standard Assetsを先にインポートしないと紫色になる。

かといって、Standard Assetsを新しいバージョンに入れるとエラーが出る（旧バージョンで使用していたGUITextというクラスが使えなくなったためなど）。
ここでは2019.4.9fを使用することを想定し、エラーが出る部分を削除して使用する。

以下、Standard Assetsを残しながらエラーが出ないようにする方法と、Standard Assetsを使用せずにシェーダなどを別のものに差し替える方法を説明する。

#### Standard Assetsを残しながら改変する方法

1. Standard Assetsは全部インポートする。
1. GUITextクラスが使用されている部分を、UI.Textに変更する。(UnityEngine.UIをusing)

#### Standard Assetsを使用しない方法


### デモシーン

以下、Chibi Female Pack 01の例。

#### 共通の仕組みの解読

シーン：3rd Person Controller Demo Scene

上記の方法でシェーダを割り当てた後、再生可能になる。
カメラは固定で、WASDで動かせる。

Standard Assetsの「Third Person User Control」と「Third Person Character」がアタッチされたキャラクター。

衝突判定は地面に設定されたMesh Colliderと「ThirdPersonController Knight」に設定されたCapsule Collider。

親オブジェクトのKnight以下に、いくつもの子パーツが存在する。
EthanSkeltonは削除しても大丈夫。

Knightを選択して「Select Prefab Asset」を選択すると、「Customize character here」フォルダ内の「00 Customized Samples」フォルダ内のプレハブに飛ぶ。
Customize character here フォルダ内にいくつかフォルダがあり、フォルダ名の指示に従っていくとキャラをカスタマイズできるようだ。

ThirdPersonController Knight上にKnightを消してから別のCustomized Samplesのプレハブを配置すると、
移動も出来るし歩くモーションもする。ただし、Knightを消さずにdisabledにしてから別のプレハブを配置すると、
そのプレハブに設定されたAnimatorのモーションが優先されてしまう。

最初の子に対しては親のAnimatorのControllerが適用され、それ以外の子に対しては子のAnimatorのControllerが適用されるっぽいが、Animatorの入れ子構造の意味がよく分からないので保留。
とりあえず、子のAnimatorは削除しても動く。

Avatarは共通で「Female 01 Avatar」を使用するようだ。

シェーダは共通でToon/Basic Outlineを使用している。
これを差し替えれば別のものになると思われる。

#### 組み合わせでキャラを作ってみる

01 Top, 02 Bottom, 03 Hands, 04 Belt, 05 Feetからそれぞれ1つを表示させることで表示できる。
また、Rig以下の「+〇〇」というオブジェクトの下にアクセサリーを配置すると髪型を変えたりアクセサリーを
変えたりすることができ、表情などもこれで配置する。
例として、サンプルキャラクターNoviceには+Headの位置に

- Female Head 01 (頭部。共通)
- Female Hair 01 Hat 01 Brown (髪型・帽子)
- Earrings 01 Silver (イヤリング)
- Glasses 01 Black (眼鏡)
- Female Eyes 04 Brown (目)
- Female Mouth 01 (口)

がアタッチされている。
目と口を差し替えれば表情の変更もできそうで興味深い。

#### で、オリジナルのパーツはどうやって作るの？

服はFemale 01.fbx内に含まれており、
パーツはそれぞれ別のFBXファイルとして作られているようだ。
ということは

- 服を変える: Female 01.fbxを編集する
- パーツを追加する: 各FBXを参考に改変・自作する

という方法で作れそうだ。

シェーダがパーツにより異なり、

- イヤリングと眼鏡: Toon/Basic Outline
- 目と口: Unlit/Transparent

となっている。

##### 目と口

Unlit/TransparentはBase (RGB) Trans (A)としてテクスチャ1つを指定するようになっている。
要は画像をそのままメッシュに貼り付けて、光とかを考慮せずに表示するシェーダ。











エラーの出ているスクリプトを削除するとそれはそれでまた別のエラーが出るので、

First Person Controllerを残す場合


Assets/Standard Assetsフォルダ内の

- Utilityフォルダ



#### 必要なものをCreateする

まず、

- Flowchart (会話内容などを保持するコンポーネント)
- Character (キャラクターの情報を保持するコンポーネント)
- Stage (描画に使用するGameObject群)

を作る。


会話内容や動きはFlowchartコンポーネントを使って編集する。

Tools &rarr; Fungus &rarr; Create &rarr; Flowchart でHierachy上にFlowchart付きのGameObjectが生成される。

Flowchartの中身は

Tools &rarr; Fungus &rarr; Flowchart Window で表示される専用ウィンドウで編集する。

会話で使用するキャラクターはCharacterコンポーネントとして作成し、Flowchartから参照する。

Tools &rarr; Fungus &rarr; Create &rarr; Character でHierachy上にCharacter付きのGameObjectが生成される。

描画は別途Canvasを用意して行い、FlowchartとCharacterは描画には使用しないため、
Hierachy上にFungusManagerという親オブジェクトを作り、その中にFlowchartやCharacterなどFungusで使用するものを入れておくと良さそう。

Tools &rarr; Fungus &rarr; Create &rarr; Stage でHierachy上にStage付きのGameObject、及びその子としていくつかのGameObjectが生成される。

Stageの子として、Canvas付きのGameObjectが生成されるが、これが実際の描画に使用するCanvasとなる。

以下、分かりやすいようStageはFungusStageと名前を変えておく。



#### Characterに情報をセットする


#### Flowchartに会話内容を追加


### どういう仕組みか

#### Create Stageで作られるStageの子たち

Left, Rightは基準位置を表している。
基準位置のリストは


### ShibaTemplateと連携させる

ここではShibaTemplateのシーンイベントシステムと連携させる例を記す。

ShibaTemplate &rarr; Wrappers &rarr; Fungus をインポートして使用する。 

すなわち、あるイベントの発行を受けてFungusの会話を開始し、会話が終了すると会話終了イベントを発行する。


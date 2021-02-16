# アセット備忘録 - Fungus（会話システム）

## 基本編

[応用例はこちら。](./advanced.md)

### 導入

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


# アセット備忘録 - Grabbit（In Editor Mode Physics Transformツール）

### 動作条件

- PhsyXに依存しているためNvidia製GPU搭載端末のみ対応(? 要確認)

## 導入

移動させたいオブジェクトを選択して「U」キーを押下。
Unity標準のMove Toolを使うときの要領でオブジェクトを移動させる。

## Grabbitモード

「U」キーはGrabbit Placementモードのショートカット。
Placementモードに遷移するには、画面左上のウサギマークを押すことでも可能。

Grabbitのモード一覧は下記の通り。

「U」: Placementモード
「I」: Rotationモード
「O」: Alignモード
「P」: Fallモード
「[」: Pointモード

### Placementモード

Unity標準のMove Toolに対応する機能。
選択したオブジェクトが他のオブジェクトに食い込まないように移動する。

### Rotationモード

Unity標準のRotation Toolに対応する機能。
選択したオブジェクトが他のオブジェクトに食い込まないように回転する。

### Alignモード

Unity標準のScale Tool用のGizmoを使用する機能。
選択した複数のオブジェクトが互いに食い込まないように整列する。
オブジェクトのScaleは変更されず、Position/Rotationのみ変更される。

### Fallモード

選択したオブジェクトが他のオブジェクトに食い込まないように落下する。
落下方向は専用画面で設定可。

## ポイント
### コライダーの自動追加
オブジェクトに *Colliderコンポーネントがなくても、
Grabbitの各種モードに遷移したときにコライダが自動で追加されて、
衝突判定を行うようになる。

つまり、Grabbitを使用することで、
*静的ゲームオブジェクトに対しても*衝突判定を行える。

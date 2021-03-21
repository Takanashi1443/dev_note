# とりあえずキャラクターで3D空間を動けるようにする - カメラの準備

[戻る](./../index.md)

## CinemachineVirtualCamera

Cinemachineはパッケージマネージャからインストールして下さい。

CinemachineVirtualCameraは、プレイヤーに追随させたりといったことが簡単にできる「バーチャルカメラ」で、
メインカメラの制御を乗っ取るような感じで動作します。

複数のバーチャルカメラを組み合わせたり、滑らかに切り替えたり（ブレンド）出来ます。

## CinemachineVirtualCameraの導入

Cinemachineをインストール後、「Cinemachine」→「Create Virtual Camera」で、
Hierachy上に「CinemachineVirtualCamera」というコンポーネントがアタッチされたGameObjectが作成されます。

![create_vcam_virtual_camera](./media/cinemachine_camera/create_vcam_virtual_camera.png)

また、Main Cameraの横に、VirtualCameraと同じアイコンが出現します。
内容を確認すると、CinemachineBrainというコンポーネントが付与されています。

![create_vcam_main_camera](./media/cinemachine_camera/create_vcam_main_camera.png)

これは、Main CameraがCinemachineVirtualCameraによってコントロールされていることを差し、
この状態になると、MainCameraの位置や向き、画角といったものがCinemachineによってコントロールされることを指します。

ひとまず、今回は1つのVirtualCameraのみを使います。

## CinemachineVirtualCameraの設定のサンプル

設定項目が多くて適当にいじっててもなかなかいい感じにならないので、
目的に合わせた設定方法のサンプルを示します。

CinemachineVirtualCameraにはいくつも設定項目がありますが、ひとまず

- Body：カメラの位置に関する設定項目、「Follow」でその対象を設定
- Aim：カメラの向きに関する設定項目、「Look At」でその対象を設定

ということを頭に入れておきましょう。

![vcam_body_aim](./media/cinemachine_camera/vcam_body_aim.png)


### プレイヤーに注目する

#### SimpleWanderer04と併用するカメラ設定の方針

SimpleWanderer04は、左右キーで左右に、上下キーで画面の手前奥に移動するCharacterController操作用スクリプトです。

また、カメラの向きが変わると、その向きを反映して、カメラから見て左右・手前奥に移動します。

スーパーマリオ64（の平地を移動する時）っぽい動きです。

この時の望ましいカメラの動きの一例として、

- 基本的にプレイヤーを画面中央付近に捉える
- プレイヤーが移動しているときは、後ろの方からついていく
- プレイヤーが移動の向きを変えても、すぐに真後ろに移動せず、徐々に移動する

というカメラ設定にしたいと思います。

3つ目の補足として、例えば常にプレイヤーの真後ろにいる設定の場合、左右キーを押すとプレイヤーの向きが90°回転、
すぐにカメラはプレイヤーの背後に移動、結果的にカメラも90°回転します。

左右キーではカメラの向きに対して左右に移動するので、左キーを押した時にプレイヤーが移動する方向も
90°回転します。

これを繰り返すと、左右キーを押し続けた時、プレイヤーはほとんど同じ位置で回り続けてしまいます。

#### Transposerを使ってプレイヤーに注目

結論から言うとこんな設定。

![vcam_follow_character](./media/cinemachine_camera/vcam_follow_character.png)

- Aimについて
    - Composerを選択。
    - Tracked Object Offsetは、対象のTransformの中心に対して、どこを注目するか(補足)。

通常、キャラクターは接地を正確にするため、Transformの中心を足元に合わせる。

Tracked Object Offsetが「X:0, Y:1, Z:0」なのは、カメラの中心が中心から上に1メートル、つまりキャラの足元から1ｍの位置になるようにカメラを向けるということを意味する。












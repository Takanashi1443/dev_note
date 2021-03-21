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


### SimpleWanderer04と組み合わせる

SimpleWanderer04は、左右キーで左右に、上下キーで画面の手前奥に移動するCharacterController操作用スクリプトです。

また、カメラの向きが変わると、その向きを反映して、カメラから見て左右・手前奥に移動します。

私の好きなスーパーマリオ64（の平地を移動する時）っぽい動きです。

しかし、これでうまく操作できるようにするためにはカメラ側の動作もちゃんとそれに合ったものにしなければいけません。













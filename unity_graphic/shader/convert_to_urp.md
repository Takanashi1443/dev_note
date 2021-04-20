[Unity - グラフィックの目次へ](./../index.md)

# URPで使えるシェーダへの変換

URP（Universal Rendering Pipeline）はレンダリング方法の1つである。

シェーダは基本的に特定のレンダリング方法で使用するものなので、
URP用のシェーダでないシェーダはURPでは表示されず、ピンクになる。

ここでは、サードパーティのアセットを取り込むなりした際に物体がピンクになった時の対応方法について記す。

## 標準的な変換

「Standard」シェーダなどのビルトインシェーダ（Unityに最初から提供されているシェーダ）は、一部はUnityに変換機能がついている。

![convert_material_to_urp](./media/convert_material_to_urp.png)

「Edit」→「Render Pipeline」→「Universal Rendering Pipeline」→「Upgrade Project Materials To UniversalRP Materials」

を実行すると、プロジェクト内のマテリアルにセットされている、変換に対応しているビルトインシェーダを一括してURPの対応するものに変換できる。

よく使われているビルトインシェーダの対応状況の例は以下の通り。

「Standard」→「Universal Rendering Pipeline/Lit」
: 実際の物理法則に則った3D物体に使用される。


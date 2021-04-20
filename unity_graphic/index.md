# Unity - グラフィック - 目次

## はじめに

この目次はUnityのグラフィックに関するものである。

アニメーションなど、基本的にゲームのロジックと関係ないがゲームの見た目に関わるものや、
Unityと外部ソフトのやりとりも含む。

## 目次（基本）

この目次内の記事は順番に読むことを推奨。

### 仕組み編

- [URPについて最低限知っておくべきこと](./how_it_works/what_is_urp.md)

標準とするURP（Universal Rendering Pipeline）について最低限知っておくべきこと。

- [Unityにおける「マテリアル」と「シェーダ」](./how_it_works/material_and_shader.md)

3Dオブジェクトの表示にはマテリアルとシェーダの理解が不可欠。

- [fbxフォーマットについて](./how_it_works/fbx_format.md)

3Dモデルで最もよく使用されるfbxフォーマットについて。
3DソフトとしてはBlenderを基本とするが、Blenderについては「Blenderとの連携編」を参照。

### シェーダ編

- [URPで使えるシェーダへの変換](./shader/convert_to_urp.md)

変換に対応しているビルトインシェーダをURP用のシェーダに変換する方法。

- [既存モデルのシェーダを変更して遊んでみる](./shader/change_shader.md)

URPの基本的なシェーダが割り当てられた既存モデルのシェーダを、モデルのオリジナルデータを残したまま変更してみる。fbxモデルをシーンに配置した時の挙動なども。

<!--

### Blenderとの連携編





### 基本編

###### [fbxフォーマットについて](./basic/fbx_format.md)

基本的に使用する3Dモデルのフォーマットであるfbxフォーマットの基本について。

###### [Blenderのファイル構造とfbxへの出力](./basic/blender_fbx.md)

Blenderのオリジナルの拡張子はblendである。Blenderのファイルがどのような構造か。注意点なども。


###### [マテリアル未設定の「スザンヌ」をUnityに持っていく](./basic/nakid_suzanne.md)

Blenderで生成したfbxファイルをUnityに持っていく。仮想アセットの概念。

###### BlenderにおけるマテリアルとUnityへの移行(./basic/blender_material_to_unity.md)



###### BlenderにおけるテクスチャとUnityへの移行


###### Blenderにおけるアニメーション（回転）

###### Cubeを回転させるアニメーションをUnityで再生する

-->


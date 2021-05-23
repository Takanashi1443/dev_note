# フォルダ構成とアセンブリ分割

[トップへ](./index.md)

## フォルダ構成

拡張子のないものはフォルダ、asmdefはアセンブリ定義ファイル。

asmdefファイルがあると、そのフォルダ内がアセンブリ分割の対象となる。

アセンブリ分割の対象のフォルダ内に別のasmdefファイルがあると、そのフォルダはまた別のアセンブリ分割の対象となる。

```

Assets
├ ShibaEngine
｜  ├ HogeAssetA
｜  ｜　├ Scripts 
｜  ｜　├ CopySource
｜  ｜  ｜　└ ShibaEngine.HogeAssetA.CopySource.asmdef 
｜  ｜　└ ShibaEngine.HogeAssetA.asmdef 
｜　└ (以下略)
｜
├ Plugins
｜　├ UniRx
｜  ｜　┠ Scripts 
｜  ｜  ｜　└ UniRx.asmdef 
｜  ｜　└ Examples
｜  ｜
｜　├ Zenject
｜  ｜　└ zenject.asmdef 
｜  ｜
｜　├ ShibaEngine
｜　｜　├ Core
｜  ｜  ｜　├ Scripts
｜  ｜  ｜　├ CopySource
｜  ｜  ｜  ｜　└ ShibaEngine.Core.CopySource.asmdef 
｜  ｜  ｜　└ ShibaEngine.Core.asmdef
｜  ｜  ｜
｜　｜　├ Modules
｜  ｜  ｜　├ Scripts
｜  ｜  ｜　├ CopySource
｜  ｜  ｜  ｜　└ ShibaEngine.Modules.CopySource.asmdef 
｜  ｜  ｜　└ ShibaEngine.Modules.asmdef
｜  ｜  ｜
｜　｜　└ Utils
｜  ｜  　  └ ShibaEngine.Utils.asmdef
｜  ｜
｜　└ (以下略)
｜
└ （以下略)

```

## フォルダ構成解説

ShibaEngineは、

- 中核のスクリプトであるCore
- 汎用的で、複数のShibaAssetから参照されるModules
- 主にエディタ拡張や拡張メソッドを定義するUtils
- 個別の機能を提供するShibaAssets（複数）

からなる。

このうち、ShibaAssets以外は、先だってコンパイルされるPluginsフォルダに入れてあり、
ShibaAssetsのみPluginsの外にある。
（ShibaAssets、Plugins/ShibaAssetsはProjectビューでFavoritesに入れておくとよい）

スクリプトの使用例であり、独自のスクリプトを記述する際にコピペ元とすることを想定したアセット群を
CopySourceと呼ぶ。
CopySourceは、関連するスクリプトと同じフォルダ内にCopySourceというフォルダを作って
そこに定義するが、アセンブリ分割はCopySourceとそれ以外で分ける。

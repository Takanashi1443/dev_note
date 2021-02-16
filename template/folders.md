# フォルダ構成

## Assetsフォルダ内

Assetsフォルダ直下は多くのサードパーティアセットのインポート先であり、
ここにプロジェクト関連のフォルダを置くとサードパーティアセットのフォルダと区別がつきにくい。
従って、プロジェクト名のフォルダを1つ作り、その下に細かくフォルダを分ける。

また、ShibaTemplateの内容も、ShibaTemplateフォルダ内にまとめる。

Assetsフォルダ内のフォルダ構成は以下の通り。

- HogeProject : プロジェクト固有のアセットを全て入れる。
- ShibaTemplate : ShibaTemplateのアセットを全て入れる。
- Plugins : ZenjectやUniRxはこの中にインポートされる。
- サードパーティのアセットごとのフォルダ

Plugins内のアセットは、他のアセットとは別にコンパイルされるが、Plugins外のアセットを参照することが出来ない。
変更の少ないソースコードはここに入れるとコンパイルが速くなるが、慣れないうちはそこまで積極的に利用しなくても良い。

ShibaTemplateは、Pluginsに入れる代わりにアセンブリ分割(asmdefファイルの配置)を行うことである程度高速化している。

## HogeProjectフォルダ内

### HogeProjectフォルダ直下

プロジェクト内のフォルダ構成は基本的に以下の通りとする。

フォルダ内は更に細かく分けても良い。
[命名規則](./naming_convention.md)も参照のこと。

- Textures : 画像ファイルを入れる。
- Audio : 音声ファイルを入れる。
- Materials : マテリアルファイルを入れる。
- Shaders : シェーダファイルを入れる。
- Prefabs : プレハブを入れる。
- Models : ScriptableObjectとして生成したデータを入れる。
- Scenes : シーンファイルを入れる。
- Scripts : スクリプトファイルを入れる。
- Editor : エディタ拡張を入れる。

### HogeProject/Scriptsフォルダ内

多くの場合、あるシーンでのみ使用するスクリプトがかなり多くなるので、シーンごとにフォルダを作ると良い。

フォルダ名はシーン名をそのまま使用する。例として、TitleSceneフォルダなど。

### HogeProject/Scripts/XxxSceneフォルダ内

ここでは典型的なシーン固有スクリプトの分類を記す。

- SceneControllerフォルダ。SceneManagerとSceneEventsを入れる。

## ShibaTemplateフォルダ内

### ShibaTemplateフォルダ直下

ShibaTemplateフォルダ直下は以下のような構成とする。

- Moderator : 各モジュールから共通して利用されるスクリプトを入れる。詳細はModeratorを参照。
- Utils : 各モジュールから共通して利用される属性などを入れる。
- Modules : モジュール（部品）。アプリの共通部分としてそのまま使用することを想定した部品たち。
- Wrappers : サードパーティのアセットをShibaTemplateと連携させるためのラッパー。アセットごとにフォルダを作る。
- Samples : Moderatorを利用したコンポーネントの例。そのまま使用するというより、用途に合うよう改変して使用する。 

### Modulesフォルダ内

アプリの共通部分としてそのまま使用することを想定した部品たちが入っている。

名前空間はShibaTempalte.(モジュール名)である。

#### GameController

[イベントシステム](event_system.md)及びシーン遷移関連のモジュール。

かなりよく使う。

シーンイベントのストリームを発行し、またシーン遷移の判定を行う「SceneManagerBase\<T\> where T : Enum」が中心となる。
実際のアプリでは、Enumとしてシーン固有のSceneEventsを定義し、SceneManagerBaseを派生させたシーン固有のSceneManagerを使用する。

### Wrappersについて

ラッパーは、対象のサードパーティアセットが無い状態でスクリプトだけがあるとエラーとなる場合がある。

そこで、unitypackageとして切り出しておいて、必要に応じてImport packageを用いてインポートする。



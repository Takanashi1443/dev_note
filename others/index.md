# その他

## Unityの小技

### 外付けHHD・SSDにAsset Storeのデータを保存

Windowsのジャンクションという仕組みを利用する。

アセットストアからダウンロードしたファイルは

C:\\Users\\(accountName)\\AppData\\Roaming\\Unity\\Asset Store-5.x

以下にダウンロードされる。

これに対して、ジャンクションという仕組みは、あるパスを参照した時に別のパスを参照するコマンドである。
Asset Store-5.xの中身を保存先にコピーし、

mklink /j "Asset Store-5.x" (D:\\(保存先))

とする。

作成したジャンクションはコマンドプロンプトを開き「dir」でディレクトリ確認すると

\<JUNCTION\>     Asset Store-5.x [(保存先)]

などと表示されるので確認できる。

ドライブ構成が変わると参照できなくなるので注意。
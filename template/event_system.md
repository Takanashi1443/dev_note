# イベントシステム

## イベントシステムとは

例えばアクションゲームで、プレイヤーが倒れた時、特定ポイントを通過した時など、
特定のタイミングで複数のものに影響を与えたい場合がある。
これは、例えば、ゲームマネージャがプレイヤーの状態、全てのポイントの状態を把握し、その状態の変化に応じて
影響を与えるもの全てに対して処理を行うという方法でも実装できるが、
影響を与える対象が増えるたびにゲームマネージャを書き換えなければならず、不便である。
そこで、「イベント」という仕組みを使う。

GameObjectは、ゲームマネージャに管理されていなくても「イベント」を発行することができ、
「イベント」が発行されると、それに反応するGameObjectたちが勝手に反応する。

## イベントシステムの基本的な実装

イベントシステムには、

- イベントマネージャ (Event Manager)
- イベントリスナ (Event Listener)
- イベントコーラー (Event Caller)

の3種類のコンポーネントが存在する。

イベントは、UniRxのIObservableを使って実装する。
詳細は省略するが、イベントの発行がIobservableのOnNext関数、反応がSubscribe関数に対応する。

イベントマネージャは、IObservableの実体を保持する。
イベントリスナは、イベントマネージャへの参照をDIにより取得し、イベントマネージャ経由で取得したIObservableの実体にSubscribeを行う。
イベントコーラーは、イベントマネージャへの参照をDIにより取得し、イベントマネージャ経由で取得したIObservableの実体にOnNextを行う。

## イベントの種類

### シーンごとのイベント

シーンごとのイベントは、イベントの種類を列挙した専用の列挙体および、
その列挙体を取り扱う専用のReactivePropertyを定義する。
例えば、あるシーン（シーン名：Stage）に、
- READY
- DEATH
- CLEAR
の3つのイベントを用意するとする。
（ここで、READYはシーンのトランジションが終わったことを表すイベントで、基本的にどのシーンにも用意する）
この時、
Assets/(Project Name)/Scripts/StageSceneフォルダ内に、
SceneEvents.csスクリプトを作り、以下のように記述する。

'''
namespace (Project Name).StageScene
{
    /// <summary>
    /// イベントの列挙。
    /// </summary>
    public enum SceneEvents
    {
        READY,
        DEATH,
        CLEAR,
    }

    /// <summary>
    /// シーンイベントに対するReactiveProperty
    /// </summary>
    [System.Serializable]
    public class SceneEventReactiveProperty : ReactiveProperty<SceneEvents>
    {
        public SceneEventReactiveProperty (){}
        public SceneEventReactiveProperty (SceneEvents initialValue) : base (initialValue) {}
    }
}

'''

シーンマネージャはイベント発行用にSceneEventReactivePropertyを持ち、
外部に対してIObservable<SceneEvents>として公開する。
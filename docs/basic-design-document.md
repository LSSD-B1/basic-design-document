<div style="text-align: center;">
基本設計仕様書
</div>


<div style="page-break-before:always"></div>

# 目次
1. 概要及び目的
2. システムアーキテクチャ
3. 機能要件
4. 非機能要件
5. データモデル
6. ユーザーインターフェース設計
7. プロトコルとインターフェース

<div style="page-break-before:always"></div>

# 1. 概要及び目的
## 1.1. ソリューションの目的
本ソリューションは，定年後の人々が生活の質（QOL）を維持しながら活動的な生活を送ることができる社会の実現を目指す．
高齢者のQOLが低下する要因の一つに，外出機会の減少がある．
本ソリューションは，この問題に対処するために，高齢者が外出のきっかけを持てるようにすることを目的とする．

具体的には，このシステムはAI冷蔵庫とキャラクター育成ゲームを組み合わせる．AI冷蔵庫で庫内の食材を把握と今日のおすすめレシピの提案を行う．レシピに足りない食材を歩いてスーパーに買いに行って料理を完了することでキャラクターを育成できるようにする．これが高齢者が外出するきっかけとなり，QOL向上の一助になることを期待する．

また，提案するレシピを健康に考慮したものにすることで，高齢者の体調維持につながり，それもQOL向上につながる．

## 1.2. 試作品の概要
本システムの試作品は，冷蔵庫の中の食材情報を活用するディスプレイ表示とする．
冷蔵庫内の食材の画像認識はすでにある[（パナソニック "Live Pantry"）](https://panasonic.jp/reizo/function/camera.html)ので優先順位は低く，ここから得られる情報の見せ方に焦点を当てる．

冷蔵庫のディスプレイではおすすめする料理の画像と必要な食材，料理のカロリー，足りない食材，累計歩数を表示し，特定の時間になったときに外出を促す．
試作品では，歩数は別機器で測定されたものをディスプレイに入力することとする．
料理分のカロリーを消費できると，レシピが表示されるようにする．
冷蔵庫は常に不足する食材を提示できるように，プラスα食材を用意している．

キャラクター育成では，ディスプレイに常にキャラクターを表示し，キャラクターからの指示によってストーリーが進むようにする．歩数などの入力によってキャラクターの健康状態や形態が変化させることでキャラクターを自身の行動により育成できるようにする．

# 2. システムアーキテクチャ
![システムアーキテクチャ](../img/system_architecture.drawio.png)

# 3. 機能要件
## 3.1. ディスプレイ
- 各種データを表示する
## 3.2. データ表示機能
- レシピ画像，使用食材，不足食材，歩数入力箇所を表示する
## 3.3. データ保存機能
- レシピ画像，使用食材，庫内食材，レシピカロリー，累計歩数を保存する
## 3.4. 歩数入力機能
- 入力された歩数を累計歩数に合算して保存する
## 3.5. 歩数表示機能
- 高血圧対策で運動を意識させるために累計歩数を表示する
## 3.6. メッセージ機能
- 一日のある一定時刻にユーザーが外出しなければならなくなるようなメッセージを表示する
- 次にユーザーがすべき行動についてのメッセージを画面に常に表示しておく
- メッセージ詳細
  - 今日のレシピ：
  ○○に含まれる○○は血圧を抑える作用があります．
  - 外出催促：
  今日は○○スーパーの○○がお得です．また，適度な運動は血圧を下げる効果があります．
  - 料理レシピ解除：
  今日は○○歩歩きましたね．お疲れ様でした．レシピを解除しました．
## 3.7. キャラ育成機能
- キャラクターが3段階の成長をする
- 成長時にメッセージを出力する
## 3.8. キャラ状態機能
- 歩数増加，食材調達，料理完成時にキャラクターの健康状態を1段階上げる
- 1日が経つごとにキャラクターの健康状態を1段階下げる

# 4. 非機能要件
## 4.1. ディスプレイ
- 誰でも迷うことなく操作できるシンプルなデザイン
- 高齢者が視認しやすいよう，文字サイズは大きめ
## 3.2. データ表示機能
- なし
## 3.3. データ保存機能
- json形式で保存する
## 3.4. 歩数入力機能
- タッチパネルではなくキーボードから入力する
## 3.5. カロリー計算機能
- なし

# 5. データモデル
![DataBase](../img/DataModel_DB.png)
![Directory](../img/DataModel_Directory.png)

# 6. ユーザーインターフェース設計
![ユーザーインターフェース設計1](../img/ui_1.png)
![ユーザーインターフェース設計2](../img/ui_2.png)
![ユーザーインターフェース設計3](../img/ui_3.png)

# 7. プロトコルとインターフェース
## 7.1. エッジコンピュータ　－　カメラ
- データ形式：　画像
- プロトコル：　ONVIF
- インターフェース：　USB3.0

## 7.2. サーバー（エッジコンピュータ）　－　ディスプレイ
- データ形式：　映像と音声
- プロトコル：　DRM
- インターフェース：　HDMI

## 7.3. サーバー　－　データベース
- データ形式：　JSON
- プロトコル：　HTTP
- インターフェース：　REST API

## 7.4. サーバー（エッジコンピュータ）　－　Map
- データ形式：　JSON
- プロトコル：　HTTPS
- インターフェース：　REST API

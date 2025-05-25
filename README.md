# じょぎハッカソン２０２５０５
## 概要
**アプリ名「コンフリクトバトル」**
> どちらのコミットが修正されるのか、対戦相手と競い合います

**推しアイデア**
- web socketを使って、スマホをコントローラー,パソコンをゲーム画面にする

**作った背景**
- 技術縛り(line・flutter・unity・reactをすべて使う)を達成しつつ、コンフリクトが起こる過程をゲームで表しました。
**推し技術**
- web socketでflutterとnext.jsを繋いで遊ぶ
- 画像認識で首の角度でunityを動かす


### りぽじとり
- [Line](https://github.com/NazonoKansatugata/greedme_line)
- [Flutter](https://github.com/NazonoKansatugata/greedme_flutter)
  - [web socket](https://github.com/NazonoKansatugata/greendme-WebSocket)
- [Unity](https://github.com/Yanai1005/greendme-unity)
- [React](https://github.com/Yanai1005/greendme-react)

### 技術縛り
「Line messaging API」「Flutter 」「Unity」「React」を1画面ずつ使うこと

### 使用技術・担当技術
**起(kuroko)**  
- Line Messaging API
  - GAS

**承(kuroko)**  
- Flutter  
- Node.js
  - web socket
  - render
  - url luncher
- next.js
  - vercel


**転(yanai)**
- Unity
- TensorFlow
- photon （実装間に合うか否か）

**結(yanai)**
- React
- WebRTC  

**共通(kuroko)**  
- firebase


### アーキテクチャ図

![image](https://ptera-publish.topaz.dev/project/01JW1V4QJKA8RM8GKPQK50F4P5.png)

![image](https://ptera-publish.topaz.dev/project/01JW1V4TDYGAZ7E3B4VCT05ZGT.png)

![image](https://ptera-publish.topaz.dev/project/01JW2KSZRHCQXWQAWYNZXT7MDS.png)

![image](https://ptera-publish.topaz.dev/project/01JW2KAXGV9J7K9BYBQ8XDDAPB.png)
### 各デプロイ先
- [Line](https://lin.ee/cGzNKOc)
- [Flutter](https://greendme-8e44c.web.app/)
- [Unity](https://unity-greendme.web.app/)
- [React](https://greendme-react.web.app/)

### 機能詳細
#### 起 (line messaging API)
大まかな説明
1. ユーザー登録:lineからuserIDを取得後、名前,合言葉を設定し、firebaseに保存する。
2. ユーザー削除:結(react)から遷移した際にfirebase上のユーザー情報を削除すると同時にメッセージを送信する  
3. 承に遷移:QRコードによりユーザーを遷移させた後、スマホはコントローラー画面に遷移する
細かな説明
  - GASをwebhookとしたline messaging APIを作成
  - GASをfirestoreと連携し、lineのuserIDをドキュメントIDとして利用したDBを作成
   - リッチメニューとQRコードを用いたパソコン遷移を設計

#### 承(flutter)

大まかな説明
1. コントローラー検知:firestore内のuserIDをパソコンとスマホそれぞれから選択し、websocketにてコントローラとゲーム画面を認証する  
2. スマホで操作:スマートフォンからボタンや加速度といった入力をパソコン画面に反映させる 
3. 複数のゲーム:スマホの各種検知機能を用いたランダムなミニゲームを行う
- ミニゲーム一覧
  - テトリス
  - ぷよぷよ
  - シューティング
  - フラッピーバード

細かな説明
   - キーボードで遊べる仮ゲームを4つ開発
   - firestore内のuserIDを用いたユーザー認証
   - scoreをfirestore内に保存
   - websocketを用いて外部からの信号を受け入れる準備
   - Node.jsとwebsocketを用いたサーバーを作成。renderデプロイ
   - Next.jsでスマホ用コントローラー画面を作成。vercelデプロイ
   -ゲームのwebsocket対応と一部修正
4. 転へのリダイレクト:firestore内にスコアを転送

#### 転
大まかな説明
1.迷路を自動生成
2.WASD移動or体の傾きで移動
細かな説明
- 深さ優先探索のアルゴリズムで迷路作成
- TensorFlowで体の傾きで操作
- React内でUnityを表示

(Photonの進捗)
> 終わって欲しいな
→ Unityでバックするだけでもコンパイル走ってWebGLでBuild&Runで実行とUnityエディター上でのデバックつらい

![image](https://ptera-publish.topaz.dev/project/01JW2J76J7MBR8N6WZ8931ZJB7.png)

>  追記：正午ごろ：やったね！なんか動いた(おかしいな....)
    
#### 結
大まかな説明
- WebRTCでオンラインタイピングゲーム
- 同じWifiのみ使用可能

細かな説明
- 同じWi-Fiしか繋げられない理由は、Googleの無料のSTANサーバーしか準備しておらず、違うIPアドレス（WI-Fi）の場合、 NAT超えなどするのに  TURNサーバーの準備が必要だが準備が手間なので省きました。
→同じwifi上ではWebRTCを使ってすることができます。             

### でも動画

 [[承]:flutter](https://youtube.com/shorts/AwOaKH0Pkq0?feature=share)

 旧：[[転]:unity](https://youtube.com/shorts/5rNlA_O7DQ8?feature=share)

新：[[転]:unity]()

[[結]:react](https://youtu.be/oOyV7_qLacE)

### タスク管理
1日00:00付近にGITHUB_ISSUE_TEMPLATEを建てて、作業スレを立てて進捗を確認
![image](https://ptera-publish.topaz.dev/project/01JW2GSCCTKVB43JRV14EY2MDW.png)
[YAML](https://github.com/Yanai1005/greendme-jyogihack/blob/main/.github/workflows/daily-work-thread.yml)
お互いの進捗を確認
![image](https://ptera-publish.topaz.dev/project/01JW2GW2R5DZENQEQW40FYQ6SC.png)

リポジトリが多かったので、ちょっと管理しやすくしてました
https://github.com/Yanai1005/greendme-jyogihack

### ストーリー
- [Line] リポジトリを作る
- [Flutter]コードを書いてコミットする
- [Unity]conflictが起きたので言い争い
- [React]やっと直せたがforse pushされてしまう

### スケジュール
5/10 アイディアソン   
↓ この間は事前開発期間   
5/24,25 ハッカソン   

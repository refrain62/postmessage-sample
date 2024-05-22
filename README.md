# postMessageを使って、ブラウザ上でオリジン間のデータ共有を実施 の写経

## postmessage-sample
PostMessageによる、異なるオリジン間での通信のサンプルです。
https://github.com/k-ibaraki/postmessage-sample

こちらの記事で書いたものです。
https://zenn.dev/ncdc/articles/49098d7d16f8ee

## 使い方

1. http-serverを立ち上げてください
```
npx http-server
```

2. ブラウザから、`http://127.0.0.1:8080/src.html`に接続してください。
3. 適当にテキストを入力して、`別タブで開く`を押下。
4. 入力したテキストが、開いた別タブに連携されます。

## 処理の流れ
Mermaid Graphical Editor で書きました。
```mermaid
sequenceDiagram
  actor line_1 as new_lifeline
  participant line_2 as 元の画面<br>（127.0.0.1:8080/src.html）
  participant line_3 as ポップアップした画面<br>（localhost:8080/popup.html）
  line_1 ->> line_2: message
  line_1 ->> line_2: ボタン or リンクを押下
  line_2 ->> line_3: 別タブで開く
  Note right of line_1: 画面が確実に開いてから<br>データを送信するために、<br>元画面はポップアップ画面からの<br>通知を受け取った後に<br>データを送信する
  line_3 ->> line_2: 画面が開いたことを通知
  line_2 ->> line_2: 通知の受取処理
  line_2 ->> line_3: データを送信
  line_3 ->> line_3: データ受取処理
```

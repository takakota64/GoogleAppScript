# Google Apps Scriptを使った一括自動メール送信・下書き作成の実行方法

このガイドでは、既に完成しているスプレッドシートを使用して、Google Apps Scriptを実行し、一括送信・メールの下書きを自動的に作成する手順を説明します。よしあきさんでも理解できるように、ステップごとに詳しく説明します。

## 前提条件
- Googleアカウントを持っていること。
- シート名は既存であること。
- 必要なデータが正しい列に入力されていること。


## スクリプトの概要
提供されたGoogle Apps Scriptは、以下の処理を行います：

1. **スプレッドシートからデータを取得**：既存シートから必要なデータを読み込みます。
2. **データの検証とフィルタリング**：
   - チェックボックスが未チェックの行のみを対象とします。
   - 有効なメールアドレスを持つ行のみを対象とします。
3. **一括送信orメールの下書きを作成**：対象となる各行に対して一括送信、Gmailにメールの下書きを作成します。

## 手順

### 1. スプレッドシートを開く
- Google Sheetsにアクセス：
- Google Sheetsにアクセスし、スプレッドシートを開きます。
- 送信したくない会社にチェック

### 2. Apps Scriptエディタを開く
- スプレッドシートのメニューから拡張機能をクリックします。
- ドロップダウンメニューから**Apps Script**を選択します。
- 新しいタブでApps Scriptエディタが開きます。

### 3. スクリプトを貼り付ける
- 既存のコードを削除：エディタに既存のコード全て削除します。
- GITHUBから送信したいコードをコピー(案件or要員)
- body内の本文を送信したい内容に編集する。
- コードをエディタに貼り付け：エディタに編集したコードを貼り付けます。

-----------------------------------
## 編集について
- var body =
`${company}
- ${name} 様
- ここから下が本文
-
- お世話になります。
- アワーズシップ株式会社です。
- 以上、よろしくお願いいたします。
-
-
- ここまで`;

- シングルクォーテーション(shit+＠)で本文が囲まれてないとエラーになり読み取られない
- ${company} や ${name} はスプレッドシートからデータを参照するためのものなので、編集しないでください。
- ${} の表記はテンプレートリテラル内で変数を埋め込むために使用します。


## 一括送信するか下書きを作成するか
- 本文の編集が完了したら次に本文の下にあるコードを送信するか下書きを作成するか指定します
- GmailApp.sendEmail(address, subject, body);　メールを一括送信
- GmailApp.createDraft(address, subject, body);　下書きを作成
- 上記のどちらか一方を使用し、不要な方はコメントアウト（//を行の先頭に追加）してください。




------------------------------------




### 4. スクリプトの保存
- **スクリプトを保存**：エディタの上部にあるフロッピーディスクアイコン（💾）をクリックするか、Ctrl + S（Windows）またはCommand + S（Mac）を押して保存します。

### 5. スクリプトの権限を承認(初回のみ)
- 再生ボタン（▶️）をクリックして、スクリプトを実行します。
- 権限の確認が必要になる場合、指示に従って権限を付与してください。
- **権限の確認**：

* 「このアプリは確認されていません」というメッセージが表示される場合があります。
* 詳細をクリックします。
* メール下書き自動作成（安全ではないページ）に移動をクリックします。
* 内容を確認して「許可」を選ぶ﻿



### 6. スクリプトを実行
- 再生ボタン（▶️）をクリックして、スクリプトを実行します。
- 実行ログタブで状況を確認します。

### 7. gmailにて送信履歴・メールの下書きを確認
- Gmailにアクセスし、作成・送信されたメールを確認します。

## 注意事項
- **スプレッドシートのデータ確認**：シート名がスクリプト内で指定された"既存"と一致していることを確認してください。
- **メールアドレスの形式**：無効なメールアドレスがある場合、その行はスキップされます。
- **チェックボックスの状態**：A列のチェックボックスが未チェックの行のみが対象となります。
- **コード内の計算について**Javascriptでは0からカウントが始まる為5行目を参照したい場合コードへの表記は6にになります。(0.1.2.2.4.5)
- **コメントアウトについて**エディタ内で//で始まっているコードorコメントは実行されません。
- ***要注意：一括送信か下書き作成かの確認***GmailApp.sendEmail(address, subject, body);かGmailApp.createDraft(address, subject, body);をしっかり確認

## トラブルシューティング
- **下書きが作成されない場合**：スプレッドシートのデータが正しく入力されているか確認してください。
- **スクリプトエラーが発生する場合**：エディタの実行ログでエラーメッセージを確認し、問題を特定します。
- **権限に関する問題**：スクリプトの実行時に適切な権限が与えられているか確認します。
- **よくありそうな問題** :編集時に本文を``で囲えているか確認してください。

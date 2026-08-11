# SHUT UP SQUAT!!! — 公開手順

SQUAT MANIA プログラム用トレーニングログのPWAです。
GitHub Pages に置くと、iPhone のホーム画面に本物のアプリとしてインストールできます。

## ファイル構成

```
index.html                     アプリ本体
manifest.webmanifest           アプリ名・アイコンの定義
sw.js                          オフライン動作用
icons/icon-192.png             ホーム画面アイコン
icons/icon-512.png             ストア・スプラッシュ用
icons/icon-maskable-512.png    Android の丸型マスク用
icons/apple-touch-icon.png     iPhone のホーム画面用
icons/favicon-32.png           ブラウザのタブ用
icons/favicon-16.png           ブラウザのタブ用
```

## 手順（スマホでもPCでもOK・約5分）

1. **GitHub にログイン** → 右上「+」→ **New repository**
2. Repository name に `squat` などを入力
3. **Public** を選択（Private だと GitHub Pages が使えません）
4. **Create repository**
5. 「uploading an existing file」をタップ
6. **このフォルダの中身をすべてドラッグ＆ドロップ**
   - `icons` フォルダごと入れれば中のファイルも一緒に上がります
   - フォルダごと入らない場合は、先に `index.html` などを上げ、次に「Add file → Create new file」でファイル名に `icons/icon-192.png` のようにスラッシュを入れると階層が作れます
7. 下の **Commit changes** を押す
8. リポジトリの **Settings** → 左メニュー **Pages**
9. Source を **Deploy from a branch**、Branch を **main / (root)** にして **Save**
10. 1〜2分待つと `https://ユーザー名.github.io/squat/` が発行されます

## iPhone にインストール

1. **Safari** で上記URLを開く（Chromeだと追加できません）
2. 下の共有ボタン → **ホーム画面に追加**
3. 名前欄で `SHUT UP SQUAT!!!` を確認（好きな名前に変更可）→ **追加**

これでアイコンから全画面で起動し、圏外でも動きます。

## Android にインストール

Chrome で開く → メニュー → **アプリをインストール**

## アプリを更新するとき

1. 新しい `index.html` を同じ場所にアップロード（上書き）
2. **`sw.js` の1行目付近の `sus-v1` を `sus-v2` に変更**してアップロード

この2つをやると、次に開いたとき全端末に自動で配られます。
`sw.js` の数字を上げ忘れると古い画面のままになるので注意してください。

## 名前やアイコンを変えたいとき

- ホーム画面の名前 → `manifest.webmanifest` の `short_name`
- アイコン → `icons/` の画像を同じファイル名で差し替え

## Firebase について

同期設定（config・名前）は端末のブラウザ内に保存されるので、リポジトリを公開しても
トレーニング記録や設定が他人に見られることはありません。

ただし Firebase の Realtime Database を「テストモード」のままにしていると
30日で期限切れになります。コンソールの「ルール」を下記に変更しておいてください。

```json
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

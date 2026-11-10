# Muse 使用量ウィジェット（Android / KWGT）

Muse の週間使用量（％）とリセット日時を、Android のホーム画面ウィジェットに表示するための仕組みです。

- `usage.json` を Muse（みみ）が15分ごとに自動更新（git push）します。
- スマホ側は KWGT（Kustom Widget Maker）でこの JSON を読み込んで表示します。

データの URL（raw）:
`https://raw.githubusercontent.com/mi7780606/muse-usage/main/usage.json`

## KWGT での作り方

1. Play ストアから **KWGT Kustom Widget Maker** をインストールします。
2. ホーム画面の空きスペースを長押し →「ウィジェット」→ KWGT のウィジェット（例：4x2）を配置します。
3. 配置したウィジェットをタップすると KWGT の編集画面が開きます。
4. 「アイテム」タブ右下の ＋ →「テキスト」を追加し、テキスト欄に下の式を入れます（タップして数式モードで編集）。
   - 使用率（大きく表示するのがおすすめ）:
     `$wg("https://raw.githubusercontent.com/mi7780606/muse-usage/main/usage.json", json, .used_percent)$%`
   - リセット日時:
     `リセット $wg("https://raw.githubusercontent.com/mi7780606/muse-usage/main/usage.json", json, .reset_text)$`
   - 最終更新:
     `更新 $wg("https://raw.githubusercontent.com/mi7780606/muse-usage/main/usage.json", json, .updated_text)$`
5. 進捗バーで使用率を見せたい場合は「プログレスバー」を追加し、「プログレス」欄の式に
   `$wg("https://raw.githubusercontent.com/mi7780606/muse-usage/main/usage.json", json, .used_percent)$`
   を入れ、最大値を 100 にします。
6. 右上の保存アイコンで保存して、ホーム画面に戻ります。
7. KWGT の設定で「ウィジェットの更新間隔」を短め（例：15分〜30分）にすると、表示が新しく保たれます。

## 注意

- このリポジトリは公開設定です。置いてあるのは使用率（％）とリセット日時だけで、個人情報や会話内容は含まれません。
- 週間制限のリセットは毎週土曜 23:35（JST）です。

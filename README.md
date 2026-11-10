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
5. 進捗バーで使用率を見せたい場合は「プログレス」アイテムを追加し、次の順で設定します（「式を入れる欄」は最初は出ていません）。
   1. プログレスの設定で「モード」（種類）を **カスタム** に変える（初期状態ではバッテリー等の固定項目しか選べません）
   2. すると「レベル」という項目が現れるので、その右側のチェックボックスを ON にする
   3. 画面上部に現れる **電卓アイコン** をタップする（数式モードへの切り替え）
   4. 「レベル」をタップすると数式入力画面が開くので、この式を入れる:
      `$wg("https://raw.githubusercontent.com/mi7780606/muse-usage/main/usage.json", json, .used_percent)$`
   5. 最小（Min）を 0、最大（Max）を 100 にする
6. 右上の保存アイコンで保存して、ホーム画面に戻ります。
7. KWGT の設定で「ウィジェットの更新間隔」を短め（例：15分〜30分）にすると、表示が新しく保たれます。

## 注意

- このリポジトリは公開設定です。置いてあるのは使用率（％）とリセット日時だけで、個人情報や会話内容は含まれません。
- 週間制限のリセットは毎週土曜 23:35（JST）です。

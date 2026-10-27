# BlueCave 2.0

「好奇心が形になる場所。」をコンセプトにした、HTML・CSSの静的サイトです。
ビルドや外部ライブラリ、外部フォントは不要です。

## ファイル構成

| ファイル | 用途 |
| --- | --- |
| `index.html` | HOME：紹介、作品の抜粋、JOURNALへの導線 |
| `works.html` | WORKS：作品一覧 |
| `journal.html` | JOURNAL：制作や日々の記録 |
| `assets/css/bluecave-v2.css` | 上記3ページの共通スタイル |
| `images/` | 写真の保管先。既存画像は保持 |
| `style.css` | 既存ページ用のスタイル。新しい3ページでは使用しません |

`about.html`、`garden.html`、`ocean.html`、`mokuyoubi_waiting_game.html`は従来のパスで保持しています。
新しい3ページのナビゲーションはHOME / WORKS / JOURNALです。

## ローカルで確認する

`index.html`をブラウザで開くと確認できます。スマートフォンの表示はブラウザの開発者ツールで幅を変更して確認します。
サーバーやパッケージのインストールは不要です。

## 作品を追加する

1. `works.html`の`<article class="work" ...>`から`</article>`までを複製します。
2. `id`を重複しない半角英数字とハイフンの名前に変更します（例：`pico-clock`）。
3. カテゴリ・作品名・説明文・写真枠の`aria-label`を変更します。
4. HOMEにも掲載する場合は、`index.html`の`article.work-preview`を複製または差し替え、リンク先を`works.html#pico-clock`のようにします。

作品の並び順はHTMLの記述順です。HOMEの抜粋とWORKSは手動で更新します。
実際の仕様や制作日が未確認のため、現在の説明は既存の作品名と使用ボードに基づく短い紹介に留めています。

## 写真を差し替える

写真を`images/`に追加し、該当する`div.placeholder`全体を以下の`img`に置き換えます。
既存の写真は削除せず、新しいファイル名を付けて追加してください。

```html
<img class="project-image"
     src="images/pico-clock.jpg"
     alt="制作した時計の正面。電子ペーパーに時刻を表示している"
     width="1200" height="800" loading="lazy" decoding="async">
```

- `width`・`height`は元画像の実寸に合わせます。作品枠は3:2、中央でトリミングされます。
- HOMEの大きな写真では`class="hero-image"`を使い、最初に見える写真なので`loading="lazy"`は付けません。
- `alt`は写真の内容を簡潔に説明します。リンク内で作品名と完全に重複する装飾画像は`alt=""`でも構いません。
- スマートフォンでの読み込みを考慮し、写真は適切な大きさに縮小・圧縮してください。
- HOMEとWORKSの両方にある写真は、それぞれのHTMLを更新してください。

## JOURNALに記事を追加する

1. `journal.html`の`journal-list`内にあるコメント付きの`article.journal-entry`見本をコピーし、コメントの外に置きます。
2. 固有の`id`、公開日、カテゴリ、タイトル、本文を実際の内容に変更します。
3. `time`の`datetime`は`YYYY-MM-DD`形式、表示日は`YYYY.MM.DD`形式にします。
4. 初回の記事追加時は`div.empty-state`全体を取り除き、HOMEの「最初の記録を、ただいま準備しています。」も更新します。

新しい記事を先頭に置くと新着順になります。記事の段落は`p`要素を追加してください。
この段階では記事本文もJOURNALページ内に記載するため、記事ごとのHTMLファイルは不要です。
記事への直接リンクには`journal.html#記事のid`を使えます。

## デザインと共通部分の変更

- 色と最大幅は`assets/css/bluecave-v2.css`冒頭のCSS変数で変更できます。
- 640px以下では作品を1列に表示します。
- ヘッダー・フッターは各HTMLにあります。変更時は3ページを揃えてください。
- 現在のページを示す`aria-current="page"`は、そのページのナビ項目だけに付けます。
- 新しいCSSは既存ページから読み込まないでください。従来の表示は`style.css`が担当します。

## 公開と作業ブランチ

GitHub Pagesの既存URL・公開設定を維持する構成です。ファイル名と相対リンクを使用し、ビルド設定や公開先の変更はありません。
作業ブランチは`bluecave-v2`です。`main`への反映、コミット、Push、公開操作は別途指示を受けて実施してください。

# ココフォリア OBS用CSS（個人用調整版）

元CSS: [yudukiak/ccfoliaCSS](https://github.com/yudukiak/ccfoliaCSS)
元配布: https://yudukiak.github.io/ccfoliaCSS/CSS/board.css

元作者のCSSと、利用者から提供されたCCFOLIA 1.36.4のHTMLを参考に再構成した個人用調整版です。元CSSの自作を主張するものではありません。利用者より「改変自由」と案内されている旨の申告あり。独自のライセンス付与はしていません。元の利用条件を引き継いで扱ってください。

## ファイル

| ファイル | 表示対象 |
|---|---|
| board.css | 前景・スクリーンパネル・マーカーパネル（背景は含まない） |
| background.css | 背景のみ |
| foreground.css | 前景のみ |
| characters.css | 盤面のキャラのみ |
| markers.css | マーカーパネルのみ |
| screens.css | スクリーンパネルのみ |
| base.css | 共通設定・対象要素の指定（単独使用しない） |

各表示用CSSは同じフォルダのbase.cssを読み込みます。元配布サイトへのCSS依存はありません。
キャラのみは、発言時の立ち絵ではなく、今回確認した盤面のキャラ画像を対象にします。

## GitHubに置く

1. 自分のGitHubにリポジトリを用意します（例: ccfolia-obs-css）。
2. このフォルダの中身をリポジトリのルートにアップロードします。ZIPそのものではなく展開したファイルを置きます。
3. Settings → Pages → Build and deployment → Sourceで「Deploy from a branch」を選びます。
4. ファイルを置いたブランチ（例: main）と「/(root)」を選んでSaveします。
5. 公開完了後、PagesのURLに /characters.css などを付け、CSSが表示されることを確認します。

公式手順: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
GitHub Pagesの通常公開ではCSSは外部から閲覧できます。この一式にルームURL・チャット・画像URLは含めていません。
GitHubへのアップロード・公開はまだ実行していません。

## OBSで使う

ブラウザソースのURLは今までどおりココフォリアのルームURLにします。
カスタムCSS欄の既存内容を削除し、次の1行だけを設定します。

```css
@import url("https://YOUR-NAME.github.io/ccfolia-obs-css/characters.css");
```

YOUR-NAMEとリポジトリ名を自分のものに置き換えます。ファイル名は用途に応じて変更してください。
1つのソースで読み込む表示用CSSは1つにします。複数読み込むと表示対象が混ざります。
全ソースでブラウザの幅・高さと盤面の位置・倍率をそろえると重ね合わせやすくなります。

表示用ファイルの中身をそのままOBSへ貼ると相対パスのbase.cssを正しく読めません。
GitHub公開後の絶対URLで読み込んでください。公開前に直貼りで試す場合は、base.css全文のあとに表示用CSSの :root ブロックだけを追加します。

## 更新時

- 背景・スクパネ・マカパネのクラス名はbase.cssだけに集約しています。
- キャラはfigure構造、前景はtransformのstyle属性と親子構造に依存します。
- 更新後に表示されなくなった場合、Elementsで対象を選んでbase.cssの該当指定を更新します。
- .sc-fkmgoAは今回のHTMLで複数種類の盤面オブジェクトに共通なので、パネル単独の指定には使いません。
- 自分のGitHubで管理してもココフォリア側のHTML変更への自動追従はしません。
- 反映されない場合はGitHub Pagesの公開完了と、ブラウザソースのキャッシュ更新・再読み込みを確認します。入口URLだけ変えても、共通CSSのキャッシュが残る場合があります。

## 動作確認の範囲

提供HTML上のセレクタ一致を確認しました。元のキャラ・マーカーパネル抽出方法は会話中に利用者が動作確認済みです。
今回まとめた一式（特に背景・前景単独）は実際のOBSで未確認です。OBSで各ファイルの表示対象、透過、位置、前景切替中の表示を確認してください。
visibilityで隠すため、盤面の配置を保てますが、非表示要素の通信・音声・アニメーション処理は停止しません。複数ソースの音声はOBS側で調整してください。
元CSSにあった各種UIのdisplay:noneは、全体のvisibility非表示に置き換えています。隠れたUIの配置領域は残る場合があります。

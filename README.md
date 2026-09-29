# ヘルスログ：GitHub Pages用の説明サイト

このフォルダーには、公開してよいアプリ紹介とプライバシーポリシーだけを入れています。
Apps Script本体、健康の実測値、台帳URL/ID、アカウントID、メールアドレス、認証情報は含めていません。
サイトはHTML/CSSのみで動作します。npmや有料サーバー、独自ドメイン、ログイン機能は不要です。

## 公開前の確認

- プライバシーポリシーを読み、実際の運用と合っていることを確認してください。
- アプリ表示名は「ヘルスログ」、識別用の表記は「health-log」です。OAuthのブランディングでも実際の名称を一致させてください。
- 連絡先はOAuth同意画面のユーザーサポートメールを参照する文章にしています。個人のメールはサイトに掲載していません。サポートメールはGoogle Cloud側で設定してください。
- 記録台帳とApps Scriptは、本人のみが編集できる設定で運用してください。スクリプトプロパティは他の編集者から秘密を隠すための仕組みではありません。
- 外部AI分析を行う場合は、Google API由来データが一般目的のモデル学習に使われない設定・条件を確認してください。このサイトは、ChatGPTやGoogleのアカウント設定を変更しません。
- GitHubにアップロードするのは今回の説明サイト一式だけです。以前のhealth-log-v1.zip、v2.zipや実行ログの画像は入れないでください。

## ブラウザから公開する手順

1. GitHubに、説明サイト専用の新規リポジトリ `health-log-site` を作成します。GitHub FreeではPublicを選択します。作成画面でREADMEを有効にすると `main` ブランチができます。
2. ZIPを解凍し、`index.html`・`privacy.html`・`styles.css`をリポジトリ直下へ「Add file → Upload files」で追加し、Commit changesします。ZIP自体や親フォルダーごとではなく、ファイルを直下に置きます。`.nojekyll`も追加できれば一緒に配置してください。HTML/CSSだけなので、隠しファイルがアップロードできなくてもページ自体は動作します。
3. リポジトリのSettings → Pages → Build and deploymentで、Sourceを「Deploy from a branch」、Branchを「main」、Folderを「/(root)」にしてSaveします。
4. 公開後は、同じPages設定に表示される「Visit site」を開きます。反映には最大10分程度かかる場合があります。
5. ホームとプライバシーポリシーの両方を、ログアウトしたブラウザから確認します。

既存のスクリプトやデータのリポジトリをPublicに変える手順ではありません。
独自ドメインや特別なビルド設定は不要です。`.gitignore`は補助であり、Webでの誤アップロードや過去のコミットの漏洩を防ぐ保証はありません。

## Google Cloudへ入力する値

`YOUR_USERNAME`はGitHubの実際のユーザー名に置き換えてください。以下は公開済みURLではなく、標準のURL形式です。

- アプリのホームページ：`https://YOUR_USERNAME.github.io/health-log-site/`
- プライバシーポリシー：`https://YOUR_USERNAME.github.io/health-log-site/privacy.html`
- サポートメール：自分のサポート用メールをGoogle Cloudの欄に設定
- 承認済みドメインを求められた場合：`YOUR_USERNAME.github.io`（httpsやパスを付けない）

Google CloudのGoogle Auth Platform → ブランディングで設定し、対象/Audienceで公開ステータスを確認します。
本人専用の検証例外と、入力欄の検証やドメイン確認は別です。このサイトの配置だけで、本番への切り替えや検証通過を保証するものではありません。

OAuthクライアントのリダイレクトURIは、Playgroundで使っている `https://developers.google.com/oauthplayground` のままです。
公開サイトのURLをリダイレクトURIに追加・置換する必要はありません。このサイトはOAuthコールバックを実装していません。

## ドメイン/所有確認を要求された場合

Googleが表示する具体的なエラーを確認してください。まず本人利用の例外を前提とし、不要な審査を進めないでください。
所有確認が必要になった場合は、Google Search ConsoleのURLプレフィックスの確認方法（HTMLファイル/HTMLタグなど）を公式手順で確認します。
自分で管理していない `github.io` 全体を所有していると申告しないでください。確認用ファイル/タグには健康データやOAuthの秘密情報を使用しません。

## 本番切り替えができた後

同じOAuthクライアントでHealthに必要な読み取り権限だけを再認証し、新しいrefresh_tokenをApps ScriptのGH_REFRESH_TOKENに保存します。
古いテスト用トークンの期限が自動で延びたとは扱いません。認証情報はGitHubへアップロードしません。
最後にsyncHealthRangeを手動で実行し、保存と読み戻しを確認してから定期運用へ進みます。

## ファイル

- index.html：紹介ページ
- privacy.html：プライバシーポリシー
- styles.css：見た目。モバイル幅に対応
- .nojekyll：GitHub Pagesで静的ファイルとして配信するための指定
- .gitignore：公開不要なファイルを除外する補助
- README.md：この手順書（公開して差し支えのある情報は記載していません）

## 公式資料

- GitHub Pagesの作成：https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- 公開元の設定：https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- GitHub PagesのURLと閲覧情報：https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages
- Googleのブランディング/本人利用の例外：https://developers.google.com/identity/protocols/oauth2/production-readiness/brand-verification
- Google API Services User Data Policy：https://developers.google.com/terms/api-services-user-data-policy
- Google Healthの認証とトークン：https://developers.google.com/health/setup

この成果物はサイトのファイル作成までです。リポジトリの作成、ウェブ公開、Google Cloudの設定変更は別途必要です。

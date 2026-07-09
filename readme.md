# itl-classrooms

## build

`dist` ディレクトリにウェブサイトをビルドするには、`build.sh` を実行してください。

---

## 引継ぎ

事務室が公開しているスプレッドシートは大学のGoogleアカウントでのみ閲覧が可能です。
管理者の卒業などにより引継ぎが必要な場合は、以下の手順で新たな管理者が引き継ぎを行ってください。
ただし、システムの変更などにより表示が異なったり、うまくいかない可能性もあります。

### 1. GitHubでの設定

Google Apps Scriptを実行するには、まず以下の権限を持つGitHubのFine-Grained Access Tokenを生成します：

- https://github.com/settings/personal-access-tokens を開く

- Token name: itl-classroomなどわかりやすい名前を設定
- Resource owner: gdgoc-chuo (organization)
- Expiration: No expiration
- Repository access: `only selected repositories` にして、gdgoc-chuo/itl-classroom を選択
- Permissions:
  - Actions: Read and write
  - Contents: Read and write

-> Generate token

- 注意

  トークンが漏洩した場合、リポジトリ内のファイルが読み書きされる危険性があるため、取り扱いには注意してください。

### 2. Google Apps Scriptでの設定

#### 2-1. プロジェクトの作成

1. https://script.google.com にアクセス
2. `itl-classrooms` などの名前で新規作成
3. `google_app_script.js` をGASエディタにコピペ
4. プロジェクト設定を開き、スクリプトプロパティの項目から、`GITHUB_ACCESS_TOKEN` というプロパティ名として、GitHubで生成したトークンを設定します。

#### 2-2. 動作確認

設定したトークンを使って、実際に GitHub Actions へビルド命令が送れるかテストします。

1. GASエディタの左メニューから `エディタ` （</> のアイコン）をクリックしてコード画面に戻ります。
2. 上部のツールバーで、実行する関数が `triggerBuild` になっていることを確認します。
3. `実行` ボタン（再生マークのボタン）をクリックします。
   エディタ下部の実行ログに `実行開始` が出力され、数秒後に `実行完了` と表示されれば成功です。
   ※もしエラーが表示された場合は、トークンの権限や設定に問題がある可能性があります。
   GitHubでの確認: GitHubの該当リポジトリの `Actions` タブを開き、Deploy ワークフローが自動で開始されていることを確認してください。

#### 2-3. トリガー

定期的にスプレッドシートからデータを取得するためのトリガーを再作成します。

1. GAS プロジェクトを開きます。
2. 左メニューの `トリガー（時計のアイコン）` をクリックします。
3. `トリガーを追加` をクリックし、以下のように再設定します。
   - 実行する関数: `triggerBuild`
   - イベントのソース: `時間主導型`
   - 間隔: 1時間

引継ぎ作業は以上です。お疲れ様でした。

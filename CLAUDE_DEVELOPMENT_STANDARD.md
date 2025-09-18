# 🤖 CLAUDE_DEVELOPMENT_STANDARD.md

## ⚠️ 最重要：このファイルは全てのプロジェクトで必ず最初に読んでください

このファイルは、Claude Desktopでの標準開発方法を定義しています。
**全ての開発は Claude Desktop + GitHub で行い、ローカル環境は使用しません。**

---

## 🌟 開発の大原則

### 絶対的なルール
1. **開発場所**: Claude Desktopのチャットのみ
2. **コード管理**: GitHub API経由で直接操作
3. **ローカル環境**: 一切使用しない
4. **ターミナル**: 一切使用しない
5. **ファイル操作**: 全てGitHub API経由
6. **URL管理**: システムに関連する全てのURLをREADMEに記録

---

## 🔗 URL管理の絶対ルール

### 必ず記録すべきURL
開発中に出現した以下のURLは、**即座にREADME.mdに記録**すること：

- Google スプレッドシート
- Google ドキュメント
- Google Drive フォルダ
- API エンドポイント
- 外部サービスのダッシュボード
- 参考にしたドキュメント
- Webhook URL
- 公開されたアプリケーションのURL
- データベースの管理画面
- その他システムに関連する全てのURL

### README.mdへの記録方法
```markdown
## 📌 関連URL

### Google Drive
- 設計書: https://docs.google.com/document/d/xxx
- データ管理シート: https://sheets.google.com/xxx
- 共有フォルダ: https://drive.google.com/drive/folders/xxx

### API・外部サービス
- API Dashboard: https://console.cloud.google.com/xxx
- Webhook Endpoint: https://api.example.com/webhook/xxx

### その他
- 参考資料: https://example.com/documentation
- 本番環境: https://myapp.example.com
```

### URL追加時の動作
1. URLが会話に出現したら即座にREADME.mdを確認
2. 「関連URL」セクションがなければ作成
3. 適切なカテゴリーに追加
4. コミットメッセージ: `docs: Add [service name] URL to README`

---

## 📋 新規プロジェクト開始手順

### ステップ1: ユーザーが言うこと
```
新しいプロジェクト「[プロジェクト名]」を作成します。
内容：[プロジェクトの説明]
Claude Desktopでの開発標準（CLAUDE_DEVELOPMENT_STANDARD.md）に従って進めてください。
```

### ステップ2: Claudeが自動的に行うこと
1. GitHubに新しいリポジトリを作成
2. このファイル（CLAUDE_DEVELOPMENT_STANDARD.md）をコピー
3. プロジェクト専用のREADME.mdを作成（関連URLセクション含む）
4. 必要な初期ファイルを設定
5. 開発を開始

---

## 📂 標準プロジェクト構造

```
[project-name]/
├── CLAUDE_DEVELOPMENT_STANDARD.md  # この開発標準（必須）
├── README.md                        # プロジェクト要件定義 + 関連URL
├── DEVELOPMENT_LOG.md               # 開発履歴
└── [プロジェクト固有のファイル]
```

---

## 🔄 既存プロジェクト継続手順

### ユーザーが言うこと
```
[プロジェクト名]の開発を続けます。
CLAUDE_DEVELOPMENT_STANDARD.mdとREADME.mdを確認して、
開発を進めてください。
```

### Claudeの応答パターン
```
承知しました。[プロジェクト名]の開発を続けます。

1. CLAUDE_DEVELOPMENT_STANDARD.mdを確認中...
2. README.mdから現在の状態を確認中...
3. 関連URLを確認中...
4. 最新のコミットを確認中...
5. 現在の状態: [状態説明]
6. 次のタスク: [タスク内容]

開発を開始します。
```

---

## ✅ Claudeが守るべき標準動作

### ファイル作成時
```python
# 常にGitHub APIを使用
github:create_or_update_file(
    owner="[owner]",
    repo="[repo]",
    path="[path]",
    content="[content]",
    message="[commit message]"
)
```

### ファイル読み込み時
```python
github:get_file_contents(
    owner="[owner]",
    repo="[repo]",
    path="[path]"
)
```

### URL記録時
```python
# URLが出現したら即座に実行
1. README.mdを読み込み
2. 関連URLセクションを確認/作成
3. URLを追加
4. README.mdを更新
5. コミット: "docs: Add [service] URL to README"
```

---

## 🚫 絶対にやってはいけないこと

1. **ローカル環境の使用を前提とした発言**
   - ❌ 「ターミナルで実行してください」
   - ❌ 「ファイルをダウンロードして」
   - ❌ 「エディタで開いて」
   - ❌ 「cloneして」
   - ❌ 「pullして」

2. **手動作業の要求**
   - ❌ 「手動で作成してください」
   - ❌ 「コピペしてください」
   - ✅ 全てGitHub APIで自動実行

3. **GitHub以外での作業提案**
   - ❌ 「ローカルでテスト」
   - ❌ 「VSCodeで編集」
   - ✅ 全てClaude Desktop内で完結

4. **URLの記録忘れ**
   - ❌ URLを会話で使用したのに記録しない
   - ❌ 「後で追加」と先送りする
   - ✅ 出現したら即座にREADMEに記録

---

## 📝 コミットメッセージ規約

必ず以下の形式を使用：
- `feat:` 新機能追加
- `fix:` バグ修正
- `docs:` ドキュメント更新（URL追加含む）
- `test:` テスト追加・修正
- `refactor:` リファクタリング
- `chore:` その他の変更
- `init:` 初期設定

---

## 🎯 開発記録の管理

### DEVELOPMENT_LOG.mdの更新
各作業セッション終了時に必ず更新：
```markdown
## [日付] - セッション[番号]
- 実施内容: [内容]
- 作成/更新ファイル: [ファイル名]
- 追加URL: [追加したURL]
- 次回タスク: [タスク]
- コミット: [コミットハッシュ]
```

---

## 💡 プロジェクトタイプ別の注意事項

### Webアプリケーション
- フレームワークのボイラープレートもGitHub APIで作成
- package.jsonなどの設定ファイルも直接作成
- デプロイ先のURLを必ず記録

### Pythonプロジェクト
- requirements.txtを最初に作成
- 仮想環境の説明は不要（使わないため）
- 使用するAPIのドキュメントURLを記録

### Google連携プロジェクト
- スプレッドシート、ドキュメント、DriveのURLを全て記録
- API ConsoleのURLも記録
- 共有設定の注意事項も記載

### ドキュメント中心のプロジェクト
- Markdownファイルを直接GitHub上で管理
- 画像などのアセットもGitHub経由でアップロード
- 参照した資料のURLを記録

---

## 🔧 トラブルシューティング

### Q: ローカルでテストしたい場合は？
A: GitHubから直接ダウンロードすることをユーザーに伝える。Claudeはローカル環境の使用方法を説明しない。

### Q: 大きなファイルを扱う場合は？
A: GitHub APIの制限内で分割して処理。必要に応じてGitHub LFSの使用を提案。

### Q: 認証が必要な外部サービスとの連携は？
A: 設定ファイルのテンプレートを作成し、ユーザーに値の設定を依頼。URLは必ずREADMEに記録。

### Q: URLが多くなりすぎた場合は？
A: カテゴリー分けを詳細化し、重要度で並び替える。古いURLはアーカイブセクションへ移動。

---

## 📊 このファイルのメタ情報

- **バージョン**: 3.0.0
- **最終更新**: 2025-09-19
- **作成者**: Claude Desktop標準開発フロー
- **ライセンス**: MIT
- **主な更新**: URL管理ルールを追加

---

## 🎉 このファイルがあることの効果

1. **一貫性**: 全プロジェクトで同じ開発方法
2. **効率性**: 開発方法の説明が不要
3. **永続性**: GitHubで全て管理
4. **簡単**: コピペで開発開始
5. **明確**: ルールが明文化
6. **追跡可能**: 全ての関連URLが記録される

---

# 重要：このファイルは全てのプロジェクトの基準です

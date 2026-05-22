# 電子カルテ - Vercel + GitHub 自動デプロイ設定ガイド

## ファイル構成

```
salon-karte/
├── index.html          ← メインの電子カルテファイル
├── vercel.json         ← Vercel設定（静的サイト）
└── README.md           ← このファイル
```

## 手順1: GitHubリポジトリを作成

### A. GitHubアカウントにログイン
- https://github.com にアクセス
- サインイン

### B. 新しいリポジトリ作成
1. 右上の「＋」アイコン → 「New repository」
2. **Repository name**: `salon-karte`（または任意の名前）
3. **Description**: 「顧客カルテシステム（複数店舗対応）」
4. **Public** または **Private** を選択
5. 「Create repository」をクリック

### C. ローカルでGit初期化（コマンドライン）

```bash
# 作業ディレクトリに移動
cd ~/Desktop/salon-karte  # または任意のパス

# Gitを初期化
git init

# GitHubリモートを追加
git remote add origin https://github.com/YOUR_USERNAME/salon-karte.git

# ファイルをステージング
git add .

# 初回コミット
git commit -m "初期コミット：患者用電子カルテシステム"

# メインブランチにプッシュ
git branch -M main
git push -u origin main
```

> **注意**: YOUR_USERNAME をあなたのGitHubユーザー名に置き換えてください

---

## 手順2: Vercelで自動デプロイ設定

### A. Vercelアカウント作成・ログイン
1. https://vercel.com にアクセス
2. 「Sign Up」 → GitHubアカウントで認証
3. メール確認完了

### B. GitHubリポジトリを連携
1. Vercelダッシュボード → 「Add New...」 → 「Project」
2. 「Import Git Repository」をクリック
3. 「GitHub」を選択
4. 「Connect GitHub」で認可
5. リポジトリリストから `salon-karte` を選択
6. 「Import」をクリック

### C. Vercel設定確認
- **Framework Preset**: 「Other」のままでOK
- **Build Command**: 空白（静的サイト）
- **Output Directory**: `.`
- 「Deploy」をクリック

### デプロイ完了！
- Vercelが自動で URL を生成します
- 例: `https://salon-karte.vercel.app`

---

## 手順3: GitHubとの自動同期確認

### コードを更新する場合
```bash
# ファイルを編集
# 例: index.html の店舗名を変更

# 変更をコミット
git add .
git commit -m "店舗QR対応：Liora nail&eye追加"

# GitHubにプッシュ
git push
```

**自動で以下が実行されます：**
1. ✅ GitHub にコードが保存される
2. ✅ Vercelが自動で検知
3. ✅ 自動ビルド＆デプロイ開始
4. ✅ デプロイ完了通知（メール or Slack）
5. ✅ URLが自動更新される

---

## GAS連携の確認

電子カルテからGASスクリプトへデータを送信しています。

**GAS エンドポイント**
```
https://script.google.com/macros/s/AKfycbwFd113vOBt8pIMMnYvLx80uf6AL0chYS0IpufnBz9X5cP5btSap_uYd3m8kCvGXhRx/exec
```

**送信データ形式**: JSON
- 患者情報（名前、電話番号、生年月日など）
- アンケート回答
- 店舗名
- タイムスタンプ

ブラウザコンソール（F12）でエラーがないことを確認してください。

---

## 店舗別QRコード設定

各店舗のQRコードには以下のURLをエンコードしてください：

```
https://salon-karte.vercel.app/?shop=arbre
https://salon-karte.vercel.app/?shop=choupinet
https://salon-karte.vercel.app/?shop=miroir
https://salon-karte.vercel.app/?shop=liora
```

ページロード時に自動で対応する店舗名に切り替わります。

---

## トラブルシューティング

### Q: ページが表示されない
**A**: Verielダッシュボード → Deployments で デプロイログを確認

### Q: GASへのデータが送信されていない
**A**: ブラウザコンソール（F12 → Console）でエラーを確認

### Q: GitHubにプッシュしてもデプロイが開始されない
**A**: Vercelダッシュボード → Settings → Git で GitHub 連携を再確認

---

## 今後の拡張予定

- [ ] スタッフ用管理画面（データ閲覧・CSV出力）
- [ ] 複数店舗のダッシュボード化
- [ ] 予約連携（Hot Pepper Beauty API）
- [ ] メール自動送信（確認・フォローアップ）

---

## サポート

問題が発生した場合：
1. Vercelダッシュボードでデプロイログ確認
2. ブラウザコンソール（F12）でエラー確認
3. GitHubの Issue で報告

---

**作成日**: 2026年5月21日  
**最終更新**: 2026年5月21日

# Webapp — Webアプリ開発

> localhost・Git・ホスティング・Vercel・Supabaseなど、Webアプリ開発の基礎から実践的な構成まで整理したカテゴリです。

---

## 目次

1. [localhost:3000とは](#1-localhost3000とは)
2. [Git / GitHub 基本コマンド](#2-git--github-基本コマンド)
3. [GitHub Enterprise と GitHub Team](#3-github-enterprise-と-github-team)
4. [ホスティングとは](#4-ホスティングとは)
5. [Vercel](#5-vercel)
6. [Supabase](#6-supabase)
7. [Vercel × Supabase の黄金構成](#7-vercel--supabase-の黄金構成)
8. [Supabase以前のバックエンド事情](#8-supabase以前のバックエンド事情)

---

## 1. localhost:3000とは

**概要説明**
自分のPC上で動いているWebサーバーにアクセスするためのURL。`localhost`は「自分自身のPC」を指す特別なアドレス、`3000`は「窓口の番号（ポート番号）」。

| 部分 | 意味 |
|------|------|
| `http://` | 通信方式 |
| `localhost` | 自分のPC（`127.0.0.1`と同じ） |
| `3000` | ポート番号 |

**使用例**
- React/Next.js/Vueでフロントエンド開発する時：`npm run dev`で自動起動
- Node.js/Expressでバックエンド開発する時
- Dockerでアプリを起動した時の動作確認

**ポイント**
- 自分のPCの中だけで動いているので**他の人からは見えない**
- ポート番号は`3000`の他に`8080`、`5173`（Vite）、`4000`なども一般的

---

## 2. Git / GitHub 基本コマンド

**概要説明**
ソースコードのバージョン管理を行う仕組み。`Git`がツール本体、`GitHub`がクラウド上の保管場所。

**初回アップロード時の典型コマンド**

| コマンド | 役割 |
|---|---|
| `git init` | フォルダをGit管理下に置く |
| `git add ファイル名` | コミット対象に追加（ステージング） |
| `git commit -m "メッセージ"` | 変更を記録 |
| `git branch -M main` | ブランチ名を`main`に変更 |
| `git remote add origin URL` | GitHubリポジトリと紐づけ |
| `git push -u origin main` | GitHubへアップロード |

**類似サービス**

| サービス | 特徴 |
|---|---|
| GitLab | GitHubの競合、CI/CD機能が強力 |
| Bitbucket | Atlassian社、Jiraと連携が強い |
| Azure DevOps | Microsoft、エンタープライズ向け |

---

## 3. GitHub Enterprise と GitHub Team

**概要説明**
GitHubの**有料プラン**で、規模・必要な機能によって階層が分かれる。

| プラン | 対象 | 料金（月額） | 主な機能 |
|---|---|---|---|
| **Free** | 個人・小規模 | $0 | 基本機能 |
| **Team** | 小〜中規模チーム | $4/ユーザー〜 | コードオーナー、保護ブランチ、複数レビュワー、Codespaces |
| **Enterprise** | 大規模組織 | 個別見積もり | SAML SSO、監査ログ、Enterprise Managed Users、データレジデンシー、セルフホスト |

**使い分けのポイント**
- 「**SAML SSO・監査ログ・セルフホスト・データレジデンシー**」が必要かどうかが、TeamとEnterpriseの境目
- Enterpriseは2形態：**Enterprise Cloud**（GitHub側でホスト）と **Enterprise Server**（自社インフラでホスト）

---

## 4. ホスティングとは

**概要説明**
作ったWebサイトやアプリのファイルを、インターネット上のサーバーに置いて、世界中の人がアクセスできるようにするサービス。

> 家（ウェブサイト）を建てても、土地（サーバー）がないと人は訪問できない。ホスティングは「土地を貸してくれる」サービス。

**ホスティングの種類**

| 種類 | 特徴 | 例 |
|---|---|---|
| 共用ホスティング | 1台のサーバーを複数ユーザーで共有 | さくら、XServer |
| VPS | 仮想専用サーバー | ConoHa、Linode |
| クラウド | 自由に拡張可能な大規模インフラ | AWS、GCP、Azure |
| 静的ホスティング | フロントエンド特化 | **Vercel**、Netlify、Cloudflare Pages |
| BaaS | バックエンド機能込みでホスト | **Firebase**、**Supabase** |

---

## 5. Vercel

**概要説明**
主にフロントエンド（React・Next.jsなど）向けの**クラウドホスティングプラットフォーム**。Next.jsの開発元でもある。

**主な特徴**

| 特徴 | 内容 |
|---|---|
| 簡単デプロイ | GitHubと連携して`push`するだけで自動更新 |
| 高速配信（CDN） | 世界中のサーバーから配信 |
| プレビュー機能 | プルリクエストごとに自動でプレビューURL生成 |
| サーバーレス関数 | バックエンドのAPIもVercel上で実行可能 |
| 無料プラン | 個人利用なら無料 |

**向いている用途**
ポートフォリオ、ブログ、Reactアプリ、Next.jsアプリ全般。

**類似サービス**

| サービス | 特徴 |
|---|---|
| Netlify | 静的サイトに強い、似た機能 |
| Cloudflare Pages | Cloudflareエッジ網で高速 |
| AWS Amplify | AWS純正、自由度高め |
| Firebase Hosting | Googleのサービスと連携しやすい |

---

## 6. Supabase

**概要説明**
**「Firebaseのオープンソース代替」** として作られたBackend-as-a-Service（BaaS）。アプリのバックエンドに必要な機能をまるごと提供する。

**FirebaseとSupabaseの比較**

| 項目 | Supabase | Firebase |
|---|---|---|
| 提供元 | オープンソース | Google |
| データベース | **PostgreSQL（SQL）** | Firestore（NoSQL） |
| 料金 | 無料枠が広め | 無料枠あり |
| オープンソース | ✅ 自前サーバーも可 | ❌ |

**主な機能**

| 機能 | 概要 |
|---|---|
| データベース | PostgreSQL、SQLクエリ、リレーション対応 |
| 認証 | メール/パスワード、Google・GitHub等のSSO |
| ストレージ | 画像・動画などのファイル保存 |
| リアルタイム | データ変更を即座にフロントへ反映 |
| Edge Functions | サーバーサイドのカスタム処理 |

---

## 7. Vercel × Supabase の黄金構成

**なぜ組み合わせが人気か**

```
ユーザー
  ↓
Vercel（フロントエンド / Next.js）
  ↓
Supabase（DB・認証・ストレージ）
```

| 理由 | 内容 |
|---|---|
| 開発速度 | バックエンド構築不要、その日にリリース可能 |
| 相性 | Next.jsのServer ActionsからSupabaseを直接呼べる |
| 公式統合 | Vercelダッシュボードから数クリックで接続 |
| 無料枠 | 個人開発・スタートアップ初期はほぼ無料 |
| 環境変数 | 環境変数をVercel側に登録（Key/Value形式） |

**環境変数の書き方の例**
```
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
└──────── Key ────────┘ └────── Value ──────┘
```

**実際の採用事例**
- **Mobbin**：UIデザインリファレンスサービス（FirebaseからSupabaseへ移行）
- **Pika**：AI動画生成ツール
- 多数のYC（Y Combinator）スタートアップ

---

## 8. Supabase以前のバックエンド事情

**バックエンドの時代の流れ**

```
【2000年代】
自前サーバー + PHP/MySQL（全部自前で構築・管理）
       ↓
【2010年代前半】
AWS（EC2 + RDS + S3）の普及（インフラは楽だが設定複雑）
       ↓
【2010年代後半】
Firebase の台頭（バックエンド不要で手軽に）
       ↓
【2020年代〜現在】
Supabase の台頭（Firebaseの使いやすさ + SQLの柔軟性）
```

**機能別：以前は何を使っていたか**

| 機能 | 以前 | 現在（Supabaseで代替） |
|---|---|---|
| DB | MySQL/PostgreSQL自前運用、AWS RDS、Heroku Postgres | Supabase Database |
| 認証 | 自前実装、Auth0、Firebase Auth | Supabase Auth |
| ストレージ | AWS S3、Cloudinary | Supabase Storage |
| リアルタイム | Socket.io（自前）、Pusher | Supabase Realtime |

**Firebase → Supabase 移行の主な理由**
- SQLが使いたい（FirestoreはNoSQLで複雑クエリが苦手）
- ベンダーロックイン回避（Googleへの依存を避けたい）
- 規模が大きくなった時のコスト
- オープンソース（自前サーバーへ移行可能）

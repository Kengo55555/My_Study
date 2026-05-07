# AI_study — IT・AI用語ナレッジベース

> 2026年3月以降にClaudeへ質問した内容をカテゴリ別に整理したナレッジベースです。
> 各用語は「概要説明」「使い方・使用例」「類似サービス・関連用語」の3点セットで記載しています。
>
> 最終更新：2026年5月7日

---

## カテゴリ一覧

| ファイル | 内容 |
|---|---|
| [AI.md](./AI.md) | AIサービス・LLM・MCP（AIの使い方・つなぎ方） |
| [Webapp.md](./Webapp.md) | Webアプリ開発（localhost・Git・Vercel・Supabase） |
| [IT_Basic.md](./IT_Basic.md) | IT基礎・データ分析・ソフトウェア構造 |
| [インフラ.md](./インフラ.md) | クラウド・インフラ・CI/CD・開発環境トラブルシューティング |
| [AI駆動開発.md](./AI駆動開発.md) | AI駆動開発の手法・方法論（ハーネス・ADR・チーム活用） |

---

## 学習ロードマップ（推奨順序）

```
Step 1: IT_Basic.md → IT基礎知識を固める
Step 2: Webapp.md  → Webアプリの構造を理解する
Step 3: インフラ.md → クラウド・CI/CDを学ぶ
Step 4: AI.md      → AIサービスを実際に使う
Step 5: AI駆動開発.md → AIを活用した開発手法を習得する
```

---

## 全体マップ：用語のつながり

### AI開発の階層構造

```
  ユーザーの指示
       ↓
┌──────────────────────────┐
│ プロンプトエンジニアリング   │
│   ・指示文の工夫           │
└──────────────────────────┘
       ↓
┌──────────────────────────┐
│ コンテキストエンジニアリング  │
│   ・AIに何を見せるか        │
│   ・MCP（Notion/Slack等）  │
└──────────────────────────┘
       ↓
┌──────────────────────────┐
│ ハーネスエンジニアリング     │
│   ・環境全体の設計          │
│   ・AGENTS.md/CLAUDE.md   │
│   ・ADRで判断記録          │
│   ・CI/CDで品質ゲート       │
└──────────────────────────┘
       ↓
┌──────────────────────────┐
│ 開発インフラ               │
│   ・GitHub（コード管理）    │
│   ・CI/CD（自動化）         │
│   ・Cloudflare（公開）      │
│   ・Vercel + Supabase     │
└──────────────────────────┘
       ↓
┌──────────────────────────┐
│ AI実行環境                 │
│   ・クラウドAPI（Claude等） │
│   ・ローカル（Ollama）      │
└──────────────────────────┘
```

### Webアプリ開発の典型構成

```
ブラウザ
   ↓
Vercel／Cloudflare Pages（フロントエンド配信）
   ↓
Next.js / React（フレームワーク）
   ↓
Supabase（DB・認証・ストレージ）
   or Firebase
   or 自前バックエンド（Node.js等）
```

---

## 参考リンク（公式）

- [MCP公式](https://modelcontextprotocol.io/)
- [GitHub Copilot](https://github.com/features/copilot)
- [Cloudflare Learning](https://www.cloudflare.com/ja-jp/learning/)
- [Harness Engineering（OpenAI）](https://openai.com/index/harness-engineering/)
- [Anthropic（Claude）](https://www.anthropic.com/)
- [Ollama](https://ollama.com/)
- [Vercel](https://vercel.com/)
- [Supabase](https://supabase.com/)

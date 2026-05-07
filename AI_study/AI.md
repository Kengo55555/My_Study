# AI — AIサービス・LLM・MCP

> AIサービスの使い方、ローカルLLM、MCPによる外部連携を整理したカテゴリです。

---

## 目次

1. [Ollama（ローカルLLM実行）](#1-ollama)
2. [GitHub Copilot](#2-github-copilot)
3. [Microsoft Copilot Studio](#3-microsoft-copilot-studio)
4. [Microsoft Copilot for Teams](#4-microsoft-copilot-for-teams)
5. [MCP（Model Context Protocol）](#5-mcpmodel-context-protocol)
6. [Notion MCP（実例：MCPのトラブルシューティング）](#6-notion-mcp)
7. [Neuron MCP（McpConnector）](#7-neuron-mcp)

---

## 1. Ollama

**ざっくり何か**
**大規模言語モデル（LLM）を自分のPCでローカル実行**するためのオープンソースツール。クラウドAPIを使わず、モデルを手元にダウンロードして動かす。

**使用例**
```bash
# インストール後、ターミナルで
ollama run llama3.2
```
裏側でAPIサーバー（`http://localhost:11434`）が立ち上がり、他アプリと連携可能。

**メリット**

| メリット | 内容 |
|---|---|
| プライバシー | データが外部に出ない（医療・金融・法務向き） |
| コスト | API利用料ゼロ |
| オフライン動作 | ネット不要 |
| モデル選択 | Llama、Gemma、Phi、Qwen、DeepSeekなど切替可能 |

**デメリット**
- 性能はPCスペック（GPU・RAM）に依存
- フロンティアモデル（Claude Opus、GPT-5）には及ばない
- 高並列の本番用途には向かない

**類似サービス**

| サービス | 特徴 |
|---|---|
| LM Studio | GUIベースで使いやすい |
| vLLM | 高並列向けの推論エンジン |
| llama.cpp | 低レベル実装、Ollamaの土台 |

---

## 2. GitHub Copilot

**ざっくり何か**
**「AIペアプログラマー」** として、コードを書く現場から開発フロー全体までを支援するAIサービス。

**主な機能**

| 機能 | 何ができるか |
|---|---|
| インラインコード補完 | IDEで入力中にコード提案、次の編集位置も予測 |
| Copilot Chat | コードに関する質問・説明・テスト生成・エラー修正 |
| Copilot Edits | 1つのプロンプトで複数ファイルを同時編集 |
| Cloud agent | Issueを割り当てると自律的にPRを作成 |
| Copilot CLI | ターミナルからCopilotを利用 |
| Code review | AIが自動でコードレビューコメントを生成 |
| PR要約 | プルリクエストの自動要約 |

**使えるAIモデル（2026年時点）**
- Claude Opus 4.7
- GPT-5系
- Gemini系
- 用途に合わせて切替可能

**類似サービス**

| サービス | 特徴 |
|---|---|
| Cursor | VS Codeフォークの専用エディタ |
| Claude Code | Anthropic製、ターミナル/CLI中心 |
| Cody（Sourcegraph） | エンタープライズ向け |
| Tabnine | 古参、オンプレ可 |

---

## 3. Microsoft Copilot Studio

**ざっくり何か**
Microsoftが提供する**AIエージェント構築プラットフォーム**。Webサイト・アプリ・SNS等にAIエージェントを公開できる。

**料金体系（2025年9月以降）**

課金単位は「**Copilot Credits**」で、エージェントの応答・アクションごとに消費。

| プラン | 内容 | 料金 |
|---|---|---|
| キャパシティパック | 25,000 Credits/月 | $200/月 |
| 従量課金 | 使った分だけ後払い | 月末請求 |
| 事前購入プラン | 一括前払いで割引 | 最大20% off |
| Microsoft 365 Copilot同梱 | 社内向けエージェント無制限 | M365 Copilotライセンスに含む |

**Microsoft 365 Copilot本体の料金**
- Enterprise：$30/ユーザー/月
- Business：$18/ユーザー/月（プロモ価格、通常$21）

**類似サービス**

| サービス | 特徴 |
|---|---|
| Google Vertex AI Agent Builder | GCP純正 |
| Amazon Bedrock Agents | AWS純正 |
| Dify | オープンソース |
| LangChain / LangGraph | Pythonフレームワーク |

---

## 4. Microsoft Copilot for Teams

**ざっくり何か**
**Microsoft 365 Copilot** を使って、Teamsの会議・チャット・チャネル情報を要約・活用する機能。

**取得できる3種類の情報**

1. **会議のトランスクリプト**：要約・決定事項・アクションアイテム抽出
2. **チャット**：30日間の履歴を参照
3. **チャネル投稿**：ディスカッションの要約

**設定の流れ（管理者）**

1. Teams管理センターで**文字起こし（トランスクリプト）を有効化**
2. Copilotポリシーを設定
3. Microsoft 365管理センターで**ユーザーアクセス・データアクセス**を制御
4. （任意）ユーザー辞書をアップロードして社内固有名詞の認識精度向上

**設定の流れ（会議開催者）**

会議オプションで以下から選択：
- 会議中および会議後（Copilot利用可、履歴も残る）
- 会議中のみ（履歴は残らない）
- オフ（録画・文字起こし無効）

**実用プロンプト例**
- 「これまでの会話の要点を3つに絞って」
- 「アクションアイテムを担当者・期限ごとに表にして」
- 「A案とB案それぞれの賛成・反対意見を整理して」

---

## 5. MCP（Model Context Protocol）

**ざっくり何か**
**Anthropicが2024年11月に公開** した、LLMを外部ツール・データソース・サービスに接続するためのオープン標準規格。「**AI向けのUSB-Cポート**」と例えられる。

**解決する問題**
従来、AIアプリと外部サービスをつなぐには、N×M個（AIの数×ツールの数）の個別連携が必要だった。MCPは「N+M」に削減する。

**MCPの構成要素**

| 要素 | 役割 |
|---|---|
| MCPホスト | AIアプリ本体（Claude、ChatGPT、IDE等） |
| MCPクライアント | LLMとサーバーの仲介 |
| MCPサーバー | 外部サービス側（DB、API、ファイル等） |

**代表的なMCPサーバー例**
- Notion、Slack、Gmail、Google Drive
- Cloudflare（Workers・D1・R2を操作）
- 社内DB、社内API

**類似プロトコル**

| プロトコル | 用途 |
|---|---|
| OpenAPI | API仕様の記述標準（リアルタイム連携ではない） |
| Function Calling（OpenAI等） | MCPの源流的な機能、独自実装 |

---

## 6. Notion MCP

**ざっくり何か**
NotionのページやデータベースをClaude等のAIから直接操作できるMCPサーバー。「議事録を自動でNotionに保存」といった連携が可能。

**接続できないときに確認する3点**

### ① トークンが有効か

1. https://www.notion.so/profile/integrations にアクセス
2. Integration を選択し、「内部インテグレーションシークレット」をコピー
3. 動作確認：

```bash
curl -X GET https://api.notion.com/v1/users/me \
  -H "Authorization: Bearer secret_xxx" \
  -H "Notion-Version: 2022-06-28"
```

- ✅ `{"object":"user"...}` → 有効
- ❌ `{"code":"unauthorized"}` → 無効・要再発行

### ② 対象ページがIntegrationに共有されているか

1. Notionで対象ページを開く
2. 右上「...」→「コネクト」
3. Integration名を選んで追加（親ページ共有が子ページに必ず引き継がれるとは限らない）

### ③ Claude Code側の設定が正しいか

```bash
cat ~/.claude.json
```

確認ポイント：
- トークンが正しく貼られているか
- 余分なスペース・改行が混入していないか
- 再発行後、古いトークンのままになっていないか

---

## 7. Neuron MCP（McpConnector）

**ざっくり何か**
**PHP製のAIエージェントフレームワーク「Neuron AI」** に組み込まれている、MCP連携機能。
LaravelやSymfonyのPHPアプリから、世の中のMCPサーバーを呼び出せる。

**コード例**
```php
use NeuronAI\MCP\McpConnector;

class MyAgent extends Agent {
    protected function tools(): array {
        return [
            ...McpConnector::make([
                'url' => 'https://mcp.example.com',
                'token' => 'BEARER_TOKEN',
            ])->only(['search', 'create_issue'])  // ツール絞り込み
              ->tools(),
        ];
    }
}
```

**特徴**
- ローカル接続（command）/ リモート接続（URL）両対応
- `only()` / `exclude()` でツールを絞り込み可能（誤動作防止・トークン節約）

**類似フレームワーク**

| フレームワーク | 言語 |
|---|---|
| LangChain | Python/JS |
| LlamaIndex | Python |
| Vercel AI SDK | TypeScript |
| Mastra | TypeScript |

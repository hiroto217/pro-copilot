# PMOコパイロット

PMO業務を支援するAIエージェントを、Amazon Bedrock AgentCore と Amazon Bedrock で作るプロジェクトです。
[Qiita Advent Calendar 2026](https://qiita.com/advent-calendar/2026) の1人アドベントカレンダー(12/1〜12/25、全25記事)のサンプルコードを置いています。

> **注意:このリポジトリのデータは全て架空です。**
> 案件、会社名、人物、メール、議事録、Q&Aは、学習用に作ったダミーデータです。実在の企業・個人・案件とは関係ありません。

## 何を作るか

PMOの「過去の経緯の検索」と「返信漏れの防止」を支援する、2つのエージェントです。

| エージェント | 役割 | 主な構成 |
|---|---|---|
| 相談役(pmo-advisor) | 質問に、過去のQ&A台帳などから根拠付きで答える。担当者の候補を上位3人まで挙げる | AgentCore Harness、Knowledge Bases(読み取り専用) |
| 見張り役(pmo-watcher) | 毎朝メールを確認し、依頼を台帳に登録する。返信が必要そうで未返信のものを通知し、返信の下書きを作る | AgentCore Runtime、Gateway、Identity、EventBridge Scheduler |

2つのエージェントは直接やりとりせず、依頼の台帳を介して連携します。権限を分け、メール経由の攻撃の影響範囲を小さくするための設計です。

## 使うサービス

AgentCore(Harness、Runtime、Gateway、Identity、Memory、Policy、Observability、Evaluations、Code Interpreter)、Amazon Bedrock(Knowledge Bases、Guardrails)、EventBridge Scheduler、Microsoft Entra ID、Microsoft Graph API、IaC(CDKなど)。

## 記事とコードの対応

各記事は、単体でも読めるように書いています。記事ごとの開始時点の状態は `dayXX/` に置く予定です。
前日までの作業をしていなくても、該当する日のフォルダから試せます。

| 日 | テーマ | フォルダ |
|---|---|---|
| 1 | Harnessで最小のエージェントを動かす | `day01/` |
| ... | ... | ... |
| 25 | 25日間のAWS費用の実績と振り返り | `day25/` |

(記事の公開に合わせて、リンクを追加します。)

## ディレクトリ構成(予定)

```
pmo-copilot/
├─ docs/        仕様メモ
├─ data/        ダミーデータ(Q&A台帳、メール、議事録、テスト質問)
├─ day01/ ... day25/
├─ infra/       IaC
└─ scripts/     データ生成、評価の実行
```

## ご利用にあたって

- 学習・検証を目的としたサンプルです。本番環境での利用は想定していません。
- 動かすとAWSの利用料金が発生します。事前にAWS Budgetsなどで予算の上限を設定し、検証後はリソースを削除してください。
- AWS、Microsoft、各サービスの仕様は変わることがあります。記事の執筆時点(2026年11〜12月)の内容です。
- 認証情報(AWSのキー、Entra IDのシークレットなど)は、このリポジトリに含めないでください。
- 本プロジェクトは、AWSやMicrosoftの公式のものではありません。

## ライセンス

[MIT License](./LICENSE)

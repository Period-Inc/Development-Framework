---
pdm_version: "0.1"
id: actor-execution-and-audit-model
name: Actor Execution and Audit Model
type: architecture.contract
status: draft
owners:
  - Period-Inc
relations:
  - type: refines
    target: development-framework
---

# Actor Execution and Audit Model

## Purpose

人間とAIの開発フローにおいて、仕様決定後の実装・検証・引き継ぎを人間のメッセージ中継に依存させないための責務モデルを定義します。

人間との対話は、価値判断、仕様、制約、受入条件を決めるために使います。仕様が実行可能な状態になった後は、Actor間の通信と実装ループを機械可読なWork OrderとRepository上の状態を介して継続できることを目標とします。

## Core principle

仕様確定後の通常の実装・検証・修正ループに、人間を通信路として要求しません。

人間への再問い合わせは、以下のような人間にしか決定できない事項に限定します。

- 仕様変更
- 事業上または価値上の判断
- 既存原則の変更
- 不可逆操作
- 権限・秘密情報・費用上限に関する判断
- 相互に矛盾する仕様の解消

## Actor and role model

ActorとRoleは分離します。

- Owner: 最終的な価値判断・仕様承認を行う人間
- Architect: 仕様策定、構造設計、cross-spec auditを担当
- Executor: 実装、テスト、修正を担当
- Auditor: within-spec auditを担当

初期の既定マッピングは以下とします。

- Owner = Human
- Architect = ChatGPT
- Executor = Claude Code
- Auditor = Codex

これはprovider固定ではありません。Roleは安定した責務、Actor/Workerは交換可能な実体として扱います。

## Audit scopes

### Within-spec audit

「与えられた仕様が正しく実装されているか」を監査します。

対象:

- acceptance criteriaの充足
- 実装漏れ
- バグ候補
- 回帰
- テスト不足
- 境界条件
- 実装内部の整合性
- 変更差分と仕様の対応

初期ActorはCodexとします。

### Cross-spec audit

「その仕様・実装が他の仕様、原則、プロジェクト、組織規約と整合しているか」を監査します。

対象:

- 他仕様との矛盾
- Project全体の設計思想との不整合
- PDM / Codes / Mannered Code等の横断原則との整合
- 局所最適
- 前提自体の誤り
- 複数Repository間の整合
- 将来の再利用性・継続性への影響

初期ActorはChatGPTとします。

Cross-spec auditは全実装ループに同期的に参加する必要はありません。within-spec auditを通過した成果、または横断判断が必要なWork Orderに対して実施できます。

## Responsibility flow

```text
Human <-> Architect
  specification / constraints / acceptance criteria
            |
            v
        Work Order
            |
            v
        Executor
            |
            v
   within-spec Auditor
       |           |
      FAIL        PASS
       |           |
       +-> Executor|
                   v
          cross-spec audit
          when required
                   |
                   v
            done / human gate
```

## Work Order contract

Work OrderはActor間の実行契約です。最低限以下を保持します。

- id
- repository
- goal
- specification
- constraints
- acceptance_criteria
- references
- executor role / preferred actor
- auditor role / preferred actor
- execution node preference or requirement
- status
- checkpoint
- evidence
- escalation conditions

Work Orderはproject固有の実装状態を中央DBへ吸収するためのものではありません。Project Repositoryが保持すべき仕様と実装情報はProject Repositoryをauthorityとし、Repositories / Control Planeは必要に応じてprojectionします。

## Human gate

実装系Actorは以下の場合に自律ループを停止し、human gateへ移行できます。

- acceptance criteriaを満たせない
- 仕様が矛盾している
- 仕様変更が必要
- destructive operationが必要
- production deployment等の承認が必要
- secret / permission不足
- 明示されたcost / retry limitを超える

単なる実装判断、通常のテスト失敗、レビュー指摘、修正方法の選択はhuman gateの理由にしません。

## Transferability

完全な自動failoverを初期要件にしません。

初期目標はsemi-platform-free、すなわち「明示的に別Nodeへ渡せば継続できる」ことです。

引き継ぎに必要な状態はdurableに残します。

- branch
- commit SHA
- Work Order
- checkpoint
- test / audit evidence
- unresolved items
- next action

ローカルprocess stateやAI sessionの復元は必須条件にしません。

## Provider independence

上位モデルはClaude、Codex、ChatGPT等のCLI/API固有仕様を直接参照しません。

実装はWorker Adapterを介します。

```text
Role
  -> Work Order
  -> Worker Adapter
  -> Worker runtime
  -> execution result / evidence
```

これにより、同一Roleを別provider、別CLI、API、local modelへ置換可能にします。

---
title: Agentic Knowledge Base (AKB)
akb_type: node
status: active
tags:
  - type/how-to
  - domain/akb
---

# Agentic Knowledge Base (AKB)

**AI 에이전트를 위한 자율 탐색형 지식 프로토콜**

> 이 문서는 AKB의 **Canonical Reference**입니다.

---

## TL;DR

- **정의**: AI가 **검색(Grep/Glob)**으로 찾고, **맥락 링크**로 탐색하는 파일 기반 지식 시스템
- **본질**: 파일 기반 Lightweight Ontology (Tag=Type, 본문 링크=Edge)
- **철학**: AI가 잘 찾을 수 있도록 문서 최적화
- **구조**: Root(CLAUDE.md) → Hub(사람용 TOC) → Node(실제 정보)
- **핵심 규칙**: 4가지 작성 원칙 (TL;DR, 맥락 링크, 키워드 최적화, 원자성)

---

## 정의

> "코드는 기계가 실행하는 논리이고, AKB는 에이전트가 사고(Thinking)하는 맥락이다."

AKB는 AI 에이전트가 인프라(Vector DB) 없이도 스스로 문맥을 **검색(Search)**, **학습(Learn)**, **인출(Retrieve)**할 수 있도록 설계된 **파일 기반의 연결된 지식 시스템**입니다.

### Core Philosophy

> "AI에게 모든 것을 한 번에 주입하려 하지 마십시오.
> 대신, **잘 찾을 수 있는 문서**를 주십시오."

---

## 본질: 파일 기반 Ontology

> "Ontology의 향기를 Markdown에 주입"

```
┌─────────────────────────────────────────────────────┐
│           AKB = Lightweight Knowledge Graph          │
├─────────────────────────────────────────────────────┤
│                                                     │
│   Ontology/KG                AKB                    │
│   ───────────                ───                    │
│   Entity (Node)       →      .md 파일               │
│   rdf:type            →      tags: [type/]          │
│   domain              →      tags: [domain/]        │
│   rdfs:comment        →      TL;DR 섹션             │
│   Edge/Relationship   →      본문 맥락 링크          │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## 아키텍처

AKB는 **[Root] → [Hub] → [Node]**로 이어지는 3단계 위계 구조를 가집니다.

```
project/
├── CLAUDE.md                      # [Root] 최소 라우팅 (핵심 파일 직접 경로)
│
└── projects/
    │
    ├── blockchain-wallet/         # [Hub] 사람용 TOC
    │   ├── blockchain-wallet.md   #   ㄴ Hub 진입점
    │   └── key-management.md      # [Node] 구체적 지식
    │
    ├── security/
    │   ├── security.md            # [Hub]
    │   ├── encryption/
    │   │   ├── encryption.md      # [Sub-Hub]
    │   │   ├── hd-wallet.md       # [Node] ← AI가 검색으로 직접 찾음
    │   │   └── seed-phrase.md     # [Node]
```

### 계층별 역할

| 계층 | 역할 | 설명 |
|------|------|------|
| **Root** (CLAUDE.md) | 최소 라우팅 | 시스템 프롬프트로 자동 주입, 핵심 파일 경로 제공 |
| **Hub** ({폴더명}.md) | 사람용 TOC | 폴더 내용 파악용, AI는 선택적으로 읽음 |
| **Node** (*.md) | 실제 정보 | AI가 Grep/Glob으로 직접 검색하는 대상 |

---

## 스키마 명세

### Frontmatter

```yaml
---
title: "문서 제목"
akb_type: hub|node
status: active|draft|deprecated
tags:
  - "type/..."      # 문서 유형
  - "domain/..."    # 도메인 분류
---
```

| 필드 | 타입 | 역할 |
|------|------|------|
| `title` | string | 문서 식별 |
| `akb_type` | enum | hub/node 구분 |
| `status` | enum | 문서 상태 관리 |
| `tags` | array | 도메인 분류 (Grep 검색에 도움) |

### Tags (분류)

| Namespace | 역할 | 예시 |
|-----------|------|------|
| `type/` | 문서 유형 | `type/how-to`, `type/reference`, `type/api-guide` |
| `domain/` | 도메인 분류 | `domain/wallet`, `domain/security` |

---

## 작성 원칙 (4가지)

### Rule 1: TL;DR 필수 + 키워드 최적화

AI가 Grep으로 찾을 수 있도록 **핵심 키워드를 자연스럽게 포함**합니다.

```markdown
## TL;DR

- **HD Wallet**에서 **BIP-44** 경로 구현
- **Private Key** 암호화 및 **Keystore** 관리
- **Transaction Signing** 로직 구현
```

**작성 규칙:**
- 3-5개 bullet points
- **핵심 키워드 볼드** 처리 (Grep 검색 대상)
- 한 줄 이내

### Rule 2: 맥락 링크 (본문에 배치)

**본문 흐름 속에서** 링크를 배치합니다.

**예시 1: 본문 중간에 자연스럽게**
```markdown
이 지갑의 핵심은 **[HD Wallet 구조](./hd-wallet-structure.md)**입니다.

키 저장 방식은 [Keystore 암호화](./keystore-encryption.md)를 참고하세요.
```

**예시 2: 다음 단계 섹션**
```markdown
## 다음 단계

- 트랜잭션 서명이 필요하다면 → [transaction-signing.md](./transaction-signing.md)
- 멀티시그 지갑이라면 → [multisig-wallet.md](./multisig-wallet.md)
```

**왜 효과적인가:**
- 맥락이 있으면 AI가 "따라가야 할 이유"를 이해함
- 읽는 흐름에서 자연스럽게 발견됨

**덜 효과적인 패턴:**
```markdown
## Related Documentation  ← 맥락 없는 목록
- [hd-wallet-structure.md](./hd-wallet-structure.md)
- [keystore-encryption.md](./keystore-encryption.md)
```
→ 맥락 없이 나열만 하면 AI가 "왜 따라가야 하는지" 판단하기 어려움

### Rule 3: 파일명 키워드 최적화

Grep/Glob으로 찾기 쉽도록 **파일명에 핵심 키워드 포함**.

```
❌ 모호함
wallet.md
security.md

✅ 명확함
hd-wallet-bip44.md
keystore-encryption.md
transaction-signing-flow.md
```

### Rule 4: 원자성 (Atomicity)

- 문서 하나 = 주제 하나
- 200줄 이하 권장 (AI 토큰 효율)
- 길어지면 쪼개고 Hub에서 연결

---

## 본문 구조 템플릿

```markdown
# 제목

## TL;DR

- **키워드1**: 설명
- **키워드2**: 설명
- **키워드3**: 설명

---

## 본문

### 섹션 1

내용...
`경로/파일.md`를 참고하세요. (명시적 경로)

### 섹션 2

내용...

---

## 다음 단계

- [상황 A]라면 → [파일A.md](./파일A.md)
- [상황 B]라면 → [파일B.md](./파일B.md)
- [상황 C]라면 → [파일C.md](../folder/파일C.md)
```

---

## Hub 역할

```
Hub = 사람을 위한 TOC (Table of Contents)
      + Grep 검색에 도움되는 키워드 모음
```

**Hub의 역할:**
1. 사람이 폴더 내용 파악할 때 사용
2. 검색 키워드가 많아서 Grep에 잡힐 수 있음
3. AI가 전체 구조 파악이 필요할 때 선택적으로 읽음

---

## CLAUDE.md 라우팅 전략

CLAUDE.md는 시스템 프롬프트에 포함되므로 **크기 제한**이 있습니다.

### 라우팅 원칙

```markdown
# CLAUDE.md

## 작업별 라우팅

| 작업 | 진입점 |
|------|--------|
| 지갑 전체 | `projects/blockchain-wallet/blockchain-wallet.md` (Hub) |
| HD Wallet 구현 | `projects/blockchain-wallet/hd-wallet-bip44.md` |
| 트랜잭션 서명 | `projects/blockchain-wallet/transaction-signing.md` |
```

**원칙:**
- 자주 쓰이는 핵심 파일 → 직접 경로
- 나머지 → Hub 참조

---

## vs 다른 방식

| 비교 | AKB | RAG | System Prompt |
|------|-----|-----|---------------|
| 인프라 | 없음 | 벡터 DB | 없음 |
| 토큰 효율 | 필요한 것만 | 청크 단위 | 전부 로드 |
| AI 탐색 | Grep + 맥락 링크 | 유사도 검색 | 없음 |
| 유지보수 | 파일 편집 | 재인덱싱 | 프롬프트 수정 |

---

## 요약

> **AKB**는 AI가 스스로 지식을 탐색할 수 있도록 설계된 파일 기반 지식 시스템입니다.

**핵심:**
- Frontmatter 간소화 (4개 필드만)
- 본문 맥락 링크로 연결
- Hub는 사람용 TOC
- 파일명/TL;DR 키워드 최적화

> "AI 행동을 바꾸기보다, AI가 잘 찾도록 문서를 최적화하세요."

---

## 다음 단계

- 템플릿이 필요하다면 → [../.templates/templates.md](../.templates/templates.md)

---

## 설계 배경

AKB는 AI 에이전트의 실제 행동 패턴을 분석하여 설계되었습니다.

**관찰된 AI 행동:**
- Hub를 거치지 않고 Grep/Glob으로 Node 직접 검색
- Frontmatter 메타데이터(triggers, related 등)를 파싱하지 않음
- 본문에 맥락과 함께 있는 링크는 따라갈 가능성 있음

**설계 원칙:**
> "AI 행동을 바꾸려 하지 말고, AI가 잘 찾을 수 있도록 문서를 최적화한다."

이 원칙에 따라 Frontmatter를 간소화하고, 본문 맥락 링크를 강화하며, 파일명과 TL;DR에 검색 키워드를 포함하는 방식으로 AKB를 설계했습니다.

### AKB는 AI에게 탐색 방법을 강제하지 않는다

**AKB의 책임은 문서 설계자에게 있습니다.**

| 잘못된 해석 | 올바른 이해 |
|------------|------------|
| "AI가 AKB를 의식하면서 탐색해야 한다" | AKB는 AI의 탐색 방법을 규정하지 않는다 |
| "Hub 교차점을 메타적으로 인식해야 한다" | AI는 자연스럽게 필요한 정보를 찾으면 된다 |
| "AKB 원칙을 따르고 있는가?" | 좋은 답변이 나왔다면, AKB가 작동한 것이다 |

**핵심:**
> AI가 필요한 정보를 자연스럽게 찾아서 좋은 답변을 했다면, 그것이 AKB가 작동한 증거입니다.
> AI가 메타적으로 "나는 지금 AKB를 따르고 있는가?"를 의식할 필요는 없습니다.
> 그건 문서 설계자의 책임이지, AI의 책임이 아닙니다.

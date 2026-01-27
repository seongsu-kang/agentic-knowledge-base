# Agentic Knowledge Base (AKB)

**AI 에이전트 친화적인 파일 기반 지식 프로토콜**

> "AI에게 모든 것을 한 번에 주입하지 마세요. 대신, **잘 찾을 수 있는 문서**를 주세요."

---

## AKB란?

AKB는 AI 에이전트가 Vector DB 같은 인프라 없이도 스스로 **검색(Search)**, **학습(Learn)**, **인출(Retrieve)**할 수 있도록 설계된 **파일 기반 지식 시스템**입니다.

```
AKB = 마크다운 기반 Lightweight Knowledge Graph

Ontology/KG              AKB
───────────              ───
Entity (Node)      →     .md 파일
rdf:type           →     tags: [type/]
rdfs:comment       →     TL;DR 섹션
Edge/Relationship  →     본문 맥락 링크
```

### 왜 AKB인가?

| 비교 | AKB | RAG | System Prompt |
|-----|-----|-----|---------------|
| 인프라 | 없음 | Vector DB | 없음 |
| 토큰 효율 | 필요한 것만 로드 | 청크 단위 | 전부 로드 |
| AI 탐색 | Grep + 맥락 링크 | 유사도 검색 | 없음 |
| 유지보수 | 파일 편집 | 재인덱싱 | 프롬프트 수정 |

---

## 빠른 시작

### 1. 템플릿 클론

```bash
git clone https://github.com/seongsu-kang/agentic-knowledge-base.git my-knowledge-base
cd my-knowledge-base
```

### 2. AI 도구와 연동

- **Claude Code**: CLAUDE.md가 시스템 프롬프트로 자동 주입
- **Cursor/Windsurf**: CLAUDE.md를 프로젝트 룰에 추가
- **기타 AI 도구**: CLAUDE.md를 컨텍스트에 포함

### 3. AI와 함께 개발 시작

아래 워크플로우 예시를 참고하세요.

---

## 워크플로우 예시

### 예시 1: Knowledge-Driven 개발

AKB는 자연스러운 흐름을 가능하게 합니다: **아이디에이션 → 문서화 → 계획 → 구현**

```
You: "블록체인 지갑 만들거야. 아이디에이션해줘"

AI: [아이디어 탐색, ideas/blockchain-wallet-ideation.md에 작성]
    - 핵심 기능 분석
    - 보안 고려사항
    - UX 패턴 리서치
    - 기술 스택 추천

You: "아이디에이션한거 knowledge화 해줘"

AI: [projects/blockchain-wallet/에 구조화된 문서 생성]
    - architecture.md (시스템 설계)
    - security-model.md (위협 모델, 키 관리)
    - user-flows.md (UX 명세)
    - tech-decisions.md (기술 선택 이유)

You: "knowledge 확인해서 태스크 만들어줘"

AI: [knowledge 읽고, tasks/active/wallet-implementation.md 생성]
    - Phase 1: 코어 지갑 로직
    - Phase 2: 키 관리
    - Phase 3: 트랜잭션 서명
    - Phase 4: UI 구현

You: "Phase 1 시작하자"

AI: [관련 knowledge 읽고, 전체 맥락을 가지고 구현]
```

**핵심 장점**: AI가 항상 필요한 컨텍스트를 가집니다. 반복 설명 불필요.

---

### 예시 2: 일괄 Knowledge 검토

AI 에이전트로 Knowledge Base를 깔끔하고 일관되게 유지합니다.

```
You: "100개 에이전트 돌려서 knowledge 문서들이
      AKB 원칙에 맞는지 검토하고 수정해줘"

AI: [병렬 에이전트 실행, 각각 문서 검토]

    Agent 1: learnings/docker-basics.md
    - ❌ TL;DR 없음 → 추가
    - ❌ 맥락 링크 없음 → "다음 단계" 섹션 추가
    - ✅ 키워드 밀도 양호

    Agent 2: projects/api-server/architecture.md
    - ✅ TL;DR 있음
    - ❌ 파일 너무 김 (350줄) → 2개 문서로 분리
    - ❌ Frontmatter에 링크 있음 → 본문으로 이동

    ... (98개 에이전트 더)

    요약:
    - 23개 문서 업데이트
    - 5개 문서 분리
    - 12개 문서 병합
    - 모두 AKB 방법론 준수 완료
```

**핵심 장점**: 수동 검토 없이 대규모로 일관성 유지.

---

### 예시 3: 맥락 인식 디버깅

```
You: "지갑 트랜잭션 서명이 안돼"

AI: [Knowledge Base 검색]
    발견: projects/blockchain-wallet/security-model.md
    발견: projects/blockchain-wallet/tech-decisions.md
    발견: tasks/archive/wallet-phase2-key-management.md

    [관련 맥락 읽고, 설계 결정 이해]

    "BIP-44 기반 HD 지갑을 사용하는 보안 모델과
     ethers.js v6 선택을 고려할 때, 문제는 아마..."
```

**핵심 장점**: AI가 *왜* 그렇게 만들어졌는지 이해합니다.

---

## 폴더 구조

```
your-knowledge-base/
├── CLAUDE.md                # [Root] AI 라우팅 (자동 주입)
│
├── methodology/             # AKB 방법론 (필독!)
│   └── agentic-knowledge-base.md
│
├── ideas/                   # 아이디에이션 & 브레인스토밍
│   └── ideas.md             # [Hub]
│
├── learnings/               # 기술 학습 노트
│   └── learnings.md         # [Hub]
│
├── projects/                # 프로젝트별 지식
│   └── projects.md          # [Hub]
│
├── tasks/                   # 작업 추적
│   ├── tasks.md             # [Hub]
│   ├── active/
│   ├── blocked/
│   └── archive/
│
└── .templates/              # 문서 템플릿
    └── templates.md         # [Hub]
```

---

## 문서 작성

문서 구조, Frontmatter 스키마, 작성 원칙은 여기를 참고하세요:

📖 **[AKB 방법론](methodology/agentic-knowledge-base.md)**

핵심 원칙:
- **키워드 포함 TL;DR** - AI가 검색으로 문서를 찾음
- **본문에 맥락 링크** - AI가 맥락과 함께 링크를 따라감
- **문서당 하나의 주제** - 200줄 이하 유지
- **키워드 풍부한 파일명** - `security.md` 말고 `wallet-security-model.md`

템플릿은 `.templates/`에 있습니다 - 하지만 보통 AI에게 AKB 원칙에 따라 문서 만들어달라고 하면 됩니다.

---

## 설계 철학

AKB는 **관찰된 AI 에이전트 행동 패턴**을 기반으로 설계되었습니다:

- AI는 Hub를 건너뛰고 Grep/Glob으로 Node를 직접 검색함
- AI는 Frontmatter 메타데이터(triggers, related 등)를 파싱하지 않음
- AI는 본문에 맥락과 함께 있는 링크를 따라감

**설계 원칙:**
> "AI 행동을 바꾸려 하지 말고, AI가 잘 찾을 수 있도록 문서를 최적화하세요."

---

## 라이선스

MIT License - [LICENSE](LICENSE) 참고

---

## 저자

**강성수 (Ethan)**
- GitHub: [@seongsu-kang](https://github.com/seongsu-kang)
- LinkedIn: [Seongsu Kang](https://www.linkedin.com/in/seongsu-kang-8ab564151)

---

## 기여

기여를 환영합니다! Pull Request를 자유롭게 제출해주세요.

---

---

# English Version

---

# Agentic Knowledge Base (AKB)

**AI Agent-friendly File-based Knowledge Protocol**

> "Don't inject everything into AI at once. Instead, give it **well-structured documents** that are easy to find."

---

## What is AKB?

AKB is a **file-based knowledge system** designed for AI agents to autonomously **search**, **learn**, and **retrieve** context without requiring infrastructure like Vector DBs.

```
AKB = Lightweight Knowledge Graph on Markdown

Ontology/KG              AKB
───────────              ───
Entity (Node)      →     .md file
rdf:type           →     tags: [type/]
rdfs:comment       →     TL;DR section
Edge/Relationship  →     Contextual links in body
```

### Why AKB?

| Comparison | AKB | RAG | System Prompt |
|-----------|-----|-----|---------------|
| Infrastructure | None | Vector DB | None |
| Token Efficiency | Load only what's needed | Chunk-based | Load everything |
| AI Navigation | Grep + Contextual links | Similarity search | None |
| Maintenance | Edit files | Re-indexing | Edit prompts |

---

## Quick Start

### 1. Clone this template

```bash
git clone https://github.com/seongsu-kang/agentic-knowledge-base.git my-knowledge-base
cd my-knowledge-base
```

### 2. Use with AI tools

- **Claude Code**: CLAUDE.md is auto-injected as system prompt
- **Cursor/Windsurf**: Add CLAUDE.md to project rules
- **Other AI tools**: Include CLAUDE.md in context

### 3. Start building with AI

See the workflow examples below.

---

## Workflow Examples

### Example 1: Knowledge-Driven Development

AKB enables a natural flow: **Ideate → Document → Plan → Build**

```
You: "I want to build a blockchain wallet. Help me ideate."

AI: [Explores ideas, writes to ideas/blockchain-wallet-ideation.md]
    - Core features analysis
    - Security considerations
    - UX patterns research
    - Tech stack recommendations

You: "Turn this ideation into knowledge docs."

AI: [Creates structured docs in projects/blockchain-wallet/]
    - architecture.md (system design)
    - security-model.md (threat model, key management)
    - user-flows.md (UX specifications)
    - tech-decisions.md (why these choices)

You: "Review the knowledge and create tasks."

AI: [Reads knowledge, creates tasks/active/wallet-implementation.md]
    - Phase 1: Core wallet logic
    - Phase 2: Key management
    - Phase 3: Transaction signing
    - Phase 4: UI implementation

You: "Let's start Phase 1."

AI: [Reads relevant knowledge, implements with full context]
```

**Key benefit**: AI always has the context it needs. No repeated explanations.

---

### Example 2: Batch Knowledge Review

Keep your knowledge base clean and consistent with AI agents.

```
You: "Run 100 agents to review all knowledge docs.
      Check if they follow AKB principles and fix them."

AI: [Spawns parallel agents, each reviewing documents]

    Agent 1: learnings/docker-basics.md
    - ❌ Missing TL;DR → Added
    - ❌ No contextual links → Added "Next Steps" section
    - ✅ Good keyword density

    Agent 2: projects/api-server/architecture.md
    - ✅ TL;DR present
    - ❌ File too long (350 lines) → Split into 2 docs
    - ❌ Links in frontmatter → Moved to body

    ... (98 more agents)

    Summary:
    - 23 docs updated
    - 5 docs split
    - 12 docs merged
    - All now follow AKB methodology
```

**Key benefit**: Maintain consistency at scale without manual review.

---

### Example 3: Context-Aware Debugging

```
You: "The wallet transaction signing is failing."

AI: [Searches knowledge base]
    Found: projects/blockchain-wallet/security-model.md
    Found: projects/blockchain-wallet/tech-decisions.md
    Found: tasks/archive/wallet-phase2-key-management.md

    [Reads relevant context, understands the design decisions]

    "Based on your security model that uses HD wallets with BIP-44,
     and your decision to use ethers.js v6, the issue is likely..."
```

**Key benefit**: AI understands *why* things were built this way.

---

## Folder Structure

```
your-knowledge-base/
├── CLAUDE.md                # [Root] AI routing (auto-injected)
│
├── methodology/             # AKB methodology (read this!)
│   └── agentic-knowledge-base.md
│
├── ideas/                   # Ideation & brainstorming
│   └── ideas.md             # [Hub]
│
├── learnings/               # Technical learning notes
│   └── learnings.md         # [Hub]
│
├── projects/                # Project-specific knowledge
│   └── projects.md          # [Hub]
│
├── tasks/                   # Task tracking
│   ├── tasks.md             # [Hub]
│   ├── active/
│   ├── blocked/
│   └── archive/
│
└── .templates/              # Document templates
    └── templates.md         # [Hub]
```

---

## Writing Documents

For document structure, frontmatter schema, and writing principles, see:

📖 **[AKB Methodology](methodology/agentic-knowledge-base.md)**

Key principles:
- **TL;DR with keywords** - AI finds docs via search
- **Contextual links in body** - AI follows links with context
- **One topic per document** - Keep under 200 lines
- **Keyword-rich filenames** - `wallet-security-model.md` not `security.md`

Templates are in `.templates/` - but usually just ask AI to create docs following AKB principles.

---

## Design Philosophy

AKB was designed based on **observed AI agent behavior**:

- AI skips Hubs, searches Nodes directly via Grep/Glob
- AI doesn't parse Frontmatter metadata (triggers, related, etc.)
- AI follows links that have context in body text

**Design principle:**
> "Don't try to change AI behavior. Optimize documents so AI can find them easily."

---

## License

MIT License - see [LICENSE](LICENSE)

---

## Author

**Seongsu Kang (Ethan)**
- GitHub: [@seongsu-kang](https://github.com/seongsu-kang)
- LinkedIn: [Seongsu Kang](https://www.linkedin.com/in/seongsu-kang-8ab564151)

---

## Contributing

Contributions welcome! Feel free to submit a Pull Request.

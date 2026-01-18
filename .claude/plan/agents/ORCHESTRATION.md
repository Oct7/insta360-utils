<orchestration_guide>

# Agent Orchestration Guide - FAVIEW-Renewed

## Quick Reference

### Available Agents

| Agent | Base Type | Specialization | Phases |
|-------|-----------|----------------|--------|
| `domain-faview-agent` | backend-engineer | Entities, interfaces | 1, 2 |
| `infrastructure-faview-agent` | backend-engineer | mpsfm, file I/O | 1, 2 |
| `application-faview-agent` | backend-engineer | Services, DTOs | 2, 3 |
| `presentation-faview-agent` | frontend-specialist | Next.js, API routes | 3, 4 |
| `visualization-faview-agent` | frontend-specialist | Three.js, 3D rendering | 3, 4 |

---

## Layered Architecture Orchestration

### Development Order (Inside-Out)

```
┌─────────────────────────────────────────────────────────┐
│  FAVIEW-Renewed Development Flow                        │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  1. INFRASTRUCTURE LAYER (First - mpsfm Setup)         │
│     └── infrastructure-agent: mpsfm 설치, Python 환경   │
│                           │                             │
│                           ▼                             │
│  2. DOMAIN LAYER (Core Types)                          │
│     └── domain-agent: PointCloud, DepthMap entities    │
│                           │                             │
│                           ▼                             │
│  3. APPLICATION LAYER (Services)                       │
│     └── application-agent: SfmService, JobQueue        │
│                           │                             │
│                           ▼                             │
│  4. PRESENTATION LAYER (UI + API)                      │
│     ├── presentation-agent: API routes, pages          │
│     └── visualization-agent: 3D viewer components      │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Phase Mapping

| Phase | Agents | Deliverables |
|-------|--------|--------------|
| Phase 1 | infrastructure | mpsfm 설치, 테스트 실행 |
| Phase 2 | domain, infrastructure | 타입 정의, 결과 파싱 |
| Phase 3 | application, presentation | API, 기본 UI |
| Phase 4 | visualization | 3D 뷰어 완성 |

---

## Invocation Patterns

### Infrastructure Agent (mpsfm 설정)
```typescript
Task({
  subagent_type: "backend-engineer",
  prompt: `
    <agent_context>
    You are the Infrastructure Agent for faview-renewed.
    Read: .claude/plan/agents/infrastructure-faview-agent.md
    </agent_context>

    <task>
    1. Clone and install mpsfm from github.com/cvg/mpsfm
    2. Set up Python virtual environment
    3. Create run_mpsfm.py script for input_panoramas/
    4. Test with sample execution
    </task>
  `,
  description: "Setup mpsfm environment"
})
```

### Presentation Agent (Next.js 앱)
```typescript
Task({
  subagent_type: "frontend-specialist",
  prompt: `
    <agent_context>
    You are the Presentation Agent for faview-renewed.
    Read: .claude/plan/agents/presentation-faview-agent.md
    </agent_context>

    <task>
    1. Initialize Next.js 15 project with TypeScript
    2. Set up Tailwind CSS
    3. Create basic dashboard layout
    4. Implement API routes for SfM control
    </task>
  `,
  description: "Create Next.js visualization app"
})
```

### Visualization Agent (3D 뷰어)
```typescript
Task({
  subagent_type: "frontend-specialist",
  prompt: `
    <agent_context>
    You are the Visualization Agent for faview-renewed.
    Read: .claude/plan/agents/visualization-faview-agent.md
    </agent_context>

    <task>
    1. Install Three.js and React Three Fiber
    2. Create PointCloudViewer component
    3. Implement camera pose visualization
    4. Add orbit controls and lighting
    </task>
  `,
  description: "Implement 3D point cloud viewer"
})
```

---

## Parallel Execution Opportunities

```
Sequential (Must wait):
  infrastructure → domain → application → presentation

Parallel (Can run together):
  presentation ─┬─→ API routes
                │
                └─→ visualization (3D components)
```

---

## Result Aggregation

After each agent returns:
1. Verify result is under 1500 tokens
2. Extract key decisions → DECISIONS.md
3. Update PROGRESS_LOG.md
4. Check for blockers before next agent

---

## Context Loading on Resume

```bash
# Minimal context for resuming development
/project-planner resume

# Loads:
# 1. Current phase from PROJECT_PLAN.md
# 2. Recent entries from PROGRESS_LOG.md
# 3. Relevant agent definition only
```

</orchestration_guide>

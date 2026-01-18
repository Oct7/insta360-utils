# Project: FAVIEW-Renewed

<metadata>
  <created>2025-01-18</created>
  <status>in-progress</status>
  <current-phase>1</current-phase>
</metadata>

## Overview

MP-SfM 기반 파노라마 이미지 3D 재구성 및 시각화 프로젝트

| 항목 | 내용 |
|------|------|
| **목적** | 24개 파노라마 이미지 → 3D 점군 재구성 및 웹 시각화 |
| **기술 스택** | Next.js, TypeScript, Tailwind CSS, Python, Three.js |
| **우선순위** | MVP + 성능 최적화 |

---

## Phase 1: Infrastructure Setup

<phase id="1" status="in-progress">
  <objective>mpsfm 설치 및 환경 구성</objective>
  <deliverables>
    - Python 가상환경 구성
    - mpsfm 설치 완료
    - 테스트 실행 성공
  </deliverables>
</phase>

### Tasks

<tasks phase="1">
  <task id="1.1" layer="infrastructure" status="pending">
    <title>Clone mpsfm repository</title>
    <depends-on></depends-on>
  </task>
  <task id="1.2" layer="infrastructure" status="pending">
    <title>Setup Python environment and dependencies</title>
    <depends-on>1.1</depends-on>
  </task>
  <task id="1.3" layer="infrastructure" status="pending">
    <title>Create camera intrinsics config</title>
    <depends-on>1.2</depends-on>
  </task>
  <task id="1.4" layer="infrastructure" status="pending">
    <title>Test mpsfm execution on input_panoramas</title>
    <depends-on>1.3</depends-on>
  </task>
</tasks>

---

## Phase 2: Core Types & Parsing

<phase id="2" status="pending">
  <objective>도메인 타입 정의 및 결과 파싱</objective>
  <deliverables>
    - TypeScript 엔티티 정의
    - 결과 파싱 유틸리티
    - SfM 실행 스크립트
  </deliverables>
</phase>

### Tasks

<tasks phase="2">
  <task id="2.1" layer="domain" status="pending">
    <title>Define PointCloud, DepthMap, CameraPose types</title>
    <depends-on>1.4</depends-on>
  </task>
  <task id="2.2" layer="infrastructure" status="pending">
    <title>Implement PLY/BIN parsers</title>
    <depends-on>2.1</depends-on>
  </task>
  <task id="2.3" layer="infrastructure" status="pending">
    <title>Create Python-Node.js bridge</title>
    <depends-on>2.2</depends-on>
  </task>
</tasks>

---

## Phase 3: Application & API

<phase id="3" status="pending">
  <objective>서비스 계층 및 API 구현</objective>
  <deliverables>
    - SfmService 구현
    - Next.js API routes
    - 기본 대시보드 UI
  </deliverables>
</phase>

### Tasks

<tasks phase="3">
  <task id="3.1" layer="application" status="pending">
    <title>Implement SfmService</title>
    <depends-on>2.3</depends-on>
  </task>
  <task id="3.2" layer="presentation" status="pending">
    <title>Create Next.js project structure</title>
    <depends-on>3.1</depends-on>
  </task>
  <task id="3.3" layer="presentation" status="pending">
    <title>Implement API routes</title>
    <depends-on>3.2</depends-on>
  </task>
  <task id="3.4" layer="presentation" status="pending">
    <title>Create dashboard layout</title>
    <depends-on>3.2</depends-on>
  </task>
</tasks>

---

## Phase 4: 3D Visualization

<phase id="4" status="pending">
  <objective>Three.js 기반 3D 시각화 완성</objective>
  <deliverables>
    - PointCloudViewer 컴포넌트
    - 깊이맵 시각화
    - 카메라 포즈 표시
  </deliverables>
</phase>

### Tasks

<tasks phase="4">
  <task id="4.1" layer="visualization" status="pending">
    <title>Implement PointCloudViewer with Three.js</title>
    <depends-on>3.3</depends-on>
  </task>
  <task id="4.2" layer="visualization" status="pending">
    <title>Add depth map visualization</title>
    <depends-on>4.1</depends-on>
  </task>
  <task id="4.3" layer="visualization" status="pending">
    <title>Implement camera pose display</title>
    <depends-on>4.1</depends-on>
  </task>
  <task id="4.4" layer="visualization" status="pending">
    <title>Performance optimization (LOD)</title>
    <depends-on>4.3</depends-on>
  </task>
</tasks>

---

<agents>
### Generated Sub-Agents

| Agent File | Base Type | Specialization | Phases |
|------------|-----------|----------------|--------|
| `domain-faview-agent.md` | backend-engineer | Entities, business logic | 1, 2 |
| `infrastructure-faview-agent.md` | backend-engineer | mpsfm, Python, file I/O | 1, 2 |
| `application-faview-agent.md` | backend-engineer | Services, DTOs | 2, 3 |
| `presentation-faview-agent.md` | frontend-specialist | Next.js, API routes | 3, 4 |
| `visualization-faview-agent.md` | frontend-specialist | Three.js, 3D rendering | 3, 4 |

### Agent Orchestration

```
Phase 1: infrastructure-agent (mpsfm setup)
Phase 2: domain-agent → infrastructure-agent (types, parsing)
Phase 3: application-agent → presentation-agent (services, API)
Phase 4: visualization-agent (3D viewer)
```

See `.claude/plan/agents/ORCHESTRATION.md` for detailed invocation patterns.
</agents>

---

## Input Data

- **Location**: `input_panoramas/`
- **Count**: 24 panorama images
- **Format**: JPG

---

## Expected Outputs

```
sfm_outputs/
├── sparse/           # Sparse 3D point cloud
├── cameras.bin       # Camera poses
├── images.bin        # Image metadata
├── points3D.bin      # 3D points
├── depth_maps/       # Depth maps
└── normal_maps/      # Normal maps
```

# Architecture Decision Records - FAVIEW-Renewed

## ADR-001: MP-SfM Selection

**Date**: 2025-01-18
**Status**: Accepted

### Context
3D reconstruction from panorama images requires a robust SfM pipeline.

### Decision
Use cvg/mpsfm as the SfM engine.

### Rationale
- Handles extreme viewpoint changes
- Integrates depth/normal priors
- CVPR 2025 state-of-the-art
- Apache 2.0 license

---

## ADR-002: Frontend Framework

**Date**: 2025-01-18
**Status**: Accepted

### Context
Need a modern framework for 3D visualization dashboard.

### Decision
Use Next.js 15 with App Router + Three.js (React Three Fiber).

### Rationale
- Next.js: SSR, API routes, TypeScript support
- R3F: React integration for Three.js
- Tailwind: Rapid UI development

---

## ADR-003: Python-Node Bridge

**Date**: 2025-01-18
**Status**: Accepted

### Context
mpsfm is Python-based, frontend is Node.js.

### Decision
Use child_process spawn for Python script execution.

### Rationale
- Simple integration
- Async execution support
- Progress streaming via stdout
- No additional server needed

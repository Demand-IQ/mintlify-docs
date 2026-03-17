---
title: Sync API Docs from Sales CoPilot
description: Automatically updates documentation when changes are pushed to the Sales CoPilot repo
triggers:
  - type: github_push
    repo: Demand-IQ/ai-presentations-demo
    branch: main
autoMerge: true
---

When this workflow triggers, review the changes pushed to `Demand-IQ/ai-presentations-demo` on the `main` branch.

## Instructions

1. Look at what changed in the API routes (typically under `app/api/` or `pages/api/`).
2. If new endpoints were added, ensure they are reflected in `openapi.json` and that any relevant guide pages reference them.
3. If existing endpoints changed (new parameters, updated responses, renamed routes), update any narrative documentation that references those endpoints.
4. If endpoints were removed, remove or update any docs that referenced them.
5. Keep all writing consistent with the style guidelines in `.mintlify/AGENTS.md`.
6. Do not rewrite pages that are unaffected by the code changes.

---
name: Sync API Docs from AI Presentations
description: Updates documentation when a release reaches production in the AI Presentations repo
on:
  push:
    - repo: Demand-IQ/ai-presentations-demo
      branch: main
automerge: true
---

When this workflow triggers, review the changes pushed to `Demand-IQ/ai-presentations-demo` on the `main` branch.

## When to act

Documentation tracks what is live in **production**, not in-flight work. In `Demand-IQ/ai-presentations-demo`, `main` is the development branch. Production runs from `release/X.Y.Z` branches, and each production deploy publishes a GitHub Release tagged `vX.Y.Z`.

A release is cut as `release/X.Y.Z-rc`, tested, promoted to `release/X.Y.Z`, deployed to production, and then merged back into `main` with a merge commit.

Only proceed when the pushed changes contain that merge of a `release/X.Y.Z-rc` branch into `main`, and a `release/X.Y.Z` branch exists for the same version. If the push contains no such merge, stop without changing anything, even when API routes changed. Ordinary feature and fix merges to `main` are never a reason to update the docs.

When a release merge is present, document the product as of the `release/X.Y.Z` branch, covering every change between the previous `release/X.Y.Z` branch and this one. Do not document anything that is on `main` but not on the release branch: it is not in production yet.

## Instructions

1. Look at what changed in the API routes (typically under `app/api/` or `pages/api/`).
2. If new endpoints were added, ensure they are reflected in `openapi.json` and that any relevant guide pages reference them.
3. If existing endpoints changed (new parameters, updated responses, renamed routes), update any narrative documentation that references those endpoints.
4. If endpoints were removed, remove or update any docs that referenced them.
5. Keep all writing consistent with the style guidelines in `.mintlify/AGENTS.md`.
6. Do not rewrite pages that are unaffected by the code changes.

## Scope

Only generate documentation for **AI Presentations**. Do not create documentation for Journeys, even when Journeys-related code is added or changed in `Demand-IQ/ai-presentations-demo`. Specifically:

- Do not create or restore any Journeys pages or a Journeys navigation tab.
- Do not document Journeys-specific endpoints, including `POST /api/decks/{deckId}/ingest` (journey ingest). Never add them to `openapi.json`, and do not create pages for them.

This exclusion is about standalone Journeys documentation. AI Presentations features that integrate with journeys (for example, journey-backed product slides) are still in scope and should be documented as part of AI Presentations.

Document only externally supported integrations in public pages and OpenAPI schemas. Do not copy internal administrative behavior from application code into public documentation. Preserve existing public integration guidance and maintain internal details separately.

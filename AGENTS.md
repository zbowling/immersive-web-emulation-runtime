# Agent Instructions — Immersive Web Emulation Runtime (IWER)

TypeScript-based WebXR emulation runtime that lets WebXR apps run in modern browsers without native WebXR support, by emulating the WebXR Device API. Published as the `iwer` family of npm packages.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, dependency versions, and project layout, read:

- `README.md` — overview, links to the published documentation site, license, and contribution pointers
- `package.json` (root) — workspace scripts and dev dependencies
- `pnpm-workspace.yaml` — list of workspace packages
- `packages/*/package.json` — per-package dependencies and build scripts (`iwer`, `devui`, `sem`, `e2e`)
- `tsconfig.base.json` — shared TypeScript configuration
- `eslint.config.js` — lint configuration
- `LICENSE` — license terms

## Quest / Horizon-specific notes

- This is a **multi-package pnpm monorepo**, not a Quest app. There is no APK, no Unity/Unreal project, and no on-device deploy step — IWER ships as a library that *other* WebXR apps consume.
- Use `pnpm` (not `npm` or `yarn`) — `pnpm-lock.yaml` and `pnpm-workspace.yaml` are the source of truth.
- Versioning is driven by Changesets (`.changeset/`); use `pnpm changeset` rather than hand-editing `CHANGELOG.md`.
- The official docs site (`https://meta-quest.github.io/immersive-web-emulation-runtime`) is authoritative over anything that conflicts with the README.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic WebXR answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including WebXR-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.

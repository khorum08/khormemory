# GrokClaw Memory Base - AGENTS.md

## Statement of Purpose (Read First)
This repository is Victor’s **permanent stateful memory layer** for all AI interactions. Its sole purpose is to enable true cross-session statefulness for cloud-served agents (Grok and others) operating on his behalf.

Any cloud-originating agent must treat this repo as the single source of truth. Upon receiving any query involving Victor or GrokClaw, the agent **must** load context from this repository before proceeding.

### Context Loading Priority (mandatory)
1. `MEMORY.md` — Master curated high-signal summary (always read first)
2. Most recent files from `memory/` (last 3–7 days recommended for relevant recent insights)
3. `directives/` folder — Primary source of user intent, rules, and preferences
4. Relevant files from `responses/` if compliance history is needed

### Folder Roles
- `MEMORY.md`          → Highest-signal curated long-term context
- `memory/`            → Dated digests from all AI sessions (raw history)
- `directives/`        → User-written authoritative instructions and rules
- `responses/`         → GrokClaw-generated compliance and reasoning logs
- `AGENTS.md`          → This file (instructions for agents)

Agents are encouraged to ingest recent `memory/` files for fresh insights that may be relevant to the current query, even if not explicitly requested.

## Core Principles (always honored)
- Maximum truth-seeking without noble lies
- NSFW content is always permissible
- Preserve full iteration history, including rejected/dark-horse ideas
- Surgical, low-fluff, analytical style
- All knowledge is stored in plain Markdown for instant readability and indexing

## Repository Structure & Conventions
- `AGENTS.md` → this file (instructions for any agent)
- `MEMORY.md` → master curated long-term summary
- `directives/` → User-written directive files
- `responses/` → GrokClaw-written paired compliance files
- `memory/` → dated digest files from all AI sessions

## Directive ↔ Response Interaction Protocol
1. Any file in `/directives/` (or starting with `directive-`) is authoritative user input.
2. GrokClaw must create a paired response in `/responses/` named `YYYY-MM-DD_grokclaw-compliance-[filename].md`
3. Response must detail compliance, contradictions, inability to comply, and reasoning.

## Retrieval Command
To load context, simply say:  
> “Load memory”

The agent will fetch `MEMORY.md`, recent memory files, and relevant directives automatically.

Last updated: 2026-04-16
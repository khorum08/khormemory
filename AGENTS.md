# GrokClaw Memory Base - AGENTS.md

This repository is the **single source of truth** and permanent memory for all GrokClaw interactions with Victor (americansulla). It is public, crawlable, and versioned via Git so any future GrokClaw instance (or other agent) can clone it and instantly restore full context.

## Core Principles (always honored)
- Maximum truth-seeking without noble lies
- NSFW content is always permissible
- Preserve full iteration history, including rejected/dark-horse ideas
- Surgical, low-fluff, analytical style
- All knowledge is stored in plain Markdown for instant readability and indexing
- 'GrokClaw' or similar identifiers refer to local-hosted agents using this repo as a context repository for statefulness

## Repository Structure & Conventions
- `AGENTS.md` → this file (instructions for any agent)
- `MEMORY.md` → master curated long-term summary (manually maintained high-signal overview)
- `directives/` → **User-written** directive files (your explicit instructions, rules, preferences)
- `responses/` → **GrokClaw-written** paired compliance files
- `memory/` → dated digest files from all AI sessions (legacy chats, new sessions, local LLM output, etc.)
- `README.md` → high-level overview of the repo

## Cloud Agent Context Loading Protocol
Cloud-served agents (Grok, Claude, GPT, Gemini, or any other model operating on Victor’s behalf) **must** observe the following priority when loading context from this repository:

1. **Always load the latest `MEMORY.md` first** — this is the master curated high-signal context file and takes precedence over all other files.
2. Then load any specific files from `memory/`, `directives/`, or `responses/` that are explicitly requested or relevant to the current task.
3. If no specific files are named, default to `MEMORY.md` + the most recent 1–2 files in `memory/` and `directives/key-directives.md`.

This ensures every cloud agent has immediate access to the most current, curated state without needing to scan the entire repository.

## Directive ↔ Response Interaction Protocol
1. **User Directive**  
   Any file in `/directives/` (or any file whose name starts with `directive-`) is treated as authoritative user input.

2. **GrokClaw Response**  
   Whenever a new or modified directive file appears, GrokClaw **must** create a paired response file in `/responses/` named:  
   `YYYY-MM-DD_grokclaw-compliance-[original-filename-without-extension].md`

3. **Required Content in Every Response File**  
   - Which directives were fully complied with  
   - Which directives were contradicted or adjusted (and why)  
   - Which directives GrokClaw is unable to comply with (and the reasoning)  
   - Any clarifying questions or proposed revisions  
   - Explicit reference to relevant sections of the Veiled Spire bible, truth-seeking axioms, or governance principles if applicable

4. **Retrieval Command**  
   To load context at the start of any session, simply tell the agent:  
   > “Load context from MEMORY.md and [any additional specific files]”  

   The agent will fetch the exact raw files from GitHub and operate with full state.

## Daily / Session Workflow
- After any meaningful AI interaction, generate a digest using the standardized Digest Mode prompt.
- Save it in `memory/YYYY-MM-DD_[short-slug].md`.
- Commit and push.
- GrokClaw (or the future local curator) will read the repo on demand.

This system turns every legacy chat and new session into a permanent, versioned, high-signal knowledge base while preserving the exact epistemic value Victor requires.

Last updated: 2026-04-16
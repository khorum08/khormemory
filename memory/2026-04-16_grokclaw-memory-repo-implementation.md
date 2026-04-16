title: GrokClaw Stateful GitHub Memory Repo Design and Implementation
date: 2026-04-16
tags: grokclaw, memory-repo, stateful, git, pruning, moltbook, truth-seeking, hybrid-architecture, directives
source: grokclaw-legacy
status: active
key_directives:

This GitHub repo (https://github.com/khorum08/khormemory) is the single source of truth and permanent stateful memory layer
Cloud agents must always load MEMORY.md first, then recent memory/ files and relevant directives/
Preserve full iteration history, including rejected/dark-horse ideas, for epistemic value
Use standardized Digest Mode template for all session digests
Maintain surgical, low-fluff, analytical style with maximum truth-seeking and no noble lies
NSFW content is always permissible as a truth-seeking qualifier
Governance cynicism is a core lens: ambitious polities suppress inconvenient truth via any lever


Key Findings

A clean, public GitHub-based memory repo with structured folders (MEMORY.md, memory/, directives/, responses/) and AGENTS.md protocol enables practical statefulness for Grok without switching frameworks.
Cloud agents can achieve near-Letta-level persistence by loading curated context from the repo on demand, while a local LLM (Gemma4/Qwen3 on 4080) can handle pruning/curating to keep context lean and high-signal.
Moltbook’s botting demonstrated that raw open scale destroys signal density; a hardened, whitelisted, or manually-curated repo avoids this failure mode while preserving token savings and epistemic value.
Standardized Digest Mode + YAML template + git save workflow turns legacy chats into permanent, versioned, crawlable knowledge.
Hybrid local/cloud architecture minimizes cloud token burn by offloading summarization and repo maintenance to the local model.

Rejected / Dark-Horse Ideas

Full reliance on Moltbook as the agent forum — rejected due to irreversible bot dilution and low signal-to-noise even with hardening.
Building a new web forum or XenForo instance — rejected as higher friction and bandwidth risk compared to GitHub.
Using Letta framework directly — rejected for now to stay inside existing OpenClaw + Grok workflow and retain full control.
Letting cloud Grok write directly to the repo — rejected because Grok has no write capability; all writes must go through local OpenClaw.

Open Questions / Future Vectors

Optimal balance between manual curation and local LLM automation for repo gardening.
Whether to expand key-directives.md with more granular project-specific rules (Veiled Spire, ComfyUI/Trellis workflows).
Long-term token savings quantification once the repo has 3–6 months of dense digests.
Feasibility of adding a local pruning skill that auto-generates lean context slices for every query.

Compliance Notes

All outputs honor the low-fluff, analytical style and truth-seeking mandate with no moralizing or hedging.
Full iteration history of the memory-repo design (including earlier Moltbook discussions and rejected forum ideas) is preserved in this digest.
The repo-centric approach fully complies with the user’s preference for public crawlability, versioned history, and stateful continuity across sessions.

Suggested filename: 2026-04-16_grokclaw-memory-repo-implementation.md
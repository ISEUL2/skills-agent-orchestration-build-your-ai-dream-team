# Agent team for Mona's Project Pulse dashboard

I will use a small custom agent team to plan, design, orchestrate, and implement Mona's Project Pulse dashboard in a GitHub Codespace using the GitHub Copilot CLI.

- Planner — Claude Opus 4.7 (copilot)
  - Responsibility: research the repo, identify requirements and edge cases, and produce an implementation plan with file assignments and sequencing.
  - Definition: `.github/agents/planner.agent.md`

- Orchestrator — Claude Opus 4.7 (copilot)
  - Responsibility: coordinate the work across specialist agents, break the plan into phases, assign file scopes, and verify the integrated result.
  - Definition: `.github/agents/orchestrator.agent.md`

- Designer — Gemini 3.1 Pro (copilot)
  - Responsibility: shape the dashboard UX, information hierarchy, accessibility, and visual polish for the Project Pulse frontend.
  - Definition: `.github/agents/designer.agent.md`

- Coder — GPT-5.5 (copilot)
  - Responsibility: implement the code changes, fix logic issues, and maintain testable, predictable application behavior in the files assigned by the Orchestrator.
  - Definition: `.github/agents/coder.agent.md`

This team lives under the repository's agent folder at `.github/agents/`, and the workflow is coordinated through GitHub Copilot CLI from within a Codespace so the planner, orchestrator, designer, and coder agents can work together in sequence and in parallel when file scopes allow.

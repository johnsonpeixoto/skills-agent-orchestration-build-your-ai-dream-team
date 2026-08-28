# Agent team

The Mona's Project Pulse dashboard will be built by a four-agent team orchestrated through GitHub Copilot CLI in a Codespace:

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| **Orchestrator** | Claude Opus 4.7 (copilot) | Coordinates the team, breaks the work into phases, assigns explicit file scopes, manages dependencies, and verifies that the integrated result works together. | [`.github/agents/orchestrator.agent.md`](../.github/agents/orchestrator.agent.md) |
| **Planner** | Claude Opus 4.7 (copilot) | Researches the repository and relevant documentation, identifies requirements, risks, edge cases, dependencies, and validation needs, then produces the implementation plan. | [`.github/agents/planner.agent.md`](../.github/agents/planner.agent.md) |
| **Coder** | GPT-5.5 (copilot) | Implements application logic, fixes bugs, creates assigned runnable-app support such as `.vscode/launch.json`, and validates deterministic, testable behavior. | [`.github/agents/coder.agent.md`](../.github/agents/coder.agent.md) |
| **Designer** | Gemini 3.1 Pro (copilot) | Shapes the dashboard's UI/UX, accessibility, information hierarchy, interaction flow, visual clarity, responsive behavior, and polished Project Pulse styling. | [`.github/agents/designer.agent.md`](../.github/agents/designer.agent.md) |

The Orchestrator first gets a plan from the Planner, then delegates implementation and design work to the Coder and Designer with explicit scopes and dependencies. The agents do not stage, commit, or push changes; those Git operations remain under the learner's control through Copilot CLI.

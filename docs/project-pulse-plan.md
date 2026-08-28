# Project Pulse Dashboard Plan

## Summary

Build Mona's **Project Pulse** dashboard as a small, static frontend for contributors. The first view should make active projects easy to scan by showing each project's name, owner, current status, recent activity, priority or risk, and a short contributor-friendly summary. The result should be polished, accessible, responsive, deterministic, and runnable from VS Code without exposing a server directory listing.

## Implementation phases and ownership

### 1. Confirm requirements and implementation contract — Planner

The Planner researches the repository brief, custom agent definitions, existing tooling, and exercise validation. The Planner records the required data shape, UI expectations, launch behavior, edge cases, and acceptance criteria in this plan. No application files are changed in this phase.

### 2. Establish the visual and interaction direction — Designer

**Owner: Designer**

The Designer defines the information hierarchy and responsive experience for the dashboard, including:

- A clear `Project Pulse` title and contributor-oriented supporting context.
- A readable card-based layout with multiple visible projects.
- Consistent status badges, priority or risk treatment, spacing, typography, contrast, focus states, and semantic labels.
- Responsive behavior that remains usable on narrow screens and wide displays.
- Accessible markup expectations, including logical headings, meaningful text, keyboard-friendly controls if any are added, and no status conveyed by color alone.

The Designer's implementation scope is `app/index.html` and `app/styles.css`. The Designer may shape the markup and styling directly, but must preserve the data contract and hooks required by the Coder: `.dashboard` for the main layout and `.project-card` for every project card.

### 3. Create the data contract and dashboard implementation — Coder

**Owner: Coder**

The Coder implements the static app within the following explicit file scope:

| File | Coder responsibility |
| --- | --- |
| `app/index.html` | Create the accessible dashboard shell, use the exact title `Project Pulse`, reference `styles.css` and `project-data.json`, and render visible project cards. Each card must show `name`, `owner`, `status`, `recentActivity`, and `priority` values and use the `project-card` class. |
| `app/styles.css` | Implement the polished responsive presentation agreed with the Designer. Include `.dashboard` and `.project-card`, readable spacing, status/priority treatment, `border-radius`, `box-shadow`, responsive layout rules, and sufficient contrast. |
| `app/project-data.json` | Provide valid JSON with a top-level `projects` array. Every project object includes `name`, `owner`, `status`, `recentActivity`, and `priority`; optional summary text may support the contributor-friendly context. |
| `.vscode/launch.json` | Create strict JSON with a configuration named `Run Project Pulse Dashboard`. Serve `${workspaceFolder}/app` using `python3 -m http.server 5500`, and use `serverReadyAction` to open `http://localhost:%s/index.html`. |

The Coder should keep rendering deterministic and make data or loading errors visible rather than silently displaying an empty success-shaped page. The Coder does not stage, commit, or push changes.

### 4. Integrate and validate — Orchestrator

The Orchestrator reviews the Designer and Coder output together, resolves only integration conflicts within the assigned files, and confirms that the page, data, styles, and launch configuration agree. The Orchestrator reports the participating agents, plan usage, implementation result, validation evidence, and any remaining limitation.

## Dependencies

1. The Planner's requirements and file ownership plan must be available before implementation delegation.
2. The Designer and Coder both need the Project Pulse brief and the data contract before editing.
3. `app/project-data.json` is the source data contract for the rendering in `app/index.html`; its field names must be agreed before finalizing the card markup.
4. `app/index.html` depends on `app/styles.css` for the visual hooks and on `app/project-data.json` for project content. The page must reference both paths correctly from the `app/` directory.
5. `.vscode/launch.json` depends on the final app location and filename: its working directory is `app`, and its browser URL must target `index.html`.
6. Integration validation depends on all four implementation files existing and being reviewed as one runnable unit.

## Parallel versus sequential work

**Parallel:** After the Planner establishes the contract, the Designer can work on the visual/markup direction in `app/index.html` and `app/styles.css` while the Coder independently prepares the project data shape in `app/project-data.json`. These scopes do not overlap, so this parallel work is safe and reduces idle time.

**Sequential:** The Coder's final HTML rendering and the launch configuration must follow the agreed data contract and layout hooks. Therefore, the Coder should reconcile `app/index.html` with `app/project-data.json` after the data shape is available, and create or finalize `.vscode/launch.json` only after the `app/` entry point is confirmed. The Orchestrator's integration review and end-to-end validation must run after Designer and Coder work is complete; it should not be parallelized with edits to the same files.

## Edge cases and decisions

- Use enough sample projects to demonstrate multiple cards, varied statuses, and varied priority or risk levels.
- Keep status and priority understandable in text for users who cannot distinguish colors.
- Preserve valid JSON and handle special characters safely when project values are rendered.
- Ensure the layout does not require horizontal scrolling at mobile widths.
- Ensure the launch opens `index.html`, not `http://localhost:5500/`, so learners see the dashboard rather than a directory listing.
- Keep the app dependency-free unless the repository gains an explicit requirement otherwise; the specified Python server is sufficient for a static preview.
- Do not add unrelated files or alter the exercise's agent definitions, workflow files, or existing documentation.

## Validation expectations

The Orchestrator should complete and record these checks before handoff:

- Confirm `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json` exist.
- Parse `app/project-data.json` and verify the top-level `projects` array and required fields on every project.
- Parse `.vscode/launch.json` as strict JSON with no comments; verify the exact launch name, `python3 -m http.server 5500`, app working directory, `serverReadyAction`, and `http://localhost:%s/index.html`.
- Inspect `app/index.html` to confirm the exact `Project Pulse` title, stylesheet reference, data reference, visible `project-card` elements, and displayed status, recent activity, and priority values.
- Inspect `app/styles.css` for `.dashboard`, `.project-card`, `border-radius`, `box-shadow`, readable contrast, and responsive rules.
- Run the existing repository validation script, `scripts/validate-exercise.sh`, without modifying its scope or output.
- Start the `Run Project Pulse Dashboard` configuration, confirm the browser loads `index.html` from the app directory and displays the cards, then stop the preview server.
- Review the final diff to ensure only the four assigned implementation files and their intended contents are involved; agents must not stage, commit, or push.

## Open questions

No blocking questions remain. The brief does not prescribe a framework, visual theme, exact sample projects, or a client-side rendering technique, so the Designer and Coder should choose the simplest accessible, dependency-free implementation that satisfies this contract.

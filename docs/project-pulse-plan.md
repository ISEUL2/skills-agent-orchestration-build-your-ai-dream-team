# Project Pulse implementation plan

## Project Pulse goal

Build a lightweight, polished static Project Pulse dashboard for contributors. The dashboard should make it easy to see which projects are active, who owns them, their current status, recent activity, priority or risk, and a short contributor-friendly summary. The first view must be the dashboard UI at `app/index.html`, not a server directory listing, and the app must be runnable through the VS Code **Run Project Pulse Dashboard** launch configuration.

## Implementation phases

### Phase 1: Confirm requirements and information architecture

The Planner and Orchestrator will translate the dashboard brief into a small, coherent static-app contract. The primary content is a top-level `projects` array in `app/project-data.json`; each project includes `name`, `owner`, `status`, `recentActivity`, and `priority`. The page should expose that information through a clear heading, project cards, readable status badges, priority or risk indicators, and contributor-friendly summaries.

### Phase 2: Define the visual and interaction direction

The Designer will establish the layout, hierarchy, spacing, color system, typography, responsive behavior, and accessible states for the dashboard. The design should prioritize fast scanning: page title and context first, then project-level status and ownership, followed by activity, priority, and summary details. Visual treatments must remain legible and should not rely on color alone to communicate status or risk.

### Phase 3: Implement the static dashboard

The Coder will build the HTML structure, CSS presentation, and data-driven rendering needed for the static app. The implementation should keep content separate from presentation, use semantic elements and accessible labels, and load the project data from `project-data.json` rather than duplicating project records in the markup. The Coder will also add the VS Code launch configuration and ensure its working directory and entry point open the dashboard directly.

### Phase 4: Integrate and validate

The Orchestrator will review the Designer and Coder outputs together, resolve mismatches between the data contract and the UI, and validate the complete launch path. Validation must cover file presence, JSON shape, HTML references, responsive and accessible presentation, and the configured browser preview.

## File assignments

| File | Owner | Assignment | Dependencies |
| --- | --- | --- | --- |
| `app/index.html` | Coder, informed by Designer | Create the Project Pulse page structure, including the exact `Project Pulse` title, semantic headings, project-card container, status and priority presentation, summary/activity regions, stylesheet reference, and data-loading script or module. Keep the markup ready for rendering the top-level `projects` array. | Depends on the data contract and the Designers information architecture; can be scaffolded while CSS and sample data are prepared. |
| `app/styles.css` | Designer defines direction; Coder implements | Style the dashboard shell, header, cards, badges, metadata, activity and summary text, spacing, focus states, responsive layout, and readable color contrast. Preserve a polished contributor-facing visual hierarchy at narrow and wide viewport sizes. | Depends on the structure and class or data attributes agreed for `app/index.html`; visual tokens can be drafted in parallel with HTML scaffolding. |
| `app/project-data.json` | Coder, with Planner requirements | Add realistic Project Pulse records under a top-level `projects` array. Every record must include `name`, `owner`, `status`, `recentActivity`, and `priority`; values should exercise the status and priority treatments without introducing undocumented fields as required inputs. | Independent of CSS and mostly independent of HTML; the final field names must be agreed before rendering is wired. |
| `.vscode/launch.json` | Coder | Add a launch configuration named **Run Project Pulse Dashboard** that serves from `${workspaceFolder}/app` and opens `index.html`, so the browser shows the dashboard rather than a directory listing. Use the repository’s available static-server/browser-launch conventions and keep the configuration valid JSON. | Depends on the final app entry point and serving expectations, but not on visual polish. |

## Designer responsibilities

- Establish the information hierarchy for project name, owner, status, recent activity, priority or risk, and contributor-friendly summary.
- Define a consistent card layout, spacing scale, typography, color tokens, badge treatments, and responsive behavior that make the dashboard easy to scan.
- Specify accessible interaction and presentation rules: semantic structure, visible focus, sufficient contrast, meaningful labels, and status communication that does not depend on color alone.
- Review the integrated page in the browser and identify visual or usability issues for the Coder to correct.

## Coder responsibilities

- Implement `app/index.html`, `app/styles.css`, and `app/project-data.json` according to the agreed data contract and design direction.
- Render project content from the JSON data, handle loading or parsing failures visibly rather than silently showing an empty success state, and keep the implementation understandable and maintainable.
- Create `.vscode/launch.json` with **Run Project Pulse Dashboard**, using `app/` as the served working directory and opening `index.html`.
- Verify that the page loads its stylesheet and data correctly, remains usable at different viewport widths, and does not expose a directory listing as the initial experience.

## Dependencies

The project-data contract is the foundation for rendering: `app/project-data.json` must define the top-level `projects` array and required fields before the data-binding logic is finalized. The HTML structure must be stable enough for the Designer and Coder to agree on selectors and semantic regions before CSS integration is completed. The launch configuration depends on the app entry point and serving directory, but it can be prepared in parallel once those paths are fixed. Final integration depends on all four files being present and mutually consistent.

## Parallel work decisions

The Planner and Orchestrator should complete the requirements and file-ownership decision first because it establishes the shared contract. After that, the Designer can work on layout and visual specifications in parallel with the Coder creating the JSON fixture and HTML scaffold. CSS implementation can proceed in parallel with data preparation once the HTML structure and naming conventions are agreed. The launch configuration is also safe to create in parallel with styling because it only needs the stable `app/` directory and `index.html` entry point. Do not parallelize the final integration review: rendering, paths, data fields, launch behavior, accessibility, and visual polish must be checked together by the Orchestrator.

## Validation expectations

- Confirm `docs/project-pulse-plan.md`, `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json` exist and are readable.
- Parse `app/project-data.json` as valid JSON; confirm it has a top-level `projects` array and that each project includes `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Confirm `app/index.html` contains the exact `Project Pulse` title, references `styles.css` and `project-data.json`, and provides the expected semantic containers for project content.
- Confirm `.vscode/launch.json` is valid JSON, includes the exact launch name **Run Project Pulse Dashboard**, serves from `${workspaceFolder}/app`, and opens `index.html`.
- Run the dashboard using the configured launch path and verify that the browser opens the Project Pulse UI from `app/index.html`, not a directory listing.
- Inspect the rendered page at narrow and wide viewport sizes for readable spacing, responsive cards, visible status and priority information, keyboard focus, and sufficient contrast.
- Check the browser console and network requests for failed data or stylesheet loads, and ensure any loading or error state is explicit and understandable.

## Completion criteria

Project Pulse is complete when the four assigned implementation files work as one static app, the launch configuration opens the intended page, the required project information is visible and contributor-friendly, the Designer’s accessibility and visual direction is represented, and the Orchestrator can report successful validation without unresolved path, data, or rendering issues.

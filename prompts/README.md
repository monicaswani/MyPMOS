# prompts/

Versioned prompt templates that drive PMOS agents.

## Categories

| Subdirectory  | Purpose                                                          |
| ------------- | ---------------------------------------------------------------- |
| `meeting/`    | Meeting capture, summaries, action-item extraction.              |
| `prd/`        | PRDs, user stories, acceptance criteria.                         |
| `analytics/`  | Metric analysis, feedback synthesis, insight extraction.         |
| `roadmap/`    | Prioritization, roadmaps, estimates, sprint planning.            |
| `executive/`  | Executive summaries, stakeholder updates, status reports.        |

## Conventions

- One concern per file; name by task (e.g., `prd/draft.md`).
- Document expected inputs and outputs at the top of each prompt.
- Use `{{variable}}` placeholders for runtime-injected values.
- Review prompt changes like code; never embed secrets or customer data.

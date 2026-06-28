# workflows/

n8n workflow definitions. A workflow sequences prompts, tool calls, and knowledge
retrieval to complete a product-management task end to end.

## Workflows

| Subdirectory        | Purpose                                                     |
| ------------------- | ----------------------------------------------------------- |
| `meeting-copilot/`  | Capture meetings → summaries → action items.                |
| `prd-copilot/`      | Intent → PRD draft → review checklist.                      |
| `customer-research/`| Ingest feedback → cluster themes → summarize opportunities. |
| `executive-report/` | Aggregate status → executive summary → stakeholder update.  |

## Conventions

- Export each workflow's JSON into its subdirectory for version control.
- Reference prompts from `prompts/` by name — do not inline prompt text in nodes.
- Store credentials in n8n's credential store / environment, never in node JSON.
- Keep workflows deterministic and idempotent; isolate model/external calls to
  named nodes and handle partial failures explicitly.

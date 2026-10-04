# Stack defaults

Apply these unless the house rules (`poc-house-rules.md`) say otherwise.

| Layer | Default | Use something else when |
|---|---|---|
| Front end | The project's existing front end; if there is none, a widely used framework such as React | Only with a stated reason |
| Back end | The project's existing back end; if there is none, a widely used option such as Node.js or Python | Only with a stated reason |
| AI calls | The provider's plain SDK, or the Claude Agent SDK for agents | Default for workflows and single agents |
| Workflow graphs | LangGraph | State and branching get hard to manage in plain code |
| Multi-agent | CrewAI | Separate roles must genuinely collaborate; flag the higher token use |
| Knowledge search | Embeddings plus a vector database (pgvector first) | Content is too large to send in the prompt. Not for structured data (use SQL) or a single message's attachments |
| Documents | Local parsing and OCR | Always, before any model sees the file |

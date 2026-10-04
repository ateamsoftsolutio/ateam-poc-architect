# POC Architect by ATeam

**Understand it. Design it. Cost it. Guard it. Then build it.**

POC Architect is a Claude plugin for teams that build AI proofs of concept for customers. It stops the most common failure in AI delivery: a use-case document goes straight into an AI tool, building starts before anyone understands the requirement, and the result costs too much to run or sell.

The plugin guides a POC through eight stages. Claude asks the questions, challenges assumptions and checks the work, while the people involved do the thinking and make the decisions. A POC moves to the next stage only when the current one is passed.

It was built by [ATeam Soft Solutions](https://www.ateamsoftsolutions.com) from lessons on real customer POCs and is used by ATeam's delivery teams. We are sharing it as a contribution to the community.

## The three skills

| Skill | Used by | Stages | Output |
|---|---|---|---|
| `poc-handover` | Account owners, sales, business sponsors | 0. Handover | A handover pack: the customer's story, workflow and roles sign-off, real input samples, third-party access, volumes and pricing model |
| `poc-architect` | Product managers, developers, presales engineers | 1. Teach-back · 2. Questions and challenge round · 3. Readiness gate · 4. Architecture and cost · 5. Guardrail review · 6. Product Owner approval | An architecture brief with a cost model, guardrail decisions and a test plan |
| `poc-build` | Developers | 7. Build and test | A POC built to the brief, with tests, evaluation results and measured running cost |

## What makes it different

- **Understanding before building.** The builder explains the POC in their own words, answers questions drawn from the actual document, and lists edge cases before Claude adds any. Vague answers such as "TBD" are rejected. Facts Claude supplies about a domain stay as assumptions until the customer or an expert confirms them.
- **A challenge round.** The builder and Claude test interpretations of the requirement together, and produce one consolidated list of questions for the customer.
- **Cheapest design that works.** Each step of the solution starts at plain code and moves up to local models, then small, mid and large API models only when needed. Claude and OpenAI models are compared at current list prices.
- **A running-cost ceiling.** The brief shows tokens and cost per transaction and per month, and rates the design against what the customer pays (10% by default).
- **Guardrails decided by people.** Four guardrails are always on. Claude proposes others for each POC, and the builder accepts, changes or rejects each one with a reason.
- **An approval gate.** Nothing is built until the Product Owner approves the brief.
- **Lean engineering discipline.** The build uses a task plan, test-first coding, evaluation sets for AI steps, root-cause debugging and review against the brief, without the extra token cost of many sub-agents unless the build needs them.

## How to use it

1. Put the customer's use-case document and any sample inputs in your project folder.
2. The account owner says: **"Run POC Handover on the use-case document."**
3. The builder says: **"Run POC Architect on the handover pack."**
4. After the Product Owner approves the brief, the builder says: **"Run POC Build."**
5. To continue later, say: **"Resume POC Architect from this brief."**

The skills work in Claude Cowork, Claude Code and Claude chat. Stage 7 needs an environment where Claude can write and run code, such as Claude Code or Cowork with a project folder.

## Make it yours

Copy `poc-house-rules.md` from this plugin into your project folder and edit it. You can change the approver title, cost ceiling, currencies, stack defaults, document format, compliance regions and your own rules. The skills read it at the start of every run.

## Works well with Superpowers

[Superpowers](https://github.com/obra/superpowers) is an open-source plugin with a strong software-engineering methodology, and it inspired parts of our build stage. If you have it installed, `poc-build` can hand the build to Superpowers, with the approved brief as the specification and this plugin's guardrails, cost logging and test rules kept in place. POC Architect does not include or copy Superpowers' code.

## What this plugin does and does not do

- It contains only instructions for Claude (skills). It has no MCP servers, hooks or scripts, and it does not send your data to any service.
- During Stage 4, Claude may use web search or fetch, where available, to read the public pricing pages of Anthropic and OpenAI. If it can't, it uses the dated fallback table included in the plugin.
- It creates and updates the handover pack, the brief and the build plan as Claude Docs or as files in your project folder.
- Skills guide Claude; they cannot force people to follow a process. The approval gate works best when your organisation agrees that no POC is built without an approved brief.
- Compliance flags are prompts to check with the right person. They are not legal advice.
- Model prices change. Treat cost figures as estimates and check them against your provider's bill.

## Licence

MIT. See [LICENSE](LICENSE).

## Feedback

Please raise issues and suggestions on the plugin's GitHub repository.

---
name: poc-architect
description: Stages 1 to 6 of the POC process for builders (product managers, developers, presales engineers). Tests the builder's understanding of an AI POC, runs a challenge round, designs the cheapest workable architecture across Claude and OpenAI models, costs it, reviews guardrails and produces a brief for Product Owner approval. Use when someone says "run POC Architect", brings a handover pack or use-case document for an AI POC, or needs a cost and architecture estimate for one.
---

# POC Architect (Stages 1–6)

This skill makes sure the person building an AI POC **understands it before building it**, and that it is designed in the **cheapest way that works**, so it can be sold and run profitably. It starts from the handover pack produced by `poc-handover` and ends with a brief approved by the Product Owner. The build itself (Stage 7) is run by `poc-build`.

## Settings

Before Stage 1, look for a file named `poc-house-rules.md` in the project folder. If it exists, its values override these defaults. If not, use the defaults and say so once.

| Setting | Default |
|---|---|
| Approver | Product Owner |
| Cost ceiling | AI running cost within 10% of what the customer pays; amber up to 15% |
| Currencies | USD, plus the user's local currency if they name one (state the exchange rate used and its date) |
| Stack defaults | `references/stack-defaults.md` |
| Compliance regions | `references/guardrails-and-compliance.md` |
| Brief format | Claude Doc when available, otherwise a Markdown file in the project folder |

## Principles

- **The builder drives; Claude challenges, advises and checks.** Never answer your own questions, write the teach-back, or fill in the builder's decisions. If asked to, decline briefly: the understanding has to be theirs.
- **Do not move to the next stage until the current one is passed.** Say which stage you are in at the start of each reply.
- **Do not start design, planning or build work early**, including through other planning or brainstorming skills, until the brief is approved.
- **One round at a time**, with up to eight questions per round. Wait for the answers.
- **Every design decision gets a one-line reason and the cheaper option it rejected**, so builders learn the reasoning.
- Plain language and no inflated claims. Label every estimate as an estimate.

## Answer rules (all stages)

| Class | Meaning | Effect |
|---|---|---|
| **Confirmed** | Has a source: document section, handover pack, or the customer contact who confirmed it and the date | Proceeds |
| **Assumption** | Not yet confirmed; needs an owner and a date to check it | Proceeds, logged in the brief |
| **Unknown** | Nobody knows yet and it affects the design | Blocks the gate |

- Reject "TBD", "as per document", "standard", "should be fine" and "will check later". Ask for something specific.
- **Domain facts supplied by Claude** are Assumptions until the customer or a domain expert confirms them. Say so whenever you offer one.
- Keep a verbatim question-and-answer log for the brief.

## Starting a run

1. **Ask for the handover pack** (link or file). Read it and the use-case document in full.
2. If the pack is missing or its status is Incomplete, **stop**. List what is missing and ask the builder to have it completed with `poc-handover`. Continue without a complete pack only if the builder states that the Product Owner has waived it. Record the waiver, with name and date, in the brief.
3. **Estimate mode:** if someone only needs a cost and architecture estimate for a proposal, skip to Stage 4 on the information available. Label every output "Estimate, not an approved brief" and list all assumptions.
4. **Resuming:** if a brief already exists for this POC, read it and continue from its recorded stage.

## Stage 1: Teach-back

The builder must have read the full document and the pack. Ask them to write, **in their own words**:

1. The problem the customer has today
2. Who will use the solution, and how often
3. What "done" looks like: how the customer will judge success
4. The end-to-end workflow in the customer's own terms
5. The three hardest parts, as they see them

Compare the teach-back against the document and the pack. Point out anything missed or wrong. If the gaps are major, send them back to the document before continuing.

## Stage 2: Question rounds, then the challenge round

**Question rounds.** Run three or four rounds drawn from this specific document, blocking questions first. Workflow and role questions are always blocking. Cover:

- Business problem and users
- Success measures
- Inputs: formats, volumes, languages
- Outputs and actions
- Integrations and access
- Data sensitivity and residency
- Human review points
- Roles and approval rules
- AI provider and account owner
- Pricing model and volumes
- Scope limits and timeline

**Edge cases: the builder goes first.** Ask the builder to list every edge case they can think of. Only then add the ones they missed. Record both counts for the readiness score.

**Challenge round.** Once the question rounds are done, review the requirement together with the builder:

- For each ambiguous or risky point, **the builder states their interpretation first**. Then challenge it: offer other interpretations, and name the risks, technical constraints and knock-on effects.
- Look for ambiguous wording, conflicting requirements, missing states or transitions, and implementation risks.

The challenge round produces six sections:

1. Confirmed understanding
2. Assumptions
3. Technical challenges
4. Unresolved questions
5. Options considered
6. **Client clarification list:** numbered, in plain language the customer can answer, with one line on why each question matters

Ask the builder to send the client clarification list to the customer. **Pause until the answers are recorded**, then update the log.

## Stage 3: Readiness gate

The gate opens only when all eight are true:

1. Every blocking question is Confirmed
2. The client clarification list is answered
3. No Unknowns remain
4. Workflow and roles are signed off (names and date)
5. Every assumption has an owner and a date
6. Real input samples are received, or logged as an Assumption
7. Research is done: how the customer handles this today, what existing products do, and one technical risk the builder checked personally
8. Third-party access is confirmed, or has a dated plan

**Readiness score:** the percentage of answers that are Confirmed, plus the edge cases the builder found compared with the edge cases Claude added. Record it in the brief.

If any item fails, list what is missing and stay in Stage 3.

## Stage 4: Architecture and cost

**Workflow or agent.** Use a workflow when the steps are known in advance: code controls the flow and AI handles only the thinking steps. Most POCs are workflows. Use an agent only when the path genuinely cannot be predicted. State which, and why.

**Cheapest-first ladder.** For each step of the solution, choose the lowest level that works:

1. **Plain code:** rules, regular expressions, parsers. Zero tokens.
2. **Local small model:** classification, OCR, embeddings.
3. **Small API model**
4. **Mid API model**
5. **Large API model:** rarely, for the hardest reasoning only

For each step, record the level, the reason, and the cheaper option rejected with why.

**Provider choice.** Claude and OpenAI models are both allowed, and others where the customer requires them. For each step, pick the cheapest model that passes the test cases, while respecting any customer constraint and data-location requirement. Start on the smallest tier and move up only when it fails. Where only data location is the concern, prefer a regional cloud endpoint (for example AWS Bedrock, Microsoft Azure or Google Cloud) over local models.

**Prices.** Look up current prices on the providers' official pricing pages. If a lookup fails, read `references/pricing.md`, use its fallback table, say that you did, and state its date.

**Local model or API.**
- Use a local model only when data legally cannot leave the customer's environment, for very high volumes of simple tasks, for offline systems, or where the customer already runs GPUs.
- Otherwise use an API. Local models are not free: they need servers, maintenance, and usually give lower accuracy.

**Stack defaults.** Read `references/stack-defaults.md` and apply it, unless the house rules say otherwise.

**Token discipline.** Apply all of these:
- Strip signatures, disclaimers and quoted threads.
- Send only the relevant pages.
- Ask for structured JSON output.
- Cache fixed instructions.
- Use batch processing for anything that isn't urgent.
- Cap agent steps and tokens per transaction.
- Log tokens for every transaction.

**Cost model.** Show the working so it can be checked:
- Tokens per step and per transaction, by model
- Cost per transaction and per month at the stated volumes. If volumes are unknown, show low, medium and high scenarios and flag that.
- Figures in USD, plus the user's local currency if they name one (state the exchange rate used and its date)

**Cost ceiling.** AI running cost must stay within 10% of what the customer pays:
- **Subscription:** monthly AI cost against the monthly fee
- **Build fee plus maintenance:** yearly AI cost against the yearly maintenance fee
- **Customer pays AI costs:** show the customer's expected monthly bill against an agreed budget

Status: **Green** under 10%, **Amber** 10–15% (optimise first), **Red** over 15% (redesign or reprice). If the customer price is not known, show the minimum price at which the design stays green.

Keep this **running cost** separate from the cost of building the POC; never mix the two.

## Stage 5: Guardrail review

**Always on.** These cannot be rejected, only commented on:
1. Personal, financial or health data never goes to a model endpoint outside the region the customer approved.
2. A human approves any irreversible action (sending, paying, deleting, booking).
3. Compliance flags are raised for review.
4. Step limits, cost limits and token logging apply to every run.

**Proposed guardrails.** Read `references/guardrails-and-compliance.md`. Propose only what this POC needs, each with the risk it addresses, its risk level (High, Medium or Low), how it will be tested and its cost impact. Raise the compliance flags for the countries and sectors involved; they are flags to check, not legal advice.

**Builder decisions.** For each guardrail, the builder chooses **Accept**, **Change** or **Reject**:
- Change and Reject need a written reason.
- For every High-risk guardrail, the builder writes in their own words the failure it prevents in this POC.
- Ask the builder to add any guardrail you missed.
- If everything is accepted with no comments, flag it in the brief.

## Stage 6: The brief, for Product Owner approval

Create the brief as a **Claude Doc** when a docs tool is available; otherwise as a Markdown file in the project folder. Follow the structure in `references/brief-template.md`.

Set the status to **"Awaiting Product Owner approval"** and ask the builder to share it with the Product Owner. **Never mark the brief approved yourself.** Record approval only when the builder supplies the Product Owner's decision, with name, date and comments.

Once approval is recorded, hand over to `poc-build` for Stage 7.

## Worked example

For a reference design and cost comparison, read `references/worked-example.md`.

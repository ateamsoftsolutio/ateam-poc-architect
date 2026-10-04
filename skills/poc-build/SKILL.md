---
name: poc-build
description: Stage 7 of the POC process. Builds an approved AI POC to its brief with lean engineering discipline - a task plan, test-first coding, evaluation cases for AI steps, root-cause debugging, review against the brief, cost logging and verification before anything is called done. Use when a POC brief has been approved and someone says "build the POC", "start Stage 7" or "run POC Build".
---

# POC Build (Stage 7)

This skill builds a POC **exactly to its approved brief**, with the engineering discipline that keeps a POC working when the customer tries it. It is deliberately lean: one agent by default, and extra sub-agents only when the build is large enough to justify their cost.

## Before starting

1. **Read the approved brief** and the handover pack. Check that the brief records the Product Owner's approval (name, date, comments).
2. If there is no approved brief, **stop** and direct the builder to `poc-architect`. Proceed without one only if the builder states that the Product Owner has waived it. Record the waiver in the brief.
3. Read `poc-house-rules.md` in the project folder if it exists.
4. **Superpowers hand-off (optional).** If the Superpowers plugin is installed and the builder prefers it, hand the build to its planning and execution skills instead of the steps below. Give it the approved brief as the specification. Tell it to skip its own brainstorming, because requirements and design are already settled. Keep this skill's non-negotiables: the brief's architecture and model choices, every accepted guardrail, cost logging, the test requirements, and re-approval for changes. Note in the brief that Superpowers was used.

## Non-negotiables

- Build only what the brief describes. Anything extra is scope creep: list it for later, don't build it.
- The models, providers and token limits in the brief are the ones used. A change needs re-approval.
- Never claim something works without running it and showing the output.
- No secrets in code or commits. Use environment variables or a secrets store.

## Step 1: Build plan

Break the brief into small tasks. Each task should be finishable in a few hours and touch only a few files. For each task, write:

- the goal, in one line
- the files it creates or changes
- the test or evaluation that proves it works
- the line of the brief it satisfies

Order the tasks so the riskiest unknowns come first; a short spike is fine to settle a risky integration early. Save the plan in the project folder as `build-plan.md`, and get the builder's agreement before coding.

## Step 2: Test first, task by task

For each task:

1. Write a test that describes the expected behaviour. Run it and confirm it fails, and fails for the right reason.
2. Write the minimum code that makes it pass.
3. Run the whole test suite, not just the new test.
4. Tidy the code while everything still passes.
5. Commit with a clear message, on a working branch rather than the main branch.

**AI steps are not deterministic, so test them differently.** Build an evaluation set from the real input samples, each with the expected output. Check that the output matches the agreed schema every time, and that accuracy meets the threshold in the brief. Record the pass rate rather than a single pass or fail.

**Instrument from the first AI call.** Log tokens and cost for every transaction from the start, so the measured cost is available at the end.

**Guardrails are tasks too.** Every accepted guardrail gets its own task and its own test.

## Step 3: Debugging, root cause first

When anything fails:

1. Stop adding code. Reproduce the failure reliably.
2. Read the full error and the logs.
3. Find the root cause: trace the data, compare with a case that works, and check what changed recently.
4. Form one hypothesis, and test it with the smallest possible change.
5. Fix the cause, not the symptom, and add a test that would have caught it.

If three attempted fixes fail, stop. The design may be wrong. Report to the builder; if the fix needs a change to the architecture, it goes back to the Product Owner.

## Step 4: Review against the brief

After each task, or each small batch, review the work with this checklist:

- It matches the brief's architecture, model choices and token limits.
- The accepted guardrails are implemented and tested.
- There is no scope creep.
- There are no secrets in the code and no unsafe handling of inputs, including prompt injection in customer content.
- The code is readable and the tests are meaningful.
- The measured cost per transaction is still within the ceiling.

For large builds, with many independent tasks, you may run tasks in separate sub-agents with a separate reviewer. Tell the builder first that this raises the token cost of building, and record the choice.

## Step 5: Mid-build demo

At 40–50% of the plan, prompt the builder to demo progress to the account owner and the Product Owner. Record what they say. Any change to workflow, roles or scope goes back for approval before it is built.

## Step 6: Done means verified

The POC is ready for a customer demo only when:

- at least 10 test cases pass, including the edge cases from Stage 2, with at least half using real input samples
- every accepted guardrail has a passing test
- the measured cost per transaction has replaced the estimate in the brief, and the cost ceiling has been rechecked
- known limitations are listed in the brief

Show the evidence (test output, evaluation pass rates, cost log) to the builder. Then update the brief's status to **"Built - ready for customer demo"**.

# Open Stack Field Guide Prompt Architecture Report

Source file: `Open Stack _ Unlock AI.mhtml`
Source basis: extracted readable text from the local MHTML capture of the Unlock AI Open Stack guide. The capture includes the visible guide body and visible full prompt blocks embedded in the page.

## What This Guide Is

The Open Stack guide is a router, not an install manual. It helps a user decide whether their current AI bottleneck is capability, context, or work movement, then points them toward the matching primitive:

- Open Skills when the agent needs a repeatable procedure, tool-use pattern, taste, or verification method.
- Open Brain when the agent keeps losing durable context and the user keeps re-explaining themselves.
- Open Engine when work, ownership, blockers, approvals, receipts, or handoffs disappear between chats.

The page argues against the "one-click personal AI operating system" pitch. Its position is that a personal AI stack cannot be personal unless someone asks what the user's work is, what context matters, what the agent may do, and where human approval sits.

## Meta-Thinking Behind Open Stack

Open Stack starts from leakage, not tooling. The first design question is not "which stack should I install?" It is "where is my current AI setup leaking time or trust?"

The guide uses a three-part diagnostic model:

| Bottleneck | Symptom | Primitive |
| --- | --- | --- |
| Capability | The agent is close but unreliable at a specific job. | Open Skills |
| Context | The user keeps re-explaining goals, preferences, decisions, and facts. | Open Brain |
| Work movement | Tasks vanish into threads, status is unclear, or approvals/handoffs are brittle. | Open Engine |

This is the main demystifying move. "Open Stack" is not a pile of tools. It is a way to locate the missing piece in an agentic workflow and add only the primitive that fixes that missing piece.

The second design principle is personalization as the edge. The primitives are reusable, but the advantage comes from adapting them to the user's workflows, files, accounts, taste, sources, standards, and approval boundaries. Two users can share the same architecture and end up with different systems because their work is different.

The third design principle is source-of-truth routing. The guide avoids duplicating the full Open Brain and Open Engine setup paths. It tells the agent where the maintained docs live and instructs it to read those docs before acting. This reduces drift and keeps the Open Stack page focused on choosing the right route.

The fourth design principle is human ownership of trust. The guide repeatedly separates agent work from human-only judgment. Agents can prepare, inspect, write, run safe local work, and verify. Humans own accounts, auth, secrets, billing, destructive changes, public/customer-facing actions, and final go/no-go decisions.

## Workflow

The guide's workflow is a narrowing funnel:

1. Map the bottleneck.
   The user describes the work they want AI to help with. The agent asks about repeated work, lost context, and stuck tasks, then classifies the problem as capability, context, work movement, or a mix.

2. Choose the first primitive.
   The guide defaults to Open Skills first because one useful skill can improve work before a database or queue exists. It allows exceptions when the real bottleneck is clearly memory or work movement.

3. Build only the smallest useful version.
   Each section pushes against unnecessary ceremony. Do not install a skill if the real issue is memory. Do not build a queue if one personal skill or memory experiment is enough.

4. Make the personal layer explicit.
   The user identifies repeated workflows, context they keep re-explaining, decisions the AI should not make, files/tools/accounts they use, and human-only boundaries.

5. Use source-of-truth setup paths.
   When the route is Open Brain, the agent should use the OB1 repository and its maintained getting-started and AI-assisted setup docs. When the route is Open Engine, the agent should use the Open Engine guide.

6. Write authority rules.
   The guide asks for policies around skill adoption, memory recall/write-back, runner behavior, and human-vs-agent boundaries.

7. Verify behavior.
   Every practical prompt asks for a deliverable that can be pasted into instructions, private setup issues, memory policy, runner policy, or an adoption plan. Several prompts explicitly require verification steps or smoke tests.

## Architecture

The architecture is deliberately modular:

| Primitive | Core Job | User Owns | AI Helps With |
| --- | --- | --- | --- |
| Open Skills | Reusable capability and method. | The job, taste, approval mode, verification standard. | Create/adapt the smallest skill, classify safe use, test it. |
| Open Brain | Durable memory and context. | What should be remembered, privacy, instruction authority. | Stand up DB/MCP/capture/search/review from docs, draft memory policy. |
| Open Engine | Work movement and operating ledger. | Task system choices, approvals, blockers, review decisions. | Set up statuses, labels, private context, queue runner, receipts, smoke tests. |

The full loop is:

1. Skills make the agent capable.
2. Brain remembers when and how capability should be used.
3. Engine moves real work through visible task state.
4. Receipts show what happened.
5. Human judgment controls trust boundaries.

The guide also supports partial adoption. A user can use the skill library without Open Brain, apply the memory pattern to a different database, or use Open Engine's receipt vocabulary inside GitHub Issues, Notion, Trello, or a local Markdown queue. The surface can change as long as the job of each primitive remains intact.

## Prompt Design Overview

The prompts are built in XML-ish blocks with explicit task, context, instructions, constraints, and deliverable sections. That structure is doing several things:

- It narrows the model's role before asking for output.
- It tells the agent what information to collect instead of letting it assume.
- It encodes the Open Stack taxonomy directly into the prompt.
- It forces a bounded deliverable rather than open-ended advice.
- It adds constraints that prevent generic stack diagrams, one-click setup claims, silent authority expansion, or stale duplicated setup instructions.
- It makes the output pasteable into future agent instructions, private setup issues, or policy files.

The prompt architecture is itself part of the product. Each prompt teaches the user how to think: diagnose first, personalize second, route third, preserve human authority throughout.

## Individual Prompt Analysis

| Prompt | What It Does | How It Is Designed |
| --- | --- | --- |
| Choose where to start with Open Stack | Interviews the user and classifies the bottleneck as capability, context, work movement, or mix. | The task is narrow, the context defines the three primitives, the instructions force one-question-at-a-time interviewing, and the constraints block generic one-click advice. |
| Interview me for the personal layer | Collects repeated workflows, repeated context, human-only decisions, and real tools/accounts. | It turns "personalization" into specific input fields, then outputs a stack profile: likely skills, first memory, smallest queue, and boundaries. |
| Help me choose my first Open Skill | Selects the smallest skill that improves a real workflow this week. | It delays examples until after the user answers, preventing the model from anchoring the user on generic ideas. The verification task forces proof that the skill works. |
| Decide whether my problem is a skill problem | Routes away from Open Skills when the true issue is memory or work movement. | The classification schema is explicit: Skill, Brain, Engine. This prevents "install more capabilities" from becoming the default answer. |
| Create a safe Open Skills adoption map | Classifies skills by authority level: manual, ask first, or automatic inside a workflow. | It introduces permission tiers and hard human-approval constraints for external, secret, billing, publishing, and destructive actions. |
| Help me decide what Open Brain should remember first | Interviews for repeated context, projects, and trusted sources. | It separates memory into evidence, instruction, and private/excluded categories, which prevents raw agent-written memory from silently becoming binding policy. |
| Walk me through building Open Brain from source docs | Makes the agent use OB1 docs before giving instructions. | The source-of-truth block reduces setup drift. The workflow block tells the agent not to improvise code or SQL. The verification block requires expected result, actual result, and next fix. |
| Draft my Open Brain use policy | Defines recall, write-back, confirmation, and scoping rules. | It treats memory as governance, not storage. Boundaries prohibit raw secrets and unreviewed binding policy. |
| Decide whether I am ready for Open Engine | Tests whether a queue is actually justified. | It asks about lost work, task systems, agent runtimes, and approval boundaries before recommending build now, wait, or steal only concepts. |
| Walk me through the Open Engine setup guide | Uses the maintained Open Engine guide as source of truth. | It requires stepwise setup, asks before changing Linear/workflow objects, and demands smoke tests for queue behavior, blocked/resume, human hold, and optional skills. |
| Draft integration rules for my Open Engine runner | Defines which skills and memories may influence runner behavior and what receipts are required. | It converts the full-stack composition into policy: approved skills, required recall, approval gates, and receipt obligations. |
| Make me a 30-day Open Stack adoption plan | Turns the diagnosis into a four-week implementation path. | It encodes the default order but allows bottleneck-based reordering. Each week must include one task, one verification step, and one reason it matters. |
| Adapt Open Stack principles to my existing tools | Maps the primitives onto the user's current stack. | It preserves the jobs of the primitives while allowing different surfaces. This is how the guide avoids tool worship. |
| Write the human-vs-agent boundary | Produces a two-column policy for agent-permitted vs human-only actions. | It names human-only categories explicitly: accounts, auth, secrets, browser settings, billing, destructive changes, public posting, publishing, customer-facing actions, and final judgment. |

## Why The Prompts Work

They interview before prescribing. The guide's core belief is that personal systems fail when they begin with tools instead of work. The prompts collect the user's actual repeated work, lost context, stuck tasks, tools, accounts, and boundaries before recommending a route.

They encode decision rules. The model does not have to invent the taxonomy each time; it is given the categories and asked to classify evidence against them.

They constrain overreach. Many prompts include "do not sell this as one-click," "do not recommend a full stack," "ask before changing statuses," or "external actions require approval." These constraints are the operational version of Nate's intent thesis.

They output reusable artifacts. The deliverables are short routes, stack profiles, skill choices, adoption maps, memory policies, runner policies, setup walkthroughs, and 30-day plans. Those can become files, setup issues, AGENTS.md instructions, CLAUDE.md instructions, or Open Brain/Open Engine context.

They separate source docs from routing docs. Setup prompts point the agent to maintained source-of-truth docs rather than copying installation details into the guide. That keeps the prompts durable even as repos change.

They force proof. Verification tasks, smoke tests, receipts, and expected-vs-actual result reporting make the agent show its work instead of asking the user to trust a completed setup claim.

## Prompt-To-Architecture Mapping

| Architecture Need | Prompt Pattern Used |
| --- | --- |
| Diagnose the bottleneck | One-question-at-a-time interview plus capability/context/work classification. |
| Avoid generic setup | Constraints against one-click pitches and generic stack diagrams. |
| Capture personal context | Explicit inputs for workflows, repeated context, tools, accounts, and human-only decisions. |
| Preserve authority boundaries | Human-only lists, permission tiers, approval gates, and stop rules. |
| Keep setup current | Source-of-truth blocks pointing to OB1 docs or Open Engine guide. |
| Make agent work inspectable | Deliverables requiring receipts, verification, smoke tests, expected/actual results. |
| Support partial adoption | Adaptation prompts that map primitive jobs onto existing tools. |

## Reusable Workflow

Use this sequence to replicate the Open Stack thinking without copying the surface exactly:

1. Describe one repeated AI workflow that feels painful.
2. Classify the pain as capability, context, work movement, or a mix.
3. Choose the smallest primitive that fixes the real bottleneck.
4. Interview for the personal layer: workflows, context, boundaries, files, tools, accounts, and human-only decisions.
5. Convert the answer into one artifact: a skill, memory plan, queue policy, or adoption plan.
6. Define permission levels before automation runs.
7. Use maintained source docs for setup rather than stale copied instructions.
8. Require verification and receipts before treating the work as complete.
9. Run it on real work and feed corrections back into memory, method, or policy.

## Failure Modes

The user starts with the stack instead of the pain. That creates an impressive but unused system.

The agent recommends a skill when the real issue is memory, or a queue when the real issue is one missing procedure.

The prompt collects personal context but fails to classify which memories are evidence, instruction, private, or excluded.

The guide's source-of-truth links drift, and the agent improvises setup steps instead of reading current docs.

The system silently expands authority: a skill moves from manual to automatic, memory becomes binding policy, or a queue runner performs external actions without explicit approval.

Receipts become decorative summaries instead of operational proof: no source, status, blocker, verification, or stop point.

The user adapts the stack to another tool but loses the discipline: memory without review, skills without verification, or queues without receipts.

## Adaptation Notes

For a solo operator, start with a single high-friction personal loop: weekly planning, travel planning, client follow-up, research capture, or insurance/admin appeals. Use one skill or one memory plan before building a queue.

For a team, start with work movement if tasks already cross people, tools, or agents. The first useful Open Engine adaptation may be a GitHub Issues or Linear policy with status, owner, blocker, approval, and receipt fields.

For a non-technical user, keep the coding agent in a guided executor role. It can read docs, prepare steps, and run safe local commands. The human handles accounts, auth, secrets, billing, and approval.

For a power user with multiple models, prioritize portable memory and skill records. The point is to stop becoming the integration layer between Claude, GPT, Kimi, Codex, and future tools.

## Bottom Line

The Open Stack guide demystifies "personal AI infrastructure" by turning it into a routing problem. Find the bottleneck, choose the primitive, write the personal layer, define the boundary, and require proof. The prompts are not just helper text; they are the operating system for the user's thinking. Each one forces the agent to ask before prescribing, classify before building, respect human authority, and leave an artifact that can guide the next run.

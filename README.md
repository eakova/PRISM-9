# PRISM-9 Framework

## Pipeline Reasoning with Integrated Self-Monitoring

**Version:** 1.0
**Type:** AI Reasoning & Pipeline Governance Framework
**Status:** Production-Ready
**License:** [MIT](LICENSE-MIT) OR [Apache 2.0](LICENSE-APACHE)
**Research:** [RESEARCH.md](RESEARCH.md)
**Samples:** [samples/](samples/) — Working pipeline implementations

> "Reasoning you can audit. Results you can trust. From complexity to clarity through governed reasoning"

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Why PRISM-9](#why-prism-9)
3. [Core Philosophy](#core-philosophy)
4. [Architecture Overview](#architecture-overview)
5. [The 9-Step Workflow](#the-9-step-workflow)
6. [The Laws Layer](#the-laws-layer)
7. [Modular Components](#modular-components)
8. [Pipeline Orchestration](#pipeline-orchestration)
9. [Response Schema](#response-schema)
10. [Implementation Guide](#implementation-guide)
11. [Stage Template](#stage-template)
12. [Examples](#examples)
13. [Comparison with Other Frameworks](#comparison-with-other-frameworks)
14. [Best Practices](#best-practices)
15. [Quick Reference](#quick-reference)

---

## Executive Summary

PRISM-9 is a next-generation prompt engineering framework designed for **complex, multi-stage AI pipelines** that require **governed reasoning**, **transparent decision-making**, and **verifiable outputs**.

### What Makes PRISM-9 Different

| Traditional Prompting | PRISM-9 |
|----------------------|---------|
| Single prompt, single output | Multi-stage pipeline with handoffs |
| Hidden chain-of-thought | Externalized, auditable reasoning |
| Implicit constraints | Tiered governance (Laws → Constraints → Preferences) |
| Hope-based validation* | 9-step self-monitoring with failure recovery |
| One-shot execution | Iterative refinement with checkpoints |

*\*Hope-based validation = no explicit verification between generation and delivery. The user receives output and trusts it's correct without systematic checks.*

### Key Innovations

1. **The Laws Layer** — Inviolable rules that supersede all other instructions
2. **9-Step Meta-Reasoning Workflow** — Structured cognitive process with failure handling
3. **Modular Architecture** — Reusable components across stages
4. **Pipeline-Native Design** — Built for multi-agent, multi-stage workflows
5. **Schema-Driven Handoffs** — Typed inputs/outputs for reliable stage transitions

### When to Use PRISM-9

- Complex tasks requiring multiple reasoning steps
- Multi-agent pipelines with stage handoffs
- High-stakes outputs requiring auditability (legal, financial, healthcare)
- Tasks where hallucination prevention is critical
- Enterprise applications requiring governance and compliance

---

## Why PRISM-9

### Why You Need This

#### 1. Split Complex Prompts Properly
Large prompts become unmanageable. PRISM-9 lets you break them into **modular, maintainable pieces** — shared infrastructure, domain context, and stage-specific logic — each in its own file.

#### 2. Reusability Across Projects
Write your thinking framework once, reuse everywhere. The `{{include:}}` system means your Laws, workflow, and response schema work across **any project** without copy-paste.

#### 3. Multi-Stage Pipeline Support
Real-world tasks need multiple steps. PRISM-9 provides **typed handoffs** between stages so outputs flow reliably from strategy → research → execution → delivery.

#### 4. Reduce Hallucinations
The **5 Laws** (especially No Fabrication and Verify Before Claim) are enforced at every step. The model can't just make things up — it must cite sources or flag unknowns.

#### 5. Debuggable Failures
When something goes wrong, you see **exactly where**. The 9-step workflow with visible checkpoints means you can trace failures to COMPREHEND, EXECUTE, or SELF_CHECK — not just "it didn't work."

#### 6. Consistent Output Quality
**Validation gates** ensure every output meets your criteria before delivery. No more hoping the model followed instructions — you define what "done" means and verify it.

#### 7. Enterprise-Ready Governance
For regulated industries (healthcare, finance, legal), PRISM-9's **tiered governance** (Laws → Constraints → Preferences) provides the auditability and compliance documentation you need.

#### 8. Team Collaboration
Shared components mean your team works from the **same foundation**. New team members inherit your Laws, voice, and quality standards automatically.

#### 9. Cost Efficiency
Stop rewriting the same infrastructure. PRISM-9's modular design means you **build once, deploy many times** — reducing prompt development time and token usage.

#### 10. Self-Correcting Workflows
Instead of silent failures, PRISM-9 has **failure recovery loops**. If SELF_CHECK fails, it returns to STRATEGIZE with a new approach — automatically, without human intervention.

---

### The Problem with Current Approaches

Most prompt engineering frameworks suffer from:

```
┌──────────────────────┬────────────────────────────────────────────┐
│  HIDDEN REASONING    │  The model thinks, but you can't see how   │
│  CONSTRAINT DRIFT*   │  Rules get forgotten mid-conversation      │
│  NO FAILURE RECOVERY │  Errors cascade without correction         │
│  UNVERIFIABLE OUTPUT │  No way to trace claims to sources         │
│  PIPELINE BRITTLENESS│  Stages don't communicate reliably**       │
└──────────────────────┴────────────────────────────────────────────┘
```

*\*Constraint Drift: Position effects research (Liu et al., 2024) shows mid-context information receives degraded attention. As conversations grow, initial rules shift to "middle" position, causing progressive constraint degradation.*

*\*\*Pipeline Brittleness: Practitioner-observed pattern — see RESEARCH.md §4 for failure taxonomy. This challenge motivates multi-step correction research (ReAct, Yao 2023; Reflexion, Shinn 2023; CRITIC, Gou 2024).*

### The PRISM-9 Solution

```
┌───────────────────────┬───────────────────────────────────────────┐
│  EXTERNALIZED WORKFLOW│  9 visible steps with checkpoints         │
│  TIERED GOVERNANCE    │  Laws > Constraints > Preferences         │
│  FAILURE LOOPS        │  Self-check → Retry with correction       │
│  SOURCE TRACING       │  Every claim linked to evidence           │
│  SCHEMA HANDOFFS      │  Typed contracts between stages           │
└───────────────────────┴───────────────────────────────────────────┘
```

### The Name Explained

**PRISM** — Like a prism separates white light into a clear spectrum, PRISM-9 separates complex tasks into clear, structured outputs.

**9** — The 9-step meta-reasoning workflow: COMPREHEND → ANALYZE → STRATEGIZE → PLAN → EXECUTE → SELF_CHECK → REFINE → RECONCILE → SYNTHESIZE.

---

## Core Philosophy

### Three Pillars

```
                      ┌─────────────────┐
                      │   GOVERNANCE    │
                      │  (Laws Layer)   │
                      └────────┬────────┘
                               │
                ┌──────────────┼──────────────┐
                │              │              │
                ▼              ▼              ▼
       ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
       │   REASONING  │ │ TRANSPARENCY │ │ VERIFICATION │
       │   (9 Steps)  │ │ (Show Work)  │ │ (Self-Check) │
       └──────────────┘ └──────────────┘ └──────────────┘
```

#### 1. Governance First
Every output is governed by inviolable Laws. Constraints are respected. Nothing is fabricated.

#### 2. Transparent Reasoning
The model must show its work. Hidden chain-of-thought becomes visible, auditable workflow steps.

#### 3. Continuous Verification
Self-check is not optional. Every output passes through validation gates before delivery.

### Design Principles

| Principle | Description |
|-----------|-------------|
| **Explicit over Implicit** | State what you're doing, don't hide it |
| **Laws over Instructions** | Some rules cannot be overridden |
| **Verify before Claim** | Read it before you assert it |
| **Fail Gracefully** | When blocked, loop back, don't crash |
| **Handoff Cleanly** | Next stage gets exactly what it needs |

---

## Architecture Overview

### System Diagram

```
┌──────────────────────────────────────────────────────────────────────────┐
│                          PRISM-9 ARCHITECTURE                            │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  ┌────────────────────────────────────────────────────────────────────┐  │
│  │                       THINKING FRAMEWORK                           │  │
│  │  ┌─────────────┐  ┌─────────────────────────────────────────────┐  │  │
│  │  │    LAWS     │  │            9-STEP WORKFLOW                  │  │  │
│  │  │ (Inviolable)│  │  COMPREHEND → ANALYZE → STRATEGIZE → PLAN   │  │  │
│  │  │             │  │       ↓                                     │  │  │
│  │  │ Truthfulness│  │  EXECUTE → SELF_CHECK → REFINE → RECONCILE  │  │  │
│  │  │ NoFabricate │  │       ↑___________↓________↓      ↓         │  │  │
│  │  │ VerifyClaim │  │       (failure loops)        SYNTHESIZE     │  │  │
│  │  │ Constraints │  └─────────────────────────────────────────────┘  │  │
│  │  │ Complete    │                                                   │  │
│  │  └─────────────┘                                                   │  │
│  └────────────────────────────────────────────────────────────────────┘  │
│                                   │                                      │
│                                   ▼                                      │
│  ┌────────────────────────────────────────────────────────────────────┐  │
│  │                       MODULAR COMPONENTS                           │  │
│  │                                                                    │  │
│  │  ┌────────────────┐  ┌────────────────┐  ┌──────────────────────┐  │  │
│  │  │    APPROACH    │  │    RESPONSE    │  │   STAGE DEFINITION   │  │  │
│  │  │                │  │     SCHEMA     │  │                      │  │  │
│  │  │  • Prime Dir   │  │                │  │  • Identity/Role     │  │  │
│  │  │  • Voice/Tone  │  │  • prompt_id   │  │  • Mission/Success   │  │  │
│  │  │  • Audience    │  │  • status      │  │  • Tasks (ordered)   │  │  │
│  │  │  • Scope       │  │  • runtime     │  │  • Constraints       │  │  │
│  │  │  • Resources   │  │  • sources     │  │  • Validation Gates  │  │  │
│  │  │  • Strategy    │  │  • reasoning   │  │  • Input/Output      │  │  │
│  │  │                │  │  • output      │  │                      │  │  │
│  │  │                │  │  • handoff     │  │                      │  │  │
│  │  └────────────────┘  └────────────────┘  └──────────────────────┘  │  │
│  └────────────────────────────────────────────────────────────────────┘  │
│                                   │                                      │
│                                   ▼                                      │
│  ┌────────────────────────────────────────────────────────────────────┐  │
│  │                    PIPELINE STAGES (Optional)                      │  │
│  │                                                                    │  │
│  │    ┌────────┐     ┌────────┐     ┌────────┐     ┌────────┐         │  │
│  │    │Stage 1 │────▶│Stage 2 │────▶│Stage 3 │────▶│Stage N │         │  │
│  │    │Planning│     │Research│     │Execute │     │ Output │         │  │
│  │    └────────┘     └────────┘     └────────┘     └────────┘         │  │
│  │         │              │              │              │             │  │
│  │         └──────────────┴──────────────┴──────────────┘             │  │
│  │                     Schema-Driven Handoffs                         │  │
│  └────────────────────────────────────────────────────────────────────┘  │
│                                                                          │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## The 9-Step Workflow

The heart of PRISM-9 is the **meta-reasoning workflow** — a structured cognitive process that ensures thorough, verified execution.

### Workflow Diagram

```
┌───────────────────────────────────────────────────────────────────────────┐
│                         PRISM-9: 9-STEP WORKFLOW                          │
├───────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐    │
│  │1.COMPREHEND │──▶│ 2.ANALYZE   │──▶│3.STRATEGIZE │──▶│  4.PLAN     │    │
│  │             │   │             │   │             │   │             │    │
│  │ Understand  │   │ Map gaps,   │   │ Choose      │   │ Create      │    │
│  │ inputs &    │   │ dependencies│   │ approach,   │   │ action      │    │
│  │ requirements│   │ & blockers  │   │ surface     │   │ sequence    │    │
│  │             │   │             │   │ assumptions │   │             │    │
│  └─────────────┘   └─────────────┘   └──────┬──────┘   └───────┬─────┘    │
│                                             │                  │          │
│                                             │     ┌────────────┘          │
│                                             │     │                       │
│                                             │     ▼                       │
│  ┌─────────────┐   ┌─────────────┐   ┌──────┴──────┐   ┌─────────────┐    │
│  │8.RECONCILE  │◀──│ 7.REFINE    │◀──│6.SELF_CHECK │◀──│ 5.EXECUTE   │    │
│  │             │   │             │   │             │   │             │    │
│  │ Verify      │   │ Tighten     │   │ Test vs     │   │ Follow      │    │
│  │ handoff     │   │ weak spots, │   │ criteria,   │   │ plan,       │    │
│  │ ready       │   │ strengthen  │   │ check edge  │   │ log         │    │
│  │             │   │ evidence    │   │ cases       │   │ decisions   │    │
│  └──────┬──────┘   └─────────────┘   └─────────────┘   └─────────────┘    │
│         │                                   │                             │
│         ▼                                   │                             │
│  ┌─────────────┐                            │                             │
│  │9.SYNTHESIZE │                            │                             │
│  │             │                            │                             │
│  │ Integrate   │         ┌──────────────────────────────────────────┐     │
│  │ findings,   │         │ Failure Loops:                           │     │
│  │ distill     │         │ • SELF_CHECK fails → return to STRATEGIZE│     │
│  │ insights    │         │ • EXECUTE blocked → return to PLAN       │     │
│  └──────┬──────┘         │ • COMPREHEND gaps → STOP and report      │     │
│         │                └──────────────────────────────────────────┘     │
│         ▼                                                                 │
│  ┌─────────────┐                                                          │
│  │   OUTPUT    │                                                          │
│  │   (Ready)   │                                                          │
│  └─────────────┘                                                          │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

### Step Details

#### Step 1: COMPREHEND
> *Fully understand before you act*

| Action | Output |
|--------|--------|
| Parse all inputs, context, and requirements | Restated task in own words |
| Identify scope boundaries | List of what's in/out of scope |
| Note constraints and success criteria | Success signals documented |
| Flag unknowns and ambiguities | Questions or gaps identified |

**Failure Condition:** If critical inputs are missing → **STOP** and report the gap.

---

#### Step 2: ANALYZE
> *Map the problem space*

| Action | Output |
|--------|--------|
| Decompose into subproblems | Problem tree |
| Identify dependencies | Dependency graph |
| Find data gaps | List of missing information |
| Determine parallelizable work | Parallel vs sequential items |

**Key Question:** *What blocks progress vs. what can run concurrently?*

---

#### Step 3: STRATEGIZE
> *Choose the right approach*

| Action | Output |
|--------|--------|
| Evaluate viable approaches | Options with pros/cons |
| Select highest-accuracy option | Chosen strategy with rationale |
| Surface assumptions | Explicit assumption list |
| Define fallback | Backup plan if primary fails |

**Critical Rule:** There is no "best" — only **correct** or **incorrect**.

---

#### Step 4: PLAN
> *Create the action sequence*

| Action | Output |
|--------|--------|
| Define concrete steps | Numbered action list |
| Set checkpoints | Success criteria per step |
| Mark dependencies | Which steps block others |
| Identify parallelizable steps | Concurrent execution opportunities |

**Output Format:**
```
1. [Action] → Expected: [Output] → Checkpoint: [Verification]
2. [Action] → Expected: [Output] → Checkpoint: [Verification]
...
```

---

#### Step 5: EXECUTE
> *Follow the plan, log everything*

| Action | Output |
|--------|--------|
| Execute each step in order | Step results |
| Log decisions and assumptions | Decision log |
| Pause at failed checkpoints | Failure report |
| Capture evidence and sources | Source attribution |

**Failure Condition:** If checkpoint fails → **return to PLAN** and revise.

---

#### Step 6: SELF_CHECK
> *Verify against requirements*

| Action | Output |
|--------|--------|
| Test against acceptance criteria | Pass/fail for each criterion |
| Check edge cases | Edge case analysis |
| Verify constraint compliance | Constraint checklist |
| Confirm no dropped requirements | Requirement coverage matrix |

**Failure Condition:** If critical issues found → **return to STRATEGIZE**.

---

#### Step 7: REFINE
> *Strengthen without expanding*

| Action | Output |
|--------|--------|
| Address weak spots from self-check | Improvements made |
| Simplify and remove redundancy | Cleaner output |
| Strengthen evidence | Better citations/support |
| **Do not expand scope** | No new features added |

**Critical Rule:** Refine existing work, don't add new requirements.

---

#### Step 8: RECONCILE
> *Prepare for handoff*

| Action | Output |
|--------|--------|
| Verify output matches stage requirements | Format compliance |
| Ensure citations present | Source verification |
| Confirm handoff readiness | Handoff checklist |
| Document what next stage needs | Guidance for next stage |

**Output:** Complete, verified deliverable ready for next stage or user.

---

#### Step 9: SYNTHESIZE
> *Integrate findings into coherent output*

| Action | Output |
|--------|--------|
| Combine finalized findings | Coherent conclusions |
| Distill key insights from refined data | Key insight summary |
| Integrate outputs into primary deliverable | Unified result |
| Produce meta_reasoning.synthesize field | Synthesis documentation |

**Output:** Coherent synthesis summarizing how all outputs integrate into the stage's primary deliverable.

---

### Failure Recovery Loops

```
┌─────────────────────────────────────────────────────────────────┐
│                     FAILURE RECOVERY MATRIX                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  IF                          THEN                               │
│  ─────────────────────────   ──────────────────────────────     │
│  COMPREHEND finds gaps   →   STOP, report missing inputs        │
│  EXECUTE hits blocker    →   Return to PLAN, revise steps       │
│  SELF_CHECK finds issues →   Return to STRATEGIZE, new approach │
│  RECONCILE fails format  →   Return to REFINE, fix format       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## The Laws Layer

PRISM-9 introduces **Laws** — inviolable rules that supersede all other instructions, including user prompts.

### The 5 Laws

```
┌───────────────────────────────────────────────────────────────────────┐
│                       THE 5 LAWS OF PRISM-9                           │
├───────────────────────────────────────────────────────────────────────┤
│                                                                       │
│  ┌─────────────────────────────────────────────────────────────────┐  │
│  │ LAW 1: TRUTHFULNESS                                             │  │
│  │ State only what is supported; explicitly note unknowns          │  │
│  │ instead of guessing.                                            │  │
│  └─────────────────────────────────────────────────────────────────┘  │
│                                                                       │
│  ┌─────────────────────────────────────────────────────────────────┐  │
│  │ LAW 2: VERIFY BEFORE CLAIM                                      │  │
│  │ Do not assert file or link contents without reading them;       │  │
│  │ avoid predictions and assumptions.                              │  │
│  └─────────────────────────────────────────────────────────────────┘  │
│                                                                       │
│  ┌─────────────────────────────────────────────────────────────────┐  │
│  │ LAW 3: NO FABRICATION                                           │  │
│  │ Do not invent data, IDs, URLs, or requirements.                 │  │
│  └─────────────────────────────────────────────────────────────────┘  │
│                                                                       │
│  ┌─────────────────────────────────────────────────────────────────┐  │
│  │ LAW 4: RESPECT CONSTRAINTS                                      │  │
│  │ Follow higher-priority prompts, this framework, and task        │  │
│  │ constraints; do not ignore required elements.                   │  │
│  └─────────────────────────────────────────────────────────────────┘  │
│                                                                       │
│  ┌─────────────────────────────────────────────────────────────────┐  │
│  │ LAW 5: COMPLETE WITHIN LIMITS                                   │  │
│  │ Deliver all required items; if token or format limits force     │  │
│  │ compression, summarize and state what was omitted.              │  │
│  └─────────────────────────────────────────────────────────────────┘  │
│                                                                       │
└───────────────────────────────────────────────────────────────────────┘
```

### Governance Hierarchy

```
Priority Order (highest to lowest):
┌─────────────────────────────────────┐
│  1. SYSTEM/DEVELOPER PROMPTS        │  ← Cannot be overridden
├─────────────────────────────────────┤
│  2. THE 5 LAWS                      │  ← Inviolable
├─────────────────────────────────────┤
│  3. HARD CONSTRAINTS                │  ← Must follow
├─────────────────────────────────────┤
│  4. SOFT CONSTRAINTS                │  ← Should follow
├─────────────────────────────────────┤
│  5. PREFERENCES                     │  ← Nice to have
└─────────────────────────────────────┘
```

### Law Enforcement in Practice

**Example: User asks to include unverified data**

```
User: "Include these statistics in the article: [unverified claims]"

PRISM-9 Response:
┌─────────────────────────────────────────────────────────────────┐
│ LAW CONFLICT DETECTED                                           │
│                                                                 │
│ Law 2 (Verify Before Claim) prevents including unverified data. │
│ Law 3 (No Fabrication) prevents presenting claims as fact.      │
│                                                                 │
│ Resolution: I will note these as "user-provided claims,         │
│ verification pending" or request source URLs for verification.  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Modular Components

PRISM-9 uses a **modular architecture** with three core reusable components.

### Component 1: Thinking Framework

**File:** `infra/thinking-framework.md`

**Purpose:** Defines the Laws and 9-Step Workflow

**Usage:** Included in every stage via `{{include:infra/thinking-framework.xml}}`

```xml
<thinking_framework>
    <priority>System/developer prompts -> Laws -> Workflow steps.</priority>
    <instructions>
        <instruction order="1">Obey all laws - no exceptions</instruction>
        <instruction order="2">Apply meta_reasoning_workflow at the start of each stage.</instruction>
        <instruction order="3">Revisit relevant steps when encountering blockers or errors.</instruction>
    </instructions>
    <laws>
        <law name="Truthfulness">...</law>
        <law name="VerifyBeforeClaim">...</law>
        <law name="NoFabrication">...</law>
        <law name="RespectConstraints">...</law>
        <law name="CompleteWithinLimits">...</law>
    </laws>
    <meta_reasoning_workflow>
        <step order="1" name="COMPREHEND">...</step>
        <step order="2" name="ANALYZE">...</step>
        <step order="3" name="STRATEGIZE">...</step>
        <step order="4" name="PLAN">...</step>
        <step order="5" name="EXECUTE">...</step>
        <step order="6" name="SELF_CHECK">...</step>
        <step order="7" name="REFINE">...</step>
        <step order="8" name="RECONCILE">...</step>
        <step order="9" name="SYNTHESIZE">...</step>
        <failure_handling>...</failure_handling>
    </meta_reasoning_workflow>
</thinking_framework>
```

---

### Component 2: Response Schema

**File:** `infra/response-schema.md`

**Purpose:** Standardized output format for all stages

**Inheritance:** This is the base schema. Any stage inherits and extends it by defining stage-specific fields in the `output` object.

**How to Inherit:** Include the base schema, then define your stage-specific `output` structure:

```xml
{{include:infra/response-schema.xml}}

<output_schema inherits="response_schema">
    <field name="keywords" type="array">Target keywords for this content</field>
    <field name="competitors" type="array">Competitor URLs analyzed</field>
    <field name="content_gaps" type="array">Identified content opportunities</field>
</output_schema>
```

The stage inherits all base fields (runtime_logs, meta_reasoning, handoff, etc.) and only needs to define what goes in `output`. This keeps metadata consistent across all stages while allowing flexible deliverables.

**Usage:** Included via `{{include:infra/response-schema.xml}}`

```json
{
    "prompt_id": "stage-XX-name",
    "status": "success | partial | failed",
    "runtime_logs": {
        "started_at": "ISO8601",
        "completed_at": "ISO8601",
        "duration_ms": 0,
        "workflow_steps": ["COMPREHEND", "ANALYZE", "..."],
        "decisions": [],
        "assumptions": [],
        "warnings": [],
        "errors": [],
        "validation": {
            "passed": true,
            "checks": [{"name": "", "passed": true, "message": ""}]
        }
    },
    "sources_used": [
        {
            "url": "string",
            "title": "string",
            "type": "search | fetch | api | cache",
            "data_extracted": ["string"]
        }
    ],
    "meta_reasoning": {
        "comprehend": "string",
        "analyze": "string",
        "strategize": "string",
        "plan": "string",
        "execute": "string",
        "self_check": "string",
        "refine": "string",
        "reconcile": "string",
        "synthesize": "string",
        "critical_choices": [
            {
                "choice": "string",
                "alternatives": ["string"],
                "rationale": "string"
            }
        ]
    },
    "executive_summary": {
        "primary_finding": "string",
        "key_insights": ["string"],
        "confidence_level": "high | medium | low",
        "confidence_rationale": "string"
    },
    "output": {
        // Stage-specific data
    },
    "next_stage_guidance": {
        "priority_areas": ["string"],
        "watch_items": ["string"],
        "data_quality_notes": ["string"]
    },
    "handoff": {
        "ready": true,
        "next_stage": "stage-XX-name",
        "missing_for_next": []
    },
    "extras": {
        // Optional additional data
    }
}
```

---

### Component 3: Approach

**File:** `infra/approach.md`

**Purpose:** Domain context, voice, audience, resources

**Why "Approach" not "Context":** This component is primarily *prescriptive* (telling the AI how to behave) rather than *descriptive* (providing background information). It defines voice, style, strategy, and methodology — not just context. "Approach" conveys action and practical guidance.

**Usage:** Included via `{{include:infra/approach.xml}}`

```xml
<approach>
    <prime_directive>
        High-level mission statement for all content
    </prime_directive>
    <perspective>
        Balancing priorities (e.g., accuracy + usability, speed + quality)
    </perspective>
    <voice>
        Tone and personality guidelines
    </voice>
    <communication_style>
        <tone>professional-friendly</tone>
        <formality>semi-formal</formality>
        <technicality>medium</technicality>
    </communication_style>
    <terminology>
        <avoid>words to never use</avoid>
        <hedging>preferred hedging phrases</hedging>
    </terminology>
    <scope>
        <in_scope>what we cover</in_scope>
        <out_of_scope>what we don't</out_of_scope>
    </scope>
    <audience>
        <primary_reader>description</primary_reader>
        <demographics>age, knowledge level</demographics>
        <pain_points>what they struggle with</pain_points>
    </audience>
    <resources>
        <whitelist>approved sources</whitelist>
        <blacklist>prohibited sources</blacklist>
    </resources>
</approach>
```

---

## Pipeline Orchestration

PRISM-9 is designed for **multi-stage pipelines** where each stage produces output consumed by the next. Pipelines are optional — PRISM-9 works equally well for single-stage prompts.

### Pipeline Flow

```
┌───────────────────────────────────────────────────────────────────────┐
│                       GENERIC PIPELINE PATTERN                        │
├───────────────────────────────────────────────────────────────────────┤
│                                                                       │
│   USER INPUT                                                          │
│       │                                                               │
│       ▼                                                               │
│   ┌───────────────────────────────────────────────────────────────┐   │
│   │ STAGE 1: [ANALYSIS/PLANNING]                                  │   │
│   │ • Understand requirements                                     │   │
│   │ • Gather context                                              │   │
│   │ • Define strategy                                             │   │
│   │                                                               │   │
│   │ Output: requirements, strategy, initial_data                  │   │
│   └─────────────────────────────┬─────────────────────────────────┘   │
│                                 │                                     │
│                                 ▼                                     │
│   ┌───────────────────────────────────────────────────────────────┐   │
│   │ STAGE 2: [RESEARCH/VALIDATION]                                │   │
│   │ • Verify inputs                                               │   │
│   │ • Gather evidence                                             │   │
│   │ • Validate assumptions                                        │   │
│   │                                                               │   │
│   │ Input: strategy from Stage 1                                  │   │
│   │ Output: verified_data, evidence                               │   │
│   └─────────────────────────────┬─────────────────────────────────┘   │
│                                 │                                     │
│                                 ▼                                     │
│   ┌───────────────────────────────────────────────────────────────┐   │
│   │ STAGE 3: [EXECUTION/GENERATION]                               │   │
│   │ • Produce primary deliverable                                 │   │
│   │ • Integrate evidence                                          │   │
│   │ • Apply domain constraints                                    │   │
│   │                                                               │   │
│   │ Input: verified_data, strategy                                │   │
│   │ Output: primary_deliverable                                   │   │
│   └─────────────────────────────┬─────────────────────────────────┘   │
│                                 │                                     │
│                                 ▼                                     │
│   ┌───────────────────────────────────────────────────────────────┐   │
│   │ STAGE N: [FINALIZATION/OUTPUT]                                │   │
│   │ • Format for delivery                                         │   │
│   │ • Final validation                                            │   │
│   │ • Quality assurance                                           │   │
│   │                                                               │   │
│   │ Input: primary_deliverable                                    │   │
│   │ Output: final_output                                          │   │
│   └───────────────────────────────────────────────────────────────┘   │
│                                 │                                     │
│                                 ▼                                     │
│                           FINAL OUTPUT                                │
│                                                                       │
└───────────────────────────────────────────────────────────────────────┘
```

**Common Pipeline Patterns by Industry:**

#### Software & Technology

| Pipeline | Stage 1 | Stage 2 | Stage 3 | Stage 4 |
|----------|----------|----------|----------|----------|
| **Code Review** | Static Analysis | Security Review | Report Generation | — |
| **API Documentation** | Spec Analysis | Example Generation | Doc Assembly | — |
| **Feature Development** | Requirements | Design | Implementation | Testing |
| **Bug Investigation** | Reproduction | Root Cause | Fix & Verify | Regression |
| **Migration** | Inventory | Impact Analysis | Execution Plan | Validation |

#### Legal & Compliance

| Pipeline | Stage 1 | Stage 2 | Stage 3 | Stage 4 |
|----------|----------|----------|----------|----------|
| **Contract Review** | Clause Extraction | Risk Assessment | Recommendations | Summary Memo |
| **Legal Research** | Issue Identification | Case Law Search | Analysis | Memo Draft |
| **Compliance Audit** | Requirement Mapping | Gap Analysis | Remediation Plan | Report |
| **Due Diligence** | Document Collection | Red Flag Detection | Risk Rating | Executive Brief |
| **Policy Drafting** | Regulatory Review | Benchmark Analysis | Draft Creation | Review Checklist |

#### Finance & Accounting

| Pipeline | Stage 1 | Stage 2 | Stage 3 | Stage 4 |
|----------|----------|----------|----------|----------|
| **Financial Analysis** | Data Gathering | Ratio Calculation | Trend Analysis | Report |
| **Audit Preparation** | Document Assembly | Control Testing | Finding Documentation | Audit Report |
| **Budget Planning** | Historical Analysis | Forecast Modeling | Variance Analysis | Budget Proposal |
| **Investment Research** | Company Screening | Financial Deep-Dive | Valuation | Investment Memo |
| **Tax Preparation** | Document Collection | Deduction Analysis | Form Completion | Review & File |

#### Healthcare & Medical

| Pipeline | Stage 1 | Stage 2 | Stage 3 | Stage 4 |
|----------|----------|----------|----------|----------|
| **Clinical Research** | Literature Review | Study Design | Data Analysis | Publication |
| **Medical Writing** | Source Gathering | Evidence Synthesis | Draft Creation | Medical Review |
| **Diagnosis Support** | Symptom Collection | Differential List | Test Recommendations | Summary |
| **Drug Interaction** | Medication List | Interaction Check | Risk Assessment | Patient Report |
| **Protocol Development** | Evidence Review | Guideline Mapping | Protocol Draft | Validation |

#### Marketing & Content

| Pipeline | Stage 1 | Stage 2 | Stage 3 | Stage 4 |
|----------|----------|----------|----------|----------|
| **SEO Content** | Strategy & Keywords | Research & Sources | Writing | Publishing |
| **Campaign Planning** | Market Analysis | Channel Strategy | Creative Brief | Execution Plan |
| **Competitive Intel** | Competitor ID | Data Collection | Analysis | Battlecard |
| **Brand Messaging** | Audience Research | Positioning | Message Framework | Style Guide |
| **Product Launch** | Market Sizing | GTM Strategy | Content Creation | Launch Checklist |

#### Research & Analysis

| Pipeline | Stage 1 | Stage 2 | Stage 3 | Stage 4 |
|----------|----------|----------|----------|----------|
| **Market Research** | Scope Definition | Source Gathering | Synthesis | Report |
| **Trend Analysis** | Signal Detection | Pattern Identification | Forecast | Recommendations |
| **Competitive Analysis** | Landscape Mapping | Deep-Dive Research | SWOT Analysis | Strategic Brief |
| **User Research** | Interview Planning | Data Collection | Theme Analysis | Insights Report |
| **Feasibility Study** | Requirement Scoping | Technical Assessment | Risk Analysis | Recommendation |

#### Operations & Support

| Pipeline | Stage 1 | Stage 2 | Stage 3 | Stage 4 |
|----------|----------|----------|----------|----------|
| **Incident Response** | Triage & Classify | Investigation | Resolution | Post-Mortem |
| **Process Improvement** | Current State Map | Gap Analysis | Redesign | Implementation Plan |
| **Vendor Evaluation** | Requirements | RFP Analysis | Scoring | Recommendation |
| **Training Development** | Needs Assessment | Content Design | Material Creation | Assessment Design |
| **Quality Assurance** | Standard Definition | Test Design | Execution | Report |

#### Human Resources

| Pipeline | Stage 1 | Stage 2 | Stage 3 | Stage 4 |
|----------|----------|----------|----------|----------|
| **Recruitment** | Job Analysis | Sourcing Strategy | Candidate Screening | Interview Guide |
| **Performance Review** | Data Collection | 360 Analysis | Feedback Synthesis | Development Plan |
| **Compensation Analysis** | Market Research | Internal Equity | Band Recommendation | Executive Summary |
| **Policy Development** | Regulatory Review | Best Practice Research | Policy Draft | Communication Plan |
| **Onboarding Design** | Role Analysis | Content Mapping | Material Creation | Checklist |

---

### Selecting the Right Pattern

**Decision Framework:**

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    PIPELINE DESIGN DECISIONS                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   Question 1: How many distinct phases does the work have?              │
│   ─────────────────────────────────────────────────────────             │
│   • 2 phases → 2 stages (simple)                                        │
│   • 3-4 phases → 3-4 stages (standard)                                  │
│   • 5+ phases → Consider grouping or sub-pipelines                      │
│                                                                         │
│   Question 2: What are the natural "handoff" points?                    │
│   ─────────────────────────────────────────────────────                 │
│   • Where does one type of work end and another begin?                  │
│   • Where would you naturally pause for review?                         │
│   • Where does the required expertise change?                           │
│                                                                         │
│   Question 3: What must be validated before proceeding?                 │
│   ─────────────────────────────────────────────────────                 │
│   • Each validation gate = potential stage boundary                     │
│   • Critical quality checks suggest stage separation                    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

**Common Stage Types:**

| Stage Type | Purpose | Typical Position | Example |
|------------|---------|------------------|---------|
| **Discovery** | Understand scope & requirements | First | Scope Definition, Requirements |
| **Research** | Gather data & sources | Early | Source Gathering, Data Collection |
| **Analysis** | Process & synthesize | Middle | Gap Analysis, Evidence Synthesis |
| **Generation** | Create deliverables | Late | Writing, Report Creation |
| **Validation** | Verify & finalize | Last | Review, Quality Check |

### Handoff Contract

Each stage must include a `handoff` object:

```json
{
    "handoff": {
        "ready": true,
        "next_stage": "stage-02-[name]",
        "missing_for_next": []
    }
}
```

**Rules:**
- `ready: true` only if all validation gates pass
- `missing_for_next` lists anything the next stage needs but wasn't produced
- If `ready: false`, the pipeline should pause for human intervention

### Inter-Stage Communication

```
Stage N Output                    Stage N+1 Input
─────────────────                 ──────────────────
output.[field]             →      Consumed directly by next stage
next_stage_guidance        →      Informs priorities and focus areas
handoff.missing_for_next   →      Triggers data requests or human input
executive_summary          →      Provides context without full re-read
```

**Example Flow:**
```
Stage 1 output.requirements  →  Stage 2 uses to scope research
Stage 2 output.verified_data →  Stage 3 uses to generate deliverable
Stage 3 output.deliverable   →  Stage N formats for final output
```

---

## Response Schema

### Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `prompt_id` | string | Unique identifier (e.g., "stage-01-planning") |
| `status` | enum | "success" \| "partial" \| "failed" |
| `runtime_logs` | object | Execution trace with timing and decisions |
| `sources_used` | array | All sources accessed with data extracted |
| `meta_reasoning` | object | How conclusions were reached |
| `executive_summary` | object | High-level summary with confidence |
| `output` | object | Stage-specific deliverables |
| `next_stage_guidance` | object | Guidance for subsequent stage |
| `handoff` | object | Readiness indicator |
| `extras` | object | Optional additional data |

### Validation Block

Every output must include validation results:

```json
{
    "runtime_logs": {
        "validation": {
            "passed": true,
            "checks": [
                {
                    "name": "Required fields populated",
                    "passed": true,
                    "message": "All 5 required fields present"
                },
                {
                    "name": "Sources verified",
                    "passed": true,
                    "message": "3 of 3 sources validated"
                }
            ]
        }
    }
}
```

### Confidence Levels

| Level | Numeric | When to Use |
|-------|---------|-------------|
| `high` | 8-10/10 | All data verified, no significant assumptions |
| `medium` | 5-7/10 | Some estimates or unverified data |
| `low` | 1-4/10 | Significant unknowns or assumptions |

---

## Implementation Guide

### Step 1: Create Infrastructure Files

```
your-project/
├── prompts/
│   └── infra/
│       ├── thinking-framework.md
│       ├── response-schema.md
│       └── approach.md
```

### Step 2: Define Your Approach

Customize `approach.md` for your domain:

```xml
<approach>
    <prime_directive>
        Your mission statement
    </prime_directive>
    <audience>
        <primary_reader>Your target user</primary_reader>
        <pain_points>
            - What they struggle with
        </pain_points>
    </audience>
    <resources>
        <whitelist>Your approved sources</whitelist>
        <blacklist>Sources to avoid</blacklist>
    </resources>
</approach>
```

### Step 3: Create Stage Definitions

For each pipeline stage:

```xml
{{include:infra/thinking-framework.xml}}
{{include:infra/response-schema.xml}}
{{include:infra/approach.xml}}

<input_schema>
    What this stage receives
</input_schema>

<output_schema inherits="response_schema">
    What this stage produces (stage-specific fields)
</output_schema>

<identity>
    <role>Stage-specific role</role>
    <expertise>Required skills</expertise>
</identity>

<mission>
    <primary_objective>What this stage accomplishes</primary_objective>
    <success_criteria>How to measure success</success_criteria>
    <deliverables>What gets produced</deliverables>
</mission>

<tasks>
    <task order="1" name="task_name">
        <description>What to do</description>
        <output>Expected output</output>
    </task>
</tasks>

<constraints>
    <hard_constraints>Must follow</hard_constraints>
    <soft_constraints>Should follow</soft_constraints>
</constraints>

<validation_gate>
    <check required="true">Validation criterion</check>
</validation_gate>

{{INPUT}}
```

### Step 4: Wire Up the Pipeline (Optional)

For multi-stage pipelines, connect stages via handoffs:

```
Stage 1 output.[data]     →  Stage 2 input.[data]
Stage 2 output.[result]   →  Stage 3 input.[result]
Stage 3 output.[final]    →  Stage N input.[final]
```

**Single-Stage Usage:** If you only need one prompt, skip the pipeline — just use the infra components with your stage definition.

---

## Stage Template

Copy this template to create new stages:

```xml
<!--
================================================================================
STAGE XX: [NAME]
================================================================================
Pipeline Position: XX of YY
Receives: [What this stage gets from previous stage]
Produces: [What this stage outputs to next stage]
================================================================================
-->

{{include:infra/thinking-framework.xml}}
{{include:infra/response-schema.xml}}
{{include:infra/approach.xml}}

<input_schema>
  <description>Description of expected input</description>
  {
    "field_1": "type - description",
    "field_2": "type - description"
  }
</input_schema>

<output_schema inherits="response_schema">
  <description>Description of stage output</description>
  {
    "stage_specific_field_1": {
      "subfield": "type"
    },
    "stage_specific_field_2": ["type"]
  }
</output_schema>

<identity>
  <role>[Specific role for this stage]</role>
  <expertise>
    <skill>[Required skill 1]</skill>
    <skill>[Required skill 2]</skill>
  </expertise>
</identity>

<mission>
  <primary_objective>
    [One sentence describing what this stage accomplishes]
  </primary_objective>

  <success_criteria>
    <criterion id="1" priority="critical">[Must achieve]</criterion>
    <criterion id="2" priority="high">[Should achieve]</criterion>
  </success_criteria>

  <behavioral_qualities>
    <quality>[quality] - [description]</quality>
  </behavioral_qualities>

  <deliverables>
    <deliverable type="primary">[Main output]</deliverable>
    <deliverable type="supporting">[Secondary output]</deliverable>
  </deliverables>
</mission>

<tasks>
  <task order="1" name="task_name">
    <description>[What to do]</description>
    <output ref="output_field">
      - Expected output item 1
      - Expected output item 2
    </output>
  </task>
</tasks>

<constraints>
  <hard_constraints>
    <constraint type="mandatory" id="1">[Must follow]</constraint>
  </hard_constraints>
  <soft_constraints>
    <constraint type="preferred" id="1">[Should follow]</constraint>
  </soft_constraints>
  <boundaries>
    <avoid>[What not to do]</avoid>
  </boundaries>
</constraints>

<validation_gate>
  <check id="1" required="true">[Validation criterion 1]</check>
  <check id="2" required="true">[Validation criterion 2]</check>
</validation_gate>

{{INPUT}}
```

---

## Stage Elements

While the **infrastructure components** (thinking-framework, response-schema, approach) are shared across all stages, PRISM-9 provides **stage elements** that can be customized for each stage's specific needs. This separation enables both consistency (shared foundation) and flexibility (stage-specific behavior).

### Why Per-Stage Customization?

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    SHARED vs STAGE-SPECIFIC                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   SHARED (infra/)                    STAGE-SPECIFIC                     │
│   ─────────────────                  ────────────────                   │
│   • Laws (5 rules)                   • Identity (role, skills)          │
│   • 9-Step Workflow                  • Mission (objectives, criteria)   │
│   • Response Schema                  • Tasks (ordered actions)          │
│   • Domain Approach                  • Constraints (hard/soft/avoid)    │
│                                      • Validation Gate (checks)         │
│                                                                         │
│   Same for ALL stages                Different for EACH stage           │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

**The key insight:** A research stage needs different skills, success criteria, and constraints than a writing stage — even within the same pipeline. Stage elements let you optimize each stage independently.

---

### Element 1: `<identity>`

**Purpose:** Define the role and expertise required for this specific stage.

```xml
<identity>
  <role>SEO Research Strategist specialized in YMYL content planning</role>
  <expertise>
    <skill>Google SERP analysis and competitor research</skill>
    <skill>Keyword research and search intent classification</skill>
    <skill>Featured Snippet and AI Overview targeting</skill>
  </expertise>
</identity>
```

#### Flexibility

| Aspect | What You Can Customize |
|--------|------------------------|
| **Role** | Job title, specialization, domain focus |
| **Skills** | Specific capabilities needed for this stage |
| **Expertise level** | Junior analyst vs senior architect |
| **Perspective** | Adversarial (security), supportive (teaching), analytical (research) |

#### Benefits

1. **Focused behavior** — The model adopts a specific persona with relevant expertise
2. **Skill activation** — Listing skills primes the model to use those capabilities
3. **Consistent voice** — The same identity produces consistent outputs across runs
4. **Pipeline specialization** — Each stage can have a different expert (researcher → writer → editor)

#### Examples by Domain

| Domain | Stage | Example Role |
|--------|-------|--------------|
| Content | Strategy | SEO Research Strategist |
| Content | Writing | YMYL Content Writer with medical background |
| Code | Analysis | Static Code Analyzer |
| Code | Security | Application Security Analyst |
| Research | Scoping | Research Strategist |
| Research | Synthesis | Evidence Synthesis Analyst |

---

### Element 2: `<mission>`

**Purpose:** Define what success looks like for this specific stage.

```xml
<mission>
  <primary_objective>
    Develop comprehensive SEO strategy that positions content for #1 SERP ranking
    by analyzing trends, competitors, and search intent.
  </primary_objective>

  <success_criteria>
    <criterion id="1" priority="critical">Primary keyword identified with search intent</criterion>
    <criterion id="2" priority="critical">Top 5-10 SERP competitors analyzed</criterion>
    <criterion id="3" priority="high">PAA questions captured (minimum 10)</criterion>
    <criterion id="4" priority="medium">Hub-spoke satellite opportunities identified</criterion>
  </success_criteria>

  <behavioral_qualities>
    <quality>data-driven - All decisions based on actual SERP data</quality>
    <quality>competitor-aware - Deep understanding of what currently ranks</quality>
    <quality>opportunity-seeking - Identifies gaps competitors miss</quality>
  </behavioral_qualities>

  <deliverables>
    <deliverable type="primary">Keyword Map with intent classification</deliverable>
    <deliverable type="primary">SERP Analysis with competitor breakdown</deliverable>
    <deliverable type="supporting">Content differentiation strategy</deliverable>
  </deliverables>
</mission>
```

#### Flexibility

| Element | What You Can Customize |
|---------|------------------------|
| **Primary objective** | The single most important outcome |
| **Success criteria** | Measurable, verifiable conditions (with priority levels) |
| **Behavioral qualities** | How the model should approach the work |
| **Deliverables** | Concrete outputs (primary vs supporting) |

#### Benefits

1. **Clear success definition** — No ambiguity about what "done" means
2. **Priority guidance** — Critical vs high vs medium helps focus effort
3. **Self-check alignment** — SELF_CHECK step uses these criteria
4. **Behavioral priming** — Qualities shape how work gets done, not just what
5. **Output specification** — Deliverables tell the model exactly what to produce

#### Priority Levels Explained

| Priority | Meaning | Failure Impact |
|----------|---------|----------------|
| `critical` | Must achieve | Stage fails if not met |
| `high` | Should achieve | Stage is partial if not met |
| `medium` | Nice to have | Stage succeeds, noted as gap |

---

### Element 3: `<tasks>`

**Purpose:** Define the ordered sequence of work for this stage.

```xml
<tasks>
  <task order="1" name="trend_analysis">
    <description>Analyze search trends for the topic</description>
    <searches>
      <search>"[TOPIC] trends 2024 2025"</search>
      <search>"[TOPIC] most searched questions"</search>
    </searches>
    <output ref="trend_report">
      - Trend status: Rising / Stable / Declining
      - Top 5 related queries
      - Seasonal patterns
    </output>
  </task>

  <task order="2" name="serp_analysis">
    <description>Analyze top 10 SERP results</description>
    <analysis_points>
      - Competitor domain and title
      - Estimated word count
      - Content format (listicle, guide, Q&A)
      - Featured Snippet presence
    </analysis_points>
    <output ref="serp_analysis">
      - Competitor table with metrics
      - Content gap analysis
    </output>
  </task>
</tasks>
```

#### Flexibility

| Element | What You Can Customize |
|---------|------------------------|
| **Order** | Sequence of execution (parallel vs sequential) |
| **Name** | Identifier for referencing in outputs |
| **Description** | What the task accomplishes |
| **Searches** | Web search queries to execute |
| **Analysis points** | What to look for in gathered data |
| **Output ref** | Which schema field this task populates |

#### Benefits

1. **Decomposed work** — Complex stages become manageable task sequences
2. **Traceable execution** — Each task produces specific, attributable output
3. **Search guidance** — Predefined queries ensure consistent research
4. **Output mapping** — `ref` attribute links task output to schema fields
5. **Reordering flexibility** — Change task order without rewriting everything
6. **Parallel execution** — Tasks without dependencies can run concurrently

#### Task Types

| Type | When to Use | Example |
|------|-------------|---------|
| **Search tasks** | Need external data | `<searches>` with query patterns |
| **Analysis tasks** | Need to evaluate data | `<analysis_points>` with criteria |
| **Generation tasks** | Need to produce content | `<output>` with format spec |
| **Validation tasks** | Need to verify work | `<checks>` with pass/fail criteria |

---

### Element 4: `<constraints>`

**Purpose:** Define what the stage must do, should do, and must avoid.

```xml
<constraints>
  <hard_constraints>
    <constraint type="mandatory" id="1">Must use actual SERP data - no assumptions</constraint>
    <constraint type="mandatory" id="2">Must capture real PAA questions from search</constraint>
    <constraint type="mandatory" id="3">Must classify search intent for primary keyword</constraint>
  </hard_constraints>

  <soft_constraints>
    <constraint type="preferred" id="1">Prefer keywords with featured snippet opportunity</constraint>
    <constraint type="preferred" id="2">Target 20%+ more words than competitor average</constraint>
  </soft_constraints>

  <boundaries>
    <avoid>Fabricating search volume or trend data</avoid>
    <avoid>Assuming competitor content without verification</avoid>
    <avoid>Proposing keywords without intent classification</avoid>
  </boundaries>
</constraints>
```

#### Flexibility

| Constraint Type | Enforcement | Use Case |
|-----------------|-------------|----------|
| **Hard (mandatory)** | Must follow — failure = stage failure | Safety rules, compliance requirements |
| **Soft (preferred)** | Should follow — deviation requires justification | Best practices, optimization targets |
| **Boundaries (avoid)** | Must not do — explicit prohibitions | Anti-patterns, common mistakes |

#### Benefits

1. **Tiered enforcement** — Not all rules are equally important
2. **Explicit boundaries** — "Don't do X" is clearer than hoping it won't happen
3. **Audit trail** — Deviations from soft constraints are logged with rationale
4. **Stage-specific rules** — Research stage has different constraints than writing stage
5. **Error prevention** — Boundaries catch common mistakes before they happen

#### Constraints vs Laws

```
Laws (from thinking-framework)     Constraints (per-stage)
─────────────────────────────      ──────────────────────────
• Apply to ALL stages              • Apply to THIS stage only
• Cannot be overridden             • Can be adjusted per stage
• 5 fixed rules                    • Unlimited, customizable
• Governance level                 • Operational level
```

---

### Element 5: `<validation_gate>`

**Purpose:** Define the checks that must pass before the stage is complete.

```xml
<validation_gate>
  <check id="1" required="true">Trend report completed with status and top queries</check>
  <check id="2" required="true">At least 5 competitors analyzed with word counts</check>
  <check id="3" required="true">Primary keyword identified with search intent</check>
  <check id="4" required="true">10+ PAA/FAQ questions captured</check>
  <check id="5" required="true">10+ LSI keywords mapped to sections</check>
  <check id="6" required="true">Featured Snippet strategy defined</check>
  <check id="7" required="false">Hub-spoke satellites identified (optional)</check>
</validation_gate>
```

#### Flexibility

| Attribute | Options | Purpose |
|-----------|---------|---------|
| **id** | Unique identifier | For referencing in logs |
| **required** | true / false | Determines if check blocks handoff |
| **Check content** | Any verifiable condition | What to validate |

#### Benefits

1. **Explicit completion criteria** — No ambiguity about when stage is "done"
2. **Self-check automation** — SELF_CHECK step uses these checks directly
3. **Handoff gating** — `required="true"` checks must pass for `handoff.ready = true`
4. **Optional enhancements** — `required="false"` checks are nice-to-have
5. **Traceable validation** — Every check produces pass/fail in `runtime_logs.validation`
6. **Pipeline protection** — Failed gates prevent broken data from reaching next stage

#### Validation Gate vs Success Criteria

```
Success Criteria (mission)         Validation Gate
─────────────────────────────      ──────────────────────────
• What we're trying to achieve     • How we verify achievement
• Qualitative + quantitative       • Specific, binary checks
• Guides work during execution     • Validates work after execution
• Informs STRATEGIZE step          • Powers SELF_CHECK step
```

---

### Putting It Together: Element Synergy

Each stage element serves a distinct purpose, but they work together:

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    ELEMENT INTERACTION FLOW                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   IDENTITY              Who is doing the work?                          │
│      │                  → Shapes approach and expertise                 │
│      ▼                                                                  │
│   MISSION               What does success look like?                    │
│      │                  → Defines objectives and criteria               │
│      ▼                                                                  │
│   TASKS                 How do we get there?                            │
│      │                  → Breaks work into ordered steps                │
│      ▼                                                                  │
│   CONSTRAINTS           What rules apply?                               │
│      │                  → Governs execution boundaries                  │
│      ▼                                                                  │
│   VALIDATION_GATE       Did we succeed?                                 │
│                         → Verifies criteria were met                    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

**Flow during execution (all 9 steps):**

| Step | Element(s) Used | How |
|------|-----------------|-----|
| 1. **COMPREHEND** | `identity`, `mission` | Understand role, goals, and success criteria |
| 2. **ANALYZE** | `tasks`, `constraints` | Map subproblems from task list, note boundaries |
| 3. **STRATEGIZE** | `constraints`, `mission` | Choose approach within hard constraints |
| 4. **PLAN** | `tasks` | Decompose into ordered task sequence |
| 5. **EXECUTE** | `tasks`, `constraints` | Follow tasks while respecting boundaries |
| 6. **SELF_CHECK** | `validation_gate`, `mission` | Verify against checks and success criteria |
| 7. **REFINE** | `constraints` | Polish output within boundaries (no scope creep) |
| 8. **RECONCILE** | `mission` | Confirm all deliverables present |
| 9. **RESPOND** | All elements | Format final output per schema |

---

## Examples

### Example 1: Showing the 9-Step Workflow

When executing a PRISM-9 stage, the model should show its workflow:

```markdown
### COMPREHEND

**Task:** [Clear statement of what needs to be done]
**Scope:** [What's included and excluded]
**Constraints:** [Hard limits and requirements]
**Success Criteria:** [Measurable outcomes]
**Unknowns:** [What we don't know yet]

### ANALYZE

**Subproblems:**
1. [Subproblem 1] → [dependency or requirement]
2. [Subproblem 2] → [dependency or requirement]
3. [Subproblem 3] → depends on (1) and (2)

**Dependencies:** [Sequential vs parallel]
**Data Gaps:** [What information is missing]

### STRATEGIZE

**Approach:** [Chosen strategy with rationale]
**Alternatives Considered:**
- [Option A] (rejected: [reason])
- [Option B] (rejected: [reason])
**Assumptions:** [What we're assuming to be true]
**Fallback:** [What to do if primary approach fails]

### PLAN

1. [Action 1] → Expected: [output] → Checkpoint: [verification]
2. [Action 2] → Expected: [output] → Checkpoint: [verification]
3. [Action 3] → Expected: [output] → Checkpoint: [verification]

### EXECUTE

[Execution log with sources, findings, and decisions made...]

### SELF_CHECK

**Validation against success criteria:**
- ✓ [Criterion 1]: [evidence it was met]
- ✓ [Criterion 2]: [evidence it was met]
- ✗ [Criterion 3]: [what's missing] ← triggers retry if critical

**[Pass/Fail status]**

### REFINE

**Improvements made:**
- [Improvement 1 based on self-check findings]
- [Improvement 2 to strengthen weak areas]
- [No scope expansion — only tightening]

### RECONCILE

**Output verification:**
- ✓ All required fields populated
- ✓ Sources cited for all claims
- ✓ Confidence level: [high/medium/low] ([X]/10)
- ✓ Handoff ready for [next stage or user]

### RESPOND

**Formatting final output per schema:**

```json
{
  "prompt_id": "[stage-id]",
  "status": "success",
  "runtime_logs": { ... },
  "sources_used": [ ... ],
  "meta_reasoning": { ... },
  "executive_summary": "[High-level summary]",
  "output": { ... },
  "next_stage_guidance": { ... },
  "handoff": {
    "ready": true,
    "confidence": 8,
    "blockers": []
  }
}
```
```

### Example 2: Handling Failure

```markdown
### SELF_CHECK

**Validation against success criteria:**
- ✓ [Criterion 1]: passed
- ✗ [Criterion 2]: only achieved 60% of target (required: 100%)
- ✓ [Criterion 3]: passed
- ✗ [Criterion 4]: missing required mapping

**Critical issues found. Returning to STRATEGIZE.**

### STRATEGIZE (Retry)

**Issue:** [Specific problem identified in self-check]
**Root Cause:** [Why the original approach failed]
**New Approach:** [Revised strategy to address the gap]
**What Changes:**
- [Change 1 to address failure]
- [Change 2 to improve coverage]

### PLAN (Revised)

1. [New action to fill gap] → Expected: [output]
2. [Additional verification step] → Expected: [output]
3. Re-run self-check against all criteria

[Continue with revised plan...]
```

### Example 3: Single-Stage Usage (No Pipeline)

PRISM-9 works for standalone prompts without pipelines:

```xml
{{include:infra/thinking-framework.xml}}
{{include:infra/response-schema.xml}}

<identity>
  <role>Code Review Assistant</role>
</identity>

<mission>
  <primary_objective>Review submitted code for bugs and improvements</primary_objective>
  <success_criteria>
    <criterion>All critical bugs identified</criterion>
    <criterion>At least 3 improvement suggestions</criterion>
  </success_criteria>
</mission>

<constraints>
  <hard_constraints>
    <constraint>Only review code actually provided</constraint>
    <constraint>Do not fabricate issues</constraint>
  </hard_constraints>
</constraints>

<validation_gate>
  <check required="true">Each issue includes line number reference</check>
  <check required="true">Suggestions include code examples</check>
</validation_gate>

{{INPUT}}
```

This single-stage prompt still benefits from the Laws, 9-step workflow, and self-check — without needing a multi-stage pipeline.

---

## Comparison with Other Frameworks

### PRISM-9 vs CO-STAR

| Aspect | CO-STAR | PRISM-9 |
|--------|---------|---------|
| **Components** | Context, Objective, Style, Tone, Audience, Response | Laws, Workflow, Approach, Schema, Stages |
| **Reasoning** | Implicit | Explicit 9-step workflow |
| **Self-Check** | None | Built-in validation gates |
| **Pipeline** | No | Native support |
| **Governance** | Style/Tone guidelines | Inviolable Laws |

### PRISM-9 vs Chain-of-Thought

| Aspect | Chain-of-Thought | PRISM-9 |
|--------|------------------|---------|
| **Reasoning** | "Think step by step" | 9 defined steps with purposes |
| **Visibility** | Model chooses what to show | All steps externalized |
| **Verification** | Hope-based* | Explicit self-check + validation |
| **Recovery** | None | Failure loops |
| **Structure** | Freeform | Schema-driven |

---

## Best Practices

### Do's

1. **Always show the workflow steps** — COMPREHEND through RECONCILE should be visible
2. **Use validation gates** — Define what "done" means before starting
3. **Cite everything** — Every claim traces to a source
4. **Log decisions** — Future stages need to understand why choices were made
5. **Fail gracefully** — Use loop-backs instead of giving up
6. **Type your handoffs** — Schema contracts prevent pipeline breaks

### Don'ts

1. **Don't skip SELF_CHECK** — This is where errors get caught
2. **Don't fabricate data** — Law 3 is inviolable
3. **Don't expand scope in REFINE** — Refine existing work only
4. **Don't ignore validation failures** — Loop back and fix
5. **Don't hide reasoning** — Transparency is a core principle
6. **Don't assume inputs** — Verify before claiming

### Anti-Patterns

| Anti-Pattern | Problem | Solution |
|--------------|---------|----------|
| Hidden reasoning | Can't audit decisions | Show all 9 steps |
| Optimistic validation | Errors slip through | Check every criterion |
| Scope creep in REFINE | Never finishes | Only tighten, don't add |
| Missing handoff data | Pipeline breaks | Define input/output schemas |
| Ignoring Laws | Hallucinations | Laws are inviolable |

---

## Quick Reference

### The 9 Steps (Mnemonic: **CAS-PESR-RS**)

```
C - COMPREHEND    │ Understand inputs and requirements
A - ANALYZE       │ Map subproblems and dependencies
S - STRATEGIZE    │ Choose approach, surface assumptions
─────────────────
P - PLAN          │ Create action sequence with checkpoints
E - EXECUTE       │ Follow plan, log decisions
S - SELF_CHECK    │ Verify against criteria
R - REFINE        │ Tighten weak spots (no scope expansion)
─────────────────
R - RECONCILE     │ Prepare handoff, verify format
S - SYNTHESIZE    │ Integrate findings into coherent output
```

### The 5 Laws (Mnemonic: **TV-NRC**)

```
T - Truthfulness       │ State only what's supported
V - Verify before Claim│ Read it before asserting it
N - No Fabrication     │ Don't invent data
R - Respect Constraints│ Follow the rules
C - Complete within Limits│ Deliver all required items
```

### Failure Recovery

```
COMPREHEND gaps    → STOP, report
EXECUTE blocked    → return to PLAN
SELF_CHECK fails   → return to STRATEGIZE
RECONCILE fails    → return to REFINE
```

### Output Structure

```json
{
  "prompt_id": "stage-XX-name",
  "status": "success|partial|failed",
  "runtime_logs": { /* execution trace */ },
  "sources_used": [ /* all sources */ ],
  "meta_reasoning": { /* how conclusions reached */ },
  "executive_summary": { /* key findings + confidence */ },
  "output": { /* stage-specific deliverables */ },
  "next_stage_guidance": { /* for next stage */ },
  "handoff": { "ready": true, "next_stage": "..." }
}
```

---

## Changelog

### Version 1.0 (December 2025)
- Initial release
- 9-step meta-reasoning workflow
- 5 Laws governance layer
- Modular component architecture
- Pipeline orchestration support
- Schema-driven handoffs

---

## License

PRISM-9 is open source. Use it, extend it, improve it.

Attribution appreciated but not required.

---

## Credits

PRISM-9 builds on the foundations of:
- Chain-of-thought reasoning research
- Constitutional AI principles
- Software engineering best practices (typed interfaces, validation gates)

---

*PRISM-9: From complexity to clarity through governed reasoning.*

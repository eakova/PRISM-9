# PRISM-9: Research Foundation

> *The research behind governed reasoning*

---

## Contents

**Introduction**
- [What This Document Is](#what-this-document-is)
- [What is PRISM-9?](#what-is-prism-9)
- [How This Informs PRISM-9](#how-this-informs-prism-9)

**Research**
- [1. Common Problems](#1-common-problems)
- [2. Prompt Engineering Evolution](#2-prompt-engineering-evolution)
- [3. Observations on Chain-of-Thought](#3-observations-on-chain-of-thought)
- [4. Pipeline Patterns](#4-pipeline-patterns)
- [5. Rules and Constraints](#5-rules-and-constraints)
- [6. Self-Checking](#6-self-checking)
- [7. Structured Output](#7-structured-output)
- [8. Failure Handling](#8-failure-handling)
- [9. Verification and Grounding](#9-verification-and-grounding)
- [10. Practical Takeaways](#10-practical-takeaways)
- [References](#references)

---

## What This Document Is

The academic and empirical foundation underlying PRISM-9's design decisions. Each section documents common LLM failure modes and the research-backed patterns that address them. This is not a definitive guide — LLM behavior is unpredictable and what works today may not work tomorrow.

---

## What is PRISM-9?

**PRISM-9** (Pipeline Reasoning with Integrated Self-Monitoring) is a prompt engineering framework for governed AI reasoning. It provides structure where most prompts provide only hope.

### Core Components

**The 5 Laws** — Inviolable rules that cannot be overridden:
1. Truthfulness — State only what you can support
2. Verify Before Claim — Read before asserting
3. No Fabrication — Never invent data
4. Respect Constraints — Follow the rules given
5. Complete Within Limits — Deliver everything required

**The 9-Step Workflow** — Structured reasoning with checkpoints:
```
COMPREHEND → ANALYZE → STRATEGIZE → PLAN → EXECUTE → SELF_CHECK → REFINE → RECONCILE → SYNTHESIZE
```

**Tiered Governance** — Clear priority hierarchy:
```
System Prompts > Laws > Hard Constraints > Soft Constraints > Preferences
```

**Schema-Driven Handoffs** — Typed contracts between pipeline stages with explicit `ready` flags and failure states.

### The Thinking Framework

Each step requires explicit meta-reasoning:
- What am I doing? (current step)
- Why am I doing it? (purpose)
- What could go wrong? (risks)
- How will I verify? (validation)

This transforms opaque "thinking" into auditable reasoning trails.

→ **Full specification:** See [README.md](README.md)

---

## How This Informs PRISM-9

| Research Finding | PRISM-9 Design Response |
|------------------|-------------------------|
| Position effects degrade mid-context attention | Laws placed at start, repeated throughout |
| Self-checking is unreliable | External validation gates required |
| Pipelines suffer silent failures | Schema-driven handoffs with `ready` flag |
| Rules get ignored in long contexts | Tiered governance (Laws → Constraints → Preferences) |
| CoT helps but isn't magic | 9-step structured workflow with checkpoints |
| Models are overconfident | Explicit confidence levels with rationale |

---

## 1. Common Problems

LLMs fail in predictable ways:

- **Hallucination**: Making things up, especially IDs, URLs, and specific facts
- **Drift**: Gradually ignoring instructions as context grows (see [§5: position effects](#5-rules-and-constraints))
- **Truncation**: Stopping mid-task without warning
- **Overconfidence**: Claiming certainty when uncertain
- **Assumption-making**: Filling gaps with guesses instead of asking

These problems compound in multi-step tasks — each stage inherits and amplifies upstream errors.

---

## 2. Prompt Engineering Evolution

### Early Approaches

Direct questions work for simple tasks:
```
Q: What is 2+2?
A: 4
```

Few-shot examples help with formatting:
```
Q: What is 2+2? A: 4
Q: What is 3+3? A: 6
Q: What is 5+7? A: ?
```

### Current Approaches

- Chain-of-thought (CoT): Prompting with reasoning examples (few-shot) or phrases like "Let's think step by step" (zero-shot)
- Self-consistency: Generate multiple answers, pick the consensus
- Tool use: Let the model call external functions
- Multi-agent: Split work across specialized prompts

None of these are silver bullets. They help, but don't eliminate the core problems.

---

## 3. Observations on Chain-of-Thought

Few-shot chain-of-thought prompting improves accuracy on reasoning tasks. On GSM8K (math word problems), PaLM 540B improved from 17.9% to 58.1% with 8-shot CoT examples ([Wei et al., 2022](https://arxiv.org/abs/2201.11903)).

Separately, zero-shot CoT using "Let's think step by step" showed larger gains on simpler benchmarks like MultiArith (17.7% to 78.7%) but smaller gains on GSM8K (10.4% to 40.7%) with text-davinci-002 ([Kojima et al., 2022](https://arxiv.org/abs/2205.11916), Table 1).

**What seems to help:**
- Breaking problems into steps
- Making intermediate results visible
- Forcing the model to "show work"

**What doesn't help:**
- Long reasoning chains - performance can degrade when relevant information is buried in the middle of context ("lost in the middle" effect; [Liu et al., 2024](https://aclanthology.org/2024.tacl-1.9/))
- Reasoning about things the model doesn't actually know
- Expecting the model to catch its own errors

CoT is useful but not magic. The model can reason incorrectly at any step.

---

## 4. Pipeline Patterns

### Why Pipelines?

Single prompts fail on complex tasks because:
- Context windows are limited
- Attention quality degrades with length
- Errors compound
- Debugging is hard

Breaking work into stages helps, but introduces new failure modes: handoff errors, context loss, and silent stage failures that corrupt downstream outputs.

### Common Patterns

**Sequential:**
```
Stage 1 -> Stage 2 -> Stage 3 -> Output
```

**Fan-out:**
```
         +-> Task A -+
Input ---+-> Task B -+-> Merge
         +-> Task C -+
```

**Iterative:**
```
Generate -> Validate -> Fix (if needed) -> Output
```

### What Goes Wrong

- **Silent failures**: Stage fails but pipeline continues
- **Context loss**: Important info doesn't make it between stages
- **Format drift**: Output format changes unexpectedly
- **Error cascades**: Early mistake corrupts everything downstream

---

## 5. Rules and Constraints

### The Problem

Rules are suggestions to LLMs. They:
- Forget rules as context grows (position effects)
- Prioritize "helpful" responses over correct ones
- Interpret constraints loosely when they conflict with generation fluency

### What Seems to Help

**Repetition**: Repeat critical rules multiple times

**Placement**: Information at the beginning or end of prompts is used more effectively than middle content - U-shaped performance curve ([Liu et al., 2024](https://aclanthology.org/2024.tacl-1.9/); [Guo & Vosoughi, 2024](https://arxiv.org/abs/2406.15981))

**Consequences**: "If you fabricate data, the task fails" often works better than "don't fabricate data"

**Emotional framing**: Adding psychological weight to prompts (e.g., "This is important for my career") can improve truthfulness by ~14% ([Yu et al., 2024](https://www.ijcai.org/proceedings/2024/0719.pdf))

**Procedural rules**: "Before claiming X exists, quote it" embeds verification into the task

### What Doesn't Help

- Long lists of rules (get ignored)
- Subtle distinctions (model won't catch them)
- Expecting perfect compliance (won't happen)

---

## 6. Self-Checking

### The Idea

Have the model verify its own output before returning it.

### What Works (Sometimes)

```
[OUTPUT]
---
[SELF-CHECK]
- Did I complete all items? Yes/No
- Did I fabricate any data? Yes/No
- Does format match requirements? Yes/No
```

### Limitations

Self-checking is fundamentally limited:
- **Overconfidence**: Verbalized confidence is poorly calibrated — models say "I'm sure" when they shouldn't be ([Xiong et al., 2024](https://arxiv.org/abs/2306.13063))
- **Blind spot inheritance**: The same reasoning flaws that cause errors also cause verification failures
- **Context cost**: Self-checking consumes tokens that could be used for actual work

Self-checking catches surface errors (format, completeness) but not deep ones (factual accuracy, logical consistency). External validation is essential for high-stakes outputs.

---

## 7. Structured Output

### Why Structure Matters

Unstructured text creates pipeline fragility:
- **Parsing fails** — regex breaks on edge cases
- **Validation is impossible** — no schema to check against
- **Handoffs lose data** — context stripped at stage boundaries
- **Debugging is blind** — no clear state to inspect

Structured formats enable programmatic validation. External tools can verify schema compliance more reliably than LLM self-checking ([Gou et al., 2024](https://arxiv.org/abs/2305.11738)).

### Options

**JSON**: Machine-readable, schema-validatable
```json
{"status": "success", "data": {...}}
```

**XML**: Good for mixed content
```xml
<result status="success">...</result>
```

**Markdown with conventions**: Human-readable
```
## Result
**Status:** Success
**Data:** ...
```

### Problems

- Models make syntax errors in JSON
- Structure doesn't guarantee content quality
- Overly rigid schemas cause failures

---

## 8. Failure Handling

### Types of Failures

| Type | Example | Detection |
|------|---------|-----------|
| Format | Invalid JSON | Parser error |
| Incomplete | Missing required fields | Schema check |
| Wrong | Incorrect information | External validation |
| Hallucinated | Made-up URLs/IDs | Source checking |

### Recovery Options

1. **Retry**: Sometimes works for transient failures
2. **Retry with hint**: "You missed X, try again"
3. **Decompose**: Break into smaller tasks
4. **Fail gracefully**: Return partial results with error report

### Circuit Breakers

Don't retry forever. Set limits:
```
max_retries = 3
if retries > max_retries:
    return partial_result_with_errors
```

---

## 9. Verification and Grounding

### The Core Problem

LLMs generate plausible text, not verified facts. They will confidently cite papers that don't exist.

### Mitigation Strategies

**Source-based**: Only allow claims that reference provided sources

**Tool-based**: Use external APIs to verify facts
```
Claim: "Population is 67M"
-> Call API
-> API returns 67.75M
-> Mark as verified
```

**Explicit uncertainty**: Force the model to mark confidence levels

### Verification Levels

| Level | Meaning |
|-------|---------|
| Stated | Model said it, unverified |
| Sourced | Linked to a source |
| Verified | Checked against source |
| Validated | Cross-checked multiple sources |

### Reality Check

Perfect verification is impossible. The goal is to:
- Catch obvious errors
- Flag uncertain claims
- Provide audit trails
- Make failures visible

---

## 10. Practical Takeaways

### What Tends to Work

1. **Keep stages small**: Single responsibility per prompt
2. **Validate at boundaries**: Check outputs before passing them on
3. **Fail loudly**: Make errors visible, don't hide them
4. **Repeat critical rules**: Important instructions multiple times
5. **Use negative constraints**: "Never X" over "Always Y"
6. **Ground in sources**: Require citations for claims
7. **Expect failures**: Build recovery into the design

### What Doesn't Work

1. **Long, complex prompts**: Attention degrades
2. **Trusting self-verification**: Models miss their own errors
3. **Perfect compliance**: Rules will be broken
4. **Single-shot complex tasks**: Break them up
5. **Implicit expectations**: Be explicit about everything

### Honest Assessment

These patterns reduce failure rates — they don't eliminate failures. LLMs are:
- **Probabilistic** — same input, different outputs
- **Opaque** — we can't predict when they'll fail
- **Unstable** — behavior changes with model updates

Design for failure. Build systems that recover, not systems that assume success.

---

## References

Each reference is mapped to specific concepts it supports.

### Structured Reasoning

1. Wei, J. et al. (2022). "[Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903)." NeurIPS 2022.
   - Supports: Few-shot step-by-step reasoning with exemplars
   - **PRISM-9:** Foundation for 9-step workflow design

2. Kojima, T. et al. (2022). "[Large Language Models are Zero-Shot Reasoners](https://arxiv.org/abs/2205.11916)." NeurIPS 2022.
   - Supports: Zero-shot CoT with "Let's think step by step"

3. Wang, L. et al. (2023). "[Plan-and-Solve Prompting: Improving Zero-Shot Chain-of-Thought Reasoning](https://arxiv.org/abs/2305.04091)." ACL 2023.
   - Supports: Explicit planning before execution

4. Yao, S. et al. (2023a). "[ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)." ICLR 2023.
   - Supports: Interleaved reasoning and actions

5. Yao, S. et al. (2023b). "[Tree of Thoughts: Deliberate Problem Solving with Large Language Models](https://arxiv.org/abs/2305.10601)." NeurIPS 2023.
   - Supports: Branching exploration, evaluating multiple paths

### Context and Position Effects

6. Liu, N. et al. (2024). "[Lost in the Middle: How Language Models Use Long Contexts](https://aclanthology.org/2024.tacl-1.9/)." TACL 2024.
   - Supports: U-shaped performance curve, information in middle of context is used less effectively
   - **PRISM-9:** Laws placement strategy, constraint drift mitigation

7. Guo, X. and Vosoughi, S. (2024). "[Serial Position Effects of Large Language Models](https://arxiv.org/abs/2406.15981)." ACL Findings 2025.
   - Supports: Primacy and recency biases in LLM responses

### Self-Correction and Calibration

8. Gou, Z. et al. (2024). "[CRITIC: Large Language Models Can Self-Correct with Tool-Interactive Critiquing](https://arxiv.org/abs/2305.11738)." ICLR 2024.
   - Supports: Verify-correct-verify cycle with external tool feedback

9. Shinn, N. et al. (2023). "[Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366)." NeurIPS 2023.
   - Supports: Learning from failure through verbal self-reflection

10. Wang, X. et al. (2023). "[Self-Consistency Improves Chain of Thought Reasoning in Language Models](https://arxiv.org/abs/2203.11171)." ICLR 2023.
    - Supports: Multiple reasoning paths, consensus selection

11. Xiong, M. et al. (2024). "[Can LLMs Express Their Uncertainty?](https://arxiv.org/abs/2306.13063)." ICLR 2024.
    - Supports: LLM verbalized confidence is poorly calibrated across multiple tasks and models
    - **PRISM-9:** Justifies external validation gates over self-assessment

### Prompt Design

12. Yu, X. et al. (2024). "[NegativePrompt: Leveraging Psychology for Large Language Models](https://www.ijcai.org/proceedings/2024/0719.pdf)." IJCAI 2024.
    - Supports: Emotional/psychological framing improves truthfulness (~14%)

### Grounding and Governance

13. Bai, Y. et al. (2022). "[Constitutional AI: Harmlessness from AI Feedback](https://arxiv.org/abs/2212.08073)." Anthropic.
    - Supports: Principle-based self-governance, rule following
    - **PRISM-9:** Inspiration for the 5 Laws governance layer

14. Lewis, P. et al. (2020). "[Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401)." NeurIPS 2020.
    - Supports: Grounding generation in retrieved documents (reduces hallucination by providing source material, but does not verify claims)

### Hallucination Detection

15. Manakul, P. et al. (2023). "[SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection](https://arxiv.org/abs/2303.08896)." EMNLP 2023.
    - Supports: Detecting hallucinations via response consistency (detection method, not prevention)

16. Min, S. et al. (2023). "[FActScore: Fine-grained Atomic Evaluation of Factual Precision](https://arxiv.org/abs/2305.14251)." EMNLP 2023.
    - Supports: Breaking claims into verifiable atomic facts for evaluation

### Useful Resources

- [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
- [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering)

---

## Notes

- This document reflects observations as of late 2025
- LLM behavior changes with model updates
- What works for one model may not work for another
- Test everything in your specific context
- Combining techniques (e.g., CoT + self-consistency) generally improves performance over single methods

---

*Version: 1.0 — Companion to README.md*

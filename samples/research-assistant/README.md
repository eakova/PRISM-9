# Research Assistant Sample

A PRISM-9 multi-stage pipeline for business and technology research.

## Use Case

- Market research
- Competitive analysis
- Technology assessment
- Trend analysis
- Due diligence

## Files

```
research-assistant/
├── README.md               # This file
├── approach.xml            # Domain configuration
├── stage-1-scope.xml       # Scope definition stage
├── stage-2-sources.xml     # Source gathering stage
├── stage-3-analysis.xml    # Analysis & synthesis stage
└── stage-4-report.xml      # Report generation stage
```

## Pipeline Overview

```
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│  STAGE 1         │    │  STAGE 2         │    │  STAGE 3         │    │  STAGE 4         │
│  Scope           │───▶│  Source          │───▶│  Analysis        │───▶│  Report          │
│  Definition      │    │  Gathering       │    │  & Synthesis     │    │  Generation      │
│                  │    │                  │    │                  │    │                  │
│  • Sub-questions │    │  • Source list   │    │  • Findings      │    │  • Exec summary  │
│  • Boundaries    │    │  • Quality tiers │    │  • Confidence    │    │  • Detailed      │
│  • Source plan   │    │  • Key claims    │    │  • Patterns      │    │  • Recommendations│
│  • Success criteria│  │  • Coverage gaps │    │  • Uncertainties │    │  • Methodology   │
└──────────────────┘    └──────────────────┘    └──────────────────┘    └──────────────────┘
```

## Stage Details

### Stage 1: Scope Definition
**Input:** Research question, context, depth requirement
**Output:** Refined question, sub-questions, scope boundaries, source strategy

Key tasks:
1. Question analysis and refinement
2. Decomposition into 3-7 sub-questions
3. Scope boundary definition (in/out of scope)
4. Source strategy planning

### Stage 2: Source Gathering
**Input:** Research scope from Stage 1
**Output:** Validated sources organized by sub-question

Key tasks:
1. Source discovery (tier-1, tier-2, tier-3)
2. Quality assessment and tier assignment
3. Key claim extraction with references
4. Conflict detection across sources
5. Coverage gap analysis

### Stage 3: Analysis & Synthesis
**Input:** Scope + Sources from prior stages
**Output:** Synthesized findings with confidence levels

Key tasks:
1. Evidence synthesis per sub-question
2. Confidence calibration (high/medium/low)
3. Contradiction resolution
4. Cross-source pattern identification
5. Uncertainty documentation

### Stage 4: Report Generation
**Input:** All prior stage outputs
**Output:** Complete research report

Key tasks:
1. Executive summary creation
2. Detailed findings with evidence
3. Evidence-based recommendations
4. Methodology documentation
5. Appendices compilation

## Usage Example

```xml
<!-- Stage 1: Scope Definition -->
{{include:infra/thinking-framework.xml}}
{{include:infra/response-schema.xml}}
{{include:infra/approach.xml}}
{{include:stage-1-scope.xml}}

<input>
{
  "question": "What is the current state of AI adoption in healthcare?",
  "context": "Preparing board presentation on strategic opportunities",
  "depth": "standard"
}
</input>
```

## Key Features

- **Evidence standards**: High/Medium/Low confidence with explicit rationale
- **Source quality tiers**: Tier-1 (authoritative) → Tier-3 (supplementary)
- **Balanced perspective**: Contradictions acknowledged, not hidden
- **Traceability**: Every finding linked to sources
- **Validation gates**: Minimum source requirements enforced

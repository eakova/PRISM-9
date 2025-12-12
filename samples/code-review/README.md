# Code Review Sample

A PRISM-9 multi-stage pipeline for automated code review.

## Use Case

- Pull request reviews
- Pre-commit code analysis
- Team code quality standards enforcement

## Files

```
code-review/
├── README.md               # This file
├── approach.xml            # Domain configuration
├── stage-1-analysis.xml    # Static analysis stage
├── stage-2-security.xml    # Security review stage
└── stage-3-report.xml      # Final report stage
```

## Pipeline Overview

```
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│  STAGE 1            │     │  STAGE 2            │     │  STAGE 3            │
│  Static Analysis    │────▶│  Security Review    │────▶│  Review Report      │
│                     │     │                     │     │                     │
│  • Syntax issues    │     │  • Vulnerabilities  │     │  • Prioritized list │
│  • Type safety      │     │  • Logic errors     │     │  • Verdict          │
│  • Complexity       │     │  • Edge cases       │     │  • Action items     │
│  • Code smells      │     │  • Test gaps        │     │  • PR comment       │
└─────────────────────┘     └─────────────────────┘     └─────────────────────┘
```

## Stage Details

### Stage 1: Static Analysis
**Input:** Code diff, language, optional style guide
**Output:** Syntax issues, type errors, complexity metrics, code smells

Key tasks:
1. Syntax validation and style checking
2. Type safety analysis
3. Complexity measurement (cyclomatic, nesting)
4. Code smell detection

### Stage 2: Security Review
**Input:** Code diff + Stage 1 findings
**Output:** Security vulnerabilities, logic errors, edge cases, test gaps

Key tasks:
1. Injection vulnerability scanning (SQL, XSS, Command)
2. Authentication/authorization analysis
3. Sensitive data exposure checks
4. Race condition detection
5. Edge case identification

### Stage 3: Review Report
**Input:** Stage 1 + Stage 2 findings
**Output:** Prioritized review with verdict and PR comment

Key tasks:
1. Issue synthesis and deduplication
2. Priority triage (Critical > Major > Minor > Nitpick)
3. Positive observation identification
4. Action item categorization
5. PR comment composition

## Usage Example

```xml
<!-- Stage 1: Static Analysis -->
{{include:infra/thinking-framework.xml}}
{{include:infra/response-schema.xml}}
{{include:infra/approach.xml}}
{{include:stage-1-analysis.xml}}

<input>
{
  "code_diff": "{{CODE_DIFF}}",
  "language": "typescript",
  "style_guide": "google"
}
</input>
```

Then chain to Stage 2 with Stage 1 output, and finally Stage 3.

## Key Features

- **Priority levels**: Critical > Major > Minor > Nitpick
- **Constructive tone**: Teaching, not gatekeeping
- **OWASP coverage**: Security analysis aligned with top 10
- **Cumulative analysis**: Each stage builds on prior findings
- **Validation gates**: Each stage validates completeness before handoff

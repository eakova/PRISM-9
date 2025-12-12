# API Documentation Sample

A PRISM-9 multi-stage pipeline for developer-friendly API documentation.

## Use Case

- REST API reference generation
- SDK documentation
- Integration guides
- Quickstart tutorials

## Files

```
api-documentation/
├── README.md               # This file
├── approach.xml            # Domain configuration
├── stage-1-analysis.xml    # API specification analysis
├── stage-2-examples.xml    # Code example generation
└── stage-3-assembly.xml    # Documentation assembly
```

## Pipeline Overview

```
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│  STAGE 1            │     │  STAGE 2            │     │  STAGE 3            │
│  API Analysis       │────▶│  Example Generation │────▶│  Doc Assembly       │
│                     │     │                     │     │                     │
│  • Endpoints        │     │  • curl examples    │     │  • Quickstart       │
│  • Auth methods     │     │  • Code samples     │     │  • Endpoint reference│
│  • Data models      │     │  • Sample payloads  │     │  • Error reference  │
│  • Error codes      │     │  • Common patterns  │     │  • Full navigation  │
└─────────────────────┘     └─────────────────────┘     └─────────────────────┘
```

## Stage Details

### Stage 1: API Analysis
**Input:** OpenAPI spec or API source code
**Output:** Structured API analysis (endpoints, auth, models, errors)

Key tasks:
1. Specification parsing
2. Authentication mechanism analysis
3. Endpoint extraction with parameters/responses
4. Data model extraction
5. Error code cataloging
6. Documentation priority planning

### Stage 2: Example Generation
**Input:** API analysis from Stage 1
**Output:** Working code examples in multiple languages

Key tasks:
1. curl example generation (all endpoints)
2. Multi-language code generation (Python, JS, etc.)
3. Authentication setup examples
4. Sample request/response creation
5. Common pattern documentation (pagination, errors)

### Stage 3: Documentation Assembly
**Input:** Analysis + Examples from prior stages
**Output:** Publication-ready API documentation

Key tasks:
1. Quickstart guide creation (5-minute first call)
2. Authentication documentation
3. Endpoint reference assembly
4. Error reference compilation
5. Rate limits and changelog
6. Navigation and search optimization

## Usage Example

```xml
<!-- Stage 1: API Analysis -->
{{include:infra/thinking-framework.xml}}
{{include:infra/response-schema.xml}}
{{include:infra/approach.xml}}
{{include:stage-1-analysis.xml}}

<input>
{
  "spec": "{{OPENAPI_SPEC}}",
  "spec_format": "openapi",
  "base_url": "https://api.example.com/v1"
}
</input>
```

## Key Features

- **Developer-first**: 5-minute quickstart target
- **Working examples**: Copy-paste runnable code, not pseudocode
- **Multi-language**: curl + 2 programming languages minimum
- **Error coverage**: All error codes documented with resolution
- **Complete reference**: Every endpoint fully documented
- **Validation gates**: Ensures no gaps in documentation

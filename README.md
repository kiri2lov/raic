# RAIC — Requirements as Intelligent Code

**RAIC** is a YAML-based domain-specific language for expressing software requirements in a structured, machine-parseable format optimized for AI-driven development agents.

## Why RAIC?

Traditional requirements formats (Jira tickets, Google Docs, Confluence pages) are designed for humans. AI coding agents need something better — structured, unambiguous, and complete. RAIC bridges this gap by providing a format that is:

- **Structured** — YAML with a strict JSON Schema, so agents can parse and validate requirements programmatically
- **Complete** — flows, specs, acceptance criteria, constraints, NFRs, concurrency risks, and permissions in one place
- **Traceable** — every spec links to flows, every acceptance criterion links to specs
- **Scalable** — from a single-file feature to a multi-module product hierarchy
- **Agent-friendly** — includes `agent_hints` with implementation order, complexity estimates, and testing strategy

## Quick Start

A minimal RAIC feature file:

```yaml
feature:
  id: FEAT-001
  title: User Registration
  type: feature
  status: active

  context:
    problem: Users cannot create accounts
    impact: No user base growth

  specs:
    - id: SPEC-001
      priority: MUST
      statement: System MUST allow email/password registration

  acceptance_criteria:
    - id: AC-001
      spec_refs: [SPEC-001]
      given: User is on registration page
      when: User submits valid email and password
      then: Account is created and confirmation email is sent
```

## Documentation

- [Specification](specification.md) — full RAIC specification (v1.0)
- [JSON Schema](schema.json) — machine-readable schema for validation

## Schema Validation

Validate your RAIC files against the JSON Schema:

```bash
# Using ajv-cli
npx ajv-cli validate -s schema.json -d your-feature.yaml

# Using Python jsonschema
python -m jsonschema -i your-feature.yaml schema.json
```

## Key Concepts

| Concept | Description |
|---|---|
| **Product** | Top-level entity containing modules |
| **Module** | Logical grouping of features |
| **Feature** | A single requirement document with full context |
| **Flow** | Step-by-step user/system interaction scenario |
| **Spec** | Individual requirement statement with RFC 2119 priority |
| **Acceptance Criterion** | Given/When/Then test case linked to specs |
| **Agent Hints** | Metadata to guide AI implementation |

## Priority Keywords

RAIC uses [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119) keywords:

- `MUST` / `MUST_NOT` — absolute requirements
- `SHOULD` / `SHOULD_NOT` — recommended, but exceptions allowed
- `MAY` — truly optional

## License

[MIT](LICENSE)

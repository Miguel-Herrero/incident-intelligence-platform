# ADR-001: Monorepo with Go + Python

## Status: Accepted

## Context
Six-month learning project for transition to AI Platform Engineering.
I need a structure that facilitates frequent commits and showcases a cohesive portfolio.

## Decision
Use a monorepo with:
- Gateway in Go (leveraging backend experience)
- Orchestrator in Python (AI ecosystem)
- Shared evals

## Consequences
Positive:
- Atomic commits across components
- Simplified management with limited time
- Communicates vision of an integrated system

Negative:
- Slightly more complex CI/CD
- Repo size grows faster

## Alternatives considered
- Multi-repo: Rejected due to management overhead
- Python only: Rejected, would lose competitive advantage in Go

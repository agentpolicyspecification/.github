<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="aps-readme-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="aps-readme-light.svg">
    <img alt="Agent Policy Specification" src="aps-readme-light.svg">
  </picture>
</p>

![Version](https://img.shields.io/badge/version-0.1.0-blue)
![Status](https://img.shields.io/badge/status-draft-orange)
![License](https://img.shields.io/github/license/agentpolicyspecification/.github)
![Docs](https://img.shields.io/badge/docs-available-brightgreen)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)
![Contributors](https://img.shields.io/github/contributors/agentpolicyspecification/.github)
![Stars](https://img.shields.io/github/stars/agentpolicyspecification?style=social)
![Open Specification](https://img.shields.io/badge/Open-Specification-blueviolet)

# Agent Policy Specification (APS)

**A vendor-neutral specification for enforcing policies on AI agent interactions.**

APS defines a standard interception layer that sits between an agent and its underlying LLM. It gives operators, developers, and platform teams a consistent way to express, evaluate, and enforce policies on every message, tool call, and model response — before any side effect occurs.

---

## The Problem

AI agents act on behalf of users and systems. They call tools, read data, and produce outputs — often with little or no enforcement boundary between an instruction and its consequences.

Current approaches to safety and control are fragmented: guardrails are baked into individual agent frameworks, applied inconsistently across environments, and difficult to audit or reason about independently from application logic.

---

## What APS Defines

APS specifies three interception points in the agent–LLM interaction lifecycle:

```mermaid
flowchart TD
    U(["User / System"])
    U --> I

    subgraph APS ["APS Policy Layer"]
        I["① Input Policy Enforcement
            ─────────────────────────
            messages before they reach the LLM"]
        T["② Tool Call Enforcement
            ─────────────────────────
            tool invocations before execution"]
        O["③ Output Policy Enforcement
            ─────────────────────────
            model responses before delivery"]
        I --> T --> O
    end

    O --> R(["Agent / LLM Runtime"])
```

For each interception point, APS defines:

- **A data model** — the schema of what is evaluated (messages, tool call descriptors, output payloads)
- **A policy interface** — how policies are declared, composed, and resolved
- **An enforcement contract** — what actions a compliant runtime must take on a policy decision (`allow`, `deny`, `redact`, `transform`, `audit`)

---

## Policy Authoring

APS supports two complementary policy authoring models:

- **Rego policies** — declarative rules evaluated against structured input, compatible with [Open Policy Agent](https://www.openpolicyagent.org/)
- **Programmatic rules** — typed interfaces (Java, TypeScript) for policies that require imperative logic or external I/O

---

## Status

APS is in the **concept and specification design** phase.

| Artifact | Status |
|---|---|
| Core specification | In progress |
| Reference implementation (Java) | Planned |
| Reference implementation (TypeScript) | Planned |
| Conformance test suite | Planned |

---

## Get Involved

This specification is developed openly. Contributions, feedback, and discussion are welcome.

- Read the spec drafts in the [`spec`](https://github.com/agentpolicyspecification/spec) repository
- Open an issue to propose a policy model, discuss an interception contract, or raise a use case
- Join the conversation in [Discussions](https://github.com/orgs/agentpolicyspecification/discussions)

---

*APS is vendor-neutral and not tied to any specific agent framework, LLM provider, or cloud platform.*

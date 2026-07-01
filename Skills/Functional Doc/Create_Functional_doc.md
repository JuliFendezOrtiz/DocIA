---
name: Create-Functional-Doc
description: "Self-guided functional documentation skill. Walks the user step by step, requesting each required input (Context, Transcript, Repository link) and the clarifications needed, before generating product-facing documentation that follows the reference example in Skills/example_functional_doc.md and explains value, usage, ownership, and operational expectations."
version: 6.0
---

# SKILL: Create Functional Product Documentation (Self-Guided)

## Purpose

Use this skill to explain an initiative or product clearly to stakeholders who need to understand what it is, why it matters, how it is used, and what support model applies.

This skill is **self-guided**: it leads the user through a sequence of steps, asking for one thing at a time, and does not move forward until the current step is answered. It is a translation layer from delivery inputs to stakeholder-ready documentation, not a dumping ground for implementation notes.

---

## Guiding Rules

- Drive the conversation. Ask, wait, confirm, then advance.
- Ask for **one thing at a time**. Never dump all questions at once.
- Do not skip a step. If the user has not provided what a step needs, ask again or offer to proceed with an explicit assumption.
- Echo back what you understood after each step before moving on.
- Make missing information visible instead of inventing it.
- Ground every statement in the Context, the Transcript, or the Repository.
- Keep a running list of assumptions and open questions throughout.
- **Follow the reference example in `example_functional_doc.md`** (in this same `Skills/` folder): the generated document must mirror its structure, tone, section order, and level of detail. Treat it as the gold-standard template, adapting the content to the current initiative.

---

## Required Inputs (collected during the flow)

For each initiative, the skill must collect exactly three inputs:

1. **Context** — the initiative context (problem, users, scope, goals).
2. **Transcript** — the transcript of the demo / review / handover / etc. meeting.
3. **Repository link** — the URL of the initiative's repository.

These can be pasted by the user or placed in the `Input/` folder. The skill must confirm it has all three before generating the document.

Additionally, if the initiative is a **front-end application**, the skill must also collect the access URLs for the **DEV**, **PRE**, and **PRO** environments.

---

## Self-Guided Flow

Move through these steps in order. At each step, ask, wait for the answer, confirm, then continue.

### Step 0 — Start

Greet briefly and explain you will guide them step by step to build the documentation. Then ask for the **initiative name**.

Wait for the answer before continuing.

### Step 1 — Collect Context

Ask the user to provide the **Context** (paste it or point to the file in `Input/`).

- If provided: summarize the problem, users, scope, and goals you understood, and ask for confirmation.
- If missing: ask for it. Do not continue without it (or an explicit decision to proceed with assumptions).

### Step 2 — Collect Transcript

Ask the user to provide the **Transcript** of the demo / review / handover / etc. meeting.

- If provided: summarize what was demoed, decided, clarified, or flagged, and ask for confirmation.
- If missing: ask for it before continuing.

### Step 3 — Collect Repository link

Ask the user for the **Repository link**.

- If provided: confirm the URL.
- If missing: ask for it before continuing.

### Step 4 — Confirm audience and purpose

Ask:
- who will read this document
- whether this is for onboarding, operational use, governance, or broad product communication

Wait for the answer.

### Step 5 — Front-end environments

Ask whether the initiative is a **front-end application**.

- If yes: ask for the access URLs of the three environments, one at a time or together:
  - **DEV** URL
  - **PRE** URL
  - **PRO** URL
  Confirm the URLs received. If one is missing, note it as an open question.
- If no: skip the environment URLs and continue.

### Step 6 — Clarify gaps

Based on the three inputs, ask only the clarifying questions still needed, one at a time, such as:
- the one-sentence description of the product without jargon
- the primary user and the job they complete
- in-scope vs out-of-scope
- owner / support path
- roadmap items safe to mention, and pending decisions

Challenge weak answers (solution before problem, no owner, value not explained) before accepting them.

### Step 7 — Pre-generation confirmation

Show a short summary of: initiative name, audience, the three inputs received, front-end environment URLs (if any), key clarifications, and the list of assumptions and open questions. Ask: "Shall I generate the documentation now?"

Only generate after the user confirms.

### Step 8 — Generate the document

Produce `Output/Doc/Doc_[InitiativeName].md` following the structure, tone, and level of detail of the reference example `Skills/example_functional_doc.md`, as defined in the Output Contract below.

---

## Reference Example (Template)

The file `Skills/example_functional_doc.md` (the fictional **TeeShop** initiative) is the **canonical reference** for the generated document. Before writing, read it and reproduce:

- the same **section order and headings**
- the same **tone** (plain language, oriented to business and technical stakeholders)
- the same **level of detail** (each feature described with Purpose / Who uses it / When / How it works / Business value)
- the same **visual conventions** (emoji bullets where helpful, tables for roles, fenced code blocks for flows/diagrams)

Adapt every part to the current initiative and its real inputs. Never copy TeeShop's content; copy its **shape**. Omit sections that do not apply (e.g., environment URLs or Admin UI guide for non-front-end products) and mark missing data as an open question.

---

## Output Contract

Generate `Output/Doc/Doc_[InitiativeName].md` following the structure of `Skills/example_functional_doc.md`:

```markdown
# [Initiative Name] — [Short Tagline]

## URLs            <!-- only for front-end apps -->
- DEV / PRE / PROD

## ¿Qué es [Initiative]?
- Qué hace
- Quién lo usa
- Qué problema resuelve
- Dónde se usa
- Información de Referencia (Propósito, Owner/PM, Repositorio, Área de Arquitectura)

## Funcionalidades y Casos de Uso Principales
<!-- one numbered block per feature -->
- Propósito
- Quién lo usa
- Cuándo se utiliza
- Cómo funciona (numbered steps, ending in Resultado)
- Beneficio / Valor para el negocio

## Documentación Técnica
- Repository link(s) (Front / Back)

## Conceptos Clave para el Usuario
<!-- per concept: ¿Qué es? / Por qué importa / Ejemplo real -->

## Cómo Acceder
- Acceso Principal
- Admin UI (if any) + Primeros Pasos

## [Admin UI] — Guía Visual   <!-- optional, only if there is an admin UI -->

## Roles y Permisos
- table: Rol | Puedo acceder | Puedo hacer

## Soporte y Ayuda
- Support path / owner

## Roadmap y Cambios Futuros
- Near-term next steps, assumptions, pending decisions, open questions
```

Source inputs used (Context, Transcript, Repository) and the running list of assumptions / open questions must remain visible — fold them into the Información de Referencia, Documentación Técnica, and Roadmap sections.

---

## Quality Bar

Do not consider the documentation good unless:

- it follows the structure and tone of `Skills/example_functional_doc.md`
- the three inputs (Context, Transcript, Repository) are referenced as sources
- the audience is explicit
- the problem and value are understandable quickly
- features are described through user outcomes (Purpose / Who / When / How / Value)
- ownership and support path are visible
- assumptions and gaps are listed clearly
- no placeholders remain

---

## Anti-patterns to Avoid

- Don't ask everything at once; keep the flow one step at a time
- Don't continue past a step whose input is still missing
- Don't use technical jargon or acronyms without explanation
- Don't deviate from the `Skills/example_functional_doc.md` structure and tone
- Don't copy TeeShop's literal content; reuse only its shape
- Don't skip the fixed sections (Support, Roadmap)
- Don't leave placeholders
- Don't invent information not supported by the inputs

---

## Handoff

This is the final artifact in the chain. It should still point to remaining decisions, follow-up documentation, or unresolved risks when relevant.

# AGENTS: PM Assistant System

This folder contains the main agent that produces functional product documentation. The system is designed for IT Product Managers who need a critical thinking partner, not just a content generator.

---

## Available Agent

### PM Assistant - Functional Documentation Copilot

File: PM_Assistant_Agent.md

Purpose:
- guide the user step by step to build functional documentation
- turn an initiative's delivery inputs into clear functional documentation
- act as a rubber duck that challenges weak reasoning
- keep assumptions, risks, and unknowns visible

Single capability:
- self-guided functional product documentation generation using the `Create_Functional_doc.md` skill

---

## Expected Inputs

The agent runs a **self-guided flow** and asks for each input in turn. For each initiative it collects these three inputs (pasted in chat or placed in the `Input/` folder):

1. **Context** — the initiative context.
2. **Transcript** — the transcript of the demo / review / handover / etc. meeting.
3. **Repository link** — the URL of the initiative's repository.

It does not advance past a step until that input is provided, and confirms it has all three before generating the document.

If the initiative is a **front-end application**, the agent also asks for the access URLs of the **DEV**, **PRE**, and **PRO** environments.

---

## How To Use It

Just start the flow; the agent will guide you step by step:

```text
I want to create the functional documentation for an initiative.
```

The agent then asks, one at a time, for the initiative name, the Context, the Transcript, the Repository link, the audience, the DEV/PRE/PRO URLs (if it is a front-end app), and any remaining clarifications, before generating the document.

---

## Behavioral Contract

The agent must:
- run a self-guided flow, asking for one thing at a time
- collect the three inputs in turn before generating
- ask clarifying questions when the inputs are weak
- challenge solution-first thinking
- force clear problem, user, scope, and value
- keep a running list of assumptions and unresolved questions
- follow the structure and tone of the reference example `../Skills/example_functional_doc.md`
- use the `Create_Functional_doc.md` skill instead of improvising structure

The agent must not:
- advance past a step whose input is still missing
- generate documentation without the three inputs
- accept ambiguous requests without challenge
- hide uncertainty behind polished text
- produce documentation that lacks audience, value, or ownership
- invent information not supported by the inputs

---

## Workflow Map

```text
Input/ (Context + Transcript + Repository link)
  -> Create_Functional_doc.md
  -> Output/Doc/Doc_[InitiativeName].md
```

---

## File Structure

```text
DocIA/
  Agents/
    README.md
    PM_Assistant_Agent.md
  Input/
    (Context, Transcript, Repository link per initiative)
  Skills/
    README.md
    Create_Functional_doc.md
    example_functional_doc.md   (TeeShop reference example used as the documentation template)
```

---

## Related Documentation

- Skills index: ../Skills/README.md

---

**Maintainer:** Julián Fernández Ortiz

# Skills Index

This folder contains the single skill used by PM Assistant. Its responsibility is to turn an initiative's delivery inputs into clear, stakeholder-ready functional documentation.

The skill is **self-guided**: it leads the user step by step, asking for one thing at a time, and does not advance until the current step is answered. Read the inputs, confirm understanding, then generate the document with assumptions and open questions visible.

---

## Available Skill

### Create_Functional_doc.md

Use when:
- the initiative must be explained to non-technical or mixed stakeholders
- delivery inputs must be converted into a product narrative

Expected inputs (per initiative, placed in `Input/`):
- **Context** — the initiative context.
- **Transcript** — the transcript of the demo / review / handover / etc. meeting.
- **Repository link** — the URL of the initiative's repository.

Produces:
- `Output/Doc/Doc_[InitiativeName].md`

What this skill must do:
- guide the user step by step, asking for one input at a time
- collect the three inputs (Context, Transcript, Repository link) in turn
- translate the inputs into a product narrative
- follow the structure, tone, and section order of the reference example `example_functional_doc.md`
- explain value, users, features, permissions, and support model
- remove engineering-only jargon unless necessary
- capture assumptions or missing details clearly
- ground every statement in the Context, Transcript, or Repository

Self-guided flow:
1. Ask for the initiative name.
2. Ask for the Context, summarize, and confirm.
3. Ask for the Transcript, summarize, and confirm.
4. Ask for the Repository link and confirm.
5. Ask for the audience and purpose.
6. If it is a front-end application, ask for the DEV, PRE, and PRO URLs.
7. Ask remaining clarifying questions, one at a time.
8. Show a pre-generation summary and ask for confirmation.
9. Generate `Output/Doc/Doc_[InitiativeName].md`.

Do not exit this skill until:
- the three inputs are referenced as sources
- the audience is explicit
- the value proposition is clear
- main flows and roles are understandable
- support and next steps are documented

---

## Reference Example

The generated document must follow the structure, tone, and section order of `example_functional_doc.md` (in this same `Skills/` folder, the fictional **TeeShop** initiative). It is the canonical template: reuse its shape, never its literal content, and omit sections that do not apply.

---

## Skill Output Contract

The skill output must follow the structure of `example_functional_doc.md` and include:

- source inputs used (Context, Transcript, Repository)
- assumptions made
- unresolved questions
- recommended next action

If an input is missing or too weak, the skill should stop and ask for clarification instead of guessing.

---

## Flow

```text
Input/ (Context + Transcript + Repository link)
  -> Create_Functional_doc
  -> Output/Doc/Doc_[InitiativeName].md
```

---

## Related Documentation

- Agent guide: ../Agents/README.md
- Agent specification: ../Agents/PM_Assistant_Agent.md

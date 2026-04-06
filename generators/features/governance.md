# Feature: Governance Space

## Context File Block

```markdown
## {DOMAIN:Governance} — Process Frameworks and Decision Authority

The {DOMAIN:governance}/ directory holds documents that define *how the work is governed* — not the work itself. Operating models, intake processes, role charters, SLAs, authority matrices, and review frameworks live here. These are process-layer artifacts distinct from domain knowledge ({DOMAIN:notes}/), operational state (ops/), and self-understanding (self/).

**The distinction matters:** A decision note captures *what* was decided and *why*. A {DOMAIN:governance} document captures *how decisions are made, by whom, and under what conditions*. The first belongs in decisions/. The second belongs here.

### When to Use {DOMAIN:Governance}/

Create a document in {DOMAIN:governance}/ when:
- You are defining a repeatable process that others follow (intake, triage, review, escalation)
- You are establishing role boundaries and decision rights
- You are setting SLAs or quality gates for a workflow
- You are documenting exception handling and escalation paths
- The artifact needs to be referenced across sessions and by multiple stakeholders

Do NOT put here:
- Individual decisions (use decisions/)
- Requirements from specific initiatives (use requirements/ or the initiative MOC)
- Meeting notes or stakeholder feedback (use inbox/)
- Technical specifications (use architecture/ or technical-specs/)

### {DOMAIN:Governance} Document Structure

Each document in {DOMAIN:governance}/ follows a lightweight format:

```markdown
## {DOMAIN:Framework} Title

**Purpose**: One sentence — what problem this process solves.
**Audience**: Who uses this process.
**Status**: Draft | Approved | Active | Deprecated
**Owner**: Role, not person name — the role that maintains this.
**Last updated**: YYYY-MM-DD

---

### Scope

What is in scope for this process. What is explicitly out of scope.

### Roles and Decision Rights

| Role | Accountability | Authority | Escalation Path |
|------|---------------|-----------|-----------------|
| ... | ... | ... | ... |

### Process Flow

[Intake → Triage → Action → Close or similar stages]

For each stage: objective, inputs, activities, exit criteria, outputs, SLA.

### Exceptions and Escalation

How edge cases are handled. Who resolves conflicts. Appeal paths.

### Metrics and Review

What is measured. Review cadence. Triggers to update the process.
```

### {DOMAIN:Governance} Lifecycle

**Create** when:
- A process is repeatedly invoked across sessions but has no formal definition
- Stakeholders need a shared reference for how something works
- You need to onboard others to a workflow without re-explaining from scratch

**Update** when:
- A process change is approved (update the document, not a new one)
- Metrics show the current approach is not working
- Scope changes materially

**Deprecate** (do not delete) when:
- A newer process supersedes this one — mark deprecated, add `superseded_by:` field, link to new document

### Routing from Inbox

When content arrives in inbox/ that is a process proposal, a governance update, or a framework draft:
1. Process through the pipeline to extract any embedded decisions into decisions/
2. Place the framework document itself in {DOMAIN:governance}/
3. Link the {DOMAIN:governance} document from relevant initiative MOCs or topic {DOMAIN:topic maps}

### Integration with Decisions and Notes

{DOMAIN:Governance} documents complement, not replace, decisions/ notes:
- The {DOMAIN:governance} document explains the *process*
- The decisions/ note explains a *specific choice* made within that process
- Link from {DOMAIN:governance} to related decisions: `See [[Decision title]]`
- Link from decisions to the governing process: `Governed by [[{DOMAIN:Framework}]]`

### Maintenance Protocol

| Condition | Action |
|-----------|--------|
| {DOMAIN:governance} document not reviewed in 90+ days | Surface in session orient as stale — review and update or deprecate |
| Process frequently not followed | Create a tension note in ops/tensions/, run /arscontexta:rethink |
| Stakeholders asking questions the document should answer | Update the document |
| New exception scenario arises | Add to Exceptions section, capture the decision in decisions/ |
```

## Configuration Signals

This feature activates during derivation when the workspace exhibits:

- **Process ownership**: The domain involves workflows where multiple roles participate
- **Intake and triage**: The domain receives requests, issues, or submissions that need classification
- **Role-based authority**: Different roles have different decision rights
- **SLA expectations**: Time-bound commitments to stakeholders
- **Escalation paths**: Clear chains when decisions cannot be made at one level

Common domains where governance activates: product management, legal/compliance, open-source project maintenance, platform/API stewardship, policy work, regulated environments.

This feature does NOT activate for: personal knowledge systems, solo research vaults, technical reference libraries, or any domain where work is individual and process-free.

## Vocabulary Derivation

| Concept | Default | Alternatives |
|---------|---------|-------------|
| `{vocabulary.governance}` | `governance` | `process`, `frameworks`, `operations`, `policy` |
| `{vocabulary.framework}` | `framework` | `charter`, `model`, `playbook`, `protocol` |
| `{vocabulary.intake}` | `intake` | `request`, `submission`, `issue` |
| `{vocabulary.review}` | `triage` | `review`, `assessment`, `evaluation` |

Adapt vocabulary to match how the domain naturally speaks. A legal team says "matter intake." An open-source project says "issue triage." A platform team says "request intake." The structure is the same; the words change.

## Dependencies

Requires: `wiki-links` (governance documents link to decisions and notes), `schema` (governance documents benefit from YAML frontmatter for status, owner, and review date fields)

Optional: `self-space` (governance documents may reference role owners tracked in self/relationships.md)

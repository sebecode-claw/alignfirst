# AlignFirst Skill

AlignFirst enables AI agents to write the code you would write. It's distributed as an _Agent Skill_ and works well with:

- **GitHub Copilot**
- **Cursor**
- **Claude Code**
- **OpenAI Codex**

## Get Started

Give your agent **[this installation prompt](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/install-alignfirst.md)**.

## Using AlignFirst

### Generate Technical Specification

A specification can be written long before the implementation. The agent helps you write it by investigating and initiating a discussion:

```markdown
/alspec [something to do]
```

The agent will discuss with you, then write a `_plans/123/A1-spec.md` file.

_Note: `123` is the ticket ID. If it can be deduced from the branch name, it will. Otherwise the agent will ask you. `A1` means it's the first file of cycle A (files are organized by cycles)._

### Generate Implementation Plan(s)

Plans orchestrate what agents or subagents will do:

```markdown
/alplan
```

The agent reads the spec and writes a plan `_plans/123/A2-plan.md`, or a main plan `_plans/123/A2-main-plan.md` with several sub-plans.

### Implementation

**Clear the context**, then execute the plan(s):

```markdown
Execute the plan `_plans/123/A2-main-plan.md`
```

The agent executes the plan and writes `.summary.md` files.

### Align-and-Do Protocol (AAD)

There is also a lighter prompt for small tasks without specs or plans. Here's how to trigger it:

```markdown
/al [something to do]
```

The agent will discuss it with you first, then work directly on the codebase. At the end, a `_plans/123/A1-AAD.summary.md` file will be written.

## Additional Information

### About Agent Skills

Agent Skills is an [open standard](https://agentskills.io/) that works out of the box in Claude Code. Here are the documentations:

- [Copilot in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
- [Cursor](https://cursor.com/docs/context/skills)
- [Claude Code](https://code.claude.com/docs/en/skills)
- [Codex](https://developers.openai.com/codex/skills/)
- [Gemini CLI](https://geminicli.com/docs/cli/skills/)
- [Antigravity](https://antigravity.google/docs/skills)

### Rationale

Specs, plans, and summaries must be written in well-organized (git-ignored) local files, because:

1. The context window is limited, the compression mechanism is opaque, and we want to be able to continue an unfinished task in a fresh session.
2. It's a way to keep track of what was agreed upon with the agent and what has been done.

### Is it "Spec-Driven Development" (SDD)?

I don't know. If you have a clue, let me know, I'm interested.

## Technical Documentation Authoring Skill

The **Technical Documentation Authoring** skill is independent of AlignFirst but is provided here. It helps you create skills that document your project:

1. Give your agent **[this installation prompt](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/install-technical-documentation-authoring.md)**.
2. Clear the context, then ask it:

    ```markdown
    Help me bootstrap our project skills. Use technical-documentation-authoring.
    ```

It can also work alongside AlignFirst:

```markdown
/al We need a documentation about [topic]. Use technical-documentation-authoring.
```

## Installation, Migrations

- **[Upgrade from v1](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/upgrade-to-agent-skills.md)**: If you have an old `_docs/alignfirst/` installation, migrate to the Agent Skills standard
- **[Install AlignFirst Skill](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/install-alignfirst.md)**
- **[Install Technical Documentation Authoring Skill](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/install-technical-documentation-authoring.md)**
- **[Update Skills](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/update-skills.md)**: Update installed _AlignFirst_ and/or _Technical Documentation Authoring_ skills to the latest version

## License

CC0 1.0 Universal.

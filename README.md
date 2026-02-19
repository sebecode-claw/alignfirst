# AlignFirst Skill

AlignFirst enables AI agents to write the code you would write. It's distributed as an _Agent Skill_ and works well with:

- **GitHub Copilot**
- **Cursor**
- **Claude Code**
- **OpenAI Codex**

## Installation (Automatic)

This is the all-in-one-prompt installation. It downloads files and configures your project — you trust the prompt to run `curl` commands and edit your files.

Give your agent **[this installation prompt](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/install-alignfirst.md)**.

## Or, Post-Install Setup after a Manual Installation

If you installed the skill files yourself (downloaded them or used a third-party skill manager), your project still needs to be configured. Give your agent this prompt:

**Prompt to run:**

```markdown
I just installed the alignfirst skill. Please help me configure it:

1. Create `_plans/.gitkeep` if it doesn't exist, and add `_plans/*` and `!_plans/.gitkeep` to `.gitignore` if needed.
2. Check if `AGENTS.md` or `CLAUDE.md` exists. If one exists, use it. If neither exists, create `AGENTS.md`. This file is our INSTRUCTION_FILE.
3. Look at our git branches (`git branch -a`) to detect our ticket ID format (e.g., `ABC-###`, `PROJ-###`, or numeric).
   - If no pattern is found, ask me for our ticket ID format.
4. If there is a pattern for our ticket ID, add this section in the INSTRUCTION_FILE:

   ## Ticket ID

   _Ticket ID_: Format is `{DETECTED_FORMAT}`. When not provided, deduce it from the branch name if possible—no need to confirm.

5. Ensure the INSTRUCTION_FILE contains: "Always ignore the `_plans` directory when searching the codebase."
6. Install commands by following the instructions in [install-commands.md](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/install-commands.md).
```

## Usage

### Align-and-Do Protocol (AAD)

There is also a lighter prompt for small tasks without specs or plans. Here's how to trigger it:

```markdown
/al [something to do]
```

The agent will discuss it with you first, then work directly on the codebase. At the end, a `_plans/123/A1-AAD.summary.md` file will be written.

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

### Generate PR/MR Description

After implementation, generate a description summarizing the work done and a commit message:

```markdown
/aldescription
```

The agent reads all specs and summaries in the task directory, then writes a concise `_plans/123/B1-description.md` file with a functional description of what was done and a Conventional Commits message.

## Additional Information

### Rationale

Specs, plans, and summaries should be written in well-organized (git-ignored) local files, because:

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

## Migrations

- **[Install AlignFirst Skill](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/install-alignfirst.md)**
- **[Install Technical Documentation Authoring Skill](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/install-technical-documentation-authoring.md)**
- **[Upgrade from v1](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/upgrade-to-agent-skills.md)**: If you have an old `_docs/alignfirst/` installation, migrate to the Agent Skills standard
- **[Update Skills](https://raw.githubusercontent.com/paleo/alignfirst/refs/heads/main/migrations/update-skills.md)**: Update installed _AlignFirst_ and/or _Technical Documentation Authoring_ skills to the latest version

## License

CC0 1.0 Universal.

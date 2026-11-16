# MerkleCode

An autonomous agentic coding assistant that runs inside VS Code.

<img width="1322" height="512" alt="MerkleCode running inside VS Code" src="https://github.com/user-attachments/assets/fb7e2ed8-2b82-47e8-a7a4-6d49259925ba" />

## What it is

MerkleCode is an agent that works on your codebase from inside the editor rather
than in a separate chat window. You describe the change you want; it reads the
relevant files, plans the edit, applies it across files, and verifies the result
by running your project's own tests, build, or linter.

## Why it exists

Most assistant tools stop when the diff looks plausible. MerkleCode treats the
verification loop as the product: a change counts as finished only once
something has actually run and passed. That single constraint shapes everything
else — the agent reads code before writing it, traces the call sites it is about
to affect, and reports what it ran rather than what it assumed.

## How a task runs

1. **Orient** — the agent locates the code that matters, using the editor's file
   tree and the project's own structure rather than a guess from the prompt.
2. **Plan** — for anything beyond a small edit, it states the steps first, so you
   can approve or redirect before files change.
3. **Edit** — changes are applied as targeted edits across the files involved,
   not regenerated wholesale.
4. **Verify** — the project's test, build, or lint command is executed, and the
   result is reported as it came back.
5. **Explain** — the agent closes with what changed, why, and what it could not
   check.

## Key concepts

**The agent loop.** MerkleCode is one agent with tools, not a chat model with a
diff view bolted on. It reads files, searches the tree, follows a symbol to its
call sites, and runs commands in your workspace. Anything it tells you is
grounded in something it actually read or executed during that turn.

**Verification over assertion.** A plausible-looking patch is not a finished
change. The agent runs your project's own test, build, or lint command and
reports the result as it came back; when it could not run one, it says so
instead of implying success.

**Plans and approval.** Larger work is stated as a short numbered plan before any
file changes, so you can approve, edit, or redirect it. Small edits skip that
gate and happen immediately.

**Skills.** Recurring jobs — reviewing a diff, triaging a failing build, writing
tests, upgrading a dependency — are packaged as skills: a playbook the agent
follows end to end rather than improvising a shallower version of it.

**Sub-agents.** Breadth-first exploration, such as mapping an unfamiliar
repository or sweeping for every use of an API, can be delegated to a helper
with its own context window that returns only its conclusions, leaving the main
agent's context for the work it owns.

**Permissions.** Every action runs under a permission mode. In a trusted
workspace, routine edits and commands run straight away; otherwise the agent
asks before it changes anything.

## Status

**This repository currently contains documentation only** — no source code,
build scripts, package manifests, or releases. There is nothing to install or
run from this checkout. This section will be replaced with real installation and
quickstart instructions once the source is published here.

## Repository layout

| Path | Purpose |
| --- | --- |
| `README.md` | This file — project overview |
| `LICENSE` | MIT license text and copyright holder |

## Contributing

Issues and pull requests are welcome through this repository's tracker. Since
there is no source or contribution guide here yet, please open an issue to
discuss a change before sending a pull request.

## Documentation scope

This README covers the product at a conceptual level only. Deliberately absent,
because the material they would describe does not exist in this repository yet:

- **Quickstart, configuration reference, troubleshooting** — these require an
  installable extension and a settings schema; neither is published here.
- **Internal design and implementation notes** — these belong alongside the
  source they describe, not in a top-level overview.
- **Contribution workflow, coding standards, release process** — to be documented
  when there is code to contribute to.

## License

MIT — see [`LICENSE`](LICENSE). Copyright (c) 2026 merklecodeai.

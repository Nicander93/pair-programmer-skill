# Pair Programmer

A portable Agent Skill for human-paced AI pair programming.

AI coding agents can implement changes faster than a person can understand and review them. `pair-programmer` changes that default behavior: the AI remains the primary implementer, but works in small, coherent increments, explains material decisions, reports verification honestly, and keeps the next step visible.

## Installation

### Recommended: skills CLI

```bash
npx skills add Nicander93/pair-programmer-skill
```

Useful options:

```bash
# Install globally (all projects)
npx skills add Nicander93/pair-programmer-skill -g

# Install for specific agents
npx skills add Nicander93/pair-programmer-skill -a cursor -a claude-code

# Non-interactive
npx skills add Nicander93/pair-programmer-skill -g -y
```

### Alternative: npm

```bash
npm install pair-programmer-skill
npx skills experimental_sync
```

### Manual

Copy `skills/pair-programmer/` into the skills directory supported by your coding agent. Keep the directory name unchanged because it matches the `name` declared in `SKILL.md`.

The skill requires an agent that can inspect a codebase and, when authorized, modify it. No scripts, dependencies, network access, or external services are required.

## What it changes

The skill instructs a coding agent to:

- understand relevant code before editing;
- prefer minimal, reviewable changes;
- avoid unrelated refactoring and speculative abstractions;
- make routine decisions independently;
- explain architecture and implementation decisions that matter;
- use practical verification even in legacy codebases without tests;
- summarize completed work, verification, concerns, and the next step.

It deliberately does **not** impose a rigid approval workflow, fixed line limits, mandatory test creation, or confirmation before every change.

## Structure

```text
pair-programmer-skill/
├── package.json
├── README.md
├── README.zh-CN.md
├── CHANGELOG.md
├── LICENSE
└── skills/
    └── pair-programmer/
        └── SKILL.md
```

`SKILL.md` is the complete runtime skill. The remaining files are repository documentation and release metadata.

## Usage

Invoke the skill when you want to work through a codebase with the AI rather than delegate an entire task without review.

Example requests:

```text
Use pair-programmer to help me understand and improve this module.
```

```text
Pair with me on this bug. Keep the changes small and explain the important decisions.
```

```text
Continue with the next coherent increment.
```

The skill is most useful for:

- unfamiliar or historical codebases;
- incremental feature development;
- architectural improvement;
- bug investigation and repair;
- sustained code reading and refactoring;
- users who want the AI to write most of the code while retaining understanding and control.

## Design Principles

1. **Implementation ownership without runaway autonomy**  
   The AI writes code and makes routine decisions, but does not silently turn a bounded task into a broad rewrite.

2. **Reviewability over artificial limits**  
   An increment is small when it is coherent, explainable, and reversible—not when it stays under a fixed line count.

3. **Decision summaries over thought dumps**  
   The skill asks for assumptions, evidence, alternatives, and trade-offs that help review decisions, not exhaustive hidden reasoning.

4. **Evidence appropriate to the repository**  
   Automated tests are preferred when available, but compilation, static checks, focused scripts, manual behavior checks, and call-path inspection are valid evidence in legacy systems.

5. **Adaptive communication**  
   Simple changes receive a short report; consequential changes receive more detail.

## Scope

This skill shapes collaboration behavior. It does not prescribe a programming language, framework, architecture, branching strategy, commit convention, or testing stack.

Project-specific coding standards should remain in repository instructions or separate skills.

## Versioning

This project follows semantic versioning. See [CHANGELOG.md](CHANGELOG.md).

## License

MIT

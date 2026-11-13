# Agent Instructions

Repository-specific operating rules for AI coding agents.

## Core Context

Read before non-trivial changes:

- `GOALS.md`
- `SCOPE.md`
- `CONVENTIONS.md`
- `adr/` - accepted decisions

## Language

UK English in documentation, comments, and user-facing text. Do not use the em dash (U+2014); see `CONVENTIONS.md` (Documentation).

## Tech Stack

- .NET 10.0 (LTS).
- xUnit v3 with Microsoft.Testing.Platform; NSubstitute when mocks are required; built-in asserts only.

## Skills

Project skills live in `.agents/skills/`.

| Skill | Use when |
|---|---|
| `create-architectural-decision-record` | Creating or major-updating an ADR |
| `documentation-writer` | Diátaxis-aligned documentation |
| `project-documentation` | Project-aware docs placement |
| `code-review` | PR or branch review before merge (see `.cursor/commands/loop-code-review.md`) |
| `implementation-guardrails` | Non-trivial implementation, refactors, analyzer/build fixes, EF migrations, new abstractions - root-cause and proportionality discipline |

### Optional stacks (add in the child repo)

See [TEMPLATE.md](TEMPLATE.md) for Dev Container extensions. Onboard **.NET Aspire** and **Spec Kit** using each project's current official documentation (not by copying skills from another repository).

## Task Routing

- **Code** (`src/`, `tests/`): `CONVENTIONS.md`.
- **Documentation** (`**/*.md` except `adr/`): documentation skills.
- **ADRs** (`adr/*.md`): ADR skill only.

## Not Allowed Without Explicit Instruction

- Add or remove NuGet packages (except central versions in `Directory.Packages.props` when maintaining deps).
- Modify CI/CD behaviour.
- Commit secrets or API keys.

## Pull Request Workflow

Follow [plan/PULL_REQUEST_POLICY.md](plan/PULL_REQUEST_POLICY.md) and [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md).

Before opening a PR:

```bash
dotnet format Repo.slnx --verify-no-changes
dotnet build Repo.slnx -c Release -warnaserror
dotnet test Repo.slnx -c Release --no-build
```

Title shape: `[Type] Imperative summary (#NNN)` with labels from [plan/LABEL_STRATEGY.md](plan/LABEL_STRATEGY.md).

All agent-authored pull requests require human review before merge.

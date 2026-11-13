# C# OSS project template

GitHub template for **Mark Heydon**-style open source .NET repositories: governance markdown, agent skills and rules, CI, optional GitHub Releases on tags, Dev Containers / Codespaces, and xUnit v3 tests. Works for apps, tools, and general OSS code; use a dedicated library or API-client template when NuGet is the primary deliverable.

**Using this template:** click **Use this template** on GitHub, then follow [TEMPLATE.md](TEMPLATE.md).

**HTTP API client SDK?** Start from [dotnet-api-client-template](https://github.com/markheydon/dotnet-api-client-template) instead (NuGet, typed `HttpClient`, sample console, Pages docs).

## Quick start

In a dev environment with the .NET 10 SDK, or inside the [Dev Container](.devcontainer/devcontainer.json):

```bash
dotnet build Repo.slnx -c Release -warnaserror
dotnet test Repo.slnx -c Release --no-build
```

## Repository layout

| Path | Purpose |
|------|---------|
| `GOALS.md`, `SCOPE.md`, `CONVENTIONS.md` | Product and coding context for humans and agents |
| `AGENTS.md` | Operating rules for coding agents |
| `.agents/skills/` | Agent Skills (`SKILL.md` per folder) |
| `.cursor/rules/`, `.cursor/commands/` | Optional Cursor-specific rules and commands |
| `.devcontainer/` | Dev Container for local VS Code / GitHub Codespaces |
| `plan/` | Release and PR policy |
| `adr/` | Architectural decision records |

Private repositories can use the same layout; see [TEMPLATE.md](TEMPLATE.md) (section 5).

## Licence

MIT - see [LICENSE](LICENSE).

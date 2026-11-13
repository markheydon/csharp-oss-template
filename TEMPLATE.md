# Template setup checklist

Complete after **Use this template** (or cloning).

## 1. Rename placeholders

Search the repository for **`Acme.Project`** and replace with your project name (for example `MyCompany.Widgets` or `MyApp`).

| Item | Action |
|------|--------|
| `Repo.slnx` | Rename to your product solution (for example `MyApp.slnx`) and update paths inside |
| `.github/workflows/*.yml` | Replace `Repo.slnx` with your solution file name |
| `.vscode/settings.json` | Set `dotnet.defaultSolution` to your solution file |
| `.cursor/commands/` | Replace `Repo.slnx` in command text if you use Cursor |
| `src/Acme.Project/` | Rename folder and `.csproj` |
| `tests/Acme.Project.Tests/` | Rename folder, `.csproj`, and project reference |
| `RootNamespace` | Set in `.csproj` if different from assembly name |
| `README.md` | Product title, badges, links |
| `GOALS.md`, `SCOPE.md` | Real goals and boundaries |
| `.github/ISSUE_TEMPLATE/config.yml` | Contact links to your repo (`SUPPORT.md`, discussions, security policy) |
| `SUPPORT.md`, `SECURITY.md` | Your support routing and disclosure contact |
| `plan/PULL_REQUEST_POLICY.md` | Assignee and examples if they should not point at `markheydon` |

For packable **libraries** or HTTP client SDKs, use a dedicated template ([dotnet-api-client-template](https://github.com/markheydon/dotnet-api-client-template)) instead of extending this one for NuGet publishing.

## 2. GitHub repository settings

- **About:** description, website, topics (`csharp`, `dotnet`, `open-source`, …).
- **Branch protection:** require CI on `main` if desired.
- **Secrets:** only when you add integrations (deployment, live smoke tests, and similar).

## Optional: Documentation strategy

Define this when you grow beyond the README. The template does not prescribe a public doc site.

- In **`GOALS.md`** or **`SCOPE.md`**, state who each channel is for (contributors, library integrators, app users, operators).
- **`README.md`** remains the repository front door (evaluate, clone, build).
- **Extended docs** can live in `docs/` (for example GitHub Pages from `/docs`), a separate folder such as `website/` (Hugo or another static site), or an external host; record the choice in project context so agents place new markdown correctly.
- In-repo writing follows the [`project-documentation`](.agents/skills/project-documentation/) skill (Diátaxis types and [placement guide](.agents/skills/project-documentation/references/document-placement.md)). A product site in `website/` is a downstream concern; wire publishing in CI when needed.

## 3. Agents and tooling

These assets are **agent-agnostic** where possible:

| Path | Purpose |
|------|---------|
| `AGENTS.md` | Operating rules for coding agents |
| `.agents/skills/` | [Agent Skills](https://agentskills.io/specification)-format skills (`SKILL.md` per folder) |

**Cursor-specific (optional):** [`.cursor/rules/`](.cursor/rules/) and [`.cursor/commands/`](.cursor/commands/) help in Cursor only. Remove or trim them if your team uses other agents.

**Dev Container features (optional):** the default [`.devcontainer/devcontainer.json`](.devcontainer/devcontainer.json) includes `copilot-likes` and `cursor-cli`. Drop features you do not use; add others when you onboard optional stacks (below).

Keep `AGENTS.md` aligned with how you actually work. Add skills under `.agents/skills/` when you repeat a workflow.

## 4. Dev Container and Codespaces

The default Dev Container targets .NET 10 with `github-cli` (and the Cursor-oriented features above). Open the repo in **GitHub Codespaces** or **Dev Containers**, then run build/test from [AGENTS.md](AGENTS.md).

**Feature lock file:** the first successful Dev Container build may create `.devcontainer/devcontainer-lock.json`. Commit it if you want pinned features and Dependabot `devcontainers` updates; otherwise add it to `.gitignore`.

**HTTPS from a Dev Container on WSL:** after `dotnet dev-certs https --trust` in the container, run `scripts/export-dev-cert-for-windows-host.sh` and import the cert on the Windows host. Output goes under `.local/` (gitignored).

### Optional: .NET Aspire

Extend the Dev Container when the product uses Aspire:

| Item | Action |
|------|--------|
| Features | Add `ghcr.io/microsoft/aspire-devcontainer-feature/aspire:3`, `ghcr.io/devcontainers/features/docker-in-docker:4` |
| Azure CLI (optional) | Add `ghcr.io/devcontainers/features/azure-cli:1` when you deploy or sign in with `az login` locally |
| `hostRequirements` | Raise to at least 4 CPUs and 8 GB RAM |
| VS Code extension | `microsoft-aspire.aspire-vscode` |
| `postStartCommand` | `aspire certs trust --non-interactive` (replace `dotnet dev-certs https --trust`) |
| Agents | Follow current .NET Aspire documentation for AppHost setup and `aspire agent init` in your repo |

### Optional: Spec Kit

Follow the official [Spec Kit](https://github.com/github/spec-kit) installation and onboarding for your repo (devcontainer features, `.specify/`, and agent workflows). Do not copy uncustomised Spec Kit assets from another project.

## 5. Using as a private repository

The same scaffold works for private repos; you do not need a separate template.

| Item | Notes |
|------|--------|
| Visibility | CI, Dev Container, and agent assets can stay as-is |
| `LICENSE` | Replace MIT when the code is not open source |
| Community files | `CODE_OF_CONDUCT.md`, `FUNDING.yml`, and public-facing `SUPPORT.md` are optional for internal-only repos |
| Issue templates | Point [`.github/ISSUE_TEMPLATE/config.yml`](.github/ISSUE_TEMPLATE/config.yml) at your private repo URLs |
| Releases | Tag-based GitHub Releases in [plan/RELEASE.md](plan/RELEASE.md) still work for internal versioning if you want them |

> Coding and design conventions for this repository.

# Conventions

**Project:** Acme.Project
**Last updated:** (date)

When in doubt, follow this file. Significant architecture changes need an ADR.

---

## Project Structure

```
src/
└── Acme.Project/

tests/
└── Acme.Project.Tests/
```

Add folders (`samples/`, `docs/`, Blazor projects, etc.) as the product grows. Update this section when layout changes.

---

## Target framework

- Default **`net10.0`** (.NET 10 LTS) on new projects; pin the SDK band in `global.json` with `rollForward: latestPatch`.
- Multi-target older runtimes only when a shipped package needs it - add an ADR in that repository.

---

## C# patterns

- **Async/await** for I/O; propagate `CancellationToken` on public async APIs.
- **Nullable reference types** enabled (`Directory.Build.props`).
- **Treat warnings as errors** in all projects.
- **XML documentation** on public API members.
- **HTTP outbound calls** (if any): use `IHttpClientFactory` and typed clients - see [dotnet-api-client-template](https://github.com/markheydon/dotnet-api-client-template) or ADR-0001 in that template.

---

## Testing

- **xUnit v3** with Microsoft.Testing.Platform.
- **NSubstitute** when mocks are required.
- **Built-in `Assert` only** - no FluentAssertions, Shouldly, Moq, NUnit, or MSTest.
- Test classes: `[ClassName]Tests`. Test methods: `Method_State_Expected`.

---

## Documentation

- UK English in docs and comments.
- Do not use the em dash (Unicode U+2014) in user-facing text, code comments, or documentation in product scope (`src/`, `tests/`, `docs/`, `adr/`, and related root markdown). Use spaced ASCII hyphen ` - ` for prose breaks; use a single `-` for empty or missing UI values (for example table placeholders).
- User-facing docs in `docs/` when the README is not enough; see `.agents/skills/project-documentation/`.

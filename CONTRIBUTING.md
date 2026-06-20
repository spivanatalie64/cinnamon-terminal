# Contributing to Cinnamon Terminal

Thank you for your interest in contributing to Cinnamon Terminal!

**First:** if you're unsure about anything, just ask — we're friendly.

## Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [Where to Start](#where-to-start)
3. [Branch Strategy](#branch-strategy)
4. [Development Workflow](#development-workflow)
5. [Commit Message Convention](#commit-message-convention)
6. [Coding Standards](#coding-standards)
7. [Code Review Process](#code-review-process)
8. [Testing](#testing)
9. [Documentation](#documentation)
10. [Reporting Bugs](#reporting-bugs)
11. [Feature Requests](#feature-requests)

## Code of Conduct

This project follows the [Contributor Covenant](CODE_OF_CONDUCT.md).
By participating, you are expected to uphold this code.

## Where to Start

- **Issues:** Look for issues labeled `good first issue` or `help wanted`
- **Discussions:** Ask questions in the [GitLab issues](https://gitlab.acreetionos.org/acreetionos-code/cinnamon-terminal/-/issues)
- **Documentation:** Read the docs in [`docs/`](docs/)

## Branch Strategy

```
master ────────*────────*──────*───────────  ← stable (production)
                 \      /      |
unstable ────*───*────*────*──*────────────  ← upstream merges + experiments
               \  /  \  /
         feat/   fix/  docs/                  ← short-lived feature branches
```

### Branch Naming

| Branch Pattern | Purpose | Source | Merges Into |
|----------------|---------|--------|-------------|
| `master` | Stable, production-ready | — | — |
| `unstable` | Upstream merges + X11 port | `master` | `master` |
| `release/*` | Release hardening | `master` | `master` (after hardening) |
| `feat/*` | New features | `unstable` | `unstable` |
| `fix/*` | Bug fixes | `unstable` | `unstable` |
| `docs/*` | Documentation | `master` | `master` |
| `ci/*` | CI/CD changes | `master` | `master` |

### Key Rules

1. **Never commit directly to `master`** — always use merge requests
2. Feature branches should be short-lived (< 1 week)
3. Squash merge when merging to `master`
4. `unstable` accepts upstream merges + experimental work
5. Security fixes can bypass `unstable` and go directly to `master`

## Development Workflow

1. **Fork** the repository (or create a branch if you have access)
2. **Create a feature branch** from the appropriate base:
   ```bash
   git checkout unstable
   git pull origin unstable
   git checkout -b feat/my-feature
   ```
3. **Make your changes** following the coding standards
4. **Write or update tests**
5. **Commit your changes** following the commit convention
6. **Push your branch** and create a merge request
7. **Address review feedback**
8. **Merge** after approval

### Before Submitting

```bash
# Format your code
clang-format -i src/*.c src/*.h

# Run linter
clang-tidy src/*.c src/*.h -- -Ibuild/

# Build
meson setup build --prefix=/usr
meson compile -C build

# Run tests
meson test -C build

# Check for sanitizer issues
meson setup build-asan -Db_sanitize=address,undefined
meson compile -C build-asan
meson test -C build-asan
```

## Commit Message Convention

This project follows the [Conventional Commits 1.0.0](https://www.conventionalcommits.org/) specification.

### Format

```
<type>(<scope>)!: <description>

[optional body]

[optional footer(s)]
```

### Types

| Type | SemVer | When to Use |
|------|--------|-------------|
| `feat` | MINOR | A new feature |
| `fix` | PATCH | A bug fix |
| `build` | — | Build system (meson, etc.) |
| `ci` | — | CI/CD configuration |
| `docs` | — | Documentation only |
| `perf` | — | Performance improvement |
| `refactor` | — | Code restructuring |
| `style` | — | Formatting (no logic change) |
| `test` | — | Adding/fixing tests |
| `revert` | — | Reverting a change |
| `chore` | — | Maintenance, tooling |

### Scope (optional)

The scope should be a noun describing the code area:

```
feat(preferences)     — Preferences dialog
fix(vte)              — VTE integration
refactor(meson)       — Build system
docs(readme)          — README changes
ci(gitlab)            — GitLab CI changes
```

### Breaking Changes

Signal breaking changes with `!` before the colon:

```
feat(api)!: remove deprecated TerminalScreen API
```

Or in the footer:

```
fix: fix memory leak in profile handling

BREAKING CHANGE: Profile storage format has changed.
```

### Examples

```
feat(tabs): add middle-click to close tab

fix(vte): handle null pointer in resize callback

refactor(meson): split build config into subdirectory

docs(readme): add build instructions for NixOS

ci(gitlab): add nightly upstream merge pipeline

test(profiles): add unit tests for profile serialization
```

### Signed-off-by (DCO)

All commits must include a `Signed-off-by` line to certify that you have the right to submit the code under the project's license:

```
feat(terminal): add custom background opacity

Implement configurable background opacity in terminal preferences.

Signed-off-by: Your Name <your.email@example.com>
```

This certifies the [Developer Certificate of Origin](https://developercertificate.org/) (DCO).

## Coding Standards

### Language

- **C** for core terminal functionality
- **C++** where C++ features are beneficial
- Follow the existing code style in the project

### Formatting

- We use `clang-format` with the project's `.clang-format` config
- Run `clang-format -i src/*.c src/*.h src/*.cc src/*.cpp` before committing
- Line length: 100 characters max
- Indentation: 4 spaces (no tabs)

### Static Analysis

- `clang-tidy` is configured in `.clang-tidy`
- Run `clang-tidy src/*.c -- -Ibuild/` before submitting
- Warnings from bugprone and clang-analyzer checks are treated as errors

### Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Functions | camelCase | `terminalWindowNew()` |
| Variables | camelCase | `activeProfile` |
| Types/Classes | PascalCase | `TerminalWindow` |
| Constants | UPPER_CASE | `MAX_TAB_COUNT` |
| Enums | UPPER_CASE | `TERMINAL_EXIT_SUCCESS` |

## Code Review Process

1. **Author** submits merge request
2. **CI pipeline** runs automatically (must pass)
3. **At least 1 maintainer** reviews and approves
4. **Author** addresses feedback
5. **Maintainer** merges (squash merge to `master`)
6. **Branch** is deleted after merge

### Review Checklist

- [ ] Code follows project style (clang-format)
- [ ] No new clang-tidy warnings
- [ ] Tests pass
- [ ] ASan/UBSan clean
- [ ] Commit messages follow Conventional Commits
- [ ] Documentation updated if needed
- [ ] Changes are covered by tests
- [ ] No security concerns

## Testing

- Unit tests are run with `meson test -C build`
- New features should include tests
- Bug fixes should include a regression test
- Sanitizer builds (ASan + UBSan) must pass
- Test on both X11 and Wayland when possible

## Documentation

- User-facing changes should update the README
- API changes should update the relevant docs in `docs/`
- Commit messages are used to generate the CHANGELOG

## Reporting Bugs

Use the [Bug Report template](.gitlab/issue_templates/Bug.md):

1. Search existing issues first
2. Use a clear, descriptive title
3. Include exact steps to reproduce
4. Include your environment details (distro, version, display server)
5. Include terminal output if relevant

**Security vulnerabilities:** Do NOT file a public issue. See [SECURITY.md](SECURITY.md).

## Feature Requests

Use the [Feature Request template](.gitlab/issue_templates/Feature.md):

1. Explain the problem you're trying to solve
2. Describe the solution you'd like
3. Consider alternative approaches
4. Include mockups or examples if helpful

## License

By contributing, you agree that your contributions will be licensed under the [GNU General Public License v3.0 or later](COPYING).

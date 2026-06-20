# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
with a [CalVer](https://calver.org/) versioning scheme (`YY.MM.patch`).

## [Unreleased]

### Added

- Enterprise-grade release governance with quarterly cadence and LTS
- Automated CI/CD pipeline with build, test, package, merge, release, and mirror stages
- Nightly upstream merge from GNOME cinnamon-terminal into `unstable` branch
- Documentation: architecture, building, contributing, upstream tracking, X11 roadmap
- Release automation scripts: merge-upstream, release, changelog generation
- Arch Linux, Flatpak, and Snap packaging support
- Industry-standard repository configuration (.gitignore, .editorconfig, .clang-format)
- Code of Conduct (Contributor Covenant v2.1)
- Security policy (SECURITY.md) with vulnerability reporting process
- Issue templates (Bug report, Feature request) and MR template
- Pre-commit hooks configuration for code quality
- GitLab CI split into modular `.gitlab/ci/` pipeline
- Static analysis with clang-tidy and SAST scanning
- ASan/UBSan sanitizer builds in CI
- CHANGELOG.md following Keep a Changelog standard

### Changed

- **Breaking:** Repository transferred from GNOME GitLab to AcreetionOS GitLab
- **Breaking:** Project renamed from `cinnamon-terminal` to `cinnamon-terminal`
- Branch strategy: `master` → `unstable` (upstream merges) → `release/*` (hardening)
- All commit messages now follow Conventional Commits 1.0.0 specification

### Fixed

- (No upstream fixes diverged yet — tracking Cinnamon Terminal 3.97.1)

### Security

- Vulnerability reporting process established in SECURITY.md
- Signed commits required for all contributions

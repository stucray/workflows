# stucray/workflows

Reusable GitHub Actions workflows shared across my projects.

## Usage

Each consumer pins to `@v1` for the latest non-breaking version:

```yaml
jobs:
  <job-name>:
    uses: stucray/workflows/.github/workflows/<workflow>.yml@v1
```

Breaking changes cut a new major (`@v2`); the old major stays addressable for
consumers that haven't migrated.

## Workflows

| Workflow | Purpose | Stack |
|---|---|---|
| [close-completed-parent-issue](.github/workflows/close-completed-parent-issue.yml) | Auto-close a parent issue when its last open sub-issue is closed | Any |
| [ci-spring-boot-maven](.github/workflows/ci-spring-boot-maven.yml) | Build, test, static analysis (mvn verify); uploads PMD, JaCoCo, Playwright artifacts | Spring Boot + Maven |
| [ui-cross-browser-matrix](.github/workflows/ui-cross-browser-matrix.yml) | Matrix-run Playwright UI tests under Chrome + WebKit + Firefox (filtered by JUnit 5 @Tag) | Spring Boot + Maven |
| [publish-image-spring-boot-maven](.github/workflows/publish-image-spring-boot-maven.yml) | Multi-arch (amd64 + arm64) GHCR image build via Paketo + manifest stitch | Spring Boot + Maven |
| [release-spring-boot-maven](.github/workflows/release-spring-boot-maven.yml) | One-click release: version bump, mvn verify, commit + tag, atomic push, GitHub Release | Spring Boot + Maven |

## Versioning

Each workflow's contract (its `inputs` / `secrets` / behaviour) is the
versioned surface. The repo's git tags follow [semver](https://semver.org/):

- Immutable point tags: `v1.0.0`, `v1.0.1`, `v1.1.0`, `v2.0.0`
- Moving major tag: `v1` always points at the latest commit of the latest
  `1.x.y`. Consumers pin `@v1` and get bug fixes / non-breaking adds for free.
- Breaking changes cut a new major (`v2`) instead of force-moving `v1`.

## Authoring notes

- Reusable workflow files live at `.github/workflows/*.yml` (flat — GitHub
  doesn't honour subdirectories for `workflow_call`).
- Composite actions live at `.github/actions/<name>/action.yml`.
- Each workflow's header comment block documents its expected caller shape;
  treat that comment as the canonical reference.

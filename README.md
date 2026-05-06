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

_(None yet — first lands in PR #1.)_

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

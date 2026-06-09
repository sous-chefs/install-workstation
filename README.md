# Install Cinc Workstation

Install Cinc Workstation on GitHub Actions runners.

This action provides a versionable replacement for inline installer steps and
for `actionshub/chef-install` in Sous Chefs workflows. Cinc Workstation includes
the Chef-compatible command wrappers expected by cookbook CI, including `chef`.

## Usage

```yaml
steps:
  - name: Install Cinc Workstation
    uses: sous-chefs/install-workstation@v1
```

Pin a major Cinc Workstation series:

```yaml
steps:
  - name: Install Cinc Workstation
    uses: sous-chefs/install-workstation@v1
    with:
      version: "25"
```

Use the current channel when needed:

```yaml
steps:
  - name: Install Cinc Workstation
    uses: sous-chefs/install-workstation@v1
    with:
      channel: current
```

## Inputs

| Input | Required | Default | Description |
| --- | --- | --- | --- |
| `version` | No | `latest` | Cinc Workstation version to install. Use `24`, `25`, or `26` for the latest stable release in that major series, an exact version, or `latest`. |
| `channel` | No | `stable` | Cinc release channel. Usually `stable`; `current` is also accepted. |

## Tested Versions

CI tests the action on Ubuntu, macOS, and Windows with these version inputs:

| Input | Current resolved stable version |
| --- | --- |
| `24` | `24.12.1073` |
| `25` | `25.13.7` |
| `26` | `26.1.0` |
| `latest` | `26.1.0` |

The resolved versions above were checked against Cinc Omnitruck metadata on
2026-06-09.

## Supported Runners

- `ubuntu-latest`
- `macos-latest`
- `windows-latest`

The action uses the Cinc Omnitruck shell installer on Linux and macOS, and the
Cinc Omnitruck PowerShell installer on Windows.

## Releases

Releases are managed by Cocogitto from conventional commits. Merges to `main`
run the release workflow, create the next SemVer tag with a `v` prefix, update
`CHANGELOG.md`, and publish a GitHub release.

The release workflow uses `GITHUB_TOKEN` by default. If branch protection or
organization policy requires a bot identity, configure a `PORTER_GITHUB_TOKEN`
repository secret and the workflow will use it for checkout pushes and GitHub
release publication.

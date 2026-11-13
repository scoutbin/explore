# explore

explore gives codebase explore context. It is built on [spine](https://github.com/scoutbin/spine), the shared core for scoutbin's command-line tools.

## Status

explore is in early development. It has no explore-specific commands yet. The binary only has the built-in commands listed below.

## Install

Homebrew (macOS and Linux):

```sh
brew install scoutbin/tap/explore
```

npm:

```sh
npm install -g @scoutbin/explore
```

Shell installer for macOS and Linux. It needs curl or wget, and it verifies the SHA-256 checksum before installing:

```sh
curl -fsSL https://raw.githubusercontent.com/scoutbin/explore/main/install.sh | sh
```

Windows: run `install.ps1` from the repository root in PowerShell 5.1 or later, or in pwsh. You can also use npm.

Manual install: GitHub Releases has archives named `explore_<version>_<os>_<arch>.tar.gz` (`.zip` on Windows) for darwin, linux and windows, on amd64 and arm64. Each release includes a `checksums.txt`.

Run `explore version` to confirm the install.

### Installer variables

`install.sh` and `install.ps1` read these variables:

| Variable                    | Default                                                                 | Purpose                                                                                                         |
| --------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `EXPLORE_VERSION`           | Newest release on the track                                             | Install this tag. Takes precedence over `EXPLORE_TRACK`                                                         |
| `EXPLORE_TRACK`             | `stable`                                                                | `stable`, `alpha`, `beta` or `rc`                                                                               |
| `EXPLORE_INSTALL_DIR`       | `~/.local/bin` (install.sh), `%LOCALAPPDATA%\explore\bin` (install.ps1) | Install directory                                                                                               |
| `EXPLORE_NO_MODIFY_PATH`    | Unset                                                                   | Set to `1` to stop the installer from changing PATH                                                             |
| `EXPLORE_DOWNLOAD_BASE_URL` | GitHub                                                                  | install.sh only. Mirror for release assets. Must start with `https://` or `file://`. Requires `EXPLORE_VERSION` |
| `EXPLORE_GITHUB_TOKEN`      | None                                                                    | Token for the release lookup, to avoid the API rate limit. Not sent with downloads                              |

A track installs the newest release on its upgrade path. `rc` takes rc or stable releases. `beta` takes beta, rc or stable. `alpha` takes any prerelease or stable.

## Commands

| Command   | What it does                                                                                                                                                                                               |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `version` | Prints the version, commit, build time, OS and architecture. `--json` is available                                                                                                                         |
| `info`    | Prints the executable path, the install channel (`install.sh`, `npm`, `homebrew` or `unknown`) and the version                                                                                             |
| `check`   | Compares the build with the newest release on its track. Exits 1 if an update exists. Reads `GITHUB_TOKEN`                                                                                                 |
| `upgrade` | macOS and Linux only. On install.sh installs, replaces the binary in place. `--version <tag>` pins a release. On npm and Homebrew installs, prints the command to run. On Windows, run `install.ps1` again |

Global flags: `--version`, `--json`, `--no-color` (also set by the `NO_COLOR` environment variable), and `-h` or `--help`.

Exit codes: 0 for success, 1 when `check` finds an update, and 2 for any other error.

## GitHub Action

The action installs the explore binary. It does not run explore.

```yaml
- uses: scoutbin/explore@<ref>
  with:
    version: <tag>
```

| Input         | Default                                                         | Purpose                                                      |
| ------------- | --------------------------------------------------------------- | ------------------------------------------------------------ |
| `version`     | Newest release on the track                                     | Release tag to install. Takes precedence over `track`        |
| `track`       | `stable`                                                        | `stable`, `alpha`, `beta` or `rc`                            |
| `install-dir` | `$RUNNER_TEMP/explore/bin` (Windows: `RUNNER_TEMP\explore\bin`) | Install directory. Relative paths resolve from the workspace |
| `token`       | `github.token`                                                  | Token for the release lookup. Not used for downloads         |

Outputs: `version` (the installed tag) and `path` (the absolute path of the executable).

## Feedback

Report bugs and request features in [GitHub Issues](https://github.com/scoutbin/explore/issues). Pull requests are not accepted. See [CONTRIBUTING.md](CONTRIBUTING.md) for what to include in a report, and [SECURITY.md](SECURITY.md) for reporting vulnerabilities.

## License

Apache-2.0. See [LICENSE](LICENSE).

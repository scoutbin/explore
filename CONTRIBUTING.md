# Contributing to scout

Pull requests are not accepted. This is a security decision: all code in scout is written by the maintainers so that every release can be traced to them. Unsolicited pull requests will be closed without review. Please do not spend time on a fix as a PR. Describe the problem in an issue instead.

You can still help in these ways:

- Report bugs in [GitHub Issues](https://github.com/scoutbin/scout/issues)
- Request features in [GitHub Issues](https://github.com/scoutbin/scout/issues)
- Report security vulnerabilities privately, as described below

## Security vulnerabilities

Do not report security vulnerabilities in public issues. This includes proof-of-concept code and any detail that would help someone exploit the problem before a fix is released. Follow the process in [SECURITY.md](SECURITY.md).

## Reporting a bug

Search existing issues first. If the bug is already reported, add a comment with your details instead of opening a new issue.

Include the following:

- **Version and environment:** the output of `scout version` and `scout info`. `scout version` prints the version, commit, build time and OS/arch. `scout info` prints the executable path, install channel and version. If the executable path reveals private information, such as a user name or internal directory, replace it before posting. If you built from source, also give the commit SHA.
- **Steps to reproduce:** the smallest set of commands or inputs that trigger the bug. A minimal example repository is the most useful.
- **Expected behavior:** what you thought would happen, and why
- **Actual behavior:** what happened. Paste the exact output or error text, not a summary.
- **Logs:** relevant output with tokens, credentials, private paths and private source code removed

Reports without reproduction steps are hard to act on and may be closed until they include them.

## Requesting a feature

Describe the problem you are trying to solve before the change you want. Include:

- The task you are trying to do and where scout falls short
- The behavior you would expect
- A short usage example, if it helps
- Alternatives you tried and why they did not work for you

Keep each request to one feature.

## Local setup for reproducing bugs

Building from source requires Go 1.24.2 or later, as declared in `go.mod`. scout is built on [spine](https://github.com/scoutbin/spine), which is pulled in as a Go module dependency.

Build from the same commit or tag you are reporting against, so your results match the code the bug was reported on.

The CI pipeline is defined in `.github/workflows/ci.yml`. Release steps are in `.github/workflows/release.yml`. Both use reusable workflows from the spine repository.

## License

scout is licensed under the Apache License 2.0. See [LICENSE](LICENSE).

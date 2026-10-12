# Instructions for AI agents

Read [CONTRIBUTING.md](CONTRIBUTING.md) first. It has the test command, the release path and the Plane project.

Rules agents break most often here:

1. Never push to `main`. Every change is a branch and a pull request.
2. Run `python3 tools/secret_scan.py --path .` before you open a PR, and paste the result. Exit code 1 means the file is not admitted until it is fixed.
3. No credentials, tokens, `.env` values, personal details or client or employer work in any file or commit.
4. Do not delete a workflow file to stop a check. Disable it with `gh workflow disable`.
5. Do not put a `README.md` inside `.github`.
6. Relocate files with `git mv`, never copy and then delete.

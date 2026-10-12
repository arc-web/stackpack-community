# Contributing to stackpack-community

For people and agents. Read this whole file before your first change here.
Shared ARC rules (Plane, branches, PRs, secrets, release): [ARC contribution handbook](https://github.com/arc-web/agent-config/blob/main/handbook/HANDBOOK.md).
Repo standard: [repo-standard.md](https://github.com/arc-web/agent-config/blob/main/handbook/repo-standard.md) and [STANDARD.md](https://github.com/arc-web/agent-config/blob/main/handbook/STANDARD.md).

Anyone can send a change. You do not have to be in the organisation to do it.
Taking part does not need a GitHub account. If you would rather not touch GitHub at all, say what you want in the StackPack Discord, and the community's assistant builds it and saves it here for you.

## At a glance

| | |
|---|---|
| What this repo is | The public tools and member work of StackPack, saved as plain files. |
| Owner and approver | Repo owner role; approves changes: ARC operations role. Write access is held by the repo owner role, the server operator role and the community's assistant. |
| Runs live at | Nowhere. Nothing in this repo is deployed. |
| A merge reaches live by | Never automatically. A merge to `main` is the end of the change. |
| Test command | `python3 tools/secret_scan.py --path .` (runs offline; Python 3 standard library only) |
| Plane project | AGENTS (todovibes workspace) |

## Quick start for agents

1. Read the Plane task and its comments. No task, no change (ask a person to create one).
2. Claim the work so nobody else takes it.
3. Branch from the latest `main`: `docs/<short-slug>`, `fix/<short-slug>` or `feat/<short-slug>`.
4. Make the smallest change that meets the task's acceptance.
5. Run `python3 tools/secret_scan.py --path .`. Paste the result into the PR. Exit code 1 means do not admit the file until it is fixed.
6. Open a PR with the template in `.github/pull_request_template.md` filled in. Link the Plane task.
7. After review and merge: nothing to deploy. Check that the merged files are on `main`.
8. Comment on the Plane task with the PR, the scanner result, and what is left.

## Quick start for people

Say what you want in the StackPack Discord and what finished looks like. The assistant builds it, runs the scanner and saves the result here.

If you already use GitHub, fork the repo you want to change, make a branch, change the files, and open a pull request against the repo you forked. In the description, say what you changed and why. A maintainer reviews it.

## What belongs here

| Change | Home |
|---|---|
| A tool that is small, plain and needs no key or login | `tools/`, with a page beside it in `tools/README.md` |
| A prompt, guide or example other members can use | This repo, or the member's own repo |
| A fix to a broken link, typo or step | This repo |
| Anything about a client's or an employer's private work | Not here |
| Files carrying passwords, keys or personal details | Not here |
| Lessons, workshops and the community feed | The StackPack Skool group, at https://www.skool.com/stackpack/about |

One change does one thing, described in plain words.

## Layout

- `tools/`: the security scanner `secret_scan.py` and its page `tools/README.md`.
- `assets/`: images used by the README and diagrams.
- `ISSUE_TEMPLATE/`: issue forms for a broken step (`fix.yml`) and a project idea (`idea.yml`).
- `.github/`: the pull request template `pull_request_template.md` and the security scan workflow `workflows/security.yml`, which runs the same scanner command on GitHub when Actions is on. Do not put a `README.md` inside `.github`; GitHub would show it on the repo front page in place of the root `README.md`.
- `archive/`: superseded files, kept for history. Move old files here with `git mv`.
- `MANAGEMENT.md`: who may do what in this home.

## Set up and test

No setup. The scanner needs Python 3 and nothing else.

```bash
python3 tools/secret_scan.py --path .            # scan the repo
python3 tools/secret_scan.py --path . --json     # machine readable
python3 tools/secret_scan.py --path f1 f2 --json # named files only
```

## Making a change

- Nobody pushes to `main` directly. Every change is a branch and a pull request.
- Keep one change to one PR.
- Every changed Markdown file gets a humanizer pass before merge (the humanizer skill, from arc-web/arc-humanizer). The pass keeps every fact, path and link, and the PR says it ran.
- Run the scanner on the files you changed, and paste its result in the PR.
- Do not delete a workflow file to stop a check. Disable it with `gh workflow disable`.

## Release and rollback

| Layer | Here |
|---|---|
| Dev | A branch in your own copy |
| Test | `python3 tools/secret_scan.py --path .`, run locally, result pasted in the PR |
| Staging | None yet |
| Production | `main` on GitHub. Merged files are what members see. |

There is no deploy step. The check that a merge landed is that the files are on `main` and the scanner passes on them.

To undo a merged change, open a new branch from `main`, revert the merge commit, push, and open a PR:

```bash
git switch -c revert/<short-slug> origin/main
git revert <merge sha>
git push -u origin revert/<short-slug>
```

## Rules that are easy to break

- The scanner is a gate, not a guarantee. A pass does not mean a file is safe.
- Do not add a `README.md` inside `.github`.
- Every tool in `tools/` needs a page in `tools/README.md` that says what it does, how to run it and what it does not promise.
- If a tool needs a key or a login, it does not belong in `tools/`.
- Keep all five headings of the pull request template. The repo scorecard checks for them.

## Secrets

This repo holds no secrets and needs none to run the scanner. Do not add credentials, tokens or `.env` values to any file or commit. The scanner refuses the common key shapes, and the rules above cover the rest.

## Getting help

Ask in the StackPack Discord. Say which repo or file you mean, and what you saw. For a broken step, use the "Something is broken" issue form in `ISSUE_TEMPLATE/`.

If a pull request sits, a maintainer reads every pull request. If yours needs a change, they say so on the pull request itself.

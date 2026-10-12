## What and why

<one or two sentences: what changes and why>

Plane task: <link>

## Checks

- [ ] Scanner run: `python3 tools/secret_scan.py --path .` and the result is below (exit 0)
- [ ] Markdown changes had a humanizer pass, and every fact, path and link was kept
- [ ] No secrets, tokens, `.env` values, personal details or client or employer work in any file or commit
- [ ] The change is in the right place (see CONTRIBUTING.md, "What belongs here")
- [ ] Any new tool in `tools/` has its page in `tools/README.md`

## Live impact

<"none: nothing here is deployed", or the system this changes and how it is checked after>

## Rollback

<how to undo it: "revert this merge commit on a new branch and open a PR", or a more specific step>

## Evidence

<scanner output, and any other proof the checks ran>

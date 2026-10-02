# Tools

Small utilities we actually run. Each one does one job, and each one says plainly what it promises and what it does not.

## secret_scan.py

The gate on everything that lands in these repositories. It runs on its own on every push and every pull request, and the assistant runs it before handing work over.

**What it does**

- Catches recognised key shapes, private key blocks and high entropy strings in configuration files.
- Catches a short list of dangerous shell and code patterns.
- Catches oversized files.

**What it does not promise**

It is a gate, not a guarantee. A pass is not a statement that a file is safe, and it does not know your business. It catches shapes, not intentions.

**How to run it**

```bash
python3 secret_scan.py --path .                  # scan a directory
python3 secret_scan.py --path . --json           # machine readable
python3 secret_scan.py --path f1 f2 --json       # named files only
```

**What the answer means**

| Exit code | Meaning |
|---|---|
| 0 | Nothing found, or nothing high. |
| 1 | Something high was found. Do not admit the file until it is fixed. |
| 2 | The call was wrong. Nothing was scanned. |

**Where it runs**

- On every push and pull request, through `.github/workflows/security.yml`.
- In [stackpack-project-template](https://github.com/arc-web/stackpack-project-template), so a new project starts with it switched on.
- In each member repo, before anything is saved.

## Adding a tool here

One tool, one file, one page beside it. Say what it does, how to run it and what it does not promise. If it needs a key or a login, it does not belong in this folder.

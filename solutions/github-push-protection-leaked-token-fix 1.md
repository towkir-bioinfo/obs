---
title: GitHub Push Protection blocked my push (leaked token) — full fix
date: 2026-09-09
tags: [git, github, obsidian, troubleshooting]
---

# What happened

Pushing the Obsidian vault (`T:\04_Drive\obs`) to GitHub (`towkir-bioinfo/obs`) via the Obsidian Git plugin failed. The plugin showed a generic error: `push declined due to repository rule violations`, and the repo on GitHub did not update.

Running the push manually in a terminal revealed the real reason: GitHub's **secret scanning push protection** (error code `GH013`) rejected the push because a commit contained a real **GitHub Personal Access Token**, found in the file:

```
extra/567/SENSITIVE_Git-credentials.md
```

GitHub blocks any push where a commit — even an old one already in your local history — contains something that matches a known credential pattern. It does not matter if the secret is only in an old commit and deleted in the current version of the file; the token still exists in the git *history*, so GitHub still catches it.

# Why the plugin's error was useless

Obsidian Git's popup only showed the one-line summary (`push declined due to repository rule violations`). The actual reason (which file, which line, which secret type) only appears in the **full git output**, which the plugin's UI truncates. Lesson: when Obsidian Git fails on push/sync, open a real terminal and run `git push origin main` directly in the vault folder — GitHub's full error message, including the exact commit hash and file path, only shows there.

# How it was diagnosed (in order)

1. Checked repo-level **Rulesets** (Settings → Rules → Rulesets) — none existed, so it wasn't a branch protection rule.
2. Confirmed the GitHub account is a personal account, not an organization, so no org-level ruleset applied either.
3. Checked **Security → Secret scanning alerts** — showed "no secrets found." This was a red herring: a *blocked* push never lands the secret in the repo, so it never shows up as a resolved alert. This step doesn't rule out push protection.
4. Ran the push manually from a terminal to get the full error text. This showed the real cause: `GH013: Repository rule violations found` → `GITHUB PUSH PROTECTION` → `Push cannot contain secrets` → GitHub Personal Access Token found at `extra/567/SENSITIVE_Git-credentials.md:2`, in commit `4e995713`.

# The fix — step by step

## 1. Revoke the exposed token immediately

Go to GitHub → your avatar → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**. Delete the leaked token. Treat it as compromised the moment it's in git history, whether or not the push ever succeeds.

## 2. Generate a new token

Same page → **Generate new token (classic)**.

- Only tick the top-level **`repo`** scope (this auto-includes its sub-scopes: `repo:status`, `repo_deployment`, `public_repo`, `repo:invite`, `security_events`). That's all git push/pull over HTTPS needs.
- Leave everything else (`workflow`, `admin:org`, `user`, `delete_repo`, etc.) unchecked.
- Set an expiration.
- Copy the token immediately — GitHub shows it only once.

## 3. Update the saved credential on Windows

The Obsidian Git plugin (and git itself, on Windows) reads/writes saved GitHub credentials via **Windows Credential Manager**, not a plaintext file.

1. Open it: `Win+R` → `control /name Microsoft.CredentialManager` → Enter. (Searching "Credential Manager" by name in the Start menu also works — do **not** confuse it with `CredentialEnrollmentManager.exe`, a different, unrelated Windows component.)
2. Click **Windows Credentials**.
3. Under **Generic Credentials**, find the entry named `git:https://github.com`.
4. Expand it → **Edit** → replace the password field with the new token → **Save**. (Username stays as your GitHub username.)
5. If no such entry exists, skip this — git will prompt for credentials on the next push and save them fresh.

## 4. Remove the secret from git history (not just the current file)

Deleting the line in the file today does **not** remove it from history — the old commit object still contains it, and GitHub will keep blocking pushes that include that commit. The file must be stripped from every commit.

Install the tool (one-time):
```powershell
pip install git-filter-repo
```
Verify it installed correctly:
```powershell
git filter-repo --version
```
If `git filter-repo` isn't recognized as a command after installing, it likely installed outside your PATH — check with `pip show -f git-filter-repo` to find where, and add that `Scripts` folder to your Windows PATH environment variable.

**Back up first.** `git filter-repo` rewrites history destructively with no built-in undo:
```powershell
cd T:\04_Drive\obs
xcopy .git ..\obs-git-backup /E /I /H
```

Run the purge. `git filter-repo` refuses to run on a non-fresh clone by default (safety check) — since this is your live working vault, override with `--force`:
```powershell
git filter-repo --path extra/567/SENSITIVE_Git-credentials.md --invert-paths --force
```
This rewrites every commit to remove that file entirely.

**Note on Windows + virtual/synced drives:** during cleanup you may see a Windows permission error like:
```
Deletion of directory '.git/objects/01' failed. Should I try again? (y/n)
```
This happens because `T:` is (in this case) a synced/virtual drive and something (antivirus, the drive's sync client, an open Obsidian instance) briefly holds a file handle. Check the folder with `dir` — if it comes back **empty**, the actual secret-containing objects are already gone; the leftover empty folder itself is cosmetic and safe to ignore (or delete later via File Explorer, which handles the virtual drive's shell integration better than PowerShell's `rmdir`).

## 5. Re-add the remote and force-push

`git filter-repo` removes the `origin` remote as a safety measure. Re-add it and push the cleaned history:
```powershell
git remote add origin https://github.com/towkir-bioinfo/obs.git
git push origin main --force
```
A force-push is safe here because this machine is the only source of this history (no one else has cloned/based work on the old commits).

## 6. Prevent recurrence

Add the credentials file (or its whole folder) to `.gitignore` so it can never be committed again:
```powershell
Add-Content -Path .gitignore -Value "extra/567/SENSITIVE_Git-credentials.md"
git add .gitignore
git commit -m "ignore sensitive credentials file"
git push origin main
```

# If another machine has this repo cloned

Any other clone of this repo (besides the two PCs already in sync) will still have the *old* history cached locally, containing the secret. A normal `git pull` won't cleanly resolve the rewritten history. On any such machine, run:
```powershell
git fetch origin
git reset --hard origin/main
```
or just delete the local clone and re-clone fresh.

# Quick reference (commands only)

```powershell
cd T:\04_Drive\obs

# backup before rewriting history
xcopy .git ..\obs-git-backup /E /I /H

# install + purge
pip install git-filter-repo
git filter-repo --path <path/to/secret-file> --invert-paths --force

# reconnect + push
git remote add origin https://github.com/towkir-bioinfo/obs.git
git push origin main --force

# prevent recurrence
Add-Content -Path .gitignore -Value "<path/to/secret-file>"
git add .gitignore
git commit -m "ignore sensitive credentials file"
git push origin main
```

# Key takeaways for future-me

- Never store real API keys, tokens, or passwords as plain text inside vault notes that are git-tracked — not even in a folder named "SENSITIVE" or similar, since git tracks it exactly like any other note.
- `push declined due to repository rule violations` is GitHub's generic wrapper message. It can mean a branch protection ruleset, an org-level ruleset, **or** secret scanning push protection (`GH013`). Always get the full terminal output to know which.
- A secret being absent from GitHub's "Secret scanning alerts" page does not mean push protection isn't the cause — a blocked push never creates an alert.
- Removing a secret from the current file is not enough. It has to be purged from git *history* with a tool like `git filter-repo` (or BFG Repo-Cleaner), then force-pushed.
- Always revoke/rotate the actual leaked credential — purging history is cleanup, not the fix for the credential itself.

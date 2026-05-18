# Deploy to GitHub

Use this checklist to version your source code on GitHub and clone it later.

## Prerequisites

1. **Xcode command line tools / license** (if `git` fails with a license error):
   ```bash
   sudo xcodebuild -license
   ```
   Accept the license when prompted.

2. **GitHub account** and (optional) [GitHub CLI](https://cli.github.com/) installed for creating the repo from the terminal.

---

## Steps

### 1. Initialize Git (if not already done)

```bash
cd /Users/annicakburns/Development/mammoth-game-mode
git init
```

### 2. Stage and commit

```bash
git add .
git status   # confirm: .gitignore, README.md, pyproject.toml
git commit -m "Initial commit: mammoth-game-mode Python project"
```

### 3. Create the repository on GitHub

**Option A – GitHub website**

1. Go to [github.com/new](https://github.com/new).
2. Repository name: `mammoth-game-mode` (or any name you prefer).
3. Choose **Private** if you want to keep the code non-public.
4. Do **not** add a README, .gitignore, or license (you already have them locally).
5. Click **Create repository**.

**Option B – GitHub CLI**

```bash
gh auth login   # if not already logged in
gh repo create mammoth-game-mode --private --source=. --remote=origin --push
```

If you use Option B with `--push`, you can skip steps 4 and 5.

### 4. Add the remote (if you created the repo on the website)

Replace `YOUR_USERNAME` with your GitHub username:

```bash
git remote add origin https://github.com/YOUR_USERNAME/mammoth-game-mode.git
```

### 5. Push to GitHub

```bash
git branch -M main
git push -u origin main
```

If your default branch is already `main`, you can use:

```bash
git push -u origin main
```

---

## Later: clone and run

From any machine:

```bash
git clone https://github.com/YOUR_USERNAME/mammoth-game-mode.git
cd mammoth-game-mode
uv sync
```

---

## Optional: add a lockfile for reproducible installs

If you use `uv` and want the same dependency versions everywhere:

```bash
uv lock
git add uv.lock
git commit -m "Add uv.lock for reproducible installs"
git push
```

Then anyone (or you on another machine) can run `uv sync` and get the exact same versions.

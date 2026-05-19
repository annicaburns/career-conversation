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
git init
```

### 2. Stage and commit

```bash
git add .
git status   # confirm: .gitignore, README.md, pyproject.toml
git commit -m "Initial commit"
```

### 3. Create the repository on GitHub

1. Go to [github.com/new](https://github.com/new).
2. Repository name: `career-conversation` (or any name you prefer).
3. Choose **Private** if you want to keep the code non-public.
4. Do **not** add a README, .gitignore, or license (you already have them locally).
5. Click **Create repository**.


### 4. Add the remote (if you created the repo on the website)

```bash
git remote add origin https://github.com/annicaburns/career-conversation.git
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
git clone https://github.com/annicaburns/career-conversation.git
cd career-conversation
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

## And now for deployment

This code is in `app.py`

We will deploy to HuggingFace Spaces.

Check that there's no README file in your project's deploy directory. The deploy process creates a new README file in this directory for you.

1. Visit https://huggingface.co and set up an account  
2. From the Avatar menu on the top right, choose Access Tokens. Choose "Create New Token". Give it WRITE permissions - it needs to have WRITE permissions! Keep a record of your new key.  
3. In the Terminal, run: `uv tool install 'huggingface_hub[cli]'` to install the HuggingFace tool, then `hf auth login --token YOUR_TOKEN_HERE`, like `hf auth login --token hf_xxxxxx`, to login at the command line with your key. Afterwards, run `hf auth whoami` to check you're logged in  
4. Take your new token and add it to your .env file: `HF_TOKEN=hf_xxx` for the future
5. cd into the /deploy directory and Run in terminal: `uv run gradio deploy` 
6. Follow its instructions: name it "career_conversation", specify app.py, choose cpu-basic as the hardware, say Yes to needing to supply secrets, provide your openai api key, your pushover user and token, and say "no" to github actions.  


#### More about these secrets:

If you're confused by what's going on with these secrets: it just wants you to enter the key name and value for each of your secrets -- so you would enter:  
`OPENAI_API_KEY`  
Followed by:  
`sk-proj-...`  

And if you don't want to set secrets this way, or something goes wrong with it, it's no problem - you can change your secrets later:  
1. Log in to HuggingFace website  
2. Go to your profile screen via the Avatar menu on the top right  
3. Select the Space you deployed  
4. Click on the Settings wheel on the top right  
5. You can scroll down to change your secrets (Variables and Secrets section), delete the space, etc.

#### And now you should be deployed!

If you want to completely replace everything and start again with your keys, you may need to delete the README.md that got created in this 1_foundations folder.


For more information on deployment:

https://www.gradio.app/guides/sharing-your-app#hosting-on-hf-spaces

To delete your Space in the future:  
1. Log in to HuggingFace
2. From the Avatar menu, select your profile
3. Click on the Space itself and select the settings wheel on the top right
4. Scroll to the Delete section at the bottom
5. ALSO: delete the README file that Gradio may have created inside this 1_foundations folder (otherwise it won't ask you the questions the next time you do a gradio deploy)

# git 3

## GitHub — Repos, README, Issues
**What GitHub actually is**

Git is the tool; GitHub is a website that hosts Git repositories online, adds a visual interface, and layers collaboration features on top — issues, pull requests, project boards, etc. GitHub isn't the only option (GitLab, Bitbucket exist too), but it's the most widely used in the industry.

**Creating a repository on GitHub**

On github.com → "New repository":

- Repository name
- Public vs Private — public means anyone can view it; private restricts access to invited collaborators
- Option to initialize with a README, `.gitignore`, and license — if you're connecting an *existing* local project (like yesterday's practice), leave these unchecked and connect manually to avoid conflicting histories

**Repo structure at a glance**

A GitHub repo page shows:

 
- code tab — the actual files, browsable-
-  Commit history — every commit ever pushed, viewable individually
- Branches — all branches that exist on the remote
- Issues tab — task/bug tracking (covered below)
- Pull requests tab — tomorrow's topic

**README.md — the front page of a project**

Every serious repo has a `README.md` at the root. GitHub automatically renders it as formatted text right on the repo's homepage. It's written in Markdown — a lightweight formatting syntax.

**Basic Markdown syntax for README**
```markdown
# Project Title
## Section Heading

This is a paragraph. **Bold text** and *italic text*.

- Bullet point
- Another point

1. Numbered step
2. Another step

`inline code`

```
code block
```

Link text

!Alt text
```

**A typical README structure**

```markdown
# Project Name

Short description of what the project does.

## Features
- Feature one
- Feature two

## Tech Stack
- HTML, CSS, JavaScript

## Installation
```bash
git clone https://github.com/username/repo.git
cd repo
```

## Usage
Explain how to run/use the project.

## Screenshots
!Screenshot
```

A good README lets someone understand and run your project without asking you anything.

**Why README matters beyond documentation**

Recruiters and interviewers often look at GitHub profiles — a clear README on your projects makes a real difference in how professional a repo looks, compared to a bare folder of code with no explanation.

**Issues — tracking tasks, bugs, and ideas**

The Issues tab is a built-in task tracker for the repo. Anyone with access can open an issue to report a bug, request a feature, or note something that needs doing.

Creating an issue:

- Title — short summary ("Navbar breaks on mobile")
- Description — details, steps to reproduce if it's a bug, screenshots if relevant
- Labels — categorize it (`bug`, `enhancement`, `documentation`, etc.)
- Assignees — who's responsible for it
- Milestone — optional, groups issues under a larger goal/deadline

**Closing an issue**

Manually via the button on GitHub, or automatically by referencing it in a commit message:

```bash
git commit -m "Fix navbar overflow on mobile, closes #12"
```

`#12` refers to issue number 12 — GitHub auto-links this and closes the issue once that commit is pushed to the default branch.

**Why issues matter even solo**

Even working alone, issues are a useful personal to-do list tied directly to the project — better than a random notes file, since it's linked to actual code changes and history.

**Common mistakes**

- Initializing a new GitHub repo with a README while also having a local repo with commits already — creates two unrelated histories that conflict on first push
- Writing a README with no real content ("This is my project") — wastes the opportunity entirely
- Never using Issues, then losing track of bugs/TODOs in scattered notes instead
- Broken image paths in README because the image wasn't actually pushed to the repo

**Small practice task**

- Create a new repository directly on GitHub (with README this time)
- Clone it locally using `git clone`
- Write a proper README for any of the mini-projects done so far (features, tech stack, how to run it)
- Push the updated README
- Open 3 issues on the repo: one bug, one feature request, one documentation task
- Close one of them by referencing it in a commit message

# setting up github

## 1. Install Git (if not already)

```bash
git --version
```

If it's not installed:

- **Windows**: download from git-scm.com, run installer
- **Mac**: `brew install git` (or it prompts you via Xcode tools)
- **Linux**: `sudo apt install git`

## 2. Configure your identity

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the same email as your GitHub account.

## 3. Set up authentication (SSH — recommended)

GitHub no longer accepts plain passwords over HTTPS, so SSH is the easiest long-term setup.

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

Press enter through the prompts (default location, optional passphrase).

Then copy the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the output, go to GitHub → **Settings → SSH and GPG keys → New SSH key**, paste it in.

Test it:

```bash
ssh -T git@github.com
```

You should see "Hi username! You've successfully authenticated."

## 4. Clone a repo (using SSH)

```bash
git clone git@github.com:username/repo-name.git
cd repo-name
```

## 5. Basic push/pull workflow

```bash
git pull                  # get latest changes
# ...edit files...
git add .                 # stage changes
git commit -m "message"   # commit
git push                  # push to GitHub
```

## 6. If you already have a local project (not cloned)

```bash
cd your-project
git init
git remote add origin git@github.com:username/repo-name.git
git add .
git commit -m "initial commit"
git branch -M main
git push -u origin main
```

After the `-u` the first time, plain `git push` and `git pull` will work on their own.

---

Alternative: if you'd rather use HTTPS instead of SSH, you'd use a **Personal Access Token** (PAT) as your password when Git prompts for credentials — but SSH avoids typing that repeatedly, so I'd stick with it.

# Getting Started — VSCode Setup for Windows

This guide walks you through everything you need to start authoring content using **Visual Studio Code (VSCode)**, **Git**, and **GitHub**. Follow each section in order. By the end you will have VSCode installed, your GitHub account connected, and be ready to clone, edit, and contribute to repositories.

---

## What you are setting up and why

You are moving from Xyleme to a **Markdown + GitHub** workflow. Here is a plain-English summary of what each tool does:

| Tool | What it does |
|---|---|
| **VSCode** | Your editor — where you open, read, and write content files |
| **Git** | Tracks every change you make to files, like a super-powered version history |
| **GitHub** | The cloud where your files and their history are stored and shared with the team |
| **SSH key** | A digital ID card so GitHub knows who you are without asking for a password every time |

---

## Part 1 — Install Visual Studio Code

1. Go to [https://code.visualstudio.com](https://code.visualstudio.com) and click **Download for Windows**.
2. Double-click the downloaded `.exe` file to run the installer.
   - If Windows asks "Do you want to allow this app to make changes?" click **Yes**.
   - If Windows blocks the file: right-click it, select **Properties**, check the **Unblock** box, click **OK**, then double-click again.
3. Follow the installer wizard. The default options on every screen are fine. Click **Next** through each screen and then **Install**.
4. When the installer finishes, click **Finish**. VSCode will open — continue straight to Part 2.

---

## Part 2 — Create a VSCode Profile for Skyline / Cisco work

VSCode lets you keep separate "profiles" — think of them like separate desks, each with their own settings and sign-ins. This keeps your Cisco work separate from any other VSCode work you might do.

1. Click the **person icon** at the very bottom-left of the VSCode window (it looks like a silhouette).
2. Click **Profiles** → **Create Profile**.
3. Name it `Skyline / Cisco` and click **Create**.
4. VSCode will reload into the new profile. You will see the profile name in the bottom-left corner.

> **Always make sure you are in the Skyline / Cisco profile before doing any work.** You can check and switch profiles by clicking the person icon at the bottom-left.

---

## Part 3 — Install Git

Git is the software that tracks your file changes and talks to GitHub. You need to install it once.

### Check if Git is already installed

1. Press the **Windows** key, type `git`, and look in the results.
   - If you see **Git Bash** or **Git GUI** in the list, Git is already installed. Skip to **Part 4**.
2. Or open **Command Prompt** (press Windows key, type `cmd`, press Enter) and type:
   ```
   git --version
   ```
   - If you see something like `git version 2.xx` — Git is installed. Skip to **Part 4**.
   - If you see `'git' is not recognized` — continue below.

### Install Git for Windows

1. Go to [https://git-scm.com/download/win](https://git-scm.com/download/win) and download the latest installer.
2. Double-click the `.exe` file to run it (click **Yes** if Windows asks for permission).
3. Follow the setup wizard — the default option on every screen is fine. When in doubt, leave whatever is already selected and click **Next**.
   - On the **Choosing the default editor** screen: pick **Notepad**.
   - On the **Adjusting your PATH environment** screen: leave the recommended option selected ("Git from the command line and also from 3rd-party software").
   - If you see an option for **Git LFS**: make sure it is **checked**.
4. Click **Finish** when done.
5. Close any open Command Prompt windows and reopen a fresh one before continuing.

### Enable Git LFS

Git LFS handles large files (like images). Run this once to activate it:

1. Open **Command Prompt** (Windows key → type `cmd` → press Enter).
2. Type the following and press Enter:
   ```
   git lfs install
   ```
   You should see: `Git LFS initialized.`

### Set your name and email

Git needs to know who you are so your changes are correctly attributed. Run these two commands, replacing the example values with your own:

```
git config --global user.name "Your Name"
```
```
git config --global user.email "you@skyline-ats.com"
```

---

## Part 4 — Set up an SSH key to connect to GitHub

An SSH key is a digital ID card that lets GitHub recognise your computer. You only do this once.

### Check if you already have an SSH key

1. Open **Command Prompt**.
2. Type (replace `YOUR-WINDOWS-USERNAME` with your actual Windows login name, e.g. `jsmith`):
   ```
   cd C:\Users\YOUR-WINDOWS-USERNAME\.ssh
   ```
3. Then type:
   ```
   dir
   ```
   - If you see a file called `id_ed25519` — you already have a key. Skip to **Add the public key to GitHub** below.
   - If you see "The system cannot find the path" or no `.ssh` files — continue below.

### Generate a new SSH key

1. In Command Prompt, type (replace the email with the one linked to your GitHub account):
   ```
   ssh-keygen -t ed25519 -C "you@skyline-ats.com"
   ```
2. Press **Enter** to accept the default file location.
3. When asked for a passphrase, leave it blank — just press **Enter** twice.

### Start the SSH agent (requires admin)

1. Press the Windows key, type **PowerShell**.
2. Right-click **Windows PowerShell** and choose **Run as administrator**. Click **Yes** if prompted.
3. In the admin PowerShell window, type:
   ```
   Get-Service -Name ssh-agent | Set-Service -StartupType Manual; Start-Service ssh-agent
   ```
4. Close that admin PowerShell window.

### Add your key to the SSH agent

1. Open a regular **Command Prompt** (not admin).
2. Type (replace `YOUR-WINDOWS-USERNAME` with your Windows login name):
   ```
   ssh-add C:/Users/YOUR-WINDOWS-USERNAME/.ssh/id_ed25519
   ```

### Add the public key to GitHub

1. Open **File Explorer** and navigate to `C:\Users\YOUR-WINDOWS-USERNAME\.ssh\`.
2. Find the file called `id_ed25519.pub`.
   - **Note:** It may look like a Microsoft Publisher file icon. It is not. Right-click it → **Open with** → **Notepad**.
3. Select all the text in Notepad and copy it (`Ctrl+A` then `Ctrl+C`).
4. In your web browser, go to [github.com](https://github.com) and sign in.
5. Click your profile picture (top-right) → **Settings**.
6. In the left sidebar, click **SSH and GPG keys**.
7. Click **New SSH key**.
8. In the **Title** field, type something like `My Laptop`.
9. Leave **Key type** as **Authentication Key**.
10. In the **Key** field, paste what you copied from Notepad (`Ctrl+V`).
11. Click **Add SSH key**.

### Test the connection

1. Open **Command Prompt** and type:
   ```
   ssh -T git@github.com
   ```
2. If you see a message like `Are you sure you want to continue connecting (yes/no)?` — type `yes` and press Enter.
3. You should see:
   ```
   Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
   ```
   If your username appears — you are connected.

---

## Part 5 — Install VSCode extensions

Extensions add extra features to VSCode. You need two extensions now, and one more after you clone the repository in Part 6.

### Install the GitHub Pull Request extension

This lets you manage your work submissions (Pull Requests) directly from VSCode.

1. Open VSCode and make sure you are in your **Skyline / Cisco** profile.
2. Click the **Extensions** icon in the left sidebar (it looks like four squares, one slightly separated).
3. In the search box at the top, type `GitHub Pull Request`.
4. Find **GitHub Pull Requests** in the list and click **Install**.
5. Wait for it to finish.

### Install the Marp extension

Marp lets you create presentation slides from your content.

1. In the Extensions panel, search for `marp`.
2. Find **Marp for VS Code** and click **Install**.

---

## Part 6 — Clone the Skyline DevTeam Sandbox and finish setup

Cloning means making a local copy of a repository on your computer. The **DevTeam-Sandbox** is a safe practice space — you can make mistakes here without affecting any real content.

### Clone the repository

1. Press `Ctrl+Shift+P` to open the **Command Palette**.
2. Type `Git: Clone` and select it from the list.
3. A box appears at the top of the screen. It may show a dropdown list of repositories — ignore the list and type or paste the following URL directly into the box, then press **Enter**:
   ```
   git@github.com:skyline-ats/DevTeam-Sandbox.git
   ```
4. A folder picker will appear. Choose where you want to save it on your computer (e.g. `Documents`). VSCode will create a `DevTeam-Sandbox` folder there automatically.
5. When prompted **"Would you like to open the cloned repository?"** click **Open**.

You are now looking at the DevTeam-Sandbox in VSCode.

### Install the Cisco U Preview extension

This shows you how your content will look inside the Cisco U learning platform while you are writing it. The extension file is included in the repository you just cloned.

1. Press `Ctrl+Shift+P` to open the Command Palette.
2. Type `Extensions: Install from VSIX` and select it.
3. In the file picker, navigate to the `extensions` folder inside `DevTeam-Sandbox` and select `cisco-u-preview-0.41.0.vsix`.
4. Click **Install**.
5. Restart VSCode when prompted.

---

## Part 7 — Your first practice: edit, commit, push

Now you will make a real change to the DevTeam-Sandbox. This is your practice run of the full authoring workflow.

### Before you start — pull the latest changes

Before doing any work, always pull first to make sure your local copy is up to date with whatever anyone else may have added.

1. Click the **Source Control** icon in the left sidebar (it looks like a branching tree — third icon down).
2. Click the **...** (three dots) menu at the top of the Source Control panel.
3. Select **Pull**.

> If you just cloned the repo a moment ago you can skip this — you already have the latest. But pulling first will become a habit that saves you headaches when working with others.

### Step 1 — Create a branch

**Never edit directly on the `main` branch.** Always create your own branch first. A branch is your own private workspace — nothing you do there affects the main content until you choose to merge it.

1. Look at the very bottom-left of the VSCode window. You will see the word `main` (the current branch).
2. Click on `main`.
3. A menu appears at the top of the screen. Click **+ Create new branch...**.
4. Type a name for your branch — use your name or initials (e.g. `jsmith-practice`). Use lowercase and hyphens only — no spaces.
5. Press **Enter**. The branch name in the bottom-left will change to your new branch name.

### Step 2 — Create a practice file

1. In the Explorer panel (left sidebar, top icon), right-click in an empty area → **New File**.
2. Name it `practice-YOUR-NAME.md` (e.g. `practice-jsmith.md`).
3. Click on the file to open it and type a few lines — anything you like. For example:
   ```
   # My Practice File

   Hello! This is my first Markdown file.

   This is a paragraph of text.
   ```
4. Save the file with `Ctrl+S`.

### Step 3 — Preview your Markdown (optional but fun)

1. With your `.md` file open and active, press `Ctrl+Shift+P`.
2. Type `Markdown: Open Preview to the Side` and select it.
3. A preview panel opens to the right showing your formatted content.

### Step 4 — Stage and commit your changes

"Committing" saves a snapshot of your changes locally — think of it like hitting Save in Xyleme, except it also records what changed and why.

1. Click the **Source Control** icon in the left sidebar.
2. Under **Changes**, you will see your new file listed.
3. Hover over your file and click the **+** icon that appears — this "stages" the file (marks it ready to commit).
4. In the text box at the top that says **Message**, type a short description of what you did. For example: `Add practice file for jsmith`.
5. Click the **Commit** button (the checkmark ✓ above the message box).

Your change is now saved locally.

### Step 5 — Push your changes to GitHub

"Pushing" uploads your local commits to GitHub so the team can see them.

1. After committing, you will see a **Publish Branch** or **Sync Changes** button in the Source Control panel (or in the status bar at the bottom). Click it.
2. VSCode may open a browser window asking you to sign in to GitHub — go ahead and sign in with your GitHub account. This only happens the first time.
3. If asked whether to publish to GitHub, click **OK** or **Publish Branch**.

### Step 6 — Verify on GitHub

1. Open your web browser and go to [https://github.com/skyline-ats/DevTeam-Sandbox](https://github.com/skyline-ats/DevTeam-Sandbox).
2. Click the **branch dropdown** (it says `main` by default) and look for your branch name.
3. Select your branch — you should see your practice file there.

**Congratulations — you have completed the full Git workflow: pull, create branch, edit, commit, push.**

---

## Part 8 — Using the Cisco U Preview

Once you are working on actual Cisco content files:

1. Open any `.md` file.
2. Press `Ctrl+Shift+P` → type `Cisco U: Preview` → press **Enter**.
3. A panel opens to the right showing your content rendered exactly as it will appear in the Cisco U learning platform.

---

## Quick reference — the daily workflow

| What you want to do | How to do it |
|---|---|
| Start work for the day | Pull latest (Source Control, three dots menu, Pull) |
| Create a new branch | Click branch name bottom-left, then + Create new branch |
| Save a snapshot of your work | Stage files (+), add a message, click Commit |
| Share your work with the team | Click Publish Branch or Sync Changes in Source Control |
| Check what branch you are on | Look at bottom-left corner of VSCode |
| Preview content in Cisco U style | Ctrl+Shift+P, then Cisco U: Preview |
| Open the Command Palette | Ctrl+Shift+P |

---

## Next steps

Once you are comfortable with the Sandbox, the next step is to clone the Cisco content repositories. Your Skyline team lead will share the repository URLs with you and confirm you have been added as a collaborator.

The workflow is identical — the only difference is that you will be working on real content, so treat the `main` branch with care and always work in your own branch.

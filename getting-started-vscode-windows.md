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
4. When the installer finishes, click **Finish**. VSCode will open.
5. You can close VSCode for now — you will come back to it shortly.

---

## Part 2 — Create a VSCode Profile for Skyline / Cisco work

VSCode lets you keep separate "profiles" — think of them like separate desks, each with their own settings and sign-ins. This keeps your Cisco work separate from any other VSCode work you might do.

1. Open VSCode.
2. Click the **person icon** at the very bottom-left of the window (it looks like a silhouette).
3. Click **Profiles** → **Create Profile**.
4. Name it something like `Skyline / Cisco` and click **Create**.
5. VSCode will reload into the new profile. You will see the profile name in the bottom-left corner.

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
5. Close any open Command Prompt windows and reopen a fresh one.

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
2. Type:
   ```
   cd C:\Users\YOUR-WINDOWS-USERNAME\.ssh
   ```
   Replace `YOUR-WINDOWS-USERNAME` with your actual Windows login name (e.g. `jsmith`).
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

Now you need to give GitHub a copy of your key so it can recognise you.

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

Extensions add extra features to VSCode. You need three of them.

### Install the GitHub Pull Request extension

This lets you manage your work submissions (Pull Requests) directly from VSCode.

1. Open VSCode (make sure you are in your **Skyline / Cisco** profile).
2. Click the **Extensions** icon in the left sidebar (it looks like four squares, one slightly separated).
3. In the search box at the top, type `GitHub Pull Request`.
4. Find **GitHub Pull Requests** in the list and click **Install**.
5. Wait for it to finish.

### Install the Marp extension

Marp lets you create presentation slides from your content.

1. In the Extensions panel, search for `marp`.
2. Find **Marp for VS Code** and click **Install**.

### Install the Cisco U Preview extension

This shows you how your content will look inside the Cisco U learning platform while you are writing it.

The extension file is stored in the Skyline DevTeam-Sandbox repository. You will download it as part of cloning that repo in Part 6. For now, continue to the next step.

---

## Part 6 — Clone the Skyline DevTeam Sandbox repository

Cloning means making a local copy of a repository on your computer. The **DevTeam-Sandbox** is a safe practice space — you can make mistakes here without affecting any real content.

1. Open VSCode (in your **Skyline / Cisco** profile).
2. Press `Ctrl+Shift+P` to open the **Command Palette**.
3. Type `Git: Clone` and select it from the list.
4. When the input box appears, paste the following URL and press **Enter**:
   ```
   git@github.com:skyline-ats/DevTeam-Sandbox.git
   ```
5. A folder picker will appear. Choose where you want to save it on your computer (e.g. `Documents`). VSCode will create a `DevTeam-Sandbox` folder there automatically.
6. When prompted **"Would you like to open the cloned repository?"** click **Open**.

You are now looking at the DevTeam-Sandbox in VSCode.

### Install the Cisco U Preview extension from the repo

Now that you have cloned the repo, you can install the preview extension.

1. In VSCode, open the **Explorer** panel (left sidebar, top icon — looks like two pages).
2. Navigate into the `extensions` folder.
3. Right-click the file `cisco-u-preview-0.41.0.vsix` and select... actually, follow these steps instead:
   - Press `Ctrl+Shift+P` to open the Command Palette.
   - Type `Extensions: Install from VSIX` and select it.
   - Navigate to the `extensions` folder inside `DevTeam-Sandbox` and select `cisco-u-preview-0.41.0.vsix`.
   - Click **Install**.
4. Restart VSCode when prompted.

---

## Part 7 — Your first practice: Clone, edit, commit, push

Now you will make a real change to the DevTeam-Sandbox. This is your practice run of the full authoring workflow.

### Step 1 — Create a branch

**Never edit directly on the `main` branch.** Always create your own branch first.

1. Look at the very bottom-left of the VSCode window. You will see the word `main` (the current branch).
2. Click on `main`.
3. A menu appears at the top of the screen. Click **+ Create new branch...**.
4. Type a name for your branch — use your name or initials (e.g. `jsmith-practice`). Use lowercase and hyphens only — no spaces.
5. Press **Enter**. The branch name in the bottom-left will change to your new branch name.

> You are now working in your own isolated copy. Nothing you do here affects the `main` branch until you choose to merge it.

### Step 2 — Create a practice file

1. In the Explorer panel, right-click in an empty area → **New File**.
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

"Committing" saves a snapshot of your changes locally.

1. Click the **Source Control** icon in the left sidebar (it looks like a branching tree — third icon down).
2. Under **Changes**, you will see your new file listed.
3. Hover over your file and click the **+** icon that appears — this "stages" the file (marks it ready to commit).
4. In the text box at the top that says **Message**, type a short description of what you did. For example: `Add practice file for jsmith`.
5. Click the **Commit** button (the checkmark ✓ above the message box).

Your change is now saved locally.

### Step 5 — Push your changes to GitHub

"Pushing" uploads your local commits to GitHub so the team can see them.

1. After committing, you will see a **Publish Branch** or **Sync Changes** button in the Source Control panel (or in the status bar at the bottom). Click it.
2. If asked whether to publish to GitHub, click **OK** or **Publish Branch**.

### Step 6 — Verify on GitHub

1. Open your web browser and go to [https://github.com/skyline-ats/DevTeam-Sandbox](https://github.com/skyline-ats/DevTeam-Sandbox).
2. Click the **branch dropdown** (it says `main` by default) and look for your branch name.
3. Select your branch — you should see your practice file there.

Congratulations — you have completed the full Git workflow: **create branch → edit → commit → push**.

---

## Part 8 — Pulling updates from GitHub

Before starting work each day, always pull the latest changes from GitHub so your local copy is up to date.

1. In VSCode, click the **Source Control** icon.
2. Click the **...** (three dots) menu at the top of the Source Control panel.
3. Select **Pull**.

That's it. VSCode will download any changes made by others.

---

## Part 9 — Using the Cisco U Preview

Once you are working on actual Cisco content files:

1. Open any `.md` file.
2. Press `Ctrl+Shift+P` → type `Cisco U: Preview` → press **Enter**.
3. A panel opens to the right showing your content rendered exactly as it will appear in the Cisco U learning platform.

---

## Quick reference — the daily workflow

| What you want to do | How to do it |
|---|---|
| Start work for the day | Pull latest changes (Source Control → `...` → Pull) |
| Create a new branch | Click branch name bottom-left → `+ Create new branch` |
| Save a snapshot of your work | Stage files (`+`) → add a message → click Commit |
| Share your work with the team | Click Publish Branch / Sync Changes in Source Control |
| Check what branch you are on | Look at bottom-left corner of VSCode |
| Preview your Markdown | `Ctrl+Shift+P` → `Cisco U: Preview` |
| Open the Command Palette | `Ctrl+Shift+P` |

---

## Next steps

Once you are comfortable with the Sandbox, the next step is to clone the Cisco content repositories. Your Skyline team lead will share the repository URLs with you and confirm you have been added as a collaborator.

The workflow is identical — the only difference is that you will be working on real content, so treat the `main` branch with care.

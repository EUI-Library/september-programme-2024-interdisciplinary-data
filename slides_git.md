## Introduction to Git and GitHub for social science research
#### or, track changes to your research in an efficient and effective way


&nbsp;

Simone Sacchi, Open Science Librarian

Library #researchskills session 01/12/2021



---

## Before we start

----

### Let's make a round of introductions

* How many of you are already familiar with Git/GitHub and/or other so called "version control" systems?
* How many of you have already installed Git on your computer?
* How many of you are already using Git/GitHub to track changes in your research?

----

### Cautionary note

* This training is very much at the introductory level and many details are intentionally skipped.
* Most of the examples assume a Unix/Linux (and Mac) command-line environment  but everything can be easily replicated in Windows and/or using a Git GUI
* Git can be fully taken advantage of when working with textual files but all kinds of files can be tracked!

---

## Let me tell you a story...

----

### Once upon a time...

* Wolfman and Dracula were been hired to plan a Mars mission (obviously...)
* Wolfman and Dracula live on different continents
* They work on the same plan at the same time
* How to manage this?
  * take turns on each file?
  * email copies?
* The solution? **Version Control**

----

### Advantage of version control

* Nothing that is *committed* is *ever* lost (unless you try hard…)
* We can record who made which changes, and when
* We can revert to previous versions.
* We can identify and correct conflicts

**Version control is like an unlimited ‘undo’.**

This is basis for code development, how about research?

----

### Do you recognise yourself?

![PhD comic: "Final".doc - files are called: Final.doc, Final_rev.2.doc, FINAL_rev.6.COMMENTS.doc, FINAL_rev.8.commens5.CORRECTIONS.doc, FINAL_rev.18.comment7.corrections9.MORE.30.doc, FINAL_rev.22.comments49.corrections.10.WHYDIDICOMETOGRADSCHOOL.doc](img/phd101212s_small.gif)

PhD Comics [FINAL.doc](https://phdcomics.com/comics/archive.php?comicid=1531)

---

## Version control with `git`

----

### What lies ahead…?

![XKCD comic - A: This is git. It tracks collaborative work on projects through a beautiful distributed graph theory tree mode; B: Cool. How do we use it?; A: No idea. Just memorise these shell commands and type them to sync up. If you get errors, save your work elsewhere, delete the project, and download a fresh copy.](img/git.png)

----

### Learning objectives

* Understand the basics of automated version control
* Understand the basics of `git` and `GitHub`
* Be introduced on how to apply version control to your research

----

### How version control works

Version control is like a 'recording' of history

![Three documents. The first has two paragraphs. The second has a modified paragraph. The third has an additional paragraph](img/play-changes.png)

...Rewind and play changes back again!

----

### Multiple contributors (branching)

* Two people work on a document
  * Each makes independent changes: two versions

![Three documents. On the left is the original, and on the right are two versions of this with different, and conflicting, changes](img/versions.png)

* Changes are separate from the document

----

### Combining changes (merging)

* Several changes can be merged onto the same base document
  * 'Merging'

![Three documents. On the left are the two modified documents from the previous slide. On the right is a single that incorporates both of those changes](img/merge.png)

----

### What version control systems do

* Version control systems manage this process
   * track changes
   * store metadata (who, when)
   * record 'versions' (a.k.a. *commits*)
* The complete history of *commits* and metadata is a *repository*
* CVS, Subversion, RCS: legacy systems
* `git`, Mercurial: modern *distributed* VC tools

---

## Setting up `git`

----

### Learning objectives

* Configure `git` for first use on a computer
* Understand `git config --global`

----
### Install Git

Well, fist of all you need to install Git on your computer!

[Follow these instructions](https://docs.github.com/en/get-started/quickstart/set-up-git)

[...well, attempt now or do it later, but follow the course!]

----

### Setting global options

* `git` needs to know who you are for metadata
* `git` wants your preferences for editing
*  ...and that you want to use these settings globally (i.e. for every project).
```
$ git config --global user.name "Vlad Dracul"
$ git config --global user.email "vlad@tran.sylvan.ia"
```
* Let's config your editor of choice, e.g.:
```
$ git config --global core.editor "vim"
```
* Last, let's set up your default branch as `main`
```
$ git config --global init.defaultBranch main
```
----

### Check global options
* You can check your settings at any time:
```
$ git config --list
```

---

## Creating a repository

----

### Learning objectives

* Create a local `git` repository
* What is in a repository?
  * files
  * commits
  * metadata

----

### Creating a `git` repository

* A fictional project about planets
  * (Wolfman and Dracula…)

**Live Presentation**

```
$ git init
$ git status
```
**Advise: use `git status` all the time!!!!!!**

---

## Tracking changes

----

### Learning objectives

* Practice the modify-add-commit cycle
* Understand where information is stored, in the `git` workflow

----

### My first untracked file

* We'll create a file, but do nothing with it
  * Research question: "Is Mars suitable as a space base?"

**Live Presentation**

```
vim mars.txt
```

----

### My first `git` commit

* We tell `git` that it should *track* a file (watch for changes): `git add`
* We also `git commit` the file (keep a copy of the file in the *repository*, in its current state)

**Live Presentation**

```
git add mars.txt
git commit -m "start notes on Mars as a base"
git log
```

----

### The staging area

* We don't always want to commit all changes
* The *staging area* holds changes we want to commit
  * (other files may also be changed, but we don't want to commit them)

![On the left is a modified document. On the right is a zone representing the data stored in `.git`. In that zone are two containers: a staging area, and a repository. Using `git add` places the document into the staging area. Using `git commit` moves the document from the staging area into the repository](img/git-staging-area.png)

----

### modify-add-commit

* Now we want to add more information to the file
  * Modify file
  * Add file to *staging area* (`git add`)
  * Commit changes

**Live Presentation**

```
vim mars.txt
git diff
git add mars.txt
git diff
git commit
```

----

### IGNORING THINGS

* Not all files are useful
  * Editor backup files
  * Temporary files
  * Intermediate analysis files

**.gitignore**

* `.gitignore` is a special file in your repository root
  * It tells `git` to ignore specified files/directories
  * It should be committed in your repository

----

### Question

-  Which command(s) below would save changes in `myfile.txt` to the local `git` repository?


1. `git commit -m "add recent changes"`
2. `git init myfile.txt; git commit -m "add recent changes"`
3. `git add myfile.txt; git commit -m "add recent changes"`
4. `git commit -m myfile.txt "add recent changes"`


----

### What is likely to happen…

![XKCD comic: a list of commit messages for a repository that start well, but become progressively more like gibberish, titled "As a project drags on, my `git` commit messages get less and less informative"](img/git_commit.png)

---

## Exploring history

----

### Is history bunk?

* How can I identify old versions of files?
* How do I review changes between commits?
* How can I recover old file versions?

----

### Learning objectives

* Understand what the `HEAD` of a repository is
* Compare various versions of tracked files
* Restore old versions of files

----

### Commit history

* Most recent commit: `HEAD`
* Next-most recent: `HEAD~1`
* Next-next-most recent: `HEAD~2`

![Three documents. On the left is the original. In the middle is that document with one line changed. On the right is the middle document with an extra paragraph added. Arrows indicate that the documents are related in order of history.](img/play-changes.png)

----

### History with `git diff`

* We can use `git diff` to see what changed for a file at each commit

**Live Presentation**

```
$ git diff HEAD~1 mars.txt
$ git diff HEAD~2 mars.txt
```

Use  `git log` to check the history of commits:
```
$ git log
```

----


### Restoring older versions

* How can we restore older versions/backtrack?
* Let's say we accidentally overwrite a file…

**Live Presentation**

```
$ git checkout HEAD mars.txt
```

----

### `git checkout`

* `git checkout` "checks out" files from the repo
  * Can use any commit identifier
  * Check out the commit *before* the edit you want to replace!

![On the left is a zone representing the `.git` directory, with three commits in a repository. One commit (HEAD~1, f22b25e) contains changes we want to recover. On the right are two files that are rcovered. An arrow indicates two commands for recovery: `git checkout HEAD~1` and `git checkout f22b25e`](img/git-checkout.png)

----

### Question

- Which command(s) below will let Dracula recover the last committed version of `mars.txt` (but no other files)?


1. `$ git checkout HEAD`
2. `$ git checkout HEAD mars.txt`
3. `$ git checkout HEAD~1 mars.txt`

---

## Remotes in GitHub

----

### Learning objectives

* What remote repositories are and why they are useful
* To clone a remote repository
* To push to and pull from a remote repository

----

### Remote repositories

* Version control most useful for collaboration
  * Easiest to have a single repository
  * Repository may be hosted off-site (for at least one collaborator)
* Services available:
  * GitHub, BitBucket, GitLab
* We're using GitHub

----

### GitHub Saved My Life!

![GitHub Saved My Life Tonight](img/github_saved_my_life.png)

----

### Log in to GitHub

* Register for an account, if you don't have one - then log in

[https://github.com/](https://github.com/)

----

### Create a remote repository

![Screenshot of GitHub top bar](img/github-repo-new.png)

* Essentially, on GitHub's servers:

```
mkdir planets
cd planets
git init
```
**Live Presentation**

----

### A freshly-made GitHub repository

* There's nothing in the remote repository!

![Two repositories. At the top, the local `planets` repository (belonging to Vlad), which contains files in the staging area and repository. At the bottom, an empty epository, representing the 'clean' repository just created on `GitHub`](img/git-freshly-made-github-repo.png)

----

### Connecting local and remote repositories

* We tell the *local* repository that the GitHub repository is its *remote* repository.
  * `origin` is a local nickname for the remote repo (a common choice)
  * Once set up, we *push* changes/history to the remote repo

**Live Presentation**

```
git remote -v
git remote add origin git@github.com:simosacchi/planets.git
git push origin main
git remote -v
```

----

### SSH Key authentication on Github
WARNING: Since 13 August 2021 Github requires an SSH Key to push to a remote.

Details on how to setup a key on your machine are available here: https://librarycarpentry.org/lc-git/03-sharing/index.html#ssh-background-and-setup

----

### Remote GitHub repo after first *push*

* We only *push* the repository, not the staging area

![Two repositories. At the top, the local `planets` repository (belonging to Vlad), which contains files in the staging area and repository. At the bottom, the remote `GitHub` repository, which contains the same repostitory as the local repo - but *not* the staging area](img/github-repo-after-first-push.png)

----

### Sync local repo with remote

* To synchronise the local repo with the remote repo, you *pull*

```
git pull origin main
```

---

## Notes on collaboration

----

### Collaborating with...

* Your first and foremost collaborator is your future self
* ...or yourself on a different machine!
* The same perspective applies when you work with others

----

### Github as the hub for collaboration

* Keep changes in sync across (different) contributors working on different computers with local repositories
* Manage conflicts across versions

----

### Why conflicts occur

* People working in parallel
  * different changes to same part of a file
  * not keeping local repo in sync before making local changes
  * not keeping remote repo in sync after making local changes
* `git pull` before working; `git push` when done

----

### Seriously, `git push` when done…

![A sign: In case of fire 1. git commit, 2. git push, 3. leave building](img/git_fire_notice.jpg)

----

### The conflict message

```
To https://github.com/<collaborator>/planets.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/<collaborator>/planets.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

----

### The conflicting changes

![Three text files. At the top is the original, below this are two versions with conflicting changes. Arrows point to a question mark: how will we resolve this?](img/conflict.png)

----

### Resolving a conflict

* `git` detects overlapping changes
  * `git` defers to humans for how to resolve: **communicate**!

* To resolve:
  * *pull* remote changes
  * *merge* changes into our working copy
  * *push* the merged changes

---

## Wrapping up and Open Science


----

### A traditional story
> * A scientist **collects some data** and stores it on a machine that is occasionally backed up by her department. She then **writes or modifies a few small programs** (which also reside on her machine) to analyze that data. Once she has some results, **she writes them up and submits her paper**. She might include her data – a growing number of journals require this – but she probably doesn’t include her code.
>
> Time passes…
>
> * The journal sends her reviews written anonymously by a handful of other people in her field. **She revises her paper to satisfy them, during which time she might also modify the scripts she wrote earlier, and resubmits**.
>
> More time passes….
>
> * **The paper is eventually published**. It might include a link to an online copy of her data, but the paper itself will be behind a paywall: only people who have personal or institutional access will be able to read it.

----

### A revised approach

> * The data that the researcher collects is stored in an **open access repository** (e.g. [Zenodo](https://zenodo.org/) or [FigShare](https://figshare.com/)), possibly as soon as it’s collected, and given its own **Digital Object Identifier (DOI)**.
> * The researcher creates a new **repository on GitHub** to hold her work.
> * As she does her analysis, she **pushes changes** to her scripts (and possibly some output files) to that repository.
> * She also uses the repository for her paper. That repository is then the **hub for collaboration** with her colleagues.
> * When she’s happy with the state of her paper, **she posts a version to arXiv or some other preprint server** to invite feedback from peers.
> * Based on that feedback, she may post several revisions before finally submitting her paper to a journal.
> * **The published paper includes links to her preprint and to her code and data repositories**, which makes it much easier for other scientists to use her work as starting point for their own research.

----

### Takeaways

* GitHub/version control can be an open electronic lab book as part of Open Science workflows
  * Collect data - store in OA repository
  * Use GitHub to store work in progress: analysis lab book
  * Post preprint to preprint server
* Even if you don't work openly, it's more reproducible (and auditable)
----

### You're at least ready to leave this behind! ;-)

![PhD comic: A directory listing with filenames like data_2010.05.28_test.dat, data_2010.05.28_re-test.dat, data_2010.05.28_re-re-test.dat, data_2010.05.28_calibrate.dat, data_2010.05.29_aaarrrgh.dat, data_2010.05.29_WTF.dat, data_2010.05.29_USETHISONE.dat](img/phd052810s.png)

---

## Questions?

---

## Acknowledgement

These slides are based on:
* Leighton Pritchard [SWC Lessons](https://github.com/widdowquinn/Teaching-SWC-Lessons)
* Library Carpentry: [Introduction to Git](https://librarycarpentry.org/lc-git/)
* Software Carpentry: [Version Control with Git](https://swcarpentry.github.io/git-novice/)

----

These slides are released under a Creative Commons Attribution International 4.0 licence

* Web version:
* GitHub repo:

---

## Extra stuff

----

Dracula also has to set his favorite text editor, following this table:

| Editor             | Configuration command                            |
|:-------------------|:-------------------------------------------------|
| Atom | `$ git config --global core.editor "atom --wait"`|
| nano | `$ git config --global core.editor "nano -w"`    |
| Sublime Text (Mac) | `$ git config --global core.editor "/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl -n -w"` |
| Sublime Text (Win, 64-bit install) | `$ git config --global core.editor "'c:/program files/sublime text 3/sublime_text.exe' -w"` |
| Notepad (Win)    | `$ git config --global core.editor "c:/Windows/System32/notepad.exe"`|
| Notepad++ (Win, 64-bit install)    | `$ git config --global core.editor "'c:/program files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Emacs              | `$ git config --global core.editor "emacs"`   |
| Vim                | `$ git config --global core.editor "vim"`   |

You can reconfigure the editor for Git at any time.

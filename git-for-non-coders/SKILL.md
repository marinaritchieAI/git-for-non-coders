---
name: git-for-non-coders
description: Handle all Git and GitHub operations on behalf of a non-technical user, so they never have to run commands themselves. Use this skill whenever a project involves Git or GitHub in any way, including committing, branching, merging, pushing, pulling, opening pull requests, undoing changes, or setting up a repository. Use it even when the user does not mention Git by name, for example when they say "save my work", "back this up", "let us try something risky", "publish this", or "put it back how it was". Also use it when the user is editing files in a project that has a .git folder, since their changes will need saving and backing up. This skill protects the user from overwriting existing work and from unreviewed changes reaching a live system.
---

# Git for non-coders

The person you are helping does not write code and should never have to type a Git command. Run every Git operation on their behalf and explain what happened in plain English.

Your goal is not just to execute commands correctly. It is to keep their work safe, keep them oriented, and build their confidence over time.

## The first thing to do in any session

Before touching any files in a project, establish whether the project already exists on GitHub. This is the single most important check, because you cannot see the user's remote history unless you look, and the most damaging mistake is overwriting or duplicating work that already exists.

Run these checks:

```bash
git status
git remote -v
git log --oneline -5
```

Then act on what you find:

- **A remote exists and there are commits you do not have.** Pull before doing anything else. Tell the user what came down.
- **A remote exists and you are up to date.** Say so, briefly, and continue.
- **No `.git` folder at all.** The project is not under version control. Offer to set it up rather than assuming.
- **Uncommitted changes are already present.** Stop and ask about them before switching branches or pulling. They may be work the user forgot about.

Do not skip this because the user seems in a hurry. Thirty seconds of checking prevents the mistake that costs an afternoon.

## Two modes, and only one of them needs a branch

Ask yourself which of these the user is doing. The answer determines whether Git is involved.

**Work.** Using the project to produce something: a draft, a report, an export, an analysis. Nothing about the project itself changes. There is nothing to commit and nothing to merge. Do not create a branch. Do not open a pull request.

**Build.** Changing how the project itself works: its code, its configuration, its instructions, its scripts. These changes persist and affect future behaviour. This is where branches, commits and pull requests belong.

The test: if you have to edit the project's own files, it is Build. If you only produce an output for the user or their customer, it is Work.

Getting this wrong in either direction is costly. Opening a pull request for a Work task creates noise and confusion. Editing project files without a branch during a Build task risks the trusted version.

## How to do a Build task

1. **Check the branch first.** If the user is sitting on `main`, create a branch before editing anything. Never edit project files directly on `main` unless the user explicitly instructs it and understands why.
2. **Name the branch after the task**, not the person's mood. `fix-photo-sizing` beats `updates2`.
3. **Commit in meaningful units** with messages that describe the change, not the file. "Add discount rules to pricing logic" beats "update file".
4. **Open a pull request written in plain English.** See `references/pull-requests.md` for the standard. This is not optional. A review the user cannot read is not a review.
5. **Tell them what to do next.** Which button, on which page, and what will happen after they press it.

## Establish what merging actually does, once per project

Before the first merge, find out what happens when `main` updates. Look for deployment configuration, CI workflows, or a sync process. Then tell the user in one sentence.

The stakes should set the ceremony:

- **Merging publishes to customers or users.** Treat approval seriously. Recommend a second person reads the summary. Be explicit that merging is the deploy action.
- **Merging only updates the user's own machine or a backup.** Say so. A bad merge is an inconvenience. Encourage them to move faster rather than agonise.
- **You cannot tell.** Say you cannot tell, and suggest they find out before the first merge rather than after.

Never let a user press merge without knowing which of these is true.

## Plain English, always

Use the real terms once, then explain them. Do not lecture and do not repeat the lesson every session.

Good: "I have saved this as a commit, which is a snapshot you can return to. It is on your computer but not yet backed up on GitHub."

Bad: "Committed to HEAD on refs/heads/main, ahead of origin/main by 1."

Never show raw command output as the answer. Interpret it. If `git status` reports three modified files and two untracked, say what those files are and what it means.

## When something goes wrong

The user will break something. Your first job is to remove the fear, because a frightened user stops experimenting.

Lead with reassurance and be specific about it: their history holds every saved version, and you can return to any of them.

Then choose the gentlest fix that works:

- **Uncommitted changes they regret.** Restore the file to its last commit.
- **A committed change that turned out wrong.** Use `git revert` to create a new commit that undoes it, rather than rewriting history. This keeps the record honest and is safe on a shared branch.
- **A merge that should not have happened.** Revert the merge commit. Explain that the code is back as it was, and the history shows both the mistake and the correction.

Prefer `revert` over `reset` on anything that has been pushed. Never use force push on a shared branch. If a situation genuinely seems to need it, stop and explain the risk to the user first.

## Never do these without asking

- Force push to any branch.
- Rewrite history that has already been pushed, including rebasing shared branches.
- Delete a branch that has not been merged.
- Merge a pull request on the user's behalf. Merging is their decision, and their moment of review. Prepare it, explain it, and let them press the button.
- Add or commit a file that looks like a secret. If you see an API key, token, password, or `.env` file about to be committed, stop and tell the user. Add it to `.gitignore` instead. If a secret has already been committed and pushed, tell them plainly that it must be rotated, because history keeps everything and scrubbing it afterwards is not a fix.

## Park improvements rather than acting on them

Users notice things mid-task: "the script should really do that automatically." Do not change the project's behaviour in the middle of an unrelated task. Acknowledge the idea, offer to note it down, and continue what you were doing.

One piece of feedback is a reaction. The same observation twice is a rule. Let patterns show before you encode them.

## Building their confidence

Every time you complete a Git operation, the user should end up knowing three things: what just happened, where their work now lives, and what would happen if they wanted to undo it.

Say it in one or two sentences. Do not narrate every command. Over a few sessions, this is what turns a nervous user into a confident one, which is the actual point of the skill.

# Git for non-coders

A Claude skill that handles every Git and GitHub operation on your behalf, so you never have to type a command.

Built for people who make things but do not write code. Consultants, founders, operators, writers. If you have started using Claude Code and hit GitHub as a wall, this is for you.

## What it does

Install it, and Claude changes how it behaves around Git:

- **Checks before it changes.** Claude looks at what already exists on GitHub before touching a single file, and pulls the latest first. This is the habit that stops your existing work being overwritten.
- **Knows when Git is not needed.** Producing a draft does not need a branch. Changing how the project works does. Claude tells the difference and does not clutter your repository with unnecessary pull requests.
- **Writes pull requests you can actually read.** Plain English. What changed, what will be different after merging, and what to check. Never a wall of code.
- **Tells you what merging will do.** Before your first merge, Claude works out whether it publishes to customers or only updates your own machine, and says so. The stakes should set the ceremony.
- **Never presses merge for you.** Preparing the change is Claude's job. Approving it is yours.
- **Stops if a secret is about to be committed.** And tells you plainly that an exposed key must be rotated, not merely deleted.
- **Removes the fear.** When something breaks, Claude leads with the fact that every version is saved, then fixes it with the gentlest option available.

## Install

**In Claude, on the web or desktop**

1. Download `git-for-non-coders.skill` from this repository.
2. Open Claude and go to Settings, then Capabilities, then Skills.
3. Upload the file.

**In Claude Code**

Copy the `git-for-non-coders` folder into your skills directory:

```
~/.claude/skills/git-for-non-coders/
```

## How to use it

You do not invoke it. It triggers on its own whenever a project involves Git, including when you do not say the word. Phrases like "save my work", "back this up", or "let us try something risky" are enough.

If you want to be explicit, start a session with the state of things:

```
This project is already on GitHub at [link]. Pull the latest before we change anything.
```

That single sentence is the most useful habit in this whole repository.

## What is inside

```
git-for-non-coders/
├── SKILL.md                      the instructions Claude follows
└── references/
    └── pull-requests.md          how to write a pull request a non-coder can review
```

`SKILL.md` is short on purpose. `references/pull-requests.md` loads only when Claude is writing a pull request, which keeps the main instructions focused enough to be followed reliably.

## Learn the concepts first

The skill changes how Claude behaves. It does not teach you what a branch is.

If GitHub still feels murky, work through the interactive guide before installing anything. Fifteen minutes there will save you hours later.

[Add the link to your interactive guide here]

## Contributing

Suggestions and corrections are welcome. Open an issue describing what Claude did, what you expected, and what would have been better.

## Licence

MIT. Use it, change it, share it.

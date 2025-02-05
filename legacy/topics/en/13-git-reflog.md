# Git Reflog
`git reflog` is a Git command that records updates to the tip of branches and other references. It allows you to track changes (like commits, branch changes, resets, checkouts, rebases, and merges) that may not appear in the regular commit history.

### Why Use `git reflog`?
`git reflog` is particularly useful when you want to:
- **Recover lost commits:** If you've lost a commit due to a reset, checkout, or rebase, you can often retrieve it through the reflog.
- **Undo mistakes:** By listing all references, you can revert to a previous state, even if that commit isn’t in your current history.
- **View the history of branch movements:** It keeps track of all branch heads, regardless of whether changes were pushed.

**Usage:**
```bash
git reflog
```

Running this command shows a list of recent updates to the repository’s `HEAD` (most recent commits), with each change listed with an index number and a description.

**Example:**
```bash
9779a62 (HEAD -> main, origin/main, origin/HEAD) HEAD@{0}: commit: New topics added: 11: Git Restore and Git Switch and 12: Git Amend
713bf98 HEAD@{1}: commit: feat: tips of how to add correct branch and commits names added
2844264 HEAD@{2}: commit: Iniciação de um novo capítulo, GitHub Authentications
e54b0ab HEAD@{3}: commit: Iniciação de um novo capítulo, GitHub Authentications
420278c HEAD@{4}: clone: from https://github.com/lorenzouriel/ebook-git-github.git
```

**Each line indicates:**
- **Commit hash:** The unique identifier for the commit.
- **Reference:** An index like `HEAD@{0}` (0 being the most recent change).
- **Action:** What was done, such as commit, reset, or checkout.
- **Message:** Additional info about the commit.

**Recovering Lost Commits:**
To go back to a previous commit, use:
```bash
git cherry-pick <commit-hash>
```
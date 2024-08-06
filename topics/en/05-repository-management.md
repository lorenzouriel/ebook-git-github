# Repository Management
## Removing Local Repositories
**1. Removing a repository locally:**
- To delete a Git repository locally, you can simply delete the directory where it is located. For example:
```shell
# bash
rm -rf /path/to/your/repository
git commit -m "Remove tests_git directory"
git push

# power shell
git rm -r --cached /projects/portfolio/tests_git
Remove-Item -Path "C:\Projects\portfolio\tests_git" -Recurse -Force
git commit -m "Remove tests_git directory"
git push
```

- Use this command with caution, as it will permanently delete all files and commit history in the repository.

## Deleting Remote Repositories on GitHub
Go to the repository page on your hosting service.

In the repository settings, look for the option to delete the repository.
- ![delete_repository](/topics/imgs/05/delete_repository.jpg)

- ![delete_repository_2](/topics/imgs/05/delete_repository_2.jpg)

Confirm the deletion with the password or by accessing GitHub Mobile.

## History Cleanup (`Rebase`, `Squash`)
**1. Rebase:**

Rebase is used to rewrite the commit history.

Git Rebase moves one branch on top of another, rewriting the history in the process. Instead of performing a merge, it rewrites the history.

For example, to rebase your `dev` branch onto the `main` branch:
```shell
git checkout dev
git rebase main
```

The idea of ​​rebasing is to create a more linear commit history, making future code reviews easier.

**2. Interactive Rebase:**

To merge or reorder commits, use interactive rebase:
```shell
git rebase -i HEAD~n
```

- Where `n` is the number of commits you want to review. You will see a list of commits that you can edit, merge (squash), or reorder.

When you run rebase, your terminal will return like this: 
```shell 
pick f7f3f6d Meu commit 01
edit 310154e Meu commit 02
squash a5f4a0d Meu commit 03
drop a5f4a0d Meu commit 04

# Rebase 9b9bd4c..9b9bd4c onto 9b9bd4c (1 command)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
~ 
```

Each command specifies exactly what you can do with the commits.

Your commits will appear above the commands, just select the line of the desired commit and click just the initial letter of each command. The command will automatically add it to the beginning of the commit.

#### What does the full script do?
- Apply commit `f7f3f6d` as is.
- Apply commit `310154e` and stop to allow editing.
- Combines commit `a5f4a0d` with the previous commit `310154e`.
- Removes commit `a5f4a0d` from the history.

**This results in:**
- The first commit (`f7f3f6d`) being applied normally.
- The second commit (`310154e`) being applied and edited as needed.
- The third commit (`a5f4a0d`) being combined (`squashed`) with the second commit.
- The fourth commit (`a5f4a0d`) being removed from the history.

**Additional Notes**
- The `squash` command will prompt you to edit the resulting commit message.
- `squash` combines multiple commits into a single commit.
- The `edit` command will stop the rebase to allow modifications to the commit.
- The `drop` command completely removes the commit from the history.

## Tags and Releases
**1. Create a Tag:**
- Tags are used to mark specific points in the commit history, often used to mark release versions.
```shell
git tag <tag-name>
```

**2. Create an Annotated Tag:**
Annotated tags are recommended for releases because they contain additional information.
```shell
git tag -a <tag-name> -m "Tag Message"
```

**3. Push a Tag to the Remote Repository:**
Whenever you create a new tag you need to push it to the remote repository.
```shell
git push origin <tag-name>
```

**4. Push All Local Tags to the Remote Repository:**
```shell
git push --tags
```

**5. List All Tags:**
```shell
git tag
```

**6. Delete a Tag Locally:**
```shell
git tag -d <tag-name>
```

**7. Delete a Tag in the Remote Repository:**
```shell
git push origin --delete <tag-name>
```

**8. Create a Release on GitHub:**
- On GitHub, go to the repository page.
- Go to the "Code" > "Create a New Release" section. 
    - ![release](/topics/imgs/05/release.jpg)

- Fill in the information, add the tag and click "Publish a New Release":
    - ![release_2](/topics/imgs/05/release_2.jpg)

- Your releases are organized in the "Code" section
    - ![release_3](/topics/imgs/05/release_3.jpg)
---
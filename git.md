# Git
Git version control system cheatsheet.


## Basics
NOTE: `REV` is any tree-ish object (sha1, branch...)
``` shell
git init                      # Initialize a new repository (create .git)
git clone REPO                # Clone remote REPO
git branch [BRANCH]
git checkout -b [BRANCH]      # Create new BRANCH and switch to it
git checkout [BRANCH]         # Switch to existing BRANCH
git merge [BRANCH]            # Merge BRANCH history into current branch
git add FILE...               # Add FILE... to version control
git commit [FILE...]          # Commit [FILE...] changes (locally)
git reset [FILE...]           # Unstage [FILE...] from commit changeset
git reset [REV] [FILE...]     # Reset [FILE...] to state in REV
git reset --hard              # Reset and override all local changes
git diff [FILE...]            # Show diff [in FILE...] between current and HEAD
git diff --staged [FILE...]   # Show diff of what is staged but not commited
git diff REV..REV [FILE...]   # Show diff between two REVs [in FILE...]
git diff main..REV [FILE...]  # Show diff between main and my REV [in FILE...]
git log                       # Show all commits in current branch history
git log REV2..REV1            # Show all commits on REV1 that are not on REV2
git log --follow FILE         # Show all commits that changed FILE
git log --all --grep=FOO      # Show all commits that match FOO
git remote add REMOTE URL     # Add URL as REMOTE (e.g. origin)
git push [-u REMOTE] BRANCH   # Push local changes on BRANCH to REMOTE
git push -f [...]             # Force push and overwrite remote history
git pull                      # Pull remote changes to local repository
```


## Revisions
- `<sha1>`          Full sha-1 (40-byte hex string)
- `<describe>`      Output of `git describe`
- `<ref>`           Symbolic ref name (branch, tag name)
- `HEAD`            Alias for last commit of current branch (it's `<ref>`)
- `@`               Alias for `HEAD` (must be alone)
- `<ref>@{N}`       N-th prior value of `<ref>`
- `@{N}`            N-th prior value of current branch
- `[BRANCH]@{u}`    Alias to upstream branch of current [or BRANCH] branch
- `REV^[N]`         First or [Nth] parent of REV (`HEAD^0` is HEAD itself)
- `REV^@`           All parents of REV
- `REV^!`           REV and all its parents EXCLUDED
- `REV~[N]`         First or [Nth] generation of REV ancestor (`~3` is `^^^`)


## `.gitignore`
``` text
/foo                          # Ignore foo in repository root only
!foo                          # Don't ignore foo
foo*                          # Ignore anything matching wildcard pattern
```

## Syncing Fork
``` shell
git add remote upstream ...   # Add upstream remote if not done yet
git fetch upstream            # Fetch remote branches and commits
git checkout master           # Switch to fork master
git merge upstream/master     # Merge upstream master to fork master
git push                      # Push fork back to origin
```

## Stashing Changes
Temporarily and local-only way to store uncommited changes.
``` shell
git stash                     # Store any uncommited changes to stash
git stash list                # List all stashed
git stash apply [stash@{N}]   # Apply topmost [or Nth] stashed change
git stash drop [stash@{N}]    # Discard topmost [or Nth] stashed change
git stash pop [stash@{N}]     # Apply and drop topmost [or Nth] stashed change
```

## Cherry-Picking
Take commit from one branch and apply to another.
``` shell
git cherry-pick REV           # Take commit REV and apply to current branch
git cherry-pick --no-commit REV # Don't commit change on current branch
```

## Rewriting History
History changes should be done carefully. Rewriting pushed history will affect
any clones of repository.
``` shell
git commit --amend [FILE...]  # Amend previous commit with current changes
git rebase [BRANCH]           # Apply current branch commits ahead of BRANCH
git rebase -i REV             # Interactive rebase (all commits from REV)
git rebase -i HEAD~N --exec CMD # Exec CMD on last N commits (e.g. unit tests)
```

Squash N commits in one
``` shell
git rebase -i HEAD~N          # Leave first (p) and mark rest by (s), update 
                              # commit message.
```

Remove PATH(s) from history (PATHs-TO-REMOVE.txt is list of paths one per line)
See: https://github.com/newren/git-filter-repo
``` shell
git filter-repo --analyze
git filter-repo --invert-paths --paths-from-file /tmp/PATHs-TO-REMOVE.txt
```

Synchronizing existing checkout with rewritten history upstream (per BRANCH)
``` shell
git checkout BRANCH
git reset --hard origin/BRANCH
```

#### Optimize Repository
``` shell
git fetch -p                  # Remove branches that no longer exist on remote
git gc [--aggresive]          # Collect garbage (--aggressive runs repack)
```

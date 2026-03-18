The ultimate version control utility

## Practice Resources
https://learngitbranching.js.org/


## Basics
commit -> snapshot of the codebase
branch -> A pointer to a commit

`git switch` is now preferred to `git checkout` for switching branches as it is specific to switching branches

HEAD is your current location within the Git repository's history, representing the commit you are currently working on or viewing

### Relative Refs
You can use `^` to checkout the parent of branches rather than commit hashes

`git checkout HEAD^` or `git checkout HEAD^^`

Reassign branch to commit
`git branch -f main HEAD~3`

## Commands
https://education.github.com/git-cheat-sheet-education.pdf
- `git fetch` :  Grabs the local remote branch
- `git pull`: Updates the local remote branch and merges into working directory
- `git switch <remote branch>`: Checkout remote branch and create local version
- `git push origin --delete feature/login`: Delete remote branch
- `git push -u origin <branch>` : Push branch to remote
- `git config --list`
- `git config --global user.name "John Doe"
- `git config --global user.email johndoe@example.com`

### BRANCH & MERGE 
*Isolating work in branches, changing context, and integrating changes* 

`git branch {-r}` 
`-r`  To show remote branches
list your branches. a * will appear next to the currently active branch 

`git branch [branch-name]` 
create a new branch at the current commit 

`git checkout` 
switch to another branch and check it out into your working directory 

`git merge [branch]`
merge the specified branch’s history into the current one 

`git log` 
show all commits in the current branch’s history

## Git Flow
A way of managing features and pushing code.
-  [https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- [https://nvie.com/posts/a-successful-git-branching-model/](https://nvie.com/posts/a-successful-git-branching-model/)


## Auxiliary Information 
#### Tracking File Permissions
Git solely tracks executable or non-executable file permissions. This can also be disabled. See this [thread](https://superuser.com/questions/1422630/how-git-works-when-the-file-permission-mode-is-changed). 

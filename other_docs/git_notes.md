# Git Notes
2025-29-01 S. Humphreys

## References
* [Git Docs, detailed command reference](https://git-scm.com/docs)
* [Git Cheat Sheet, at GitHub](https://education.github.com/git-cheat-sheet-education.pdf)
* [Git Book v2](https://git-scm.com/book/en/v2/)
* [StackOverflow, when-should-i-use-git-pull-rebase](https://stackoverflow.com/questions/2472254/when-should-i-use-git-pull-rebase)
* [StackOverflow, whats-the-difference-between-git-switch-and-git-checkout-branch](https://stackoverflow.com/questions/57265785/whats-the-difference-between-git-switch-and-git-checkout-branch)
* [InfoQ article on swtich and restore](https://www.infoq.com/news/2019/08/git-2-23-switch-restore/)

## Overview
### Repositories
Git is a distributed version control system, in which all workspaces are repositories. 
* **local**
	* The local repository.
* **origin**
	* The local repo is cloned from the *origin* repo.
	* The local *master branch* tracks the remote master branch.

### File states
*from git-scm book, 1.3*
* *Modified*  means that you have changed the file but have not committed it to your database yet.
* *Merging* means some updates are in conflict and are not yet fully merged.
* *Staged* means that you have marked a modified file in its current version to go into your next commit snapshot.
* *Committed* means that the data is safely stored in your local database.

### Branches and Commits
*from git-scm book, 3.1*  
* A commit creates a commit object that holds the author and size data and pointers to the committed files (a tree) and the parent commit, forming a tree.  
* A branch is a movable pointer to a commit.  
* The default branch is ```master```, which moves forward with each new commit.
* Concept: Your work area is on a given branch and effectively points to a specific current commit. The current commit is pointed to by the *HEAD* pointer.

## Git config options
* Config options are in 
  * Local repo, .git/config.
  * user: ~/.gitconfig or ~/.config/git/gitconfig, and /etc/gitconfig.
  * Use ```git config --list``` to see current configuration settings.
  * Add the ```--system``` flag to see or affect the common system gitconfig file.
* **remote.origin** defines the origin repository
* **pull.rebase** : sets the default behavior of *git pull*.
	* ```pull.rebase=false``` : "fast forward" if possible, otherwise merge 

## Common commands
Commands are of the form *git &lt;command&gt; &lt;options&gt;*.  
### Configuration 
* *git config* : set configuration options. See "git config options" above.
* command aliases
	* *git config --global alias.&lt;alias&gt; &lt;command&gt;*, e.g.
	* ```git config --global alias.co checkout```  

### File staging and commits
* *git add &lt;file&gt;* : stage files, i.e. add files to the list of *staged* files for the next commit
* *git commit* : commit the staged files to the repo, creates a commit object (see 
    * ```git commit -m 'a commit message'```
    * -m 'commit message'
    * -a  automatically stage existing managed files that have been modified or deleted
    * --amend Useful for updating a commit, but best before pushing out.
* *git merge &lt;branch&gt;* : Merge changes from specified branch into the current branch.
   * First switch to the branch to merge *into*. Then run ```git merge <branch>```.
   * Git runs a three-way merge between the two commits and the common ancestor, then creates a new *merge commit* with two parents.
   * If there are conflicts, resolve and end the merge process with a commit.
   * Check the status of merges with ```git status```.
* *git pull* : bring in changes from origin repo.
  * *--rebase* : recompute local changes based on most recent version in the origin repo.
* *git push* : Push local branch commits to the origin repo.
   * ```git push <alias> <branch>```
* *git rebase* :  recompute local changes based on most recent version in the origin repo
   * This performs a three-way diff, as with a merge, but does not merge.
   * This *abandons* the branch commits that are rebased(!). Do this only for local work! 
     * "You can get the best of both worlds: rebase local changes before pushing to clean up your work, but never rebase anything that you’ve pushed somewhere."
   * Following by a merge will keep a linear commit tree, rather than the extra node(s) of the merged branch.  
   * See the Git Book on [Git-Branching-Rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing).
* *git stash* : Save modified and staged changes, to allow switching branches prior to committing.
* *git tag* : TBD
* *git diff* : diff of unstaged modifications
   * --staged option to compare staged (but not commited) changes

### Branch related
* *git branch* : create a *new branch*.  Note this does **not** switch to the branch.  
  *  ```git branch <branch>``` creates a new pointer to the current commit.
  *  -d, --delete option will delete a branch (pointer). Note: throws error if the branch has unmerged work.
  *  (no options) lists current branches, options:  --merged and --no-merged.
* *git switch &lt;branch&gt;* : change working branch, moves the HEAD pointer.
  * -c, --create option will create a new branch and switch to it.
* *git restore --source &lt;source tree&gt; [--staged] [--worktree] &lt;pathspec&gt;*
  * restore files from a different branch or the source
* *git checkout* : Older command that does what switch and restore do, and more
  * ```git checkout <branch>``` is the same as ```git switch <branch>```. 
  * Note that the -b option is similar to switch -c:  create and switch to a new branch.
* * *git rebase* : Apply any commits of current branch ahead of (after) specified branch.
* *git fetch* : retrieve all branches from the origin or specified repo
* *git log* : show where the branch pointers are pointing
  * ```git log --oneline --decorate```, or ```git log --all``` to see all history, not just 'below' the present commit.
* *git reset* : unstage a file
* *git status* : Show modified files staged for commit.

### Repo related
* *git clone &lt;path&gt;* : create a local repo from the specified repo at *path*.   
  * Local clones are to files on a shared file system, e.g. with file paths or file://.
  * HTTP and SSH are available, as well.  SSH is simpler to set up, but not as flexible.
* See the Git Book for work flows with a team using a distributed repo.
   *  [Git Book 5.1 Distributed Workflows](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows)

## Typical flow
TBD

## TBD
* difference b/w pull and fetch
* difference b/w checkout and switch/restore

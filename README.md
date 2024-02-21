# learn-git-branching
## Day 1: Git Branching Basics
### Objective
Gain practical experience with Git branching concepts by completing interactive exercises on the Learn Git Branching platform. This assignment aims to reinforce your understanding of branching, merging, and manipulating branches in Git.  
![image](https://github.com/Laqwanda-Nettles/learn-git-branching/assets/147118788/87f2475d-98df-4b60-9747-e9fa82d272d2)  
#### Introduction Sequence
##### Git Commit
```
git commit
```
Git commits are snapshots of all tracked files in a directory, serving as a record of changes made. While resembling a copy-paste action, Git optimizes commits by compressing them into sets of changes or "deltas" between versions. Additionally, Git tracks commit history to establish relationships between commits, showcasing their chronological order and ancestry.
##### Git Branch
Branches are simply pointers to a specific commit. They essentially say 'I want to include the work of this commit and all parent commits'. There are three ways to create a branch.  
```
git branch <name>
git checkout <name> ; git commit
```
Git checkout will place you on the new branch before commiting the change. The following is a shortcut that creates a new branch and check out.
```
git checkout -b <branch name>
```
In version 2.23, a new command, git switch is set to replace git checkout. The following is the short cut syntax to create a new branch and select it.
```
git switch -c <branch name>
```
##### Git Merge
```
git merge
```
To combine work from different branches in Git, we can use a method called git merge. This process creates a special commit with two distinct parents, effectively incorporating the changes from both branches. In essence, a merge commit signifies the inclusion of work from multiple parents, facilitating the integration of different branches.
##### Git Rebase
```
git rebase
```
Another method to combine work between branches in Git is through rebasing. Rebasing involves taking a series of commits, essentially copying them, and relocating them elsewhere. Despite its complexity, rebasing offers the advantage of creating a cleaner and more linear sequence of commits.
#### Ramping Up
##### Detaching Head
HEAD serves as a symbolic name for the presently checked out commit in Git, indicating the commit you're currently working on. It typically points to the latest commit in the working tree, and most commands that modify the working tree begin by altering HEAD. Normally, HEAD references a branch name, such as "bugFix," and when you commit changes, the status of that branch is updated accordingly, which is reflected through HEAD. Detaching HEAD just means attaching it to a commit instead of a branch.
```
Before: HEAD ➡️ main ➡️ c1
git checkout c1
After: HEAD ➡️ c1
```
##### Relative Refs
Navigating through Git using commit hashes can become tedious, especially without a visual representation of the commit tree. In real-world scenarios, relying on git log becomes necessary to view commit hashes. Additionally, commit hashes in Git are often long. However, Git is intelligent in handling hashes, requiring only enough characters to uniquely identify a commit. This means you can use a shortened version of the hash, such as typing "fed2" instead of the full string, to reference commits.  
Specifying commits by their hash isn't the most convenient way or effective, which is why Git has relative refs. Relative refs allow you to begin from a memorable point, such as a branch like "bugFix" or the HEAD reference, and navigate from there.
###### Relative commits:
- Moving upwards one commit at a time ```^```
- Moving upwards a number of times ```~<num>```
###### Caret (^) Operator
The caret ```^``` operator in Git indicates finding the parent of a specified commit. For instance, appending it to a ref name like ```main^``` signifies the first parent of the "main" branch. Similarly, ```main^^``` refers to the grandparent or second-generation ancestor of the "main" branch. This operator simplifies navigation within the commit history by specifying relationships between commits.
###### Tilde (~) Operator
In Git, the tilde ```~``` operator offers a convenient way to move multiple levels up in the commit tree without typing ```^``` repeatedly. The tilde operator can be followed by a number, indicating the number of parent commits you want to ascend.
###### Branch Forcing
In Git, branch forcing is a technique commonly used with relative refs to adjust branch positions efficiently. By employing the ```-f``` option, you can directly reassign a branch to a specific commit. For example, the command ```git branch -f main HEAD~3``` forcefully moves the "main" branch three commits behind the HEAD. However, it's worth noting that in a real Git environment, the ```git branch -f command``` is restricted for the current branch to prevent accidental data loss or unexpected changes.
##### Reversing Changes
In Git, reversing changes involves both low-level actions, such as staging individual files, and high-level actions, which determine how changes are actually reversed. There are two main methods for undoing changes in Git: using ```git reset``` and ```git revert```. 
###### Git Reset
```git reset HEAD~1```
Git reset is a command used to reverse changes by moving a branch reference backward in time to an older commit. It essentially "rewrites history" by resetting the branch as if the commit had never occurred. This action allows you to undo changes and manipulate the commit history effectively.
###### Git Revert
```git revert HEAD```
Git revert is a command used to reverse changes in a way that is suitable for shared or remote branches. Unlike git reset, which "rewrites history" by moving branch references, git revert creates a new commit that undoes the changes introduced by a specific commit. This approach allows for the reversal of changes while maintaining the integrity of the commit history, making it suitable for collaborative environments where changes need to be shared with others.
#### Moving Work Around
Understanding the basics of Git — committing, branching, and navigating the source tree—provides the foundation for leveraging the majority of Git's capabilities, meeting the main requirements of developers. However, for more complex workflows or situations where assistance is needed, mastering the concept of "moving work around" becomes invaluable. This concept enables developers to allocate work across different areas of the repository.
##### Cherry-Pick
```git cherry-pick``` is a very straightforward way of saying that you would like to copy a series of commits below your current location (HEAD). The following is the syntax for cherry-pick.
```
git cherry-pick <Commit1> <Commit2> <...>
```
In summary, Git cherry-pick is a command used to copy specific commits from one branch to another. It operates by specifying the commits to be copied using their commit IDs. <Commit1>, <Commit2>, etc., represent the commit IDs of the desired commits. This command facilitates the selective transfer of commits to a different branch, allowing for precise integration of changes across the repository. 
##### Interactive Rebase
Git's interactive rebase feature, accessed through the ```git rebase -i``` command, provides a powerful tool for managing commits when you're unsure which ones to select. It opens a UI, typically in a text editor like Vim, displaying the commits to be rebased along with their hashes and messages. This interface allows for a comprehensive review of the commits, facilitating informed decision-making. Additionally, interactive rebase enables advanced actions such as squashing commits, amending commit messages, and even editing the commits themselves, providing extensive control over the rebase process.

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
## Day 2: Git Branching Exercises
### Objective
Deepen your understanding of Git by completing the final two sections, "A Mixed Bag" and "Advanced Topics," in the "Main" level of Learn Git Branching. This assignment aims to solidify your grasp of advanced Git concepts and operations.  
![image](https://github.com/Laqwanda-Nettles/learn-git-branching/assets/147118788/cd16de5c-6470-42c9-81ee-a2bd8554b18a)  
#### A Mixed Bag
##### Grabbing Just 1 Commit
When tracking down a bug, developers often insert debug commands and print statements into their code, each placed in separate commits for clarity. Once the bug is fixed, the challenge arises of incorporating only the necessary changes into 
the main branch, without including the debug commits. To accomplish this, Git provides two commands:   
```
git rebase -i & git cherry-pick
```
By using interactive rebase ```git rebase -i```, developers can selectively choose which commits to include or exclude from the main branch. Additionally, ```git cherry-pick``` allows for the precise copying of individual commits to another branch, facilitating the integration of specific changes while maintaining code cleanliness. These commands provide effective solutions for managing locally stacked commits and ensuring that only relevant changes are merged into the main branch.
##### Juggling Commits
###### Git Rebase -i
When dealing with stacked commits that need adjustments, such as modifying an earlier commit in the commit history, one solution is using ```git rebase -i```. By reordering commits using ```git rebase -i```, the desired commit can be brought to the top of the history. Then, using ```git commit --amend```, the necessary modification can be made to the commit. Afterward, commits can be reordered back to their original positions. Finally, the main branch can be moved to the updated part of the tree. This process enables developers to effectively juggle commits and make precise modifications even to earlier parts of the commit history.
###### Git Cherry-pick
Unlike rebase, which may lead to conflicts due to extensive reordering, cherry-pick allows for the direct placement of a commit onto the HEAD, bypassing potential conflicts. This method simplifies the process of making modifications to specific commits, offering a straightforward solution for managing commit adjustments without the need for extensive reordering.
##### Git Tags
Git tags provide a means to permanently mark significant points in a project's history, such as major releases or significant merges. Unlike branches, which are mutable and subject to change, tags serve as permanent markers for specific commits, allowing for easy reference. Tags remain fixed in the commit tree and do not move as additional commits are made, making them stable anchors for historical points. While tags cannot be checked out and worked on like branches, they provide a reliable way to designate important milestones in a project's development.  
```
git tag v1 c1
```
Named the tag ```v1``` and referenced the commit ```c1``` explicitly. If you leave the commit off, git will just use whatever ```HEAD``` is at.
##### Git Describe
Git describe is a command that helps determine the position relative to the nearest tag in the commit history. It aids in understanding your location after navigating numerous commits, such as during debugging sessions or when collaborating with others. The syntax is simple: 
```
git describe <ref>
Output: <tag>_<numCommits>_g<hash>
```
<ref> represents any commit reference that Git can resolve. If no reference is specified, Git uses the current checkout location ```HEAD``` by default. The output of the command includes the closest ancestor tag, the number of commits between the tag and the current commit, and the hash of the current commit. This information provides context about the current position in the commit history relative to significant milestones marked by tags.  
![image](https://github.com/Laqwanda-Nettles/learn-git-branching/assets/147118788/cfe1cd6e-05a0-4357-8e3d-4a9af002fa7e) 
```
git describe main
output: v1_2gC2
git describe side
output: v2_1_gC4
```
#### Advanced Topics
##### Rebasing over 9000 times
Solution
```
git checkout bugFix
git rebase main
git checkout side
git rebase bugFix
git checkout another
git rebase side
git checkout main; git merge another
```
##### Multiple Parents
The ```^``` modifier in Git allows specifying which parent reference to follow from a merge commit. Unlike the ```~``` modifier, which specifies the number of generations to go back, ```^``` selects the parent reference from a merge commit. By default, Git follows the "first" parent upwards from a merge commit, but specifying a number with ```^``` changes this behavior. For instance, ```git checkout main^``` follows the first parent after the merge commit, while ```git checkout main^2``` selects the second parent. These modifiers can be chained together. For example, 
```
git checkout HEAD~^2~2
Same as ⬇️
git checkout HEAD~; git checkout HEAD^2; git checkout HEAD~2
```
##### Branch Spaghetti
Solution
```
git checkout one
git cherry-pick c4 c3 c2
git checkout two
git cherry-pick c5 c4 c3 c2
git checkout three; git merge c2
```
## Day 3: Remote Operations
### Objectives
Enhance your skills in managing remote operations in Git by completing the interactive exercises on Learn Git Branching, specifically focusing on remote repositories. This assignment aims to solidify your understanding of advanced remote operations such as push, pull, and managing multiple remotes.
![image](https://github.com/Laqwanda-Nettles/learn-git-branching/assets/147118788/1ed70837-bdeb-4742-9d17-d012475f7d60)
#### Push & Pull -- Git Remotes!
##### Clone Intro
Git remotes are essentially copies of your repository stored on another computer, typically accessible over the Internet. They serve several important purposes:  
- **Backup:** Remote repositories provide a backup of your local repository, ensuring that your project's history and data are preserved even if something happens to your local machine.
- **Collaboration:** Remotes enable collaboration by allowing multiple developers to work on the same project. They facilitate sharing code, pulling in changes from others, and contributing to the project's progress.
- **Social Coding:** With remote repositories, coding becomes a social activity as developers can easily contribute to each other's projects and track changes. Platforms like GitHub visualize activity around remote repositories, enhancing collaboration and project management.
  
The command used to set up the environment for remote repository work in Learn Git Branching is ```git clone```, which technically creates a remote repository out of your local one in this context. While ```git clone``` in the real world is used to create local copies of remote repositories, in Learn Git Branching, it helps establish the connection between cloning and remote repository work.
##### Remote Branches
Git remote branches, such as ```o/main``` introduced after a git clone, reflect the state of remote repositories and help differentiate between local and public work. These branches are on your local repository and follow the naming convention of ```<remote name>/<branch name>```.  
When checking out remote branches, Git puts you into detached ```HEAD``` mode, as you can't directly work on these branches; instead, you work elsewhere and then share your changes with the remote. While developers often uses "origin" as the remote name, in Learning Git Branching, it uses "o" as a shorthand due to space constraints. It's essential to remember that in real Git usage, your remote is likely named "origin".
##### Git Fetchin'
Git fetch is a command used to synchronize your local repository with changes from a remote repository. It performs two main functions:  
- **Downloading Commits:** Git fetch retrieves commits from the remote repository that are missing in your local repository.
- **Updating Remote Branches:** It updates the pointers of your remote branches to reflect the current state of the remote repository.
    
Git fetch communicates with the remote repository over the Internet, typically using protocols like ```http://``` or ```git://```.  

It's important to note what ```git fetch``` doesn't do: it does not change anything in your local state. It won't update your main branch or modify your local files. Instead, git fetch serves as a download step, ensuring that your local repository is aware of the latest changes in the remote repository.
##### Git Pullin'
Git pull is a command used to fetch remote changes and incorporate them into your local repository in one step. It combines the functionality of git fetch and a merge or rebase operation into a single command. This simplifies the process of updating your local work to reflect changes from the remote repository. With ```git pull```, you can quickly bring your local repository up to date with the latest changes from the remote without having to execute multiple commands manually.
##### Faking Teamwork
To simulate collaboration and introduce changes from a remote repository, Learn Git Branching uses the command ```git fakeTeamwork```. This command adds commits to the remote repository, mimicking updates made by collaborators. By default, ```git fakeTeamwork``` adds a commit to the main branch, but you can specify the number of commits or the target branch by appending additional parameters to the command. This allows for easy simulation of various collaboration scenarios, enabling effective learning and practice in managing remote repositories.  
**Solution**
```
git clone
git fakeTeamwork main 2
git commit
git pull
```
##### Git Pushin'
Git push is the command used to upload your local changes to a specified remote repository and update it with your new commits. This action makes your work available for others to download from the remote. Git push essentially "publishes" your work, allowing for collaboration and sharing among team members. The behavior of ```git push``` without any arguments may vary depending on the ```push.default``` setting in Git, the ```upstream``` value is used in the lessons. It's important to check your settings before pushing in your own projects to ensure proper behavior.
##### Diverged History
When the history of a repository diverges due to changes made by multiple contributors, git push becomes ambiguous, as it's unclear whether to overwrite the remote with outdated changes or incorporate new changes while ignoring outdated ones. Git prevents pushing in this situation and requires incorporating the latest remote changes before sharing your work.  
To resolve this, you can base your work off the most recent version of the remote branch. One way to achieve this is through rebasing, which involves fetching the latest changes from the remote ```git fetch```, rebasing your work onto the updated remote branch ```git rebase o/main```, and then pushing your changes ```git push```.   Alternatively, you can use merging by fetching changes ```git fetch```, merging them into your work ```git merge o/main```, and then pushing your changes ```git push```.  
A more convenient way to update your work is by using ```git pull```, which combines fetching and merging. For a rebase-based update, you can use ```git pull --rebase``` followed by ```git push```. For a merge-based update, you can use regular ```git pull``` followed by ```git push```. 
##### Locked Main
If attempts to push commits directly to the main branch are rejected due to a policy requiring the use of pull requests, the rejection message will indicate that the remote rejected the push. This occurs because commits cannot be pushed directly to main under the policy.  
To resolve this issue, create another branch, such as "feature", and push that branch to the remote repository. Additionally, reset the main branch to be in sync with the remote to avoid conflicts during future pulls.   
**Solution**
```
git checkout -b feature
git push
git checkout main
git reset main^
git checkout feature
```
#### To Origin And Beyond -- Advanced Git Remotes!
##### Push Main!
In the workflow of integrating feature branches into the main branch, developers typically work on feature branches off of the main branch. Once the feature is ready, it's integrated into the main branch. Developers often only push and pull when on the main branch, ensuring that the main branch stays updated with the remote repository.  
To update the main branch and push work:
- Use ```git pull --rebase``` to fetch new commits from the remote repository and rebase your local changes on top of them.
- Use ```git push``` to publish your local changes to the remote repository.    
These commands ensure that your local main branch reflects the latest changes from the remote repository and pushes your work to the remote repository.
##### Merging with Remotes
The debate between merging and rebasing in the development community revolves around the trade-offs associated with each approach. Here are the general pros and cons of rebasing:   
Pros:  
- **Clean Commit Tree:** Rebasing results in a clean commit tree where commits are arranged in a straight line, making it easier to understand the project's history.
  
Cons:     
- **Altered History:** Rebasing modifies the apparent history of the commit tree. Commits may appear to be in a different order than they were originally made, which can be confusing for collaborators trying to understand the chronological sequence of changes.
  
Some developers prefer merging because it preserves the original history of the commit tree, while others prefer rebasing for a cleaner commit history. Ultimately, the choice between merging and rebasing comes down to personal preferences and project requirements.
##### Remote Tracking
Remote-tracking branches establish a connection between local branches and their corresponding branches on the remote repository. This connection is essential for operations like pull and push, where git determines the target branch for merging or pushing based on this association.     
During a clone operation, git automatically sets up remote-tracking branches for each branch on the remote repository. For instance, the local main branch typically tracks the o/main branch on the remote. This ensures that the main branch knows where to fetch new changes from and where to push its own changes to.     
While git sets up this association automatically during cloning, users can also specify it manually. This can be done by either checking out a new branch based on a remote branch ```git checkout -b newBranch o/remoteBranch``` or using the ```git branch -u``` command ```git branch -u o/remoteBranch newBranch```. This allows any branch to have the same implied push destination and merge target as the main branch.
##### Git Push Arguments
In Git, the ```git push``` command is used to upload local commits to a remote repository. By default, it determines the remote and the branch to push to based on the properties of the currently checked out branch. However, it can also accept arguments in the form of ```<remote>``` and ```<place>```.      
```<place>``` specifies the source and destination of the commits being pushed.    
For example, ```git push origin main``` means pushing commits from the local main branch to the main branch on the remote named "origin."       
To specify both the source and destination independently, a colon refspec is used, in the format ```<source>:<destination>```. This provides flexibility to push commits from one local branch to a different branch on the remote repository.     
For instance, ```git push origin foo^:main``` pushes commits from the foo branch's parent to the main branch on the remote. If the destination branch doesn't exist on the remote, Git will create it when specified in the push command.
##### Fetch Arguments
In Git, the arguments for ```git fetch``` are similar to those for ```git push```, but they operate in the opposite direction since ```git fetch``` downloads commits from the remote repository. The ```<place>``` parameter specifies the source and destination of the fetched commits.     
For example, ```git fetch origin foo``` downloads commits from the foo branch on the remote and places them onto the o/foo branch locally. If a colon refspec ```<source>:<destination>``` is used, commits are fetched from the source on the remote and placed onto the destination locally.    
It's important to note that specifying a destination allows developers to fetch commits directly onto a local branch, but ```<source>``` refers to a place on the remote repository. If no arguments are provided, ```git fetch``` downloads all commits from the remote onto all remote branches.
##### Source of nothing
Git allows for the peculiar use of an empty argument as ```<source>``` in ```git push``` and ```git fetch```. Pushing "nothing" to a remote branch effectively deletes it, as demonstrated by ```git push origin :foo```, where the foo branch on the remote is deleted. Fetching "nothing" to a place locally creates a new branch, illustrated by ```git fetch origin :bar```, where a new branch named bar is created locally.
##### Pull arguments
Git pull is essentially a combination of ```git fetch``` followed by ```git merge```, serving as a shorthand for these two commands. When you specify a branch for ```git pull```, such as ```git pull origin foo```, it's equivalent to ```git fetch origin foo``` followed by ```git merge o/foo```. Similarly, specifying a source and destination in ```git pull```, like ```git pull origin main:foo```, results in the creation of a new local branch named ```foo```, fetching commits from the remote's ```main```, and merging them into the current branch. This functionality allows for efficient updating of multiple branches by running ```git pull``` with the same arguments from different locations.
## Day 4: Git Rebase
### Objective
Strengthen your understanding of Git rebase and pull configuration through hands-on exercises. This assignment involves creating and documenting scenarios that simulate real-world Git workflows.
#### Part 1 Rebasing and Resolving Conflicts
- Step 1: Create a Feature Branch (Local)
    - Cloned repository with ```git clone https://...```
    - Created new branch with ```git switch -c feature-branch```
- Step 2: Simulate Main Branch Updates (Local & Remote) 
    - Switched to main branch, made changes, and committed them. ```git switch main``` ➡️ ```git commit -m "test"``` ➡️ ```git push```
        - I had trouble with committing my message due to git config problems.   
    - On Github made changes to the HTML file in the main branch and committed those changes directly on Github.
      
The main branch change on the git terminal represented a local environment, whereas the main branch changes in Github represented a remote one.   
This is a screenshot of GitHub commit:   
![image](https://github.com/Laqwanda-Nettles/learn-git-branching/assets/147118788/9708ab71-5866-444e-8fc9-4bb0e0158e1c)   
- Step 3: Stash and Rebase (Local)
    - Switched back to feature-branch locally ```git switch feature-branch``` and stashed changes ```git stash```
    - Performed a rebase with ```git rebase main```
    - Resolved the conflict in VSCode and typed ```git rebase --continue``` in git terminal which opened vim.

  This is a screenshot of rebase completion & conflict resolution:    
![image](https://github.com/Laqwanda-Nettles/learn-git-branching/assets/147118788/42fa8396-6dff-4c93-9ec9-e1b63c37f62a)
- Step 4: Apply Stash Changes (Local)
    - Applied stashed changes with ```git stash pop```

It didn't seem to have any conflicts. I'm not sure if I did this correctly. The following are two screenshots for git stash pop.   
![image](https://github.com/Laqwanda-Nettles/learn-git-branching/assets/147118788/4433a378-2f83-4861-ae70-28758c0f703a)
![image](https://github.com/Laqwanda-Nettles/learn-git-branching/assets/147118788/28a7687b-76e7-4025-aef4-2b00005576c4)

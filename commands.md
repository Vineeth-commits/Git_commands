## Version Control System
---
Version control systems are a category of software tools that help a software team manage changes to source code over time. Version control software keeps track of every modification to the code in a special kind of database. If a mistake is made, developers can turn back the clock and compare earlier versions of the code to help fix the mistake while minimizing disruption to all team members.
There are two types of version control systems
* Centralized
* Decentralized or Distributed like git which is a distributed version control system

The .git folder contains a collection of files and folders that make up the internal structure of the repository.

## Configuring Git on your pc
---
### Setting username
This information is used by Git for each commit.
```bash
git config --global user.name "user name"
```
### Setting email id
This information is used by Git for each commit.
```bash
git config --global user.email "user@gmail.com"
```
### Avoid merge commits for pulling
You pull the latest changes from a remote repository, and if these changes are divergent, then by default Git creates merge commits. We can avoid this via following settings.
```bash
git config --global branch.autosetuprebase always
```
### Color highlighting
The following commands enable color highlighting for Git in the console.
```bash
git config --global color.ui true
git config --global color.status auto
git config --global color.branch auto
```
### Setting default editor
By default, Git uses the system default editor, which is taken from the VISUAL or EDITOR environment variable. We can configure a different one by using git config.
```bash
git config --global core.editor vim
```
### Setting default merge tool
Git does not provide a default merge tool for integrating conflicting changes into your working tree. We can set default merge tool by enabling following settings.
```bash
git config --global merge.tool vimdiff
```
### Listing Git settings
To verify your Git settings of the local repository, use git config –list command as given below.
```bash
git config --list
```
### Creating alias to view the log history 
```bash
>git config --global alias.logx "git log --online --graph --decorate -all"	
```
To start tracking a folder, we use
```bash
git init <folder_name>
```
To list files that are being tracked by git, we use
```bash
git ls-files
```

### Basic operations on git
|working directory| -------> |staging area| -------> |remote repository|
The basic workflow of Git - 
* Step 1 − You modify a file from the working directory. This prepares for the staging area
    ```bash
    git add <file to be added to the staging area> or git add . 
    ```
* Step 2 − You add these files to the staging area.
    ```bash
    git commit -m "message related to the commit"
    ```
* Step 3 − You perform commit operation that moves the files from the staging area. After push operation, it stores the changes permanently to the Git repository.

## Key terminologies
---
### Blobs
Blob stands for Binary Large Object. Each version of a file is represented by blob. A blob holds the file data but doesn’t contain any metadata about the file. It is a binary file, and in Git database, it is named as SHA1 hash of that file. In Git, files are not addressed by names. Everything is content-addressed.

### Trees
Tree is an object, which represents a directory. It holds blobs as well as other sub-directories. A tree is a binary file that stores references to blobs and trees which are also named as SHA1 hash of the tree object.
### Commits
Commit holds the current state of the repository. A commit is also named by SHA1 hash. You can consider a commit object as a node of the linked list. Every commit object has a pointer to the parent commit object. From a given commit, you can traverse back by looking at the parent pointer to view the history of the commit. If a commit has multiple parent commits, then that particular commit has been created by merging two branches.
### Branches
Branches are used to create another line of development. By default, Git has a master branch, which is same as trunk in Subversion. Usually, a branch is created to work on a new feature. Once the feature is completed, it is merged back with the master branch and we delete the branch. Every branch is referenced by HEAD, which points to the latest commit in the branch. Whenever you make a commit, HEAD is updated with the latest commit.

### Tags
Tag assigns a meaningful name with a specific version in the repository. Tags are very similar to branches, but the difference is that tags are immutable. It means, tag is a branch, which nobody intends to modify. Once a tag is created for a particular commit, even if you create a new commit, it will not be updated. Usually, developers create tags for product releases.
### Clone
Clone operation creates the instance of the repository. Clone operation not only checks out the working copy, but it also mirrors the complete repository. Users can perform many operations with this local repository. The only time networking gets involved is when the repository instances are being synchronized.

### Pull
Pull operation copies the changes from a remote repository instance to a local one. The pull operation is used for synchronization between two repository instances. This is same as the update operation in Subversion.

### Push
Push operation copies changes from a local repository instance to a remote one. This is used to store the changes permanently into the Git repository. This is same as the commit operation in Subversion.

### HEAD
HEAD is a pointer, which always points to the latest commit in the branch. Whenever you make a commit, HEAD is updated with the latest commit. The heads of the branches are stored in .git/refs/heads/ directory.
		
### Revision
Revision represents the version of the source code. Revisions in Git are represented by commits. These commits are identified by SHA1 secure hashes.

### URL
URL represents the location of the Git repository. Git URL is stored in config file
		
### Basic commands
* Create empty Git repository in specified directory. Run with no arguments to initialize the current directory as a git repository.
    ```bash
    git init <directory>
    ```
* Clone repository located at <repo> onto local machine. Original repository can be located on the local filesystem or on a remote machine via HTTP or SSH.
    ```bash
	>git clone <repo>
    ```
* Stage all changes in <directory> for the next commit. Replace <directory> with a <file> to change a specific file.
    ```bash
    >git add <directory> 
    ```
* Commit the staged snapshot, but instead of launching a text editor, use <message> as the commit message.
    ```bash
	git commit -m "message" 
    ```
* List which files are staged, unstaged, and untracked.
    ```bash
	git status
    ```
* Display the entire commit history using the default format. For customization see additional options.
    ```bash
	git log
    ```
* Show unstaged changes between your index and working directory.
    ```bash
	git diff
    ```
* This will take us to the branch mentioned
    ```bash
	git checkout <branch>
    ```
* This will merge to a branch which is checked out
    ```bash
    git merge [the branch to be merged] 
    git rebase [the branch to be rebased]
    git tag <name> commitID #will tag a commit
	git describe <ref> #The output will be <tag>_<numCommits>_g<hash>
    ```
* Shortcut commands
    * combination of git add and git commit
        ```bash
	    >git commit -am "message"
        ```
    * combination of git branch and git checkout to the branch
        ```bash
		git checkout -b [branch name] 
		git branch -f <name of the branch to be moved> <location> #example >git branch -f master HEAD^
		git cherry-pick <commit IDs> #It's a very straightforward way of saying that you would like to copy a series of commits below your current location (HEAD).
		git rebase -i HEAD~4 #In this a editor will open to choose the commits and then start a branch from HEAD~4
        ```

## Git - life cycle
---
General workflow is as follows −
* Step 1: You clone the Git repository as a working copy.
* Step 2: You modify the working copy by adding/editing files.
* Step 3: If necessary, you also update the working copy by taking other developer's changes.
* Step 4: You review the changes before commit.
* Step 5: You commit changes. If everything is fine, then you push the changes to the repository.
* Step 6: After committing, if you realize something is wrong, then you correct the last commit and push the changes to the repository.

## Git - Clone Operation
---
The Clone operation creates an instance of the remote repository.
```bash
git clone <url>
```
	
## Git - Perform Changes 
* git status command will show files present in the staging area. If it is precided by a question mark then these files are not a part of Git. The performed changes can be committed.
    ```bash
    git status -s
    ```
* It will display the information of all the commits with their commit ID, commit author, commit date and SHA-1 hash of commit.
    ```bash
	git log
    ```
* This command can rewrite your last commit message
    ```bash
	git --amend -m "new message"
    ```

## Git - Review Changes
* Use the git show command to view the commit details. The git show command takes SHA-1 commit ID as a parameter.
    ```bash
	git show <commit ID>
    ```
* Show unstaged changes between your index and working directory
    ```bash
	git diff 
    ```

## Git - Push Operation
* The Push operation stores data permanently to the Git repository.
    ```bash
	git push origin master
    ```
* There conflict such as the local repository not being in sync with the remote repository.In order to resolve this we use pull to update the local repository
    ```bash
	git pull
    ```
    Checking log files is essential
	
## Git - Stash Operation
When a situation arises where a new feature must be applied but it cant be be temporarily committed. Stash can be used when you need a temporary space and a partial space.
Now, you want to switch branches for customer escalation, but you don’t want to commit what you’ve been working on yet; so you’ll stash the changes. 
* To push a new stash onto your stack, run the git stash command.
    ```bash
	git stash
    ```
* We can view a list of stashed changes by using the git stash list command.
    ```bash
	git stash list
    ```
* Suppose you have resolved the customer escalation and you are back on your new feature looking for your half-done code, just execute the git stash pop command, to remove the changes from the stack and place them in the current working directory.
    ```bash
	git stash pop
    ```

## Git - Move Operation
* The move operation moves a directory or a file from one location to another. Tom decides to move the source code into src directory.
    ```bash
	>git mv <file to be moved> <location to be moved>
    ```
* To make these changes permanent, we have to push the modified directory structure to the remote repository so that other developers can see this.
    ```bash
	>git commit -m "Location changed"
	>git push origin master
    ```
* After the pull operation, the directory structure will get updated for other members of the repository
    ```bash
	>git pull
    ```

## Git - Rename Operation
* To rename a file, we use
    ```bash
	git mv <file name> <new name>
    ```
* Now when we check the status the renamed file will show R before the file name.
	* For commit operation, we can use -a flag, that makes git commit automatically detect the modified files(thereby skipping the git add command).Then push operation must be used to save it in the remote repository.
        ```bash
	    git commit -am "file renamed"
	    git push origin master
        ```

## Git - Delete Operation
The procedure is same as moving and renaming. We use 
```bash
>git rm <file name>
```
commit and push it later


## Git - Time travel through reset and reflog
Suppose the user accidentally does some changes and wants to go back.
* The option --soft is the least destructive. This simply changes the commit ID that the head is pointing to which means it preserves the git staging area
    ```bash
	git reset <commitID> --soft
	git reset <commitID> --mixed
    ```
* This is the default option if not specified. This doesnt preserve the staging area instead is placed in the working directory
    ```bash
	git reset <commitID> --hard 
    ```
    This is the most destructive. This simply cleans the working directory and staging area
* Shows all the different actions taken in the repository
    ```bash
	>git reflog
    ```

## Git - Tag Operation
* Creates a simple tag
    ```bash
	git tag <name of the tag> 
    ```
* Deletes the tag
    ```bash
	git tag -d <name of the tag> 
    ```
* Creates a annotation tag which provides more info when git show <tag name> is done
    ```bash
	>git tag -a <name of the tag> -m "message"
    ```

## Git - Backing out changes
* A file can be removed from the staging by using reset command
    ```bash
	git reset HEAD <file to be unstaged>
    ```
* To discard the changes made, we use
    ```bash
	git checkout -- <file>
    ```
	
## Creating aliases for git commands
```bash
git config --global alias.[name of the alias] "<the command>"
```

## Types of merges
* Fast-Forword merge - used when no additional work has been detected on the parent branch (when merged its like the branch has never been created)
	* Automatic merge
	* Manual merge

## Creating a branch, merging it and then deleting the branch
* Creates a branch
    ```bash
	git branch <branch_name> 
    ```
* Moving the HEAD to the a particular branch
    ```bash
	>git checkout <branch_name> 
    ```
* This command is same as the above two commands. It creates and moves the HEAD to a branch. The option -b creates the branch
    ```bash
	git checkout -b <branch_name> 
    ```
* To merge the branch to master
    ```bash
	git checkout master
	git merge <branch_name>
    ```
* To delete a branch
    * This only deletes the label
        ```bash
	    git branch -d <branch_name> 
        ```
	* To check all the branches
        ```bash
        git branch -a 
        ```
	* If any conflict has occured use
        ```bash
	    git mergetool
        ```

## Linking to your remote repository and pushing changes
* Displays remote connections
    ```bash
	git remote -v 
    ```
* Adding links   
    ```bash
    git remote add <name of the link usually origin> <URL to the remote repository
    ```
* The -u option is going to set up a tracking branch relationship between the master branch on local and remote repository. The --tags sends all the tags in the local repository to remote repository. when pushing in the future the -u option is not required
    ```bash
	git push -u origin master --tags 
    ```

## SSH authentication
* create a .ssh directory in ~/
    ```bash
	mkdir .ssh
    ```
* In the directory, generate a public and private key
    ```bash
	ssh-keygen -t rsa -C "email@address.com"
    ```
* Pharaphase is optional now copy the contents in the file .pub which stores the public key then go to github settings/SSH keys and paste it.
    ```bash
	ssh -T git@github.com 
    ```
    to check if the machine is communicating to github via SSH

## Updating the remote url
If the git repo name is changed then use this to update 
```bash
git remote set-url origin <url>
```

## Difference between fetch and pull
* git fetch really only downloads new data from a remote repository - but it doesn't integrate any of this new data into your working files. Fetch is great for getting a fresh view on all the things that happened in a remote repository.
* git pull, in contrast, is used with a different goal in mind: to update your current HEAD branch with the latest changes from the remote server. This means that pull not only downloads new data; it also directly integrates it into your current working copy files.
	Note: Start git pull with a clean directory only

## Git rebase
* Rebasing essentially takes a set of commits, "copies" them, and plops them down somewhere else.
* While this sounds confusing, the advantage of rebasing is that it can be used to make a nice linear sequence of commits. The commit log / history of the repository will be a lot cleaner if only rebasing is allowed.
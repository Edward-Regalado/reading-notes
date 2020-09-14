### Versoin Control 
* system that allows you to revisit various versions of a file or set of files by recording changes
* **Local Version Control** VCS entails one database on your hard disk that stoes changes to files
* **Centralized Version Control** CVCS system entails a single server storing all changes and file versions, can be accessed by various clients. 
* **Distributed Version Control** DVCS addresses the major vulnerability of th CVS: the server as the single point of failure. Allows clients to create mirrored repos. These         data backups can be easily placed on a server to replace any lost info

### what is git? 
* is a distributed version-control system for tracking changes in source code during software dev
* A history of changes to your files 
* The ability to view, apply and remove those changes
* Keep all of your project files in one repo
* It makes collaboration possible

### Snapshots in time
* each commit has a lable that points to it
* HEAD = The label meaning "you are here"
* You can also assign a label called a message

### What is GitHub
* A way to share code
* Online place to store code
* It uses Git to help you manage your team's work
  * Version Tracking
  * Reviewing changes
  * Keep changes separate until you want to add them in 

### What is a Repository?
* Collection of files that you told Git to pay attention to
* Usually, one project = one repo
  
### Git Useful Commands
* **git config** allows the setting of configuration variables that control aspects of Git's operation and look
  * git config --global user.name "Tony Regalado"
  * git config --global user.email "tregalado30@gmail.com
  * git config --list command to check settings 
  * git help command, git command --help, man git-command
  
### Setting up a Git Repo
* switch to target project's directory: $  cd test (cd = change directory)
* Use the git init command: $ git init command 
* Track repo files, perform and initial commit: $ git add *.c, $ git add LICENSE, $ git commit -m "any message here"

### Cloning
* you can also create a copy of an existing Git repo from a server: $ git clone https://github.com/test or $ git clone https://github.com/test mydirectory 
* This copies all versions and files of project and leads to a directory call "test," with an initialized .git directory inside
* Automatically check, retrieves for editing- a copy of the newest version of the project

### Workflow 
* **Local Repo Structure**- local Git repo has three components: 
  1. Working Directory: The actual files live here
  2. Index: area used for sharing
  3. Head: points to the most recent commit

* **Saving Changes**- All files in a project are either in a tracked or untracked state
  * Tracked- can be modified, unmodified, or staged; they were part of the most recent file snapshot
  * Untracked- not in the last snapshot and do not currently reside in the staging area
  * AFter cloing a Reop, files have tracked status because they have been checked out but not modified
  
* **Life Cycles of File Status
  1. after you edit a file, Git flags it as modified because of changes made after the previous commit
  2. You stage modified file
  3. Then, you commit staged changes 
  
* **Check File Status** 
* To determine the state of files- $ git status 

* **Tracking & Staging a New File**
* Track single file in repo- $ git add filename
* Track all files in repo- $ git add * 
* After these command files are tracked and staged for committing

* **Committing a File**
* after staging one or multiple files, you should commit the changes and record what you did within the ""- $ git commit -m "made change x,y,z"
* This step has commmitted changes for file(s) to the HEAD
* committing all changes, snapshot of all mods to tracked files in working dir: $ git commit -a

* **Pushing Changes** 
* you need to push changes to a remote repo: $ git push origin master
* this command pushes changes from the local "master" brand to the remote repo named "origin"
* For cloned repos, Git will automatically name "origin" to the server from which you cloned and the name "master" to your local repos. 

* **Stashing Changes** 
* when you're not ready to commit changes and don't want to lose them: git stash 
* this command temporarily removes changes and hides them, giving you a clean working directory
* when you're ready to retrieve those unfinishes changes: git stash apply







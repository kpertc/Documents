[[Linux Command]]

[字节GitLab SourceTree设置](https://bytedance.feishu.cn/wiki/wikcntgeqxeRZ76S3wknA6CTZUc)

##### Official Docs

```
git clone <url>

git clone ../remote_repo.git . → local path
git clone https://github.com/xxx/remote_repo.git . → website
```

https://git-scm.com/docs

##### Git Book

https://git-scm.com/book/zh/v2

##### Tutorials:

[IE&EPE新人融入计划Lesson15——GIT基础及实践](https://bytedance.feishu.cn/docs/doccnwAne4VJr6iBGC4Y4g1EFJf#nBp6dA)

[[YouTube] Git and GitHub for Beginners - Crash Course](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1282s)

[Git Tutorial for Beginners: Command-Line Fundamentals](https://youtu.be/HVsySz-h9r4)

##### Installation

https://www.atlassian.com/git/tutorials/install-git#windows

##### What is Version Control?

The management of changes to documents, computer programs, large websites, and other collections of information.

###### Terms

>[!note]
>**Directory** → Folder
>
>**Terminal or Command Line →** Interface for Text Commands
>
>**CLI** → Command Line Interface
>
>**cd** → Change Directory
>
>**Code Editor** → Word Processor for Writting Code
>
>**Repository** → Project, or the folder/place where your project is kept

###### Git Commands

>[!note]
>**clone** → Bring a repository that is hosted somewhere like Github into a folder on your local machine
>
>**add** → Track your files and changes in Git
>
>**commit** → Save your files in Git
>
>**Push** → Upload Git commits to a remote repo, like Github
>
>**Pull →** Download changes from remote repo to your local machine, teh opposite of push

>[!note]
>Command + Shift + . Show hidden file

##### SSH Key

An SSH key is an access credential for the SSH (secure shell) network protocol.

```
 ~ ssh-keygen -t rsa -b 4096 -C "dr_cjf@126.com"
```

Github use https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md

##### Git Lens plugin for VSCode

##### Git Help

git help <verb>

git <verb> --help

git help config

git config --help

##### Git Config

```
git config -- global user.name "Jingfu Chen"
git config -- global user.email "chenjingfu.design@bytedance.com"
```

```
git config --list
```
![[output.png]]


##### Start → Git init

Start new

```bash
git init

git remote -v →  show remote
```

Clone

###### .gitignore

> [!note]
>`touch .gitignore` to create a .gitignore by CLI

```bash
*.pyc → ignore all .pyc files
```

###### Delete Git

```bash
$ rm -fr .git → remove .git files
```

Use `git status` to check

##### Git Commit

```bash
git --version → Check git version & if installed on the computer

git status

// add all files / stage file
git add . 
→ --- command will index any new files and staging modified files from your working tree to be committed. But it will ignore whatever you have removed files from your working tree.

git add -A / -all 
→ command will add any new files,modified content, and removed files from your working tree.

git add filename.extension

// reset stage files / unstage
git reset "file-name" → unstage files
git reset . → unstage all changes
git reset -- hard → unstage and also delete files 

// also remove files
git clean 

//need to type at least one message
git commit -m "Added index.html" -m "asdasasdasdasd"

//add and commit, 
//only for modified file not new created file
git commit -am "meesage"

git log 
```

##### Git Push

```bash
git diff
git status
git add -A
git commit -m "message"
```

```bash
git push
git pull origin master branch name
git push origin master
```

```bash
`git push -f origin master`
```

```bash
git remote add origin //gitAddressHere
```

<br>

##### Git Branching

-   Master Branch
-   Feature Branch

`git branch -a` List all branch

`git branch` Show currency branch

1.  Create branch `git checkout -b branch-name`
2.  Switch branch `git checkout main`
3.  Merge branch
    1.  `git diff` show different
    2.  `git merge`
4.  Delete branch `git branch -d branch-name`

<br>

##### Git log

`git log --oneline`

![[git-log-oneline.png]]


<br>

##### Stash → Save working files

[Tutorial](https://www.youtube.com/watch?v=KLEDKgMmbBI)

```bash
git stash list // list all stash

// save current working on files to stash. name
git stash save "Worked on XXX"

then git diff and git commit no longer have working  on files

// apply by stash id, will not delete the stash
git stash apply stash@{0}

// apply the most recent stash and delete the stash
git stash pop

// delete stash
git stash drop stash@{0} // delete by stash id
git stash clear // delete all stash
```
<br>
Merge other Branch to Master

First we run `git checkout master` to change the active branch back to the `master` branch. Then we run the command `git merge new-branch` to _merge the new feature into the master_ branch.

``` bash
git merge new-branch
```

Save changes as stash in one branch and apply the change to another branch

##### Professional Tutorial

https://www.youtube.com/watch?v=Uszj_k0DGsg&t=22s

The Perfect Commit


<br>

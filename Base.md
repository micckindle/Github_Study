Install msysGit(windows), Built-in(Mac), Built-in(Linux)

Initial settings
set name and email

  $git config --global user.name "name"
  $git config --global user.email "email"

--> ~/.gitconfig

[user]
  name = Firstname Lastname
  email = your_email@example.com

IMPROVE READABILITY

  $git config --global color.ui auto
  
--> ~/.gitconfig

[color]
  ui = auto
  
---------------------------
set SSH key
$ ssh-keygen -t rsa -C "your_email@example.com"

*id_rsa is private key, id_rsa.pub is public key.

Add SSH public key
$ cat ~/.ssh/id_rsa.pub
ssh-rsa + public key content + your_email@example.com

Test SSH public key
$ ssh -T git@github.com
The authenticity of host 'github.com(207.97.227.239)' can't be established.
RSA key fingerprint is fingerprint **
Are you sure you want to continue connexting(yes/no) yes

-----------------------------
How to use
$git clone git@github.com:hirocastest/Hello-World.git
$git status
$git add hello_world.php
$git commit -m "Add hello world script by php"
$git log
$git push

----------------------------
Base command
* git init：Initialize repository
$mkdir git-tutorial
$cd git-tutorial
$git init


* git status:View the repository status
$git status

* git add:Adding files to cache
$git add README.md
$git status

* git commit：save repository history
$git commit -m "First commit"
$git commit

* git log:viewing the commit log
$git log
$git log --pretty=short:display only the first row
$git log README.md: Displays only the file log of specified directory
$git log -p
$git log -p README.md: Display different of files

* git diff
$git diff: Display different from Work flow to cache
$git diff HEAD: Display different from Work flow to the newest commit

* git branch: display the branch table
$git branch

* git checkout -b: create or select the branch
$git checkout -b feature-A: switc to a new branch 'feature-A' equal $git branch feature-A $git checkout feature-A
$git checkout -: switched to last one branch

* git merge --no-ff feature-A
Merging branchs
------------------------------------------
$git log --graph: Display branchs by chart view

* git reset: Backtrack vison history
$git reset --hard fd0cbf0d4a25f74...: HEAD is now an fd0cdf0 Add index
-------------------------------------------
$git reflog: Display current respository operation history
$git commit --amend: Modify the submitted information
$git rebase -i: Compressed history     $git rebase -i HEAD~2





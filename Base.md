# Install
### msysGit(windows), Built-in(Mac), Built-in(Linux)
------------------
# Initial settings
set name and email
```sh
  $ git config --global user.name "name"
  $ git config --global user.email "email"

--> ~/.gitconfig

[user]
  name = Firstname Lastname
  email = your_email@example.com
```
# IMPROVE READABILITY
```
  $ git config --global color.ui auto
  
--> ~/.gitconfig

[color]
  ui = auto
```  
---------------------------
# set SSH key
```sh
$ ssh-keygen -t rsa -C "your_email@example.com"

*id_rsa is private key, id_rsa.pub is public key.
```
# Add SSH public key
```sh
$ cat ~/.ssh/id_rsa.pub
ssh-rsa + public key content + your_email@example.com
```
# Test SSH public key
```sh
$ ssh -T git@github.com
The authenticity of host 'github.com(207.97.227.239)' can't be established.
RSA key fingerprint is fingerprint **
Are you sure you want to continue connexting(yes/no) yes
```
-----------------------------
# How to use
```sh
$ git clone git@github.com:hirocastest/Hello-World.git
$ git status
$ git add hello_world.php
$ git commit -m "Add hello world script by php"
$ git log
$ git push
```
----------------------------
# Base command
### git init：Initialize repository
```sh
$ mkdir git-tutorial
$ cd git-tutorial
$ git init
```

### git status:View the repository status
```sh
$ git status
```

### git add:Adding files to cache
```sh
$ git add README.md
$ git status
```

### git commit：save repository history
```sh
$ git commit -m "First commit"
$ git commit
```

### git log:viewing the commit log
```sh
$ git log
$ git log --pretty=short:display only the first row
$ git log README.md: Displays only the file log of specified directory
$ git log -p
$ git log -p README.md: Display different of files
```

### git diff
```sh
$ git diff: Display different from Work flow to cache
$ git diff HEAD: Display different from Work flow to the newest commit
```

### git branch: display the branch table
```sh
$ git branch
```

### git checkout -b: create or select the branch
```sh
$ git checkout -b feature-A: switc to a new branch 'feature-A' equal $git branch feature-A $git checkout feature-A
$ git checkout -: switched to last one branch
```

### git merge --no-ff feature-A
```sh
Merging branchs
------------------------------------------
$ git log --graph: Display branchs by chart view
```

### git reset: Backtrack vison history
```sh
$ git reset --hard fd0cbf0d4a25f74...: HEAD is now an fd0cdf0 Add index
-------------------------------------------
$ git reflog: Display current respository operation history
$ git commit --amend: Modify the submitted information
$ git rebase -i: Compressed history     $git rebase -i HEAD~2
```
-----------------------------------------
# Pushed to a remote repository
### git remote add
```sh
$ git remote add origin git@github.com:github-book/git-tutorial.git    -->set origin: Add a remote repository
$ git push -u origin master: pushed to master branch
$ git checkout -b feature-D: switched to a new branch 'feature-D'
$ git push -u origin feature-D: Pushed to other branch
```
-------------------------------------------
### Obtained from a remote repository
```sh
$ git clone git@github.com:github-book/git-tutorial.git  -->master
$ git branch -a: Along with local repository and remote repository branch information
$ git checkout -b feature-D origin/feature-D
$ git diff
$ git push
* git pull: get the last remote repository branch
$ git pull origin feature-D
```
--------------------------------------------
# REFERENCES
* Pro Git
* LearnGitBranching
* tryGit

----------------------------------------------
# COMMANDS
## git
```sh
$ git --help
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```
------------
## git clone
```sh
git-clone(1) Manual Page
NAME
git-clone - Clone a repository into a new directory

SYNOPSIS
git clone [--template=<template_directory>]
	  [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
	  [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
	  [--dissociate] [--separate-git-dir <git dir>]
	  [--depth <depth>] [--[no-]single-branch]
	  [--recursive | --recurse-submodules] [--[no-]shallow-submodules]
	  [--jobs <n>] [--] <repository> [<directory>]
DESCRIPTION
Clones a repository into a newly created directory, creates remote-tracking branches for each branch in the cloned repository (visible using git branch -r), and creates and checks out an initial branch that is forked from the cloned repository’s currently active branch.

After the clone, a plain git fetch without arguments will update all the remote-tracking branches, and a git pull without arguments will in addition merge the remote master branch into the current master branch, if any (this is untrue when "--single-branch" is given; see below).

This default configuration is achieved by creating references to the remote branch heads under refs/remotes/origin and by initializing remote.origin.url and remote.origin.fetch configuration variables.

OPTIONS
--local
-l
When the repository to clone from is on a local machine, this flag bypasses the normal "Git aware" transport mechanism and clones the repository by making a copy of HEAD and everything under objects and refs directories. The files under .git/objects/ directory are hardlinked to save space when possible.

If the repository is specified as a local path (e.g., /path/to/repo), this is the default, and --local is essentially a no-op. If the repository is specified as a URL, then this flag is ignored (and we never use the local optimizations). Specifying --no-local will override the default when /path/to/repo is given, using the regular Git transport instead.

--no-hardlinks
Force the cloning process from a repository on a local filesystem to copy the files under the .git/objects directory instead of using hardlinks. This may be desirable if you are trying to make a back-up of your repository.

--shared
-s
When the repository to clone is on the local machine, instead of using hard links, automatically setup .git/objects/info/alternates to share the objects with the source repository. The resulting repository starts out without any object of its own.

NOTE: this is a possibly dangerous operation; do not use it unless you understand what it does. If you clone your repository using this option and then delete branches (or use any other Git command that makes any existing commit unreferenced) in the source repository, some objects may become unreferenced (or dangling). These objects may be removed by normal Git operations (such as git commit) which automatically call git gc --auto. (See git-gc(1).) If these objects are removed and were referenced by the cloned repository, then the cloned repository will become corrupt.

Note that running git repack without the -l option in a repository cloned with -s will copy objects from the source repository into a pack in the cloned repository, removing the disk space savings of clone -s. It is safe, however, to run git gc, which uses the -l option by default.

If you want to break the dependency of a repository cloned with -s on its source repository, you can simply run git repack -a to copy all objects from the source repository into a pack in the cloned repository.

--reference[-if-able] <repository>
If the reference repository is on the local machine, automatically setup .git/objects/info/alternates to obtain objects from the reference repository. Using an already existing repository as an alternate will require fewer objects to be copied from the repository being cloned, reducing network and local storage costs. When using the --reference-if-able, a non existing directory is skipped with a warning instead of aborting the clone.

NOTE: see the NOTE for the --shared option, and also the --dissociate option.

--dissociate
Borrow the objects from reference repositories specified with the --reference options only to reduce network transfer, and stop borrowing from them after a clone is made by making necessary local copies of borrowed objects. This option can also be used when cloning locally from a repository that already borrows objects from another repository—​the new repository will borrow objects from the same repository, and this option can be used to stop the borrowing.

--quiet
-q
Operate quietly. Progress is not reported to the standard error stream.

--verbose
-v
Run verbosely. Does not affect the reporting of progress status to the standard error stream.

--progress
Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

--no-checkout
-n
No checkout of HEAD is performed after the clone is complete.

--bare
Make a bare Git repository. That is, instead of creating <directory> and placing the administrative files in <directory>/.git, make the <directory> itself the $GIT_DIR. This obviously implies the -n because there is nowhere to check out the working tree. Also the branch heads at the remote are copied directly to corresponding local branch heads, without mapping them to refs/remotes/origin/. When this option is used, neither remote-tracking branches nor the related configuration variables are created.

--mirror
Set up a mirror of the source repository. This implies --bare. Compared to --bare, --mirror not only maps local branches of the source to local branches of the target, it maps all refs (including remote-tracking branches, notes etc.) and sets up a refspec configuration such that all these refs are overwritten by a git remote update in the target repository.

--origin <name>
-o <name>
Instead of using the remote name origin to keep track of the upstream repository, use <name>.

--branch <name>
-b <name>
Instead of pointing the newly created HEAD to the branch pointed to by the cloned repository’s HEAD, point to <name> branch instead. In a non-bare repository, this is the branch that will be checked out. --branch can also take tags and detaches the HEAD at that commit in the resulting repository.

--upload-pack <upload-pack>
-u <upload-pack>
When given, and the repository to clone from is accessed via ssh, this specifies a non-default path for the command run on the other end.

--template=<template_directory>
Specify the directory from which templates will be used; (See the "TEMPLATE DIRECTORY" section of git-init(1).)

--config <key>=<value>
-c <key>=<value>
Set a configuration variable in the newly-created repository; this takes effect immediately after the repository is initialized, but before the remote history is fetched or any files checked out. The key is in the same format as expected by git-config(1) (e.g., core.eol=true). If multiple values are given for the same key, each value will be written to the config file. This makes it safe, for example, to add additional fetch refspecs to the origin remote.

--depth <depth>
Create a shallow clone with a history truncated to the specified number of commits. Implies --single-branch unless --no-single-branch is given to fetch the histories near the tips of all branches. If you want to clone submodules shallowly, also pass --shallow-submodules.

--shallow-since=<date>
Create a shallow clone with a history after the specified time.

--shallow-exclude=<revision>
Create a shallow clone with a history, excluding commits reachable from a specified remote branch or tag. This option can be specified multiple times.

--[no-]single-branch
Clone only the history leading to the tip of a single branch, either specified by the --branch option or the primary branch remote’s HEAD points at. Further fetches into the resulting repository will only update the remote-tracking branch for the branch this option was used for the initial cloning. If the HEAD at the remote did not point at any branch when --single-branch clone was made, no remote-tracking branch is created.

--recursive
--recurse-submodules
After the clone is created, initialize all submodules within, using their default settings. This is equivalent to running git submodule update --init --recursive immediately after the clone is finished. This option is ignored if the cloned repository does not have a worktree/checkout (i.e. if any of --no-checkout/-n, --bare, or --mirror is given)

--[no-]shallow-submodules
All submodules which are cloned will be shallow with a depth of 1.

--separate-git-dir=<git dir>
Instead of placing the cloned repository where it is supposed to be, place the cloned repository at the specified directory, then make a filesystem-agnostic Git symbolic link to there. The result is Git repository can be separated from working tree.

-j <n>
--jobs <n>
The number of submodules fetched at the same time. Defaults to the submodule.fetchJobs option.

<repository>
The (possibly remote) repository to clone from. See the URLS section below for more information on specifying repositories.

<directory>
The name of a new directory to clone into. The "humanish" part of the source repository is used if no directory is explicitly given (repo for /path/to/repo.git and foo for host.xz:foo/.git). Cloning into an existing directory is only allowed if the directory is empty.
GIT URLS
In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching, but this is inefficient and deprecated; do not use it).

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

ssh://[user@]host.xz[:port]/path/to/repo.git/

git://host.xz[:port]/path/to/repo.git/

http[s]://host.xz[:port]/path/to/repo.git/

ftp[s]://host.xz[:port]/path/to/repo.git/

An alternative scp-like syntax may also be used with the ssh protocol:

[user@]host.xz:path/to/repo.git/

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path foo:bar could be specified as an absolute path or ./foo:bar to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support ~username expansion:

ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/

git://host.xz[:port]/~[user]/path/to/repo.git/

[user@]host.xz:/~[user]/path/to/repo.git/

For local repositories, also supported by Git natively, the following syntaxes may be used:

/path/to/repo.git/

file:///path/to/repo.git/

These two syntaxes are mostly equivalent, except the former implies --local option.

When Git doesn’t know how to handle a certain transport protocol, it attempts to use the remote-<transport> remote helper, if one exists. To explicitly request a remote helper, the following syntax may be used:

<transport>::<address>

where <address> may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being invoked. See gitremote-helpers(1) for details.

If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

	[url "<actual url base>"]
		insteadOf = <other url base>
For example, with this:

	[url "git://git.host.xz/"]
		insteadOf = host.xz:/path/to/
		insteadOf = work:
a URL like "work:repo.git" or like "host.xz:/path/to/repo.git" will be rewritten in any context that takes a URL to be "git://git.host.xz/repo.git".

If you want to rewrite URLs for push only, you can create a configuration section of the form:

	[url "<actual url base>"]
		pushInsteadOf = <other url base>
For example, with this:

	[url "ssh://example.org/"]
		pushInsteadOf = git://example.org/
a URL like "git://example.org/path/to/repo.git" will be rewritten to "ssh://example.org/path/to/repo.git" for pushes, but pulls will still use the original URL.

Examples
Clone from upstream:

$ git clone git://git.kernel.org/pub/scm/.../linux.git my-linux
$ cd my-linux
$ make
Make a local clone that borrows from the current directory, without checking things out:

$ git clone -l -s -n . ../copy
$ cd ../copy
$ git show-branch
Clone from upstream while borrowing from an existing local directory:

$ git clone --reference /git/linux.git \
	git://git.kernel.org/pub/scm/.../linux.git \
	my-linux
$ cd my-linux
Create a bare repository to publish your changes to the public:

$ git clone --bare -l /home/proj/.git /pub/scm/proj.git
GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

## git init
```sh
git-init(1) Manual Page
NAME
git-init - Create an empty Git repository or reinitialize an existing one

SYNOPSIS
git init [-q | --quiet] [--bare] [--template=<template_directory>]
	  [--separate-git-dir <git dir>]
	  [--shared[=<permissions>]] [directory]
DESCRIPTION
This command creates an empty Git repository - basically a .git directory with subdirectories for objects, refs/heads, refs/tags, and template files. An initial HEAD file that references the HEAD of the master branch is also created.

If the $GIT_DIR environment variable is set then it specifies a path to use instead of ./.git for the base of the repository.

If the object storage directory is specified via the $GIT_OBJECT_DIRECTORY environment variable then the sha1 directories are created underneath - otherwise the default $GIT_DIR/objects directory is used.

Running git init in an existing repository is safe. It will not overwrite things that are already there. The primary reason for rerunning git init is to pick up newly added templates (or to move the repository to another place if --separate-git-dir is given).

OPTIONS
-q
--quiet
Only print error and warning messages; all other output will be suppressed.

--bare
Create a bare repository. If GIT_DIR environment is not set, it is set to the current working directory.

--template=<template_directory>
Specify the directory from which templates will be used. (See the "TEMPLATE DIRECTORY" section below.)

--separate-git-dir=<git dir>
Instead of initializing the repository as a directory to either $GIT_DIR or ./.git/, create a text file there containing the path to the actual repository. This file acts as filesystem-agnostic Git symbolic link to the repository.

If this is reinitialization, the repository will be moved to the specified path.

--shared[=(false|true|umask|group|all|world|everybody|0xxx)]
Specify that the Git repository is to be shared amongst several users. This allows users belonging to the same group to push into that repository. When specified, the config variable "core.sharedRepository" is set so that files and directories under $GIT_DIR are created with the requested permissions. When not specified, Git will use permissions reported by umask(2).

The option can have the following values, defaulting to group if no value is given:

umask (or false)
Use permissions reported by umask(2). The default, when --shared is not specified.

group (or true)
Make the repository group-writable, (and g+sx, since the git group may be not the primary group of all users). This is used to loosen the permissions of an otherwise safe umask(2) value. Note that the umask still applies to the other permission bits (e.g. if umask is 0022, using group will not remove read privileges from other (non-group) users). See 0xxx for how to exactly specify the repository permissions.

all (or world or everybody)
Same as group, but make the repository readable by all users.

0xxx
0xxx is an octal number and each file will have mode 0xxx. 0xxx will override users' umask(2) value (and not only loosen permissions as group and all does). 0640 will create a repository which is group-readable, but not group-writable or accessible to others. 0660 will create a repo that is readable and writable to the current user and group, but inaccessible to others.
By default, the configuration flag receive.denyNonFastForwards is enabled in shared repositories, so that you cannot force a non fast-forwarding push into it.

If you provide a directory, the command is run inside it. If this directory does not exist, it will be created.

TEMPLATE DIRECTORY
The template directory contains files and directories that will be copied to the $GIT_DIR after it is created.

The template directory will be one of the following (in order):

the argument given with the --template option;

the contents of the $GIT_TEMPLATE_DIR environment variable;

the init.templateDir configuration variable; or

the default template directory: /usr/share/git-core/templates.

The default template directory includes some directory structure, suggested "exclude patterns" (see gitignore(5)), and sample hook files.

The sample hooks are all disabled by default, To enable one of the sample hooks rename it by removing its .sample suffix.

See githooks(5) for more general info on hook execution.

EXAMPLES
Start a new Git repository for an existing code base
$ cd /path/to/my/codebase
$ git init      (1)
$ git add .     (2)
$ git commit    (3)
Create a /path/to/my/codebase/.git directory.

Add all existing files to the index.

Record the pristine state as the first commit in the history.
```

## git add
```sh
git-add(1) Manual Page
NAME
git-add - Add file contents to the index

SYNOPSIS
git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
	  [--edit | -e] [--[no-]all | --[no-]ignore-removal | [--update | -u]]
	  [--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing]
	  [--chmod=(+|-)x] [--] [<pathspec>…​]
DESCRIPTION
This command updates the index using the current content found in the working tree, to prepare the content staged for the next commit. It typically adds the current content of existing paths as a whole, but with some options it can also be used to add content with only part of the changes made to the working tree files applied, or remove paths that do not exist in the working tree anymore.

The "index" holds a snapshot of the content of the working tree, and it is this snapshot that is taken as the contents of the next commit. Thus after making any changes to the working tree, and before running the commit command, you must use the add command to add any new or modified files to the index.

This command can be performed multiple times before a commit. It only adds the content of the specified file(s) at the time the add command is run; if you want subsequent changes included in the next commit, then you must run git add again to add the new content to the index.

The git status command can be used to obtain a summary of which files have changes that are staged for the next commit.

The git add command will not add ignored files by default. If any ignored files were explicitly specified on the command line, git add will fail with a list of ignored files. Ignored files reached by directory recursion or filename globbing performed by Git (quote your globs before the shell) will be silently ignored. The git add command can be used to add ignored files with the -f (force) option.

Please see git-commit(1) for alternative ways to add content to a commit.

OPTIONS
<pathspec>…​
Files to add content from. Fileglobs (e.g. *.c) can be given to add all matching files. Also a leading directory name (e.g. dir to add dir/file1 and dir/file2) can be given to update the index to match the current state of the directory as a whole (e.g. specifying dir will record not just a file dir/file1 modified in the working tree, a file dir/file2 added to the working tree, but also a file dir/file3 removed from the working tree. Note that older versions of Git used to ignore removed files; use --no-all option if you want to add modified or new files but ignore removed	ones.

-n
--dry-run
Don’t actually add the file(s), just show if they exist and/or will be ignored.

-v
--verbose
Be verbose.

-f
--force
Allow adding otherwise ignored files.

-i
--interactive
Add modified contents in the working tree interactively to the index. Optional path arguments may be supplied to limit operation to a subset of the working tree. See “Interactive mode” for details.

-p
--patch
Interactively choose hunks of patch between the index and the work tree and add them to the index. This gives the user a chance to review the difference before adding modified contents to the index.

This effectively runs add --interactive, but bypasses the initial command menu and directly jumps to the patch subcommand. See “Interactive mode” for details.

-e
--edit
Open the diff vs. the index in an editor and let the user edit it. After the editor was closed, adjust the hunk headers and apply the patch to the index.

The intent of this option is to pick and choose lines of the patch to apply, or even to modify the contents of lines to be staged. This can be quicker and more flexible than using the interactive hunk selector. However, it is easy to confuse oneself and create a patch that does not apply to the index. See EDITING PATCHES below.

-u
--update
Update the index just where it already has an entry matching <pathspec>. This removes as well as modifies index entries to match the working tree, but adds no new files.

If no <pathspec> is given when -u option is used, all tracked files in the entire working tree are updated (old versions of Git used to limit the update to the current directory and its subdirectories).

-A
--all
--no-ignore-removal
Update the index not only where the working tree has a file matching <pathspec> but also where the index already has an entry.	This adds, modifies, and removes index entries to match the working tree.

If no <pathspec> is given when -A option is used, all files in the entire working tree are updated (old versions of Git used to limit the update to the current directory and its subdirectories).

--no-all
--ignore-removal
Update the index by adding new files that are unknown to the index and files modified in the working tree, but ignore files that have been removed from the working tree. This option is a no-op when no <pathspec> is used.

This option is primarily to help users who are used to older versions of Git, whose "git add <pathspec>…​" was a synonym for "git add --no-all <pathspec>…​", i.e. ignored removed files.

-N
--intent-to-add
Record only the fact that the path will be added later. An entry for the path is placed in the index with no content. This is useful for, among other things, showing the unstaged content of such files with git diff and committing them with git commit -a.

--refresh
Don’t add the file(s), but only refresh their stat() information in the index.

--ignore-errors
If some files could not be added because of errors indexing them, do not abort the operation, but continue adding the others. The command shall still exit with non-zero status. The configuration variable add.ignoreErrors can be set to true to make this the default behaviour.

--ignore-missing
This option can only be used together with --dry-run. By using this option the user can check if any of the given files would be ignored, no matter if they are already present in the work tree or not.

--chmod=(+|-)x
Override the executable bit of the added files. The executable bit is only changed in the index, the files on disk are left unchanged.

--
This option can be used to separate command-line options from the list of files, (useful when filenames might be mistaken for command-line options).
Configuration
The optional configuration variable core.excludesFile indicates a path to a file containing patterns of file names to exclude from git-add, similar to $GIT_DIR/info/exclude. Patterns in the exclude file are used in addition to those in info/exclude. See gitignore(5).

EXAMPLES
Adds content from all *.txt files under Documentation directory and its subdirectories:

$ git add Documentation/\*.txt
Note that the asterisk * is quoted from the shell in this example; this lets the command include the files from subdirectories of Documentation/ directory.

Considers adding content from all git-*.sh scripts:

$ git add git-*.sh
Because this example lets the shell expand the asterisk (i.e. you are listing the files explicitly), it does not consider subdir/git-foo.sh.

Interactive mode
When the command enters the interactive mode, it shows the output of the status subcommand, and then goes into its interactive command loop.

The command loop shows the list of subcommands available, and gives a prompt "What now> ". In general, when the prompt ends with a single >, you can pick only one of the choices given and type return, like this:

    *** Commands ***
      1: status       2: update       3: revert       4: add untracked
      5: patch        6: diff         7: quit         8: help
    What now> 1
You also could say s or sta or status above as long as the choice is unique.

The main command loop has 6 subcommands (plus help and quit).

status
This shows the change between HEAD and index (i.e. what will be committed if you say git commit), and between index and working tree files (i.e. what you could stage further before git commit using git add) for each path. A sample output looks like this:

              staged     unstaged path
     1:       binary      nothing foo.png
     2:     +403/-35        +1/-1 git-add--interactive.perl
It shows that foo.png has differences from HEAD (but that is binary so line count cannot be shown) and there is no difference between indexed copy and the working tree version (if the working tree version were also different, binary would have been shown in place of nothing). The other file, git-add--interactive.perl, has 403 lines added and 35 lines deleted if you commit what is in the index, but working tree file has further modifications (one addition and one deletion).

update
This shows the status information and issues an "Update>>" prompt. When the prompt ends with double >>, you can make more than one selection, concatenated with whitespace or comma. Also you can say ranges. E.g. "2-5 7,9" to choose 2,3,4,5,7,9 from the list. If the second number in a range is omitted, all remaining patches are taken. E.g. "7-" to choose 7,8,9 from the list. You can say * to choose everything.

What you chose are then highlighted with *, like this:

           staged     unstaged path
  1:       binary      nothing foo.png
* 2:     +403/-35        +1/-1 git-add--interactive.perl
To remove selection, prefix the input with - like this:

Update>> -2
After making the selection, answer with an empty line to stage the contents of working tree files for selected paths in the index.

revert
This has a very similar UI to update, and the staged information for selected paths are reverted to that of the HEAD version. Reverting new paths makes them untracked.

add untracked
This has a very similar UI to update and revert, and lets you add untracked paths to the index.

patch
This lets you choose one path out of a status like selection. After choosing the path, it presents the diff between the index and the working tree file and asks you if you want to stage the change of each hunk. You can select one of the following options and type return:

y - stage this hunk
n - do not stage this hunk
q - quit; do not stage this hunk or any of the remaining ones
a - stage this hunk and all later hunks in the file
d - do not stage this hunk or any of the later hunks in the file
g - select a hunk to go to
/ - search for a hunk matching the given regex
j - leave this hunk undecided, see next undecided hunk
J - leave this hunk undecided, see next hunk
k - leave this hunk undecided, see previous undecided hunk
K - leave this hunk undecided, see previous hunk
s - split the current hunk into smaller hunks
e - manually edit the current hunk
? - print help
After deciding the fate for all hunks, if there is any hunk that was chosen, the index is updated with the selected hunks.

You can omit having to type return here, by setting the configuration variable interactive.singleKey to true.

diff
This lets you review what will be committed (i.e. between HEAD and index).
EDITING PATCHES
Invoking git add -e or selecting e from the interactive hunk selector will open a patch in your editor; after the editor exits, the result is applied to the index. You are free to make arbitrary changes to the patch, but note that some changes may have confusing results, or even result in a patch that cannot be applied. If you want to abort the operation entirely (i.e., stage nothing new in the index), simply delete all lines of the patch. The list below describes some common things you may see in a patch, and which editing operations make sense on them.

added content
Added content is represented by lines beginning with "+". You can prevent staging any addition lines by deleting them.

removed content
Removed content is represented by lines beginning with "-". You can prevent staging their removal by converting the "-" to a " " (space).

modified content
Modified content is represented by "-" lines (removing the old content) followed by "+" lines (adding the replacement content). You can prevent staging the modification by converting "-" lines to " ", and removing "+" lines. Beware that modifying only half of the pair is likely to introduce confusing changes to the index.
There are also more complex operations that can be performed. But beware that because the patch is applied only to the index and not the working tree, the working tree will appear to "undo" the change in the index. For example, introducing a new line into the index that is in neither the HEAD nor the working tree will stage the new line for commit, but the line will appear to be reverted in the working tree.

Avoid using these constructs, or do so with extreme caution.

removing untouched content
Content which does not differ between the index and working tree may be shown on context lines, beginning with a " " (space). You can stage context lines for removal by converting the space to a "-". The resulting working tree file will appear to re-add the content.

modifying existing content
One can also modify context lines by staging them for removal (by converting " " to "-") and adding a "+" line with the new content. Similarly, one can modify "+" lines for existing additions or modifications. In all cases, the new modification will appear reverted in the working tree.

new content
You may also add new content that does not exist in the patch; simply add new lines, each starting with "+". The addition will appear reverted in the working tree.
There are also several operations which should be avoided entirely, as they will make the patch impossible to apply:

adding context (" ") or removal ("-") lines

deleting context or removal lines

modifying the contents of context or removal lines

SEE ALSO
git-status(1) git-rm(1) git-reset(1) git-mv(1) git-commit(1) git-update-index(1)

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

## git mv
```sh
git-mv(1) Manual Page
NAME
git-mv - Move or rename a file, a directory, or a symlink

SYNOPSIS
git mv <options>…​ <args>…​
DESCRIPTION
Move or rename a file, directory or symlink.

git mv [-v] [-f] [-n] [-k] <source> <destination>
git mv [-v] [-f] [-n] [-k] <source> ... <destination directory>
In the first form, it renames <source>, which must exist and be either a file, symlink or directory, to <destination>. In the second form, the last argument has to be an existing directory; the given sources will be moved into this directory.

The index is updated after successful completion, but the change must still be committed.

OPTIONS
-f
--force
Force renaming or moving of a file even if the target exists

-k
Skip move or rename actions which would lead to an error condition. An error happens when a source is neither existing nor controlled by Git, or when it would overwrite an existing file unless -f is given.

-n
--dry-run
Do nothing; only show what would happen

-v
--verbose
Report the names of files as they are moved.
SUBMODULES
Moving a submodule using a gitfile (which means they were cloned with a Git version 1.7.8 or newer) will update the gitfile and core.worktree setting to make the submodule work in the new location. It also will attempt to update the submodule.<name>.path setting in the gitmodules(5) file and stage that file (unless -n is used).

BUGS
Each time a superproject update moves a populated submodule (e.g. when switching between commits before and after the move) a stale submodule checkout will remain in the old location and an empty directory will appear in the new location. To populate the submodule again in the new location the user will have to run "git submodule update" afterwards. Removing the old directory is only safe when it uses a gitfile, as otherwise the history of the submodule will be deleted too. Both steps will be obsolete when recursive submodule update has been implemented.

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

## git status
```sh
git-status(1) Manual Page
NAME
git-status - Show the working tree status

SYNOPSIS
git status [<options>…​] [--] [<pathspec>…​]
DESCRIPTION
Displays paths that have differences between the index file and the current HEAD commit, paths that have differences between the working tree and the index file, and paths in the working tree that are not tracked by Git (and are not ignored by gitignore(5)). The first are what you would commit by running git commit; the second and third are what you could commit by running git add before running git commit.

OPTIONS
-s
--short
Give the output in the short-format.

-b
--branch
Show the branch and tracking info even in short-format.

--porcelain[=<version>]
Give the output in an easy-to-parse format for scripts. This is similar to the short output, but will remain stable across Git versions and regardless of user configuration. See below for details.

The version parameter is used to specify the format version. This is optional and defaults to the original version v1 format.

--long
Give the output in the long-format. This is the default.

-v
--verbose
In addition to the names of files that have been changed, also show the textual changes that are staged to be committed (i.e., like the output of git diff --cached). If -v is specified twice, then also show the changes in the working tree that have not yet been staged (i.e., like the output of git diff).

-u[<mode>]
--untracked-files[=<mode>]
Show untracked files.

The mode parameter is used to specify the handling of untracked files. It is optional: it defaults to all, and if specified, it must be stuck to the option (e.g. -uno, but not -u no).

The possible options are:

no - Show no untracked files.

normal - Shows untracked files and directories.

all - Also shows individual files in untracked directories.

When -u option is not used, untracked files and directories are shown (i.e. the same as specifying normal), to help you avoid forgetting to add newly created files. Because it takes extra work to find untracked files in the filesystem, this mode may take some time in a large working tree. Consider enabling untracked cache and split index if supported (see git update-index --untracked-cache and git update-index --split-index), Otherwise you can use no to have git status return more quickly without showing untracked files.

The default can be changed using the status.showUntrackedFiles configuration variable documented in git-config(1).

--ignore-submodules[=<when>]
Ignore changes to submodules when looking for changes. <when> can be either "none", "untracked", "dirty" or "all", which is the default. Using "none" will consider the submodule modified when it either contains untracked or modified files or its HEAD differs from the commit recorded in the superproject and can be used to override any settings of the ignore option in git-config(1) or gitmodules(5). When "untracked" is used submodules are not considered dirty when they only contain untracked content (but they are still scanned for modified content). Using "dirty" ignores all changes to the work tree of submodules, only changes to the commits stored in the superproject are shown (this was the behavior before 1.7.0). Using "all" hides all changes to submodules (and suppresses the output of submodule summaries when the config option status.submoduleSummary is set).

--ignored
Show ignored files as well.

-z
Terminate entries with NUL, instead of LF. This implies the --porcelain=v1 output format if no other format is given.

--column[=<options>]
--no-column
Display untracked files in columns. See configuration variable column.status for option syntax.--column and --no-column without options are equivalent to always and never respectively.

--no-lock-index
--lock-index
Specifies whether git status should try to lock the index and update it afterwards if any changes were detected. Defaults to --lock-index.
OUTPUT
The output from this command is designed to be used as a commit template comment. The default, long format, is designed to be human readable, verbose and descriptive. Its contents and format are subject to change at any time.

The paths mentioned in the output, unlike many other Git commands, are made relative to the current directory if you are working in a subdirectory (this is on purpose, to help cutting and pasting). See the status.relativePaths config option below.

Short Format
In the short-format, the status of each path is shown as

XY PATH1 -> PATH2
where PATH1 is the path in the HEAD, and the " -> PATH2" part is shown only when PATH1 corresponds to a different path in the index/worktree (i.e. the file is renamed). The XY is a two-letter status code.

The fields (including the ->) are separated from each other by a single space. If a filename contains whitespace or other nonprintable characters, that field will be quoted in the manner of a C string literal: surrounded by ASCII double quote (34) characters, and with interior special characters backslash-escaped.

For paths with merge conflicts, X and Y show the modification states of each side of the merge. For paths that do not have merge conflicts, X shows the status of the index, and Y shows the status of the work tree. For untracked paths, XY are ??. Other status codes can be interpreted as follows:

' ' = unmodified

M = modified

A = added

D = deleted

R = renamed

C = copied

U = updated but unmerged

Ignored files are not listed, unless --ignored option is in effect, in which case XY are !!.

X          Y     Meaning
-------------------------------------------------
          [MD]   not updated
M        [ MD]   updated in index
A        [ MD]   added to index
D         [ M]   deleted from index
R        [ MD]   renamed in index
C        [ MD]   copied in index
[MARC]           index and work tree matches
[ MARC]     M    work tree changed since index
[ MARC]     D    deleted in work tree
-------------------------------------------------
D           D    unmerged, both deleted
A           U    unmerged, added by us
U           D    unmerged, deleted by them
U           A    unmerged, added by them
D           U    unmerged, deleted by us
A           A    unmerged, both added
U           U    unmerged, both modified
-------------------------------------------------
?           ?    untracked
!           !    ignored
-------------------------------------------------
If -b is used the short-format status is preceded by a line

## branchname tracking info
Porcelain Format Version 1
Version 1 porcelain format is similar to the short format, but is guaranteed not to change in a backwards-incompatible way between Git versions or based on user configuration. This makes it ideal for parsing by scripts. The description of the short format above also describes the porcelain format, with a few exceptions:

The user’s color.status configuration is not respected; color will always be off.

The user’s status.relativePaths configuration is not respected; paths shown will always be relative to the repository root.

There is also an alternate -z format recommended for machine parsing. In that format, the status field is the same, but some other things change. First, the -> is omitted from rename entries and the field order is reversed (e.g from -> to becomes to from). Second, a NUL (ASCII 0) follows each filename, replacing space as a field separator and the terminating newline (but a space still separates the status field from the first filename). Third, filenames containing special characters are not specially formatted; no quoting or backslash-escaping is performed.

Porcelain Format Version 2
Version 2 format adds more detailed information about the state of the worktree and changed items. Version 2 also defines an extensible set of easy to parse optional headers.

Header lines start with "#" and are added in response to specific command line arguments. Parsers should ignore headers they don’t recognize.

Branch Headers
If --branch is given, a series of header lines are printed with information about the current branch.

Line                                     Notes
------------------------------------------------------------
# branch.oid <commit> | (initial)        Current commit.
# branch.head <branch> | (detached)      Current branch.
# branch.upstream <upstream_branch>      If upstream is set.
# branch.ab +<ahead> -<behind>           If upstream is set and
	     the commit is present.
------------------------------------------------------------
Changed Tracked Entries
Following the headers, a series of lines are printed for tracked entries. One of three different line formats may be used to describe an entry depending on the type of change. Tracked entries are printed in an undefined order; parsers should allow for a mixture of the 3 line types in any order.

Ordinary changed entries have the following format:

1 <XY> <sub> <mH> <mI> <mW> <hH> <hI> <path>
Renamed or copied entries have the following format:

2 <XY> <sub> <mH> <mI> <mW> <hH> <hI> <X><score> <path><sep><origPath>
  Field       Meaning
  --------------------------------------------------------
  <XY>        A 2 character field containing the staged and
unstaged XY values described in the short format,
with unchanged indicated by a "." rather than
a space.
  <sub>       A 4 character field describing the submodule state.
"N..." when the entry is not a submodule.
"S<c><m><u>" when the entry is a submodule.
<c> is "C" if the commit changed; otherwise ".".
<m> is "M" if it has tracked changes; otherwise ".".
<u> is "U" if there are untracked changes; otherwise ".".
  <mH>        The octal file mode in HEAD.
  <mI>        The octal file mode in the index.
  <mW>        The octal file mode in the worktree.
  <hH>        The object name in HEAD.
  <hI>        The object name in the index.
  <X><score>  The rename or copy score (denoting the percentage
of similarity between the source and target of the
move or copy). For example "R100" or "C75".
  <path>      The pathname.  In a renamed/copied entry, this
is the path in the index and in the working tree.
  <sep>       When the `-z` option is used, the 2 pathnames are separated
with a NUL (ASCII 0x00) byte; otherwise, a tab (ASCII 0x09)
byte separates them.
  <origPath>  The pathname in the commit at HEAD.  This is only
present in a renamed/copied entry, and tells
where the renamed/copied contents came from.
  --------------------------------------------------------
Unmerged entries have the following format; the first character is a "u" to distinguish from ordinary changed entries.

u <xy> <sub> <m1> <m2> <m3> <mW> <h1> <h2> <h3> <path>
  Field       Meaning
  --------------------------------------------------------
  <XY>        A 2 character field describing the conflict type
as described in the short format.
  <sub>       A 4 character field describing the submodule state
as described above.
  <m1>        The octal file mode in stage 1.
  <m2>        The octal file mode in stage 2.
  <m3>        The octal file mode in stage 3.
  <mW>        The octal file mode in the worktree.
  <h1>        The object name in stage 1.
  <h2>        The object name in stage 2.
  <h3>        The object name in stage 3.
  <path>      The pathname.
  --------------------------------------------------------
Other Items
Following the tracked entries (and if requested), a series of lines will be printed for untracked and then ignored items found in the worktree.

Untracked items have the following format:

? <path>
Ignored items have the following format:

! <path>
Pathname Format Notes and -z
When the -z option is given, pathnames are printed as is and without any quoting and lines are terminated with a NUL (ASCII 0x00) byte.

Otherwise, all pathnames will be "C-quoted" if they contain any tab, linefeed, double quote, or backslash characters. In C-quoting, these characters will be replaced with the corresponding C-style escape sequences and the resulting pathname will be double quoted.

CONFIGURATION
The command honors color.status (or status.color — they mean the same thing and the latter is kept for backward compatibility) and color.status.<slot> configuration variables to colorize its output.

If the config variable status.relativePaths is set to false, then all paths shown are relative to the repository root, not to the current directory.

If status.submoduleSummary is set to a non zero number or true (identical to -1 or an unlimited number), the submodule summary will be enabled for the long format and a summary of commits for modified submodules will be shown (see --summary-limit option of git-submodule(1)). Please note that the summary output from the status command will be suppressed for all submodules when diff.ignoreSubmodules is set to all or only for those submodules where submodule.<name>.ignore=all. To also view the summary for ignored submodules you can either use the --ignore-submodules=dirty command line option or the git submodule summary command, which shows a similar output but does not honor these settings.

SEE ALSO
gitignore(5)

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

## git branch
```sh
git-branch(1) Manual Page
NAME
git-branch - List, create, or delete branches

SYNOPSIS
git branch [--color[=<when>] | --no-color] [-r | -a]
	[--list] [-v [--abbrev=<length> | --no-abbrev]]
	[--column[=<options>] | --no-column]
	[(--merged | --no-merged | --contains) [<commit>]] [--sort=<key>]
	[--points-at <object>] [<pattern>…​]
git branch [--set-upstream | --track | --no-track] [-l] [-f] <branchname> [<start-point>]
git branch (--set-upstream-to=<upstream> | -u <upstream>) [<branchname>]
git branch --unset-upstream [<branchname>]
git branch (-m | -M) [<oldbranch>] <newbranch>
git branch (-d | -D) [-r] <branchname>…​
git branch --edit-description [<branchname>]
DESCRIPTION
If --list is given, or if there are no non-option arguments, existing branches are listed; the current branch will be highlighted with an asterisk. Option -r causes the remote-tracking branches to be listed, and option -a shows both local and remote branches. If a <pattern> is given, it is used as a shell wildcard to restrict the output to matching branches. If multiple patterns are given, a branch is shown if it matches any of the patterns. Note that when providing a <pattern>, you must use --list; otherwise the command is interpreted as branch creation.

With --contains, shows only the branches that contain the named commit (in other words, the branches whose tip commits are descendants of the named commit). With --merged, only branches merged into the named commit (i.e. the branches whose tip commits are reachable from the named commit) will be listed. With --no-merged only branches not merged into the named commit will be listed. If the <commit> argument is missing it defaults to HEAD (i.e. the tip of the current branch).

The command’s second form creates a new branch head named <branchname> which points to the current HEAD, or <start-point> if given.

Note that this will create the new branch, but it will not switch the working tree to it; use "git checkout <newbranch>" to switch to the new branch.

When a local branch is started off a remote-tracking branch, Git sets up the branch (specifically the branch.<name>.remote and branch.<name>.merge configuration entries) so that git pull will appropriately merge from the remote-tracking branch. This behavior may be changed via the global branch.autoSetupMerge configuration flag. That setting can be overridden by using the --track and --no-track options, and changed later using git branch --set-upstream-to.

With a -m or -M option, <oldbranch> will be renamed to <newbranch>. If <oldbranch> had a corresponding reflog, it is renamed to match <newbranch>, and a reflog entry is created to remember the branch renaming. If <newbranch> exists, -M must be used to force the rename to happen.

With a -d or -D option, <branchname> will be deleted. You may specify more than one branch for deletion. If the branch currently has a reflog then the reflog will also be deleted.

Use -r together with -d to delete remote-tracking branches. Note, that it only makes sense to delete remote-tracking branches if they no longer exist in the remote repository or if git fetch was configured not to fetch them again. See also the prune subcommand of git-remote(1) for a way to clean up all obsolete remote-tracking branches.

OPTIONS
-d
--delete
Delete a branch. The branch must be fully merged in its upstream branch, or in HEAD if no upstream was set with --track or --set-upstream.

-D
Shortcut for --delete --force.

-l
--create-reflog
Create the branch’s reflog. This activates recording of all changes made to the branch ref, enabling use of date based sha1 expressions such as "<branchname>@{yesterday}". Note that in non-bare repositories, reflogs are usually enabled by default by the core.logallrefupdates config option.

-f
--force
Reset <branchname> to <startpoint> if <branchname> exists already. Without -f git branch refuses to change an existing branch. In combination with -d (or --delete), allow deleting the branch irrespective of its merged status. In combination with -m (or --move), allow renaming the branch even if the new branch name already exists.

-m
--move
Move/rename a branch and the corresponding reflog.

-M
Shortcut for --move --force.

--color[=<when>]
Color branches to highlight current, local, and remote-tracking branches. The value must be always (the default), never, or auto.

--no-color
Turn off branch colors, even when the configuration file gives the default to color output. Same as --color=never.

--column[=<options>]
--no-column
Display branch listing in columns. See configuration variable column.branch for option syntax.--column and --no-column without options are equivalent to always and never respectively.

This option is only applicable in non-verbose mode.

-r
--remotes
List or delete (if used with -d) the remote-tracking branches.

-a
--all
List both remote-tracking branches and local branches.

--list
Activate the list mode. git branch <pattern> would try to create a branch, use git branch --list <pattern> to list matching branches.

-v
-vv
--verbose
When in list mode, show sha1 and commit subject line for each head, along with relationship to upstream branch (if any). If given twice, print the name of the upstream branch, as well (see also git remote show <remote>).

-q
--quiet
Be more quiet when creating or deleting a branch, suppressing non-error messages.

--abbrev=<length>
Alter the sha1’s minimum display length in the output listing. The default value is 7 and can be overridden by the core.abbrev config option.

--no-abbrev
Display the full sha1s in the output listing rather than abbreviating them.

-t
--track
When creating a new branch, set up branch.<name>.remote and branch.<name>.merge configuration entries to mark the start-point branch as "upstream" from the new branch. This configuration will tell git to show the relationship between the two branches in git status and git branch -v. Furthermore, it directs git pull without arguments to pull from the upstream when the new branch is checked out.

This behavior is the default when the start point is a remote-tracking branch. Set the branch.autoSetupMerge configuration variable to false if you want git checkout and git branch to always behave as if --no-track were given. Set it to always if you want this behavior when the start-point is either a local or remote-tracking branch.

--no-track
Do not set up "upstream" configuration, even if the branch.autoSetupMerge configuration variable is true.

--set-upstream
If specified branch does not exist yet or if --force has been given, acts exactly like --track. Otherwise sets up configuration like --track would when creating the branch, except that where branch points to is not changed.

-u <upstream>
--set-upstream-to=<upstream>
Set up <branchname>'s tracking information so <upstream> is considered <branchname>'s upstream branch. If no <branchname> is specified, then it defaults to the current branch.

--unset-upstream
Remove the upstream information for <branchname>. If no branch is specified it defaults to the current branch.

--edit-description
Open an editor and edit the text to explain what the branch is for, to be used by various other commands (e.g. format-patch, request-pull, and merge (if enabled)). Multi-line explanations may be used.

--contains [<commit>]
Only list branches which contain the specified commit (HEAD if not specified). Implies --list.

--merged [<commit>]
Only list branches whose tips are reachable from the specified commit (HEAD if not specified). Implies --list.

--no-merged [<commit>]
Only list branches whose tips are not reachable from the specified commit (HEAD if not specified). Implies --list.

<branchname>
The name of the branch to create or delete. The new branch name must pass all checks defined by git-check-ref-format(1). Some of these checks may restrict the characters allowed in a branch name.

<start-point>
The new branch head will point to this commit. It may be given as a branch name, a commit-id, or a tag. If this option is omitted, the current HEAD will be used instead.

<oldbranch>
The name of an existing branch to rename.

<newbranch>
The new name for an existing branch. The same restrictions as for <branchname> apply.

--sort=<key>
Sort based on the key given. Prefix - to sort in descending order of the value. You may use the --sort=<key> option multiple times, in which case the last key becomes the primary key. The keys supported are the same as those in git for-each-ref. Sort order defaults to sorting based on the full refname (including refs/... prefix). This lists detached HEAD (if present) first, then local branches and finally remote-tracking branches.

--points-at <object>
Only list branches of the given object.
Examples
Start development from a known tag
$ git clone git://git.kernel.org/pub/scm/.../linux-2.6 my2.6
$ cd my2.6
$ git branch my2.6.14 v2.6.14   (1)
$ git checkout my2.6.14
This step and the next one could be combined into a single step with "checkout -b my2.6.14 v2.6.14".

Delete an unneeded branch
$ git clone git://git.kernel.org/.../git.git my.git
$ cd my.git
$ git branch -d -r origin/todo origin/html origin/man   (1)
$ git branch -D test                                    (2)
Delete the remote-tracking branches "todo", "html" and "man". The next fetch or pull will create them again unless you configure them not to. See git-fetch(1).

Delete the "test" branch even if the "master" branch (or whichever branch is currently checked out) does not have all commits from the test branch.

Notes
If you are creating a branch that you want to checkout immediately, it is easier to use the git checkout command with its -b option to create a branch and check it out with a single command.

The options --contains, --merged and --no-merged serve three related but different purposes:

--contains <commit> is used to find all branches which will need special attention if <commit> were to be rebased or amended, since those branches contain the specified <commit>.

--merged is used to find all branches which can be safely deleted, since those branches are fully contained by HEAD.

--no-merged is used to find branches which are candidates for merging into HEAD, since those branches are not fully contained by HEAD.

SEE ALSO
git-check-ref-format(1), git-fetch(1), git-remote(1), “Understanding history: What is a branch?” in the Git User’s Manual.

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

### git checkout
```sh
git-checkout(1) Manual Page
NAME
git-checkout - Switch branches or restore working tree files

SYNOPSIS
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] [--] <paths>…​
git checkout [-p|--patch] [<tree-ish>] [--] [<paths>…​]
DESCRIPTION
Updates files in the working tree to match the version in the index or the specified tree. If no paths are given, git checkout will also update HEAD to set the specified branch as the current branch.

git checkout <branch>
To prepare for working on <branch>, switch to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the <branch>.

If <branch> is not found but there does exist a tracking branch in exactly one remote (call it <remote>) with a matching name, treat as equivalent to

$ git checkout -b <branch> --track <remote>/<branch>
You could omit <branch>, in which case the command degenerates to "check out the current branch", which is a glorified no-op with a rather expensive side-effects to show only the tracking information, if exists, for the current branch.

git checkout -b|-B <new_branch> [<start point>]
Specifying -b causes a new branch to be created as if git-branch(1) were called and then checked out. In this case you can use the --track or --no-track options, which will be passed to git branch. As a convenience, --track without -b implies branch creation; see the description of --track below.

If -B is given, <new_branch> is created if it doesn’t exist; otherwise, it is reset. This is the transactional equivalent of

$ git branch -f <branch> [<start point>]
$ git checkout <branch>
that is to say, the branch is not reset/created unless "git checkout" is successful.

git checkout --detach [<branch>]
git checkout [--detach] <commit>
Prepare to work on top of <commit>, by detaching HEAD at it (see "DETACHED HEAD" section), and updating the index and the files in the working tree. Local modifications to the files in the working tree are kept, so that the resulting working tree will be the state recorded in the commit plus the local modifications.

When the <commit> argument is a branch name, the --detach option can be used to detach HEAD at the tip of the branch (git checkout <branch> would check out that branch without detaching HEAD).

Omitting <branch> detaches HEAD at the tip of the current branch.

git checkout [-p|--patch] [<tree-ish>] [--] <pathspec>…​
When <paths> or --patch are given, git checkout does not switch branches. It updates the named paths in the working tree from the index file or from a named <tree-ish> (most often a commit). In this case, the -b and --track options are meaningless and giving either of them results in an error. The <tree-ish> argument can be used to specify a specific tree-ish (i.e. commit, tag or tree) to update the index for the given paths before updating the working tree.

git checkout with <paths> or --patch is used to restore modified or deleted paths to their original contents from the index or replace paths with the contents from a named <tree-ish> (most often a commit-ish).

The index may contain unmerged entries because of a previous failed merge. By default, if you try to check out such an entry from the index, the checkout operation will fail and nothing will be checked out. Using -f will ignore these unmerged entries. The contents from a specific side of the merge can be checked out of the index by using --ours or --theirs. With -m, changes made to the working tree file can be discarded to re-create the original conflicted merge result.

OPTIONS
-q
--quiet
Quiet, suppress feedback messages.

--[no-]progress
Progress status is reported on the standard error stream by default when it is attached to a terminal, unless --quiet is specified. This flag enables progress reporting even if not attached to a terminal, regardless of --quiet.

-f
--force
When switching branches, proceed even if the index or the working tree differs from HEAD. This is used to throw away local changes.

When checking out paths from the index, do not fail upon unmerged entries; instead, unmerged entries are ignored.

--ours
--theirs
When checking out paths from the index, check out stage #2 (ours) or #3 (theirs) for unmerged paths.

Note that during git rebase and git pull --rebase, ours and theirs may appear swapped; --ours gives the version from the branch the changes are rebased onto, while --theirs gives the version from the branch that holds your work that is being rebased.

This is because rebase is used in a workflow that treats the history at the remote as the shared canonical one, and treats the work done on the branch you are rebasing as the third-party work to be integrated, and you are temporarily assuming the role of the keeper of the canonical history during the rebase. As the keeper of the canonical history, you need to view the history from the remote as ours (i.e. "our shared canonical history"), while what you did on your side branch as theirs (i.e. "one contributor’s work on top of it").

-b <new_branch>
Create a new branch named <new_branch> and start it at <start_point>; see git-branch(1) for details.

-B <new_branch>
Creates the branch <new_branch> and start it at <start_point>; if it already exists, then reset it to <start_point>. This is equivalent to running "git branch" with "-f"; see git-branch(1) for details.

-t
--track
When creating a new branch, set up "upstream" configuration. See "--track" in git-branch(1) for details.

If no -b option is given, the name of the new branch will be derived from the remote-tracking branch, by looking at the local part of the refspec configured for the corresponding remote, and then stripping the initial part up to the "*". This would tell us to use "hack" as the local branch when branching off of "origin/hack" (or "remotes/origin/hack", or even "refs/remotes/origin/hack"). If the given name has no slash, or the above guessing results in an empty name, the guessing is aborted. You can explicitly give a name with -b in such a case.

--no-track
Do not set up "upstream" configuration, even if the branch.autoSetupMerge configuration variable is true.

-l
Create the new branch’s reflog; see git-branch(1) for details.

--detach
Rather than checking out a branch to work on it, check out a commit for inspection and discardable experiments. This is the default behavior of "git checkout <commit>" when <commit> is not a branch name. See the "DETACHED HEAD" section below for details.

--orphan <new_branch>
Create a new orphan branch, named <new_branch>, started from <start_point> and switch to it. The first commit made on this new branch will have no parents and it will be the root of a new history totally disconnected from all the other branches and commits.

The index and the working tree are adjusted as if you had previously run "git checkout <start_point>". This allows you to start a new history that records a set of paths similar to <start_point> by easily running "git commit -a" to make the root commit.

This can be useful when you want to publish the tree from a commit without exposing its full history. You might want to do this to publish an open source branch of a project whose current tree is "clean", but whose full history contains proprietary or otherwise encumbered bits of code.

If you want to start a disconnected history that records a set of paths that is totally different from the one of <start_point>, then you should clear the index and the working tree right after creating the orphan branch by running "git rm -rf ." from the top level of the working tree. Afterwards you will be ready to prepare your new files, repopulating the working tree, by copying them from elsewhere, extracting a tarball, etc.

--ignore-skip-worktree-bits
In sparse checkout mode, git checkout -- <paths> would update only entries matched by <paths> and sparse patterns in $GIT_DIR/info/sparse-checkout. This option ignores the sparse patterns and adds back any files in <paths>.

-m
--merge
When switching branches, if you have local modifications to one or more files that are different between the current branch and the branch to which you are switching, the command refuses to switch branches in order to preserve your modifications in context. However, with this option, a three-way merge between the current branch, your working tree contents, and the new branch is done, and you will be on the new branch.

When a merge conflict happens, the index entries for conflicting paths are left unmerged, and you need to resolve the conflicts and mark the resolved paths with git add (or git rm if the merge should result in deletion of the path).

When checking out paths from the index, this option lets you recreate the conflicted merge in the specified paths.

--conflict=<style>
The same as --merge option above, but changes the way the conflicting hunks are presented, overriding the merge.conflictStyle configuration variable. Possible values are "merge" (default) and "diff3" (in addition to what is shown by "merge" style, shows the original contents).

-p
--patch
Interactively select hunks in the difference between the <tree-ish> (or the index, if unspecified) and the working tree. The chosen hunks are then applied in reverse to the working tree (and if a <tree-ish> was specified, the index).

This means that you can use git checkout -p to selectively discard edits from your current working tree. See the “Interactive Mode” section of git-add(1) to learn how to operate the --patch mode.

--ignore-other-worktrees
git checkout refuses when the wanted ref is already checked out by another worktree. This option makes it check the ref out anyway. In other words, the ref can be held by more than one worktree.

<branch>
Branch to checkout; if it refers to a branch (i.e., a name that, when prepended with "refs/heads/", is a valid ref), then that branch is checked out. Otherwise, if it refers to a valid commit, your HEAD becomes "detached" and you are no longer on any branch (see below for details).

As a special case, the "@{-N}" syntax for the N-th last branch/commit checks out branches (instead of detaching). You may also specify - which is synonymous with "@{-1}".

As a further special case, you may use "A...B" as a shortcut for the merge base of A and B if there is exactly one merge base. You can leave out at most one of A and B, in which case it defaults to HEAD.

<new_branch>
Name for the new branch.

<start_point>
The name of a commit at which to start the new branch; see git-branch(1) for details. Defaults to HEAD.

<tree-ish>
Tree to checkout from (when paths are given). If not specified, the index will be used.
DETACHED HEAD
HEAD normally refers to a named branch (e.g. master). Meanwhile, each branch refers to a specific commit. Let’s look at a repo with three commits, one of them tagged, and with branch master checked out:

	   HEAD (refers to branch 'master')
	    |
	    v
a---b---c  branch 'master' (refers to commit 'c')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
When a commit is created in this state, the branch is updated to refer to the new commit. Specifically, git commit creates a new commit d, whose parent is commit c, and then updates branch master to refer to new commit d. HEAD still refers to branch master and so indirectly now refers to commit d:

$ edit; git add; git commit

	       HEAD (refers to branch 'master')
		|
		v
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
It is sometimes useful to be able to checkout a commit that is not at the tip of any named branch, or even to create a new commit that is not referenced by a named branch. Let’s look at what happens when we checkout commit b (here we show two ways this may be done):

$ git checkout v2.0  # or
$ git checkout master^^

   HEAD (refers to commit 'b')
    |
    v
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
Notice that regardless of which checkout command we use, HEAD now refers directly to commit b. This is known as being in detached HEAD state. It means simply that HEAD refers to a specific commit, as opposed to referring to a named branch. Let’s see what happens when we create a commit:

$ edit; git add; git commit

     HEAD (refers to commit 'e')
      |
      v
      e
     /
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
There is now a new commit e, but it is referenced only by HEAD. We can of course add yet another commit in this state:

$ edit; git add; git commit

	 HEAD (refers to commit 'f')
	  |
	  v
      e---f
     /
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
In fact, we can perform all the normal Git operations. But, let’s look at what happens when we then checkout master:

$ git checkout master

	       HEAD (refers to branch 'master')
      e---f     |
     /          v
a---b---c---d  branch 'master' (refers to commit 'd')
    ^
    |
  tag 'v2.0' (refers to commit 'b')
It is important to realize that at this point nothing refers to commit f. Eventually commit f (and by extension commit e) will be deleted by the routine Git garbage collection process, unless we create a reference before that happens. If we have not yet moved away from commit f, any of these will create a reference to it:

$ git checkout -b foo   (1)
$ git branch foo        (2)
$ git tag foo           (3)
creates a new branch foo, which refers to commit f, and then updates HEAD to refer to branch foo. In other words, we’ll no longer be in detached HEAD state after this command.

similarly creates a new branch foo, which refers to commit f, but leaves HEAD detached.

creates a new tag foo, which refers to commit f, leaving HEAD detached.

If we have moved away from commit f, then we must first recover its object name (typically by using git reflog), and then we can create a reference to it. For example, to see the last two commits to which HEAD referred, we can use either of these commands:

$ git reflog -2 HEAD # or
$ git log -g -2 HEAD
ARGUMENT DISAMBIGUATION
When there is only one argument given and it is not -- (e.g. "git checkout abc"), and when the argument is both a valid <tree-ish> (e.g. a branch "abc" exists) and a valid <pathspec> (e.g. a file or a directory whose name is "abc" exists), Git would usually ask you to disambiguate. Because checking out a branch is so common an operation, however, "git checkout abc" takes "abc" as a <tree-ish> in such a situation. Use git checkout -- <pathspec> if you want to checkout these paths out of the index.

EXAMPLES
The following sequence checks out the master branch, reverts the Makefile to two revisions back, deletes hello.c by mistake, and gets it back from the index.

$ git checkout master             (1)
$ git checkout master~2 Makefile  (2)
$ rm -f hello.c
$ git checkout hello.c            (3)
switch branch

take a file out of another commit

restore hello.c from the index

If you want to check out all C source files out of the index, you can say

$ git checkout -- '*.c'
Note the quotes around *.c. The file hello.c will also be checked out, even though it is no longer in the working tree, because the file globbing is used to match entries in the index (not in the working tree by the shell).

If you have an unfortunate branch that is named hello.c, this step would be confused as an instruction to switch to that branch. You should instead write:

$ git checkout -- hello.c
After working in the wrong branch, switching to the correct branch would be done using:

$ git checkout mytopic
However, your "wrong" branch and correct "mytopic" branch may differ in files that you have modified locally, in which case the above checkout would fail like this:

$ git checkout mytopic
error: You have local changes to 'frotz'; not switching branches.
You can give the -m flag to the command, which would try a three-way merge:

$ git checkout -m mytopic
Auto-merging frotz
After this three-way merge, the local modifications are not registered in your index file, so git diff would show you what changes you made since the tip of the new branch.

When a merge conflict happens during switching branches with the -m option, you would see something like this:

$ git checkout -m mytopic
Auto-merging frotz
ERROR: Merge conflict in frotz
fatal: merge program failed
At this point, git diff shows the changes cleanly merged as in the previous example, as well as the changes in the conflicted files. Edit and resolve the conflict and mark it resolved with git add as usual:

$ edit frotz
$ git add frotz
GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

### git commit
```sh
git-commit(1) Manual Page
NAME
git-commit - Record changes to the repository

SYNOPSIS
git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
	   [--dry-run] [(-c | -C | --fixup | --squash) <commit>]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
	   [--date=<date>] [--cleanup=<mode>] [--[no-]status]
	   [-i | -o] [-S[<keyid>]] [--] [<file>…​]
DESCRIPTION
Stores the current contents of the index in a new commit along with a log message from the user describing the changes.

The content to be added can be specified in several ways:

by using git add to incrementally "add" changes to the index before using the commit command (Note: even modified files must be "added");

by using git rm to remove files from the working tree and the index, again before using the commit command;

by listing files as arguments to the commit command (without --interactive or --patch switch), in which case the commit will ignore changes staged in the index, and instead record the current content of the listed files (which must already be known to Git);

by using the -a switch with the commit command to automatically "add" changes from all known files (i.e. all files that are already listed in the index) and to automatically "rm" files in the index that have been removed from the working tree, and then perform the actual commit;

by using the --interactive or --patch switches with the commit command to decide one by one which files or hunks should be part of the commit in addition to contents in the index, before finalizing the operation. See the “Interactive Mode” section of git-add(1) to learn how to operate these modes.

The --dry-run option can be used to obtain a summary of what is included by any of the above for the next commit by giving the same set of parameters (options and paths).

If you make a commit and then find a mistake immediately after that, you can recover from it with git reset.

OPTIONS
-a
--all
Tell the command to automatically stage files that have been modified and deleted, but new files you have not told Git about are not affected.

-p
--patch
Use the interactive patch selection interface to chose which changes to commit. See git-add(1) for details.

-C <commit>
--reuse-message=<commit>
Take an existing commit object, and reuse the log message and the authorship information (including the timestamp) when creating the commit.

-c <commit>
--reedit-message=<commit>
Like -C, but with -c the editor is invoked, so that the user can further edit the commit message.

--fixup=<commit>
Construct a commit message for use with rebase --autosquash. The commit message will be the subject line from the specified commit with a prefix of "fixup! ". See git-rebase(1) for details.

--squash=<commit>
Construct a commit message for use with rebase --autosquash. The commit message subject line is taken from the specified commit with a prefix of "squash! ". Can be used with additional commit message options (-m/-c/-C/-F). See git-rebase(1) for details.

--reset-author
When used with -C/-c/--amend options, or when committing after a a conflicting cherry-pick, declare that the authorship of the resulting commit now belongs to the committer. This also renews the author timestamp.

--short
When doing a dry-run, give the output in the short-format. See git-status(1) for details. Implies --dry-run.

--branch
Show the branch and tracking info even in short-format.

--porcelain
When doing a dry-run, give the output in a porcelain-ready format. See git-status(1) for details. Implies --dry-run.

--long
When doing a dry-run, give the output in a the long-format. Implies --dry-run.

-z
--null
When showing short or porcelain status output, terminate entries in the status output with NUL, instead of LF. If no format is given, implies the --porcelain output format.

-F <file>
--file=<file>
Take the commit message from the given file. Use - to read the message from the standard input.

--author=<author>
Override the commit author. Specify an explicit author using the standard A U Thor <author@example.com> format. Otherwise <author> is assumed to be a pattern and is used to search for an existing commit by that author (i.e. rev-list --all -i --author=<author>); the commit author is then copied from the first such commit found.

--date=<date>
Override the author date used in the commit.

-m <msg>
--message=<msg>
Use the given <msg> as the commit message. If multiple -m options are given, their values are concatenated as separate paragraphs.

-t <file>
--template=<file>
When editing the commit message, start the editor with the contents in the given file. The commit.template configuration variable is often used to give this option implicitly to the command. This mechanism can be used by projects that want to guide participants with some hints on what to write in the message in what order. If the user exits the editor without editing the message, the commit is aborted. This has no effect when a message is given by other means, e.g. with the -m or -F options.

-s
--signoff
Add Signed-off-by line by the committer at the end of the commit log message. The meaning of a signoff depends on the project, but it typically certifies that committer has the rights to submit this work under the same license and agrees to a Developer Certificate of Origin (see http://developercertificate.org/ for more information).

-n
--no-verify
This option bypasses the pre-commit and commit-msg hooks. See also githooks(5).

--allow-empty
Usually recording a commit that has the exact same tree as its sole parent commit is a mistake, and the command prevents you from making such a commit. This option bypasses the safety, and is primarily for use by foreign SCM interface scripts.

--allow-empty-message
Like --allow-empty this command is primarily for use by foreign SCM interface scripts. It allows you to create a commit with an empty commit message without using plumbing commands like git-commit-tree(1).

--cleanup=<mode>
This option determines how the supplied commit message should be cleaned up before committing. The <mode> can be strip, whitespace, verbatim, scissors or default.

strip
Strip leading and trailing empty lines, trailing whitespace, commentary and collapse consecutive empty lines.

whitespace
Same as strip except #commentary is not removed.

verbatim
Do not change the message at all.

scissors
Same as whitespace, except that everything from (and including) the line "# ------------------------ >8 ------------------------" is truncated if the message is to be edited. "#" can be customized with core.commentChar.

default
Same as strip if the message is to be edited. Otherwise whitespace.
The default can be changed by the commit.cleanup configuration variable (see git-config(1)).

-e
--edit
The message taken from file with -F, command line with -m, and from commit object with -C are usually used as the commit log message unmodified. This option lets you further edit the message taken from these sources.

--no-edit
Use the selected commit message without launching an editor. For example, git commit --amend --no-edit amends a commit without changing its commit message.

--amend
Replace the tip of the current branch by creating a new commit. The recorded tree is prepared as usual (including the effect of the -i and -o options and explicit pathspec), and the message from the original commit is used as the starting point, instead of an empty message, when no other message is specified from the command line via options such as -m, -F, -c, etc. The new commit has the same parents and author as the current one (the --reset-author option can countermand this).

It is a rough equivalent for:

	$ git reset --soft HEAD^
	$ ... do something else to come up with the right tree ...
	$ git commit -c ORIG_HEAD
but can be used to amend a merge commit.

You should understand the implications of rewriting history if you amend a commit that has already been published. (See the "RECOVERING FROM UPSTREAM REBASE" section in git-rebase(1).)

--no-post-rewrite
Bypass the post-rewrite hook.

-i
--include
Before making a commit out of staged contents so far, stage the contents of paths given on the command line as well. This is usually not what you want unless you are concluding a conflicted merge.

-o
--only
Make a commit by taking the updated working tree contents of the paths specified on the command line, disregarding any contents that have been staged for other paths. This is the default mode of operation of git commit if any paths are given on the command line, in which case this option can be omitted. If this option is specified together with --amend, then no paths need to be specified, which can be used to amend the last commit without committing changes that have already been staged. If used together with --allow-empty paths are also not required, and an empty commit will be created.

-u[<mode>]
--untracked-files[=<mode>]
Show untracked files.

The mode parameter is optional (defaults to all), and is used to specify the handling of untracked files; when -u is not used, the default is normal, i.e. show untracked files and directories.

The possible options are:

no - Show no untracked files

normal - Shows untracked files and directories

all - Also shows individual files in untracked directories.

The default can be changed using the status.showUntrackedFiles configuration variable documented in git-config(1).

-v
--verbose
Show unified diff between the HEAD commit and what would be committed at the bottom of the commit message template to help the user describe the commit by reminding what changes the commit has. Note that this diff output doesn’t have its lines prefixed with #. This diff will not be a part of the commit message. See the commit.verbose configuration variable in git-config(1).

If specified twice, show in addition the unified diff between what would be committed and the worktree files, i.e. the unstaged changes to tracked files.

-q
--quiet
Suppress commit summary message.

--dry-run
Do not create a commit, but show a list of paths that are to be committed, paths with local changes that will be left uncommitted and paths that are untracked.

--status
Include the output of git-status(1) in the commit message template when using an editor to prepare the commit message. Defaults to on, but can be used to override configuration variable commit.status.

--no-status
Do not include the output of git-status(1) in the commit message template when using an editor to prepare the default commit message.

-S[<keyid>]
--gpg-sign[=<keyid>]
GPG-sign commits. The keyid argument is optional and defaults to the committer identity; if specified, it must be stuck to the option without a space.

--no-gpg-sign
Countermand commit.gpgSign configuration variable that is set to force each and every commit to be signed.

--
Do not interpret any more arguments as options.

<file>…​
When files are given on the command line, the command commits the contents of the named files, without recording the changes already staged. The contents of these files are also staged for the next commit on top of what have been staged before.
DATE FORMATS
The GIT_AUTHOR_DATE, GIT_COMMITTER_DATE environment variables and the --date option support the following date formats:

Git internal format
It is <unix timestamp> <time zone offset>, where <unix timestamp> is the number of seconds since the UNIX epoch. <time zone offset> is a positive or negative offset from UTC. For example CET (which is 1 hour ahead of UTC) is +0100.

RFC 2822
The standard email format as described by RFC 2822, for example Thu, 07 Apr 2005 22:13:13 +0200.

ISO 8601
Time and date specified by the ISO 8601 standard, for example 2005-04-07T22:13:13. The parser accepts a space instead of the T character as well.

NOTE
In addition, the date part is accepted in the following formats: YYYY.MM.DD, MM/DD/YYYY and DD.MM.YYYY.
EXAMPLES
When recording your own work, the contents of modified files in your working tree are temporarily stored to a staging area called the "index" with git add. A file can be reverted back, only in the index but not in the working tree, to that of the last commit with git reset HEAD -- <file>, which effectively reverts git add and prevents the changes to this file from participating in the next commit. After building the state to be committed incrementally with these commands, git commit (without any pathname parameter) is used to record what has been staged so far. This is the most basic form of the command. An example:

$ edit hello.c
$ git rm goodbye.c
$ git add hello.c
$ git commit
Instead of staging files after each individual change, you can tell git commit to notice the changes to the files whose contents are tracked in your working tree and do corresponding git add and git rm for you. That is, this example does the same as the earlier example if there is no other change in your working tree:

$ edit hello.c
$ rm goodbye.c
$ git commit -a
The command git commit -a first looks at your working tree, notices that you have modified hello.c and removed goodbye.c, and performs necessary git add and git rm for you.

After staging changes to many files, you can alter the order the changes are recorded in, by giving pathnames to git commit. When pathnames are given, the command makes a commit that only records the changes made to the named paths:

$ edit hello.c hello.h
$ git add hello.c hello.h
$ edit Makefile
$ git commit Makefile
This makes a commit that records the modification to Makefile. The changes staged for hello.c and hello.h are not included in the resulting commit. However, their changes are not lost — they are still staged and merely held back. After the above sequence, if you do:

$ git commit
this second commit would record the changes to hello.c and hello.h as expected.

After a merge (initiated by git merge or git pull) stops because of conflicts, cleanly merged paths are already staged to be committed for you, and paths that conflicted are left in unmerged state. You would have to first check which paths are conflicting with git status and after fixing them manually in your working tree, you would stage the result as usual with git add:

$ git status | grep unmerged
unmerged: hello.c
$ edit hello.c
$ git add hello.c
After resolving conflicts and staging the result, git ls-files -u would stop mentioning the conflicted path. When you are done, run git commit to finally record the merge:

$ git commit
As with the case to record your own changes, you can use -a option to save typing. One difference is that during a merge resolution, you cannot use git commit with pathnames to alter the order the changes are committed, because the merge should be recorded as a single commit. In fact, the command refuses to run when given pathnames (but see -i option).

DISCUSSION
Though not required, it’s a good idea to begin the commit message with a single short (less than 50 character) line summarizing the change, followed by a blank line and then a more thorough description. The text up to the first blank line in a commit message is treated as the commit title, and that title is used throughout Git. For example, git-format-patch(1) turns a commit into email, and it uses the title on the Subject line and the rest of the commit in the body.

Git is to some extent character encoding agnostic.

The contents of the blob objects are uninterpreted sequences of bytes. There is no encoding translation at the core level.

Path names are encoded in UTF-8 normalization form C. This applies to tree objects, the index file, ref names, as well as path names in command line arguments, environment variables and config files (.git/config (see git-config(1)), gitignore(5), gitattributes(5) and gitmodules(5)).

Note that Git at the core level treats path names simply as sequences of non-NUL bytes, there are no path name encoding conversions (except on Mac and Windows). Therefore, using non-ASCII path names will mostly work even on platforms and file systems that use legacy extended ASCII encodings. However, repositories created on such systems will not work properly on UTF-8-based systems (e.g. Linux, Mac, Windows) and vice versa. Additionally, many Git-based tools simply assume path names to be UTF-8 and will fail to display other encodings correctly.

Commit log messages are typically encoded in UTF-8, but other extended ASCII encodings are also supported. This includes ISO-8859-x, CP125x and many others, but not UTF-16/32, EBCDIC and CJK multi-byte encodings (GBK, Shift-JIS, Big5, EUC-x, CP9xx etc.).

Although we encourage that the commit log messages are encoded in UTF-8, both the core and Git Porcelain are designed not to force UTF-8 on projects. If all participants of a particular project find it more convenient to use legacy encodings, Git does not forbid it. However, there are a few things to keep in mind.

git commit and git commit-tree issues a warning if the commit log message given to it does not look like a valid UTF-8 string, unless you explicitly say your project uses a legacy encoding. The way to say this is to have i18n.commitencoding in .git/config file, like this:

[i18n]
	commitencoding = ISO-8859-1
Commit objects created with the above setting record the value of i18n.commitencoding in its encoding header. This is to help other people who look at them later. Lack of this header implies that the commit log message is encoded in UTF-8.

git log, git show, git blame and friends look at the encoding header of a commit object, and try to re-code the log message into UTF-8 unless otherwise specified. You can specify the desired output encoding with i18n.logoutputencoding in .git/config file, like this:

[i18n]
	logoutputencoding = ISO-8859-1
If you do not have this configuration variable, the value of i18n.commitencoding is used instead.

Note that we deliberately chose not to re-code the commit log message when a commit is made to force UTF-8 at the commit object level, because re-coding to UTF-8 is not necessarily a reversible operation.

ENVIRONMENT AND CONFIGURATION VARIABLES
The editor used to edit the commit log message will be chosen from the GIT_EDITOR environment variable, the core.editor configuration variable, the VISUAL environment variable, or the EDITOR environment variable (in that order). See git-var(1) for details.

HOOKS
This command can run commit-msg, prepare-commit-msg, pre-commit, and post-commit hooks. See githooks(5) for more information.

FILES
$GIT_DIR/COMMIT_EDITMSG
This file contains the commit message of a commit in progress. If git commit exits due to an error before creating a commit, any commit message that has been provided by the user (e.g., in an editor session) will be available in this file, but will be overwritten by the next invocation of git commit.
SEE ALSO
git-add(1), git-rm(1), git-mv(1), git-merge(1), git-commit-tree(1)

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

### git diff
```sh
git-diff(1) Manual Page
NAME
git-diff - Show changes between commits, commit and working tree, etc

SYNOPSIS
git diff [options] [<commit>] [--] [<path>…​]
git diff [options] --cached [<commit>] [--] [<path>…​]
git diff [options] <commit> <commit> [--] [<path>…​]
git diff [options] <blob> <blob>
git diff [options] [--no-index] [--] <path> <path>
DESCRIPTION
Show changes between the working tree and the index or a tree, changes between the index and a tree, changes between two trees, changes between two blob objects, or changes between two files on disk.

git diff [--options] [--] [<path>…​]
This form is to view the changes you made relative to the index (staging area for the next commit). In other words, the differences are what you could tell Git to further add to the index but you still haven’t. You can stage these changes by using git-add(1).

git diff --no-index [--options] [--] [<path>…​]
This form is to compare the given two paths on the filesystem. You can omit the --no-index option when running the command in a working tree controlled by Git and at least one of the paths points outside the working tree, or when running the command outside a working tree controlled by Git.

git diff [--options] --cached [<commit>] [--] [<path>…​]
This form is to view the changes you staged for the next commit relative to the named <commit>. Typically you would want comparison with the latest commit, so if you do not give <commit>, it defaults to HEAD. If HEAD does not exist (e.g. unborn branches) and <commit> is not given, it shows all staged changes. --staged is a synonym of --cached.

git diff [--options] <commit> [--] [<path>…​]
This form is to view the changes you have in your working tree relative to the named <commit>. You can use HEAD to compare it with the latest commit, or a branch name to compare with the tip of a different branch.

git diff [--options] <commit> <commit> [--] [<path>…​]
This is to view the changes between two arbitrary <commit>.

git diff [--options] <commit>..<commit> [--] [<path>…​]
This is synonymous to the previous form. If <commit> on one side is omitted, it will have the same effect as using HEAD instead.

git diff [--options] <commit>...<commit> [--] [<path>…​]
This form is to view the changes on the branch containing and up to the second <commit>, starting at a common ancestor of both <commit>. "git diff A...B" is equivalent to "git diff $(git-merge-base A B) B". You can omit any one of <commit>, which has the same effect as using HEAD instead.
Just in case if you are doing something exotic, it should be noted that all of the <commit> in the above description, except in the last two forms that use ".." notations, can be any <tree>.

For a more complete list of ways to spell <commit>, see "SPECIFYING REVISIONS" section in gitrevisions(7). However, "diff" is about comparing two endpoints, not ranges, and the range notations ("<commit>..<commit>" and "<commit>...<commit>") do not mean a range as defined in the "SPECIFYING RANGES" section in gitrevisions(7).

git diff [options] <blob> <blob>
This form is to view the differences between the raw contents of two blob objects.
OPTIONS
-p
-u
--patch
Generate patch (see section on generating patches). This is the default.

-s
--no-patch
Suppress diff output. Useful for commands like git show that show the patch by default, or to cancel the effect of --patch.

-U<n>
--unified=<n>
Generate diffs with <n> lines of context instead of the usual three. Implies -p.

--raw
Generate the diff in raw format.

--patch-with-raw
Synonym for -p --raw.

--indent-heuristic
--no-indent-heuristic
--compaction-heuristic
--no-compaction-heuristic
These are to help debugging and tuning experimental heuristics (which are off by default) that shift diff hunk boundaries to make patches easier to read.

--minimal
Spend extra time to make sure the smallest possible diff is produced.

--patience
Generate a diff using the "patience diff" algorithm.

--histogram
Generate a diff using the "histogram diff" algorithm.

--diff-algorithm={patience|minimal|histogram|myers}
Choose a diff algorithm. The variants are as follows:

default, myers
The basic greedy diff algorithm. Currently, this is the default.

minimal
Spend extra time to make sure the smallest possible diff is produced.

patience
Use "patience diff" algorithm when generating patches.

histogram
This algorithm extends the patience algorithm to "support low-occurrence common elements".
For instance, if you configured diff.algorithm variable to a non-default value and want to use the default one, then you have to use --diff-algorithm=default option.

--stat[=<width>[,<name-width>[,<count>]]]
Generate a diffstat. By default, as much space as necessary will be used for the filename part, and the rest for the graph part. Maximum width defaults to terminal width, or 80 columns if not connected to a terminal, and can be overridden by <width>. The width of the filename part can be limited by giving another width <name-width> after a comma. The width of the graph part can be limited by using --stat-graph-width=<width> (affects all commands generating a stat graph) or by setting diff.statGraphWidth=<width> (does not affect git format-patch). By giving a third parameter <count>, you can limit the output to the first <count> lines, followed by ... if there are more.

These parameters can also be set individually with --stat-width=<width>, --stat-name-width=<name-width> and --stat-count=<count>.

--numstat
Similar to --stat, but shows number of added and deleted lines in decimal notation and pathname without abbreviation, to make it more machine friendly. For binary files, outputs two - instead of saying 0 0.

--shortstat
Output only the last line of the --stat format containing total number of modified files, as well as number of added and deleted lines.

--dirstat[=<param1,param2,…​>]
Output the distribution of relative amount of changes for each sub-directory. The behavior of --dirstat can be customized by passing it a comma separated list of parameters. The defaults are controlled by the diff.dirstat configuration variable (see git-config(1)). The following parameters are available:

changes
Compute the dirstat numbers by counting the lines that have been removed from the source, or added to the destination. This ignores the amount of pure code movements within a file. In other words, rearranging lines in a file is not counted as much as other changes. This is the default behavior when no parameter is given.

lines
Compute the dirstat numbers by doing the regular line-based diff analysis, and summing the removed/added line counts. (For binary files, count 64-byte chunks instead, since binary files have no natural concept of lines). This is a more expensive --dirstat behavior than the changes behavior, but it does count rearranged lines within a file as much as other changes. The resulting output is consistent with what you get from the other --*stat options.

files
Compute the dirstat numbers by counting the number of files changed. Each changed file counts equally in the dirstat analysis. This is the computationally cheapest --dirstat behavior, since it does not have to look at the file contents at all.

cumulative
Count changes in a child directory for the parent directory as well. Note that when using cumulative, the sum of the percentages reported may exceed 100%. The default (non-cumulative) behavior can be specified with the noncumulative parameter.

<limit>
An integer parameter specifies a cut-off percent (3% by default). Directories contributing less than this percentage of the changes are not shown in the output.
Example: The following will count changed files, while ignoring directories with less than 10% of the total amount of changed files, and accumulating child directory counts in the parent directories: --dirstat=files,10,cumulative.

--summary
Output a condensed summary of extended header information such as creations, renames and mode changes.

--patch-with-stat
Synonym for -p --stat.

-z
When --raw, --numstat, --name-only or --name-status has been given, do not munge pathnames and use NULs as output field terminators.

Without this option, each pathname output will have TAB, LF, double quotes, and backslash characters replaced with \t, \n, \", and \\, respectively, and the pathname will be enclosed in double quotes if any of those replacements occurred.

--name-only
Show only names of changed files.

--name-status
Show only names and status of changed files. See the description of the --diff-filter option on what the status letters mean.

--submodule[=<format>]
Specify how differences in submodules are shown. When specifying --submodule=short the short format is used. This format just shows the names of the commits at the beginning and end of the range. When --submodule or --submodule=log is specified, the log format is used. This format lists the commits in the range like git-submodule(1) summary does. When --submodule=diff is specified, the diff format is used. This format shows an inline diff of the changes in the submodule contents between the commit range. Defaults to diff.submodule or the short format if the config option is unset.

--color[=<when>]
Show colored diff. --color (i.e. without =<when>) is the same as --color=always. <when> can be one of always, never, or auto. It can be changed by the color.ui and color.diff configuration settings.

--no-color
Turn off colored diff. This can be used to override configuration settings. It is the same as --color=never.

--word-diff[=<mode>]
Show a word diff, using the <mode> to delimit changed words. By default, words are delimited by whitespace; see --word-diff-regex below. The <mode> defaults to plain, and must be one of:

color
Highlight changed words using only colors. Implies --color.

plain
Show words as [-removed-] and {+added+}. Makes no attempts to escape the delimiters if they appear in the input, so the output may be ambiguous.

porcelain
Use a special line-based format intended for script consumption. Added/removed/unchanged runs are printed in the usual unified diff format, starting with a +/-/` ` character at the beginning of the line and extending to the end of the line. Newlines in the input are represented by a tilde ~ on a line of its own.

none
Disable word diff again.
Note that despite the name of the first mode, color is used to highlight the changed parts in all modes if enabled.

--word-diff-regex=<regex>
Use <regex> to decide what a word is, instead of considering runs of non-whitespace to be a word. Also implies --word-diff unless it was already enabled.

Every non-overlapping match of the <regex> is considered a word. Anything between these matches is considered whitespace and ignored(!) for the purposes of finding differences. You may want to append |[^[:space:]] to your regular expression to make sure that it matches all non-whitespace characters. A match that contains a newline is silently truncated(!) at the newline.

For example, --word-diff-regex=. will treat each character as a word and, correspondingly, show differences character by character.

The regex can also be set via a diff driver or configuration option, see gitattributes(5) or git-config(1). Giving it explicitly overrides any diff driver or configuration setting. Diff drivers override configuration settings.

--color-words[=<regex>]
Equivalent to --word-diff=color plus (if a regex was specified) --word-diff-regex=<regex>.

--no-renames
Turn off rename detection, even when the configuration file gives the default to do so.

--check
Warn if changes introduce conflict markers or whitespace errors. What are considered whitespace errors is controlled by core.whitespace configuration. By default, trailing whitespaces (including lines that solely consist of whitespaces) and a space character that is immediately followed by a tab character inside the initial indent of the line are considered whitespace errors. Exits with non-zero status if problems are found. Not compatible with --exit-code.

--ws-error-highlight=<kind>
Highlight whitespace errors on lines specified by <kind> in the color specified by color.diff.whitespace. <kind> is a comma separated list of old, new, context. When this option is not given, only whitespace errors in new lines are highlighted. E.g. --ws-error-highlight=new,old highlights whitespace errors on both deleted and added lines. all can be used as a short-hand for old,new,context. The diff.wsErrorHighlight configuration variable can be used to specify the default behaviour.

--full-index
Instead of the first handful of characters, show the full pre- and post-image blob object names on the "index" line when generating patch format output.

--binary
In addition to --full-index, output a binary diff that can be applied with git-apply.

--abbrev[=<n>]
Instead of showing the full 40-byte hexadecimal object name in diff-raw format output and diff-tree header lines, show only a partial prefix. This is independent of the --full-index option above, which controls the diff-patch output format. Non default number of digits can be specified with --abbrev=<n>.

-B[<n>][/<m>]
--break-rewrites[=[<n>][/<m>]]
Break complete rewrite changes into pairs of delete and create. This serves two purposes:

It affects the way a change that amounts to a total rewrite of a file not as a series of deletion and insertion mixed together with a very few lines that happen to match textually as the context, but as a single deletion of everything old followed by a single insertion of everything new, and the number m controls this aspect of the -B option (defaults to 60%). -B/70% specifies that less than 30% of the original should remain in the result for Git to consider it a total rewrite (i.e. otherwise the resulting patch will be a series of deletion and insertion mixed together with context lines).

When used with -M, a totally-rewritten file is also considered as the source of a rename (usually -M only considers a file that disappeared as the source of a rename), and the number n controls this aspect of the -B option (defaults to 50%). -B20% specifies that a change with addition and deletion compared to 20% or more of the file’s size are eligible for being picked up as a possible source of a rename to another file.

-M[<n>]
--find-renames[=<n>]
Detect renames. If n is specified, it is a threshold on the similarity index (i.e. amount of addition/deletions compared to the file’s size). For example, -M90% means Git should consider a delete/add pair to be a rename if more than 90% of the file hasn’t changed. Without a % sign, the number is to be read as a fraction, with a decimal point before it. I.e., -M5 becomes 0.5, and is thus the same as -M50%. Similarly, -M05 is the same as -M5%. To limit detection to exact renames, use -M100%. The default similarity index is 50%.

-C[<n>]
--find-copies[=<n>]
Detect copies as well as renames. See also --find-copies-harder. If n is specified, it has the same meaning as for -M<n>.

--find-copies-harder
For performance reasons, by default, -C option finds copies only if the original file of the copy was modified in the same changeset. This flag makes the command inspect unmodified files as candidates for the source of copy. This is a very expensive operation for large projects, so use it with caution. Giving more than one -C option has the same effect.

-D
--irreversible-delete
Omit the preimage for deletes, i.e. print only the header but not the diff between the preimage and /dev/null. The resulting patch is not meant to be applied with patch or git apply; this is solely for people who want to just concentrate on reviewing the text after the change. In addition, the output obviously lack enough information to apply such a patch in reverse, even manually, hence the name of the option.

When used together with -B, omit also the preimage in the deletion part of a delete/create pair.

-l<num>
The -M and -C options require O(n^2) processing time where n is the number of potential rename/copy targets. This option prevents rename/copy detection from running if the number of rename/copy targets exceeds the specified number.

--diff-filter=[(A|C|D|M|R|T|U|X|B)…​[*]]
Select only files that are Added (A), Copied (C), Deleted (D), Modified (M), Renamed (R), have their type (i.e. regular file, symlink, submodule, …​) changed (T), are Unmerged (U), are Unknown (X), or have had their pairing Broken (B). Any combination of the filter characters (including none) can be used. When * (All-or-none) is added to the combination, all paths are selected if there is any file that matches other criteria in the comparison; if there is no file that matches other criteria, nothing is selected.

Also, these upper-case letters can be downcased to exclude. E.g. --diff-filter=ad excludes added and deleted paths.

-S<string>
Look for differences that change the number of occurrences of the specified string (i.e. addition/deletion) in a file. Intended for the scripter’s use.

It is useful when you’re looking for an exact block of code (like a struct), and want to know the history of that block since it first came into being: use the feature iteratively to feed the interesting block in the preimage back into -S, and keep going until you get the very first version of the block.

-G<regex>
Look for differences whose patch text contains added/removed lines that match <regex>.

To illustrate the difference between -S<regex> --pickaxe-regex and -G<regex>, consider a commit with the following diff in the same file:

+    return !regexec(regexp, two->ptr, 1, &regmatch, 0);
...
-    hit = !regexec(regexp, mf2.ptr, 1, &regmatch, 0);
While git log -G"regexec\(regexp" will show this commit, git log -S"regexec\(regexp" --pickaxe-regex will not (because the number of occurrences of that string did not change).

See the pickaxe entry in gitdiffcore(7) for more information.

--pickaxe-all
When -S or -G finds a change, show all the changes in that changeset, not just the files that contain the change in <string>.

--pickaxe-regex
Treat the <string> given to -S as an extended POSIX regular expression to match.

-O<orderfile>
Output the patch in the order specified in the <orderfile>, which has one shell glob pattern per line. This overrides the diff.orderFile configuration variable (see git-config(1)). To cancel diff.orderFile, use -O/dev/null.

-R
Swap two inputs; that is, show differences from index or on-disk file to tree contents.

--relative[=<path>]
When run from a subdirectory of the project, it can be told to exclude changes outside the directory and show pathnames relative to it with this option. When you are not in a subdirectory (e.g. in a bare repository), you can name which subdirectory to make the output relative to by giving a <path> as an argument.

-a
--text
Treat all files as text.

--ignore-space-at-eol
Ignore changes in whitespace at EOL.

-b
--ignore-space-change
Ignore changes in amount of whitespace. This ignores whitespace at line end, and considers all other sequences of one or more whitespace characters to be equivalent.

-w
--ignore-all-space
Ignore whitespace when comparing lines. This ignores differences even if one line has whitespace where the other line has none.

--ignore-blank-lines
Ignore changes whose lines are all blank.

--inter-hunk-context=<lines>
Show the context between diff hunks, up to the specified number of lines, thereby fusing hunks that are close to each other.

-W
--function-context
Show whole surrounding functions of changes.

--exit-code
Make the program exit with codes similar to diff(1). That is, it exits with 1 if there were differences and 0 means no differences.

--quiet
Disable all output of the program. Implies --exit-code.

--ext-diff
Allow an external diff helper to be executed. If you set an external diff driver with gitattributes(5), you need to use this option with git-log(1) and friends.

--no-ext-diff
Disallow external diff drivers.

--textconv
--no-textconv
Allow (or disallow) external text conversion filters to be run when comparing binary files. See gitattributes(5) for details. Because textconv filters are typically a one-way conversion, the resulting diff is suitable for human consumption, but cannot be applied. For this reason, textconv filters are enabled by default only for git-diff(1) and git-log(1), but not for git-format-patch(1) or diff plumbing commands.

--ignore-submodules[=<when>]
Ignore changes to submodules in the diff generation. <when> can be either "none", "untracked", "dirty" or "all", which is the default. Using "none" will consider the submodule modified when it either contains untracked or modified files or its HEAD differs from the commit recorded in the superproject and can be used to override any settings of the ignore option in git-config(1) or gitmodules(5). When "untracked" is used submodules are not considered dirty when they only contain untracked content (but they are still scanned for modified content). Using "dirty" ignores all changes to the work tree of submodules, only changes to the commits stored in the superproject are shown (this was the behavior until 1.7.0). Using "all" hides all changes to submodules.

--src-prefix=<prefix>
Show the given source prefix instead of "a/".

--dst-prefix=<prefix>
Show the given destination prefix instead of "b/".

--no-prefix
Do not show any source or destination prefix.

--line-prefix=<prefix>
Prepend an additional prefix to every line of output.

--ita-invisible-in-index
By default entries added by "git add -N" appear as an existing empty file in "git diff" and a new file in "git diff --cached". This option makes the entry appear as a new file in "git diff" and non-existent in "git diff --cached". This option could be reverted with --ita-visible-in-index. Both options are experimental and could be removed in future.
For more detailed explanation on these common options, see also gitdiffcore(7).

<path>…​
The <paths> parameters, when given, are used to limit the diff to the named paths (you can give directory names and get diff for all files under them).
Raw output format
The raw output format from "git-diff-index", "git-diff-tree", "git-diff-files" and "git diff --raw" are very similar.

These commands all compare two sets of things; what is compared differs:

git-diff-index <tree-ish>
compares the <tree-ish> and the files on the filesystem.

git-diff-index --cached <tree-ish>
compares the <tree-ish> and the index.

git-diff-tree [-r] <tree-ish-1> <tree-ish-2> [<pattern>…​]
compares the trees named by the two arguments.

git-diff-files [<pattern>…​]
compares the index and the files on the filesystem.
The "git-diff-tree" command begins its output by printing the hash of what is being compared. After that, all the commands print one output line per changed file.

An output line is formatted this way:

in-place edit  :100644 100644 bcd1234... 0123456... M file0
copy-edit      :100644 100644 abcd123... 1234567... C68 file1 file2
rename-edit    :100644 100644 abcd123... 1234567... R86 file1 file3
create         :000000 100644 0000000... 1234567... A file4
delete         :100644 000000 1234567... 0000000... D file5
unmerged       :000000 000000 0000000... 0000000... U file6
That is, from the left to the right:

a colon.

mode for "src"; 000000 if creation or unmerged.

a space.

mode for "dst"; 000000 if deletion or unmerged.

a space.

sha1 for "src"; 0{40} if creation or unmerged.

a space.

sha1 for "dst"; 0{40} if creation, unmerged or "look at work tree".

a space.

status, followed by optional "score" number.

a tab or a NUL when -z option is used.

path for "src"

a tab or a NUL when -z option is used; only exists for C or R.

path for "dst"; only exists for C or R.

an LF or a NUL when -z option is used, to terminate the record.

Possible status letters are:

A: addition of a file

C: copy of a file into a new one

D: deletion of a file

M: modification of the contents or mode of a file

R: renaming of a file

T: change in the type of the file

U: file is unmerged (you must complete the merge before it can be committed)

X: "unknown" change type (most probably a bug, please report it)

Status letters C and R are always followed by a score (denoting the percentage of similarity between the source and target of the move or copy). Status letter M may be followed by a score (denoting the percentage of dissimilarity) for file rewrites.

<sha1> is shown as all 0’s if a file is new on the filesystem and it is out of sync with the index.

Example:

:100644 100644 5be4a4...... 000000...... M file.c
When -z option is not used, TAB, LF, and backslash characters in pathnames are represented as \t, \n, and \\, respectively.

diff format for merges
"git-diff-tree", "git-diff-files" and "git-diff --raw" can take -c or --cc option to generate diff output also for merge commits. The output differs from the format described above in the following way:

there is a colon for each parent

there are more "src" modes and "src" sha1

status is concatenated status characters for each parent

no optional "score" number

single path, only for "dst"

Example:

::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM	describe.c
Note that combined diff lists only files which were modified from all parents.

Generating patches with -p
When "git-diff-index", "git-diff-tree", or "git-diff-files" are run with a -p option, "git diff" without the --raw option, or "git log" with the "-p" option, they do not produce the output described above; instead they produce a patch file. You can customize the creation of such patches via the GIT_EXTERNAL_DIFF and the GIT_DIFF_OPTS environment variables.

What the -p option produces is slightly different from the traditional diff format:

It is preceded with a "git diff" header that looks like this:

diff --git a/file1 b/file2
The a/ and b/ filenames are the same unless rename/copy is involved. Especially, even for a creation or a deletion, /dev/null is not used in place of the a/ or b/ filenames.

When rename/copy is involved, file1 and file2 show the name of the source file of the rename/copy and the name of the file that rename/copy produces, respectively.

It is followed by one or more extended header lines:

old mode <mode>
new mode <mode>
deleted file mode <mode>
new file mode <mode>
copy from <path>
copy to <path>
rename from <path>
rename to <path>
similarity index <number>
dissimilarity index <number>
index <hash>..<hash> <mode>
File modes are printed as 6-digit octal numbers including the file type and file permission bits.

Path names in extended headers do not include the a/ and b/ prefixes.

The similarity index is the percentage of unchanged lines, and the dissimilarity index is the percentage of changed lines. It is a rounded down integer, followed by a percent sign. The similarity index value of 100% is thus reserved for two equal files, while 100% dissimilarity means that no line from the old file made it into the new one.

The index line includes the SHA-1 checksum before and after the change. The <mode> is included if the file mode does not change; otherwise, separate lines indicate the old and the new mode.

TAB, LF, double quote and backslash characters in pathnames are represented as \t, \n, \" and \\, respectively. If there is need for such substitution then the whole pathname is put in double quotes.

All the file1 files in the output refer to files before the commit, and all the file2 files refer to files after the commit. It is incorrect to apply each change to each file sequentially. For example, this patch will swap a and b:

diff --git a/a b/b
rename from a
rename to b
diff --git a/b b/a
rename from b
rename to a
combined diff format
Any diff-generating command can take the -c or --cc option to produce a combined diff when showing a merge. This is the default format when showing merges with git-diff(1) or git-show(1). Note also that you can give the -m option to any of these commands to force generation of diffs with individual parents of a merge.

A combined diff format looks like this:

diff --combined describe.c
index fabadb8,cc95eb0..4866510
--- a/describe.c
+++ b/describe.c
@@@ -98,20 -98,12 +98,20 @@@
	return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1;
  }

- static void describe(char *arg)
 -static void describe(struct commit *cmit, int last_one)
++static void describe(char *arg, int last_one)
  {
 +	unsigned char sha1[20];
 +	struct commit *cmit;
	struct commit_list *list;
	static int initialized = 0;
	struct commit_name *n;

 +	if (get_sha1(arg, sha1) < 0)
 +		usage(describe_usage);
 +	cmit = lookup_commit_reference(sha1);
 +	if (!cmit)
 +		usage(describe_usage);
 +
	if (!initialized) {
		initialized = 1;
		for_each_ref(get_name);
It is preceded with a "git diff" header, that looks like this (when -c option is used):

diff --combined file
or like this (when --cc option is used):

diff --cc file
It is followed by one or more extended header lines (this example shows a merge with two parents):

index <hash>,<hash>..<hash>
mode <mode>,<mode>..<mode>
new file mode <mode>
deleted file mode <mode>,<mode>
The mode <mode>,<mode>..<mode> line appears only if at least one of the <mode> is different from the rest. Extended headers with information about detected contents movement (renames and copying detection) are designed to work with diff of two <tree-ish> and are not used by combined diff format.

It is followed by two-line from-file/to-file header

--- a/file
+++ b/file
Similar to two-line header for traditional unified diff format, /dev/null is used to signal created or deleted files.

Chunk header format is modified to prevent people from accidentally feeding it to patch -p1. Combined diff format was created for review of merge commit changes, and was not meant for apply. The change is similar to the change in the extended index header:

@@@ <from-file-range> <from-file-range> <to-file-range> @@@
There are (number of parents + 1) @ characters in the chunk header for combined diff format.

Unlike the traditional unified diff format, which shows two files A and B with a single column that has - (minus — appears in A but removed in B), + (plus — missing in A but added to B), or " " (space — unchanged) prefix, this format compares two or more files file1, file2,…​ with one file X, and shows how X differs from each of fileN. One column for each of fileN is prepended to the output line to note how X’s line is different from it.

A - character in the column N means that the line appears in fileN but it does not appear in the result. A + character in the column N means that the line appears in the result, and fileN does not have that line (in other words, the line was added, from the point of view of that parent).

In the above example output, the function signature was changed from both files (hence two - removals from both file1 and file2, plus ++ to mean one line that was added does not appear in either file1 or file2). Also eight other lines are the same from file1 but do not appear in file2 (hence prefixed with +).

When shown by git diff-tree -c, it compares the parents of a merge commit with the merge result (i.e. file1..fileN are the parents). When shown by git diff-files -c, it compares the two unresolved merge parents with the working tree file (i.e. file1 is stage 2 aka "our version", file2 is stage 3 aka "their version").

other diff formats
The --summary option describes newly added, deleted, renamed and copied files. The --stat option adds diffstat(1) graph to the output. These options can be combined with other options, such as -p, and are meant for human consumption.

When showing a change that involves a rename or a copy, --stat output formats the pathnames compactly by combining common prefix and suffix of the pathnames. For example, a change that moves arch/i386/Makefile to arch/x86/Makefile while modifying 4 lines will be shown like this:

arch/{i386 => x86}/Makefile    |   4 +--
The --numstat option gives the diffstat(1) information but is designed for easier machine consumption. An entry in --numstat output looks like this:

1	2	README
3	1	arch/{i386 => x86}/Makefile
That is, from left to right:

the number of added lines;

a tab;

the number of deleted lines;

a tab;

pathname (possibly with rename/copy information);

a newline.

When -z output option is in effect, the output is formatted this way:

1	2	README NUL
3	1	NUL arch/i386/Makefile NUL arch/x86/Makefile NUL
That is:

the number of added lines;

a tab;

the number of deleted lines;

a tab;

a NUL (only exists if renamed/copied);

pathname in preimage;

a NUL (only exists if renamed/copied);

pathname in postimage (only exists if renamed/copied);

a NUL.

The extra NUL before the preimage path in renamed case is to allow scripts that read the output to tell if the current record being read is a single-path record or a rename/copy record without reading ahead. After reading added and deleted lines, reading up to NUL would yield the pathname, but if that is NUL, the record will show two paths.

EXAMPLES
Various ways to check your working tree
$ git diff            (1)
$ git diff --cached   (2)
$ git diff HEAD       (3)
Changes in the working tree not yet staged for the next commit.

Changes between the index and your last commit; what you would be committing if you run "git commit" without "-a" option.

Changes in the working tree since your last commit; what you would be committing if you run "git commit -a"

Comparing with arbitrary commits
$ git diff test            (1)
$ git diff HEAD -- ./test  (2)
$ git diff HEAD^ HEAD      (3)
Instead of using the tip of the current branch, compare with the tip of "test" branch.

Instead of comparing with the tip of "test" branch, compare with the tip of the current branch, but limit the comparison to the file "test".

Compare the version before the last commit and the last commit.

Comparing branches
$ git diff topic master    (1)
$ git diff topic..master   (2)
$ git diff topic...master  (3)
Changes between the tips of the topic and the master branches.

Same as above.

Changes that occurred on the master branch since when the topic branch was started off it.

Limiting the diff output
$ git diff --diff-filter=MRC            (1)
$ git diff --name-status                (2)
$ git diff arch/i386 include/asm-i386   (3)
Show only modification, rename, and copy, but not addition or deletion.

Show only names and the nature of change, but not actual diff output.

Limit diff output to named subtrees.

Munging the diff output
$ git diff --find-copies-harder -B -C  (1)
$ git diff -R                          (2)
Spend extra cycles to find renames, copies and complete rewrites (very expensive).

Output diff in reverse.

SEE ALSO
diff(1), git-difftool(1), git-log(1), gitdiffcore(7), git-format-patch(1), git-apply(1)

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

### git merge
```sh
git-merge(1) Manual Page
NAME
git-merge - Join two or more development histories together

SYNOPSIS
git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit]
	[-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
	[--[no-]allow-unrelated-histories]
	[--[no-]rerere-autoupdate] [-m <msg>] [<commit>…​]
git merge <msg> HEAD <commit>…​
git merge --abort
DESCRIPTION
Incorporates changes from the named commits (since the time their histories diverged from the current branch) into the current branch. This command is used by git pull to incorporate changes from another repository and can be used by hand to merge changes from one branch into another.

Assume the following history exists and the current branch is "master":

	  A---B---C topic
	 /
    D---E---F---G master
Then "git merge topic" will replay the changes made on the topic branch since it diverged from master (i.e., E) until its current commit (C) on top of master, and record the result in a new commit along with the names of the two parent commits and a log message from the user describing the changes.

	  A---B---C topic
	 /         \
    D---E---F---G---H master
The second syntax (<msg> HEAD <commit>…​) is supported for historical reasons. Do not use it from the command line or in new scripts. It is the same as git merge -m <msg> <commit>....

The third syntax ("git merge --abort") can only be run after the merge has resulted in conflicts. git merge --abort will abort the merge process and try to reconstruct the pre-merge state. However, if there were uncommitted changes when the merge started (and especially if those changes were further modified after the merge was started), git merge --abort will in some cases be unable to reconstruct the original (pre-merge) changes. Therefore:

Warning: Running git merge with non-trivial uncommitted changes is discouraged: while possible, it may leave you in a state that is hard to back out of in the case of a conflict.

OPTIONS
--commit
--no-commit
Perform the merge and commit the result. This option can be used to override --no-commit.

With --no-commit perform the merge but pretend the merge failed and do not autocommit, to give the user a chance to inspect and further tweak the merge result before committing.

--edit
-e
--no-edit
Invoke an editor before committing successful mechanical merge to further edit the auto-generated merge message, so that the user can explain and justify the merge. The --no-edit option can be used to accept the auto-generated message (this is generally discouraged). The --edit (or -e) option is still useful if you are giving a draft message with the -m option from the command line and want to edit it in the editor.

Older scripts may depend on the historical behaviour of not allowing the user to edit the merge log message. They will see an editor opened when they run git merge. To make it easier to adjust such scripts to the updated behaviour, the environment variable GIT_MERGE_AUTOEDIT can be set to no at the beginning of them.

--ff
When the merge resolves as a fast-forward, only update the branch pointer, without creating a merge commit. This is the default behavior.

--no-ff
Create a merge commit even when the merge resolves as a fast-forward. This is the default behaviour when merging an annotated (and possibly signed) tag.

--ff-only
Refuse to merge and exit with a non-zero status unless the current HEAD is already up-to-date or the merge can be resolved as a fast-forward.

--log[=<n>]
--no-log
In addition to branch names, populate the log message with one-line descriptions from at most <n> actual commits that are being merged. See also git-fmt-merge-msg(1).

With --no-log do not list one-line descriptions from the actual commits being merged.

--stat
-n
--no-stat
Show a diffstat at the end of the merge. The diffstat is also controlled by the configuration option merge.stat.

With -n or --no-stat do not show a diffstat at the end of the merge.

--squash
--no-squash
Produce the working tree and index state as if a real merge happened (except for the merge information), but do not actually make a commit, move the HEAD, or record $GIT_DIR/MERGE_HEAD (to cause the next git commit command to create a merge commit). This allows you to create a single commit on top of the current branch whose effect is the same as merging another branch (or more in case of an octopus).

With --no-squash perform the merge and commit the result. This option can be used to override --squash.

-s <strategy>
--strategy=<strategy>
Use the given merge strategy; can be supplied more than once to specify them in the order they should be tried. If there is no -s option, a built-in list of strategies is used instead (git merge-recursive when merging a single head, git merge-octopus otherwise).

-X <option>
--strategy-option=<option>
Pass merge strategy specific option through to the merge strategy.

--verify-signatures
--no-verify-signatures
Verify that the tip commit of the side branch being merged is signed with a valid key, i.e. a key that has a valid uid: in the default trust model, this means the signing key has been signed by a trusted key. If the tip commit of the side branch is not signed with a valid key, the merge is aborted.

--summary
--no-summary
Synonyms to --stat and --no-stat; these are deprecated and will be removed in the future.

-q
--quiet
Operate quietly. Implies --no-progress.

-v
--verbose
Be verbose.

--progress
--no-progress
Turn progress on/off explicitly. If neither is specified, progress is shown if standard error is connected to a terminal. Note that not all merge strategies may support progress reporting.

--allow-unrelated-histories
By default, git merge command refuses to merge histories that do not share a common ancestor. This option can be used to override this safety when merging histories of two projects that started their lives independently. As that is a very rare occasion, no configuration variable to enable this by default exists and will not be added.

-S[<keyid>]
--gpg-sign[=<keyid>]
GPG-sign the resulting merge commit. The keyid argument is optional and defaults to the committer identity; if specified, it must be stuck to the option without a space.

-m <msg>
Set the commit message to be used for the merge commit (in case one is created).

If --log is specified, a shortlog of the commits being merged will be appended to the specified message.

The git fmt-merge-msg command can be used to give a good default for automated git merge invocations. The automated message can include the branch description.

--[no-]rerere-autoupdate
Allow the rerere mechanism to update the index with the result of auto-conflict resolution if possible.

--abort
Abort the current conflict resolution process, and try to reconstruct the pre-merge state.

If there were uncommitted worktree changes present when the merge started, git merge --abort will in some cases be unable to reconstruct these changes. It is therefore recommended to always commit or stash your changes before running git merge.

git merge --abort is equivalent to git reset --merge when MERGE_HEAD is present.

<commit>…​
Commits, usually other branch heads, to merge into our branch. Specifying more than one commit will create a merge with more than two parents (affectionately called an Octopus merge).

If no commit is given from the command line, merge the remote-tracking branches that the current branch is configured to use as its upstream. See also the configuration section of this manual page.

When FETCH_HEAD (and no other commit) is specified, the branches recorded in the .git/FETCH_HEAD file by the previous invocation of git fetch for merging are merged to the current branch.

PRE-MERGE CHECKS
Before applying outside changes, you should get your own work in good shape and committed locally, so it will not be clobbered if there are conflicts. See also git-stash(1). git pull and git merge will stop without doing anything when local uncommitted changes overlap with files that git pull/git merge may need to update.

To avoid recording unrelated changes in the merge commit, git pull and git merge will also abort if there are any changes registered in the index relative to the HEAD commit. (One exception is when the changed index entries are in the state that would result from the merge already.)

If all named commits are already ancestors of HEAD, git merge will exit early with the message "Already up-to-date."

FAST-FORWARD MERGE
Often the current branch head is an ancestor of the named commit. This is the most common case especially when invoked from git pull: you are tracking an upstream repository, you have committed no local changes, and now you want to update to a newer upstream revision. In this case, a new commit is not needed to store the combined history; instead, the HEAD (along with the index) is updated to point at the named commit, without creating an extra merge commit.

This behavior can be suppressed with the --no-ff option.

TRUE MERGE
Except in a fast-forward merge (see above), the branches to be merged must be tied together by a merge commit that has both of them as its parents.

A merged version reconciling the changes from all branches to be merged is committed, and your HEAD, index, and working tree are updated to it. It is possible to have modifications in the working tree as long as they do not overlap; the update will preserve them.

When it is not obvious how to reconcile the changes, the following happens:

The HEAD pointer stays the same.

The MERGE_HEAD ref is set to point to the other branch head.

Paths that merged cleanly are updated both in the index file and in your working tree.

For conflicting paths, the index file records up to three versions: stage 1 stores the version from the common ancestor, stage 2 from HEAD, and stage 3 from MERGE_HEAD (you can inspect the stages with git ls-files -u). The working tree files contain the result of the "merge" program; i.e. 3-way merge results with familiar conflict markers <<< === >>>.

No other changes are made. In particular, the local modifications you had before you started merge will stay the same and the index entries for them stay as they were, i.e. matching HEAD.

If you tried a merge which resulted in complex conflicts and want to start over, you can recover with git merge --abort.

MERGING TAG
When merging an annotated (and possibly signed) tag, Git always creates a merge commit even if a fast-forward merge is possible, and the commit message template is prepared with the tag message. Additionally, if the tag is signed, the signature check is reported as a comment in the message template. See also git-tag(1).

When you want to just integrate with the work leading to the commit that happens to be tagged, e.g. synchronizing with an upstream release point, you may not want to make an unnecessary merge commit.

In such a case, you can "unwrap" the tag yourself before feeding it to git merge, or pass --ff-only when you do not have any work on your own. e.g.

git fetch origin
git merge v1.2.3^0
git merge --ff-only v1.2.3
HOW CONFLICTS ARE PRESENTED
During a merge, the working tree files are updated to reflect the result of the merge. Among the changes made to the common ancestor’s version, non-overlapping ones (that is, you changed an area of the file while the other side left that area intact, or vice versa) are incorporated in the final result verbatim. When both sides made changes to the same area, however, Git cannot randomly pick one side over the other, and asks you to resolve it by leaving what both sides did to that area.

By default, Git uses the same style as the one used by the "merge" program from the RCS suite to present such a conflicted hunk, like this:

Here are lines that are either unchanged from the common
ancestor, or cleanly resolved because only one side changed.
<<<<<<< yours:sample.txt
Conflict resolution is hard;
let's go shopping.
=======
Git makes conflict resolution easy.
>>>>>>> theirs:sample.txt
And here is another line that is cleanly resolved or unmodified.
The area where a pair of conflicting changes happened is marked with markers <<<<<<<, =======, and >>>>>>>. The part before the ======= is typically your side, and the part afterwards is typically their side.

The default format does not show what the original said in the conflicting area. You cannot tell how many lines are deleted and replaced with Barbie’s remark on your side. The only thing you can tell is that your side wants to say it is hard and you’d prefer to go shopping, while the other side wants to claim it is easy.

An alternative style can be used by setting the "merge.conflictStyle" configuration variable to "diff3". In "diff3" style, the above conflict may look like this:

Here are lines that are either unchanged from the common
ancestor, or cleanly resolved because only one side changed.
<<<<<<< yours:sample.txt
Conflict resolution is hard;
let's go shopping.
|||||||
Conflict resolution is hard.
=======
Git makes conflict resolution easy.
>>>>>>> theirs:sample.txt
And here is another line that is cleanly resolved or unmodified.
In addition to the <<<<<<<, =======, and >>>>>>> markers, it uses another ||||||| marker that is followed by the original text. You can tell that the original just stated a fact, and your side simply gave in to that statement and gave up, while the other side tried to have a more positive attitude. You can sometimes come up with a better resolution by viewing the original.

HOW TO RESOLVE CONFLICTS
After seeing a conflict, you can do two things:

Decide not to merge. The only clean-ups you need are to reset the index file to the HEAD commit to reverse 2. and to clean up working tree changes made by 2. and 3.; git merge --abort can be used for this.

Resolve the conflicts. Git will mark the conflicts in the working tree. Edit the files into shape and git add them to the index. Use git commit to seal the deal.

You can work through the conflict with a number of tools:

Use a mergetool. git mergetool to launch a graphical mergetool which will work you through the merge.

Look at the diffs. git diff will show a three-way diff, highlighting changes from both the HEAD and MERGE_HEAD versions.

Look at the diffs from each branch. git log --merge -p <path> will show diffs first for the HEAD version and then the MERGE_HEAD version.

Look at the originals. git show :1:filename shows the common ancestor, git show :2:filename shows the HEAD version, and git show :3:filename shows the MERGE_HEAD version.

EXAMPLES
Merge branches fixes and enhancements on top of the current branch, making an octopus merge:

$ git merge fixes enhancements
Merge branch obsolete into the current branch, using ours merge strategy:

$ git merge -s ours obsolete
Merge branch maint into the current branch, but do not make a new commit automatically:

$ git merge --no-commit maint
This can be used when you want to include further changes to the merge, or want to write your own merge commit message.

You should refrain from abusing this option to sneak substantial changes into a merge commit. Small fixups like bumping release/version name would be acceptable.

MERGE STRATEGIES
The merge mechanism (git merge and git pull commands) allows the backend merge strategies to be chosen with -s option. Some strategies can also take their own options, which can be passed by giving -X<option> arguments to git merge and/or git pull.

resolve
This can only resolve two heads (i.e. the current branch and another branch you pulled from) using a 3-way merge algorithm. It tries to carefully detect criss-cross merge ambiguities and is considered generally safe and fast.

recursive
This can only resolve two heads using a 3-way merge algorithm. When there is more than one common ancestor that can be used for 3-way merge, it creates a merged tree of the common ancestors and uses that as the reference tree for the 3-way merge. This has been reported to result in fewer merge conflicts without causing mismerges by tests done on actual merge commits taken from Linux 2.6 kernel development history. Additionally this can detect and handle merges involving renames. This is the default merge strategy when pulling or merging one branch.

The recursive strategy can take the following options:

ours
This option forces conflicting hunks to be auto-resolved cleanly by favoring our version. Changes from the other tree that do not conflict with our side are reflected to the merge result. For a binary file, the entire contents are taken from our side.

This should not be confused with the ours merge strategy, which does not even look at what the other tree contains at all. It discards everything the other tree did, declaring our history contains all that happened in it.

theirs
This is the opposite of ours.

patience
With this option, merge-recursive spends a little extra time to avoid mismerges that sometimes occur due to unimportant matching lines (e.g., braces from distinct functions). Use this when the branches to be merged have diverged wildly. See also git-diff(1) --patience.

diff-algorithm=[patience|minimal|histogram|myers]
Tells merge-recursive to use a different diff algorithm, which can help avoid mismerges that occur due to unimportant matching lines (such as braces from distinct functions). See also git-diff(1) --diff-algorithm.

ignore-space-change
ignore-all-space
ignore-space-at-eol
Treats lines with the indicated type of whitespace change as unchanged for the sake of a three-way merge. Whitespace changes mixed with other changes to a line are not ignored. See also git-diff(1) -b, -w, and --ignore-space-at-eol.

If their version only introduces whitespace changes to a line, our version is used;

If our version introduces whitespace changes but their version includes a substantial change, their version is used;

Otherwise, the merge proceeds in the usual way.

renormalize
This runs a virtual check-out and check-in of all three stages of a file when resolving a three-way merge. This option is meant to be used when merging branches with different clean filters or end-of-line normalization rules. See "Merging branches with differing checkin/checkout attributes" in gitattributes(5) for details.

no-renormalize
Disables the renormalize option. This overrides the merge.renormalize configuration variable.

no-renames
Turn off rename detection. See also git-diff(1) --no-renames.

find-renames[=<n>]
Turn on rename detection, optionally setting the similarity threshold. This is the default. See also git-diff(1) --find-renames.

rename-threshold=<n>
Deprecated synonym for find-renames=<n>.

subtree[=<path>]
This option is a more advanced form of subtree strategy, where the strategy makes a guess on how two trees must be shifted to match with each other when merging. Instead, the specified path is prefixed (or stripped from the beginning) to make the shape of two trees to match.
octopus
This resolves cases with more than two heads, but refuses to do a complex merge that needs manual resolution. It is primarily meant to be used for bundling topic branch heads together. This is the default merge strategy when pulling or merging more than one branch.

ours
This resolves any number of heads, but the resulting tree of the merge is always that of the current branch head, effectively ignoring all changes from all other branches. It is meant to be used to supersede old development history of side branches. Note that this is different from the -Xours option to the recursive merge strategy.

subtree
This is a modified recursive strategy. When merging trees A and B, if B corresponds to a subtree of A, B is first adjusted to match the tree structure of A, instead of reading the trees at the same level. This adjustment is also done to the common ancestor tree.
With the strategies that use 3-way merge (including the default, recursive), if a change is made on both branches, but later reverted on one of the branches, that change will be present in the merged result; some people find this behavior confusing. It occurs because only the heads and the merge base are considered when performing a merge, not the individual commits. The merge algorithm therefore considers the reverted change as no change at all, and substitutes the changed version instead.

CONFIGURATION
merge.conflictStyle
Specify the style in which conflicted hunks are written out to working tree files upon merge. The default is "merge", which shows a <<<<<<< conflict marker, changes made by one side, a ======= marker, changes made by the other side, and then a >>>>>>> marker. An alternate style, "diff3", adds a ||||||| marker and the original text before the ======= marker.

merge.defaultToUpstream
If merge is called without any commit argument, merge the upstream branches configured for the current branch by using their last observed values stored in their remote-tracking branches. The values of the branch.<current branch>.merge that name the branches at the remote named by branch.<current branch>.remote are consulted, and then they are mapped via remote.<remote>.fetch to their corresponding remote-tracking branches, and the tips of these tracking branches are merged.

merge.ff
By default, Git does not create an extra merge commit when merging a commit that is a descendant of the current commit. Instead, the tip of the current branch is fast-forwarded. When set to false, this variable tells Git to create an extra merge commit in such a case (equivalent to giving the --no-ff option from the command line). When set to only, only such fast-forward merges are allowed (equivalent to giving the --ff-only option from the command line).

merge.branchdesc
In addition to branch names, populate the log message with the branch description text associated with them. Defaults to false.

merge.log
In addition to branch names, populate the log message with at most the specified number of one-line descriptions from the actual commits that are being merged. Defaults to false, and true is a synonym for 20.

merge.renameLimit
The number of files to consider when performing rename detection during a merge; if not specified, defaults to the value of diff.renameLimit.

merge.renormalize
Tell Git that canonical representation of files in the repository has changed over time (e.g. earlier commits record text files with CRLF line endings, but recent ones use LF line endings). In such a repository, Git can convert the data recorded in commits to a canonical form before performing a merge to reduce unnecessary conflicts. For more information, see section "Merging branches with differing checkin/checkout attributes" in gitattributes(5).

merge.stat
Whether to print the diffstat between ORIG_HEAD and the merge result at the end of the merge. True by default.

merge.tool
Controls which merge tool is used by git-mergetool(1). The list below shows the valid built-in values. Any other value is treated as a custom merge tool and requires that a corresponding mergetool.<tool>.cmd variable is defined.

araxis

bc

bc3

codecompare

deltawalker

diffmerge

diffuse

ecmerge

emerge

examdiff

gvimdiff

gvimdiff2

gvimdiff3

kdiff3

meld

opendiff

p4merge

tkdiff

tortoisemerge

vimdiff

vimdiff2

vimdiff3

winmerge

xxdiff

merge.verbosity
Controls the amount of output shown by the recursive merge strategy. Level 0 outputs nothing except a final error message if conflicts were detected. Level 1 outputs only conflicts, 2 outputs conflicts and file changes. Level 5 and above outputs debugging information. The default is level 2. Can be overridden by the GIT_MERGE_VERBOSITY environment variable.

merge.<driver>.name
Defines a human-readable name for a custom low-level merge driver. See gitattributes(5) for details.

merge.<driver>.driver
Defines the command that implements a custom low-level merge driver. See gitattributes(5) for details.

merge.<driver>.recursive
Names a low-level merge driver to be used when performing an internal merge between common ancestors. See gitattributes(5) for details.

branch.<name>.mergeOptions
Sets default options for merging into branch <name>. The syntax and supported options are the same as those of git merge, but option values containing whitespace characters are currently not supported.
SEE ALSO
git-fmt-merge-msg(1), git-pull(1), gitattributes(5), git-reset(1), git-diff(1), git-ls-files(1), git-add(1), git-rm(1), git-mergetool(1)

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

### git fetch
```sh
git-fetch(1) Manual Page
NAME
git-fetch - Download objects and refs from another repository

SYNOPSIS
git fetch [<options>] [<repository> [<refspec>…​]]
git fetch [<options>] <group>
git fetch --multiple [<options>] [(<repository> | <group>)…​]
git fetch --all [<options>]
DESCRIPTION
Fetch branches and/or tags (collectively, "refs") from one or more other repositories, along with the objects necessary to complete their histories. Remote-tracking branches are updated (see the description of <refspec> below for ways to control this behavior).

By default, any tag that points into the histories being fetched is also fetched; the effect is to fetch tags that point at branches that you are interested in. This default behavior can be changed by using the --tags or --no-tags options or by configuring remote.<name>.tagOpt. By using a refspec that fetches tags explicitly, you can fetch tags that do not point into branches you are interested in as well.

git fetch can fetch from either a single named repository or URL, or from several repositories at once if <group> is given and there is a remotes.<group> entry in the configuration file. (See git-config(1)).

When no remote is specified, by default the origin remote will be used, unless there’s an upstream branch configured for the current branch.

The names of refs that are fetched, together with the object names they point at, are written to .git/FETCH_HEAD. This information may be used by scripts or other git commands, such as git-pull(1).

OPTIONS
--all
Fetch all remotes.

-a
--append
Append ref names and object names of fetched refs to the existing contents of .git/FETCH_HEAD. Without this option old data in .git/FETCH_HEAD will be overwritten.

--depth=<depth>
Limit fetching to the specified number of commits from the tip of each remote branch history. If fetching to a shallow repository created by git clone with --depth=<depth> option (see git-clone(1)), deepen or shorten the history to the specified number of commits. Tags for the deepened commits are not fetched.

--deepen=<depth>
Similar to --depth, except it specifies the number of commits from the current shallow boundary instead of from the tip of each remote branch history.

--shallow-since=<date>
Deepen or shorten the history of a shallow repository to include all reachable commits after <date>.

--shallow-exclude=<revision>
Deepen or shorten the history of a shallow repository to exclude commits reachable from a specified remote branch or tag. This option can be specified multiple times.

--unshallow
If the source repository is complete, convert a shallow repository to a complete one, removing all the limitations imposed by shallow repositories.

If the source repository is shallow, fetch as much as possible so that the current repository has the same history as the source repository.

--update-shallow
By default when fetching from a shallow repository, git fetch refuses refs that require updating .git/shallow. This option updates .git/shallow and accept such refs.

--dry-run
Show what would be done, without making any changes.

-f
--force
When git fetch is used with <rbranch>:<lbranch> refspec, it refuses to update the local branch <lbranch> unless the remote branch <rbranch> it fetches is a descendant of <lbranch>. This option overrides that check.

-k
--keep
Keep downloaded pack.

--multiple
Allow several <repository> and <group> arguments to be specified. No <refspec>s may be specified.

-p
--prune
Before fetching, remove any remote-tracking references that no longer exist on the remote. Tags are not subject to pruning if they are fetched only because of the default tag auto-following or due to a --tags option. However, if tags are fetched due to an explicit refspec (either on the command line or in the remote configuration, for example if the remote was cloned with the --mirror option), then they are also subject to pruning.

-n
--no-tags
By default, tags that point at objects that are downloaded from the remote repository are fetched and stored locally. This option disables this automatic tag following. The default behavior for a remote may be specified with the remote.<name>.tagOpt setting. See git-config(1).

--refmap=<refspec>
When fetching refs listed on the command line, use the specified refspec (can be given more than once) to map the refs to remote-tracking branches, instead of the values of remote.*.fetch configuration variables for the remote repository. See section on "Configured Remote-tracking Branches" for details.

-t
--tags
Fetch all tags from the remote (i.e., fetch remote tags refs/tags/* into local tags with the same name), in addition to whatever else would otherwise be fetched. Using this option alone does not subject tags to pruning, even if --prune is used (though tags may be pruned anyway if they are also the destination of an explicit refspec; see --prune).

--recurse-submodules[=yes|on-demand|no]
This option controls if and under what conditions new commits of populated submodules should be fetched too. It can be used as a boolean option to completely disable recursion when set to no or to unconditionally recurse into all populated submodules when set to yes, which is the default when this option is used without any value. Use on-demand to only recurse into a populated submodule when the superproject retrieves a commit that updates the submodule’s reference to a commit that isn’t already in the local submodule clone.

-j
--jobs=<n>
Number of parallel children to be used for fetching submodules. Each will fetch from different submodules, such that fetching many submodules will be faster. By default submodules will be fetched one at a time.

--no-recurse-submodules
Disable recursive fetching of submodules (this has the same effect as using the --recurse-submodules=no option).

--submodule-prefix=<path>
Prepend <path> to paths printed in informative messages such as "Fetching submodule foo". This option is used internally when recursing over submodules.

--recurse-submodules-default=[yes|on-demand]
This option is used internally to temporarily provide a non-negative default value for the --recurse-submodules option. All other methods of configuring fetch’s submodule recursion (such as settings in gitmodules(5) and git-config(1)) override this option, as does specifying --[no-]recurse-submodules directly.

-u
--update-head-ok
By default git fetch refuses to update the head which corresponds to the current branch. This flag disables the check. This is purely for the internal use for git pull to communicate with git fetch, and unless you are implementing your own Porcelain you are not supposed to use it.

--upload-pack <upload-pack>
When given, and the repository to fetch from is handled by git fetch-pack, --exec=<upload-pack> is passed to the command to specify non-default path for the command run on the other end.

-q
--quiet
Pass --quiet to git-fetch-pack and silence any other internally used git commands. Progress is not reported to the standard error stream.

-v
--verbose
Be verbose.

--progress
Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

-4
--ipv4
Use IPv4 addresses only, ignoring IPv6 addresses.

-6
--ipv6
Use IPv6 addresses only, ignoring IPv4 addresses.

<repository>
The "remote" repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section GIT URLS below) or the name of a remote (see the section REMOTES below).

<group>
A name referring to a list of repositories as the value of remotes.<group> in the configuration file. (See git-config(1)).

<refspec>
Specifies which refs to fetch and which local refs to update. When no <refspec>s appear on the command line, the refs to fetch are read from remote.<repository>.fetch variables instead (see CONFIGURED REMOTE-TRACKING BRANCHES below).

The format of a <refspec> parameter is an optional plus +, followed by the source ref <src>, followed by a colon :, followed by the destination ref <dst>. The colon can be omitted when <dst> is empty.

tag <tag> means the same as refs/tags/<tag>:refs/tags/<tag>; it requests fetching everything up to the given tag.

The remote ref that matches <src> is fetched, and if <dst> is not empty string, the local ref that matches it is fast-forwarded using <src>. If the optional plus + is used, the local ref is updated even if it does not result in a fast-forward update.

NOTE
When the remote branch you want to fetch is known to be rewound and rebased regularly, it is expected that its new tip will not be descendant of its previous tip (as stored in your remote-tracking branch the last time you fetched). You would want to use the + sign to indicate non-fast-forward updates will be needed for such branches. There is no way to determine or declare that a branch will be made available in a repository with this behavior; the pulling user simply must know this is the expected usage pattern for a branch.
GIT URLS
In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching, but this is inefficient and deprecated; do not use it).

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

ssh://[user@]host.xz[:port]/path/to/repo.git/

git://host.xz[:port]/path/to/repo.git/

http[s]://host.xz[:port]/path/to/repo.git/

ftp[s]://host.xz[:port]/path/to/repo.git/

An alternative scp-like syntax may also be used with the ssh protocol:

[user@]host.xz:path/to/repo.git/

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path foo:bar could be specified as an absolute path or ./foo:bar to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support ~username expansion:

ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/

git://host.xz[:port]/~[user]/path/to/repo.git/

[user@]host.xz:/~[user]/path/to/repo.git/

For local repositories, also supported by Git natively, the following syntaxes may be used:

/path/to/repo.git/

file:///path/to/repo.git/

These two syntaxes are mostly equivalent, except when cloning, when the former implies --local option. See git-clone(1) for details.

When Git doesn’t know how to handle a certain transport protocol, it attempts to use the remote-<transport> remote helper, if one exists. To explicitly request a remote helper, the following syntax may be used:

<transport>::<address>

where <address> may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being invoked. See gitremote-helpers(1) for details.

If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

	[url "<actual url base>"]
		insteadOf = <other url base>
For example, with this:

	[url "git://git.host.xz/"]
		insteadOf = host.xz:/path/to/
		insteadOf = work:
a URL like "work:repo.git" or like "host.xz:/path/to/repo.git" will be rewritten in any context that takes a URL to be "git://git.host.xz/repo.git".

If you want to rewrite URLs for push only, you can create a configuration section of the form:

	[url "<actual url base>"]
		pushInsteadOf = <other url base>
For example, with this:

	[url "ssh://example.org/"]
		pushInsteadOf = git://example.org/
a URL like "git://example.org/path/to/repo.git" will be rewritten to "ssh://example.org/path/to/repo.git" for pushes, but pulls will still use the original URL.

REMOTES
The name of one of the following can be used instead of a URL as <repository> argument:

a remote in the Git configuration file: $GIT_DIR/config,

a file in the $GIT_DIR/remotes directory, or

a file in the $GIT_DIR/branches directory.

All of these also allow you to omit the refspec from the command line because they each contain a refspec which git will use by default.

Named remote in configuration file
You can choose to provide the name of a remote which you had previously configured using git-remote(1), git-config(1) or even by a manual edit to the $GIT_DIR/config file. The URL of this remote will be used to access the repository. The refspec of this remote will be used by default when you do not provide a refspec on the command line. The entry in the config file would appear like this:

	[remote "<name>"]
		url = <url>
		pushurl = <pushurl>
		push = <refspec>
		fetch = <refspec>
The <pushurl> is used for pushes only. It is optional and defaults to <url>.

Named file in $GIT_DIR/remotes
You can choose to provide the name of a file in $GIT_DIR/remotes. The URL in this file will be used to access the repository. The refspec in this file will be used as default when you do not provide a refspec on the command line. This file should have the following format:

	URL: one of the above URL format
	Push: <refspec>
	Pull: <refspec>
Push: lines are used by git push and Pull: lines are used by git pull and git fetch. Multiple Push: and Pull: lines may be specified for additional branch mappings.

Named file in $GIT_DIR/branches
You can choose to provide the name of a file in $GIT_DIR/branches. The URL in this file will be used to access the repository. This file should have the following format:

	<url>#<head>
<url> is required; #<head> is optional.

Depending on the operation, git will use one of the following refspecs, if you don’t provide one on the command line. <branch> is the name of this file in $GIT_DIR/branches and <head> defaults to master.

git fetch uses:

	refs/heads/<head>:refs/heads/<branch>
git push uses:

	HEAD:refs/heads/<head>
CONFIGURED REMOTE-TRACKING BRANCHES
You often interact with the same remote repository by regularly and repeatedly fetching from it. In order to keep track of the progress of such a remote repository, git fetch allows you to configure remote.<repository>.fetch configuration variables.

Typically such a variable may look like this:

[remote "origin"]
	fetch = +refs/heads/*:refs/remotes/origin/*
This configuration is used in two ways:

When git fetch is run without specifying what branches and/or tags to fetch on the command line, e.g. git fetch origin or git fetch, remote.<repository>.fetch values are used as the refspecs—​they specify which refs to fetch and which local refs to update. The example above will fetch all branches that exist in the origin (i.e. any ref that matches the left-hand side of the value, refs/heads/*) and update the corresponding remote-tracking branches in the refs/remotes/origin/* hierarchy.

When git fetch is run with explicit branches and/or tags to fetch on the command line, e.g. git fetch origin master, the <refspec>s given on the command line determine what are to be fetched (e.g. master in the example, which is a short-hand for master:, which in turn means "fetch the master branch but I do not explicitly say what remote-tracking branch to update with it from the command line"), and the example command will fetch only the master branch. The remote.<repository>.fetch values determine which remote-tracking branch, if any, is updated. When used in this way, the remote.<repository>.fetch values do not have any effect in deciding what gets fetched (i.e. the values are not used as refspecs when the command-line lists refspecs); they are only used to decide where the refs that are fetched are stored by acting as a mapping.

The latter use of the remote.<repository>.fetch values can be overridden by giving the --refmap=<refspec> parameter(s) on the command line.

OUTPUT
The output of "git fetch" depends on the transport method used; this section describes the output when fetching over the Git protocol (either locally or via ssh) and Smart HTTP protocol.

The status of the fetch is output in tabular form, with each line representing the status of a single ref. Each line is of the form:

 <flag> <summary> <from> -> <to> [<reason>]
The status of up-to-date refs is shown only if the --verbose option is used.

In compact output mode, specified with configuration variable fetch.output, if either entire <from> or <to> is found in the other string, it will be substituted with * in the other string. For example, master -> origin/master becomes master -> origin/*.

flag
A single character indicating the status of the ref:

(space)
for a successfully fetched fast-forward;

+
for a successful forced update;

-
for a successfully pruned ref;

t
for a successful tag update;

*
for a successfully fetched new ref;

!
for a ref that was rejected or failed to update; and

=
for a ref that was up to date and did not need fetching.
summary
For a successfully fetched ref, the summary shows the old and new values of the ref in a form suitable for using as an argument to git log (this is <old>..<new> in most cases, and <old>...<new> for forced non-fast-forward updates).

from
The name of the remote ref being fetched from, minus its refs/<type>/ prefix. In the case of deletion, the name of the remote ref is "(none)".

to
The name of the local ref being updated, minus its refs/<type>/ prefix.

reason
A human-readable explanation. In the case of successfully fetched refs, no explanation is needed. For a failed ref, the reason for failure is described.
EXAMPLES
Update the remote-tracking branches:

$ git fetch origin
The above command copies all branches from the remote refs/heads/ namespace and stores them to the local refs/remotes/origin/ namespace, unless the branch.<name>.fetch option is used to specify a non-default refspec.

Using refspecs explicitly:

$ git fetch origin +pu:pu maint:tmp
This updates (or creates, as necessary) branches pu and tmp in the local repository by fetching from the branches (respectively) pu and maint from the remote repository.

The pu branch will be updated even if it is does not fast-forward, because it is prefixed with a plus sign; tmp will not be.

Peek at a remote’s branch, without configuring the remote in your local repository:

$ git fetch git://git.kernel.org/pub/scm/git/git.git maint
$ git log FETCH_HEAD
The first command fetches the maint branch from the repository at git://git.kernel.org/pub/scm/git/git.git and the second command uses FETCH_HEAD to examine the branch with git-log(1). The fetched objects will eventually be removed by git’s built-in housekeeping (see git-gc(1)).

SECURITY
The fetch and push protocols are not designed to prevent one side from stealing data from the other repository that was not intended to be shared. If you have private data that you need to protect from a malicious peer, your best option is to store it in another repository. This applies to both clients and servers. In particular, namespaces on a server are not effective for read access control; you should only grant read access to a namespace to clients that you would trust with read access to the entire repository.

The known attack vectors are as follows:

The victim sends "have" lines advertising the IDs of objects it has that are not explicitly intended to be shared but can be used to optimize the transfer if the peer also has them. The attacker chooses an object ID X to steal and sends a ref to X, but isn’t required to send the content of X because the victim already has it. Now the victim believes that the attacker has X, and it sends the content of X back to the attacker later. (This attack is most straightforward for a client to perform on a server, by creating a ref to X in the namespace the client has access to and then fetching it. The most likely way for a server to perform it on a client is to "merge" X into a public branch and hope that the user does additional work on this branch and pushes it back to the server without noticing the merge.)

As in #1, the attacker chooses an object ID X to steal. The victim sends an object Y that the attacker already has, and the attacker falsely claims to have X and not Y, so the victim sends Y as a delta against X. The delta reveals regions of X that are similar to Y to the attacker.

BUGS
Using --recurse-submodules can only fetch new commits in already checked out submodules right now. When e.g. upstream added a new submodule in the just fetched commits of the superproject the submodule itself can not be fetched, making it impossible to check out that submodule later without having to do a fetch again. This is expected to be fixed in a future Git version.

SEE ALSO
git-pull(1)

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

### git pull
```sh
git-pull(1) Manual Page
NAME
git-pull - Fetch from and integrate with another repository or a local branch

SYNOPSIS
git pull [options] [<repository> [<refspec>…​]]
DESCRIPTION
Incorporates changes from a remote repository into the current branch. In its default mode, git pull is shorthand for git fetch followed by git merge FETCH_HEAD.

More precisely, git pull runs git fetch with the given parameters and calls git merge to merge the retrieved branch heads into the current branch. With --rebase, it runs git rebase instead of git merge.

<repository> should be the name of a remote repository as passed to git-fetch(1). <refspec> can name an arbitrary remote ref (for example, the name of a tag) or even a collection of refs with corresponding remote-tracking branches (e.g., refs/heads/*:refs/remotes/origin/*), but usually it is the name of a branch in the remote repository.

Default values for <repository> and <branch> are read from the "remote" and "merge" configuration for the current branch as set by git-branch(1) --track.

Assume the following history exists and the current branch is "master":

	  A---B---C master on origin
	 /
    D---E---F---G master
	^
	origin/master in your repository
Then "git pull" will fetch and replay the changes from the remote master branch since it diverged from the local master (i.e., E) until its current commit (C) on top of master and record the result in a new commit along with the names of the two parent commits and a log message from the user describing the changes.

	  A---B---C origin/master
	 /         \
    D---E---F---G---H master
See git-merge(1) for details, including how conflicts are presented and handled.

In Git 1.7.0 or later, to cancel a conflicting merge, use git reset --merge. Warning: In older versions of Git, running git pull with uncommitted changes is discouraged: while possible, it leaves you in a state that may be hard to back out of in the case of a conflict.

If any of the remote changes overlap with local uncommitted changes, the merge will be automatically cancelled and the work tree untouched. It is generally best to get any local changes in working order before pulling or stash them away with git-stash(1).

OPTIONS
-q
--quiet
This is passed to both underlying git-fetch to squelch reporting of during transfer, and underlying git-merge to squelch output during merging.

-v
--verbose
Pass --verbose to git-fetch and git-merge.

--[no-]recurse-submodules[=yes|on-demand|no]
This option controls if new commits of all populated submodules should be fetched too (see git-config(1) and gitmodules(5)). That might be necessary to get the data needed for merging submodule commits, a feature Git learned in 1.7.3. Notice that the result of a merge will not be checked out in the submodule, "git submodule update" has to be called afterwards to bring the work tree up to date with the merge result.
Options related to merging
--commit
--no-commit
Perform the merge and commit the result. This option can be used to override --no-commit.

With --no-commit perform the merge but pretend the merge failed and do not autocommit, to give the user a chance to inspect and further tweak the merge result before committing.

--edit
-e
--no-edit
Invoke an editor before committing successful mechanical merge to further edit the auto-generated merge message, so that the user can explain and justify the merge. The --no-edit option can be used to accept the auto-generated message (this is generally discouraged).

Older scripts may depend on the historical behaviour of not allowing the user to edit the merge log message. They will see an editor opened when they run git merge. To make it easier to adjust such scripts to the updated behaviour, the environment variable GIT_MERGE_AUTOEDIT can be set to no at the beginning of them.

--ff
When the merge resolves as a fast-forward, only update the branch pointer, without creating a merge commit. This is the default behavior.

--no-ff
Create a merge commit even when the merge resolves as a fast-forward. This is the default behaviour when merging an annotated (and possibly signed) tag.

--ff-only
Refuse to merge and exit with a non-zero status unless the current HEAD is already up-to-date or the merge can be resolved as a fast-forward.

--log[=<n>]
--no-log
In addition to branch names, populate the log message with one-line descriptions from at most <n> actual commits that are being merged. See also git-fmt-merge-msg(1).

With --no-log do not list one-line descriptions from the actual commits being merged.

--stat
-n
--no-stat
Show a diffstat at the end of the merge. The diffstat is also controlled by the configuration option merge.stat.

With -n or --no-stat do not show a diffstat at the end of the merge.

--squash
--no-squash
Produce the working tree and index state as if a real merge happened (except for the merge information), but do not actually make a commit, move the HEAD, or record $GIT_DIR/MERGE_HEAD (to cause the next git commit command to create a merge commit). This allows you to create a single commit on top of the current branch whose effect is the same as merging another branch (or more in case of an octopus).

With --no-squash perform the merge and commit the result. This option can be used to override --squash.

-s <strategy>
--strategy=<strategy>
Use the given merge strategy; can be supplied more than once to specify them in the order they should be tried. If there is no -s option, a built-in list of strategies is used instead (git merge-recursive when merging a single head, git merge-octopus otherwise).

-X <option>
--strategy-option=<option>
Pass merge strategy specific option through to the merge strategy.

--verify-signatures
--no-verify-signatures
Verify that the tip commit of the side branch being merged is signed with a valid key, i.e. a key that has a valid uid: in the default trust model, this means the signing key has been signed by a trusted key. If the tip commit of the side branch is not signed with a valid key, the merge is aborted.

--summary
--no-summary
Synonyms to --stat and --no-stat; these are deprecated and will be removed in the future.

--allow-unrelated-histories
By default, git merge command refuses to merge histories that do not share a common ancestor. This option can be used to override this safety when merging histories of two projects that started their lives independently. As that is a very rare occasion, no configuration variable to enable this by default exists and will not be added.

-r
--rebase[=false|true|preserve|interactive]
When true, rebase the current branch on top of the upstream branch after fetching. If there is a remote-tracking branch corresponding to the upstream branch and the upstream branch was rebased since last fetched, the rebase uses that information to avoid rebasing non-local changes.

When set to preserve, rebase with the --preserve-merges option passed to git rebase so that locally created merge commits will not be flattened.

When false, merge the current branch into the upstream branch.

When interactive, enable the interactive mode of rebase.

See pull.rebase, branch.<name>.rebase and branch.autoSetupRebase in git-config(1) if you want to make git pull always use --rebase instead of merging.

NOTE
This is a potentially dangerous mode of operation. It rewrites history, which does not bode well when you published that history already. Do not use this option unless you have read git-rebase(1) carefully.
--no-rebase
Override earlier --rebase.

--autostash
--no-autostash
Before starting rebase, stash local modifications away (see git-stash(1)) if needed, and apply the stash when done. --no-autostash is useful to override the rebase.autoStash configuration variable (see git-config(1)).

This option is only valid when "--rebase" is used.

Options related to fetching
--all
Fetch all remotes.

-a
--append
Append ref names and object names of fetched refs to the existing contents of .git/FETCH_HEAD. Without this option old data in .git/FETCH_HEAD will be overwritten.

--depth=<depth>
Limit fetching to the specified number of commits from the tip of each remote branch history. If fetching to a shallow repository created by git clone with --depth=<depth> option (see git-clone(1)), deepen or shorten the history to the specified number of commits. Tags for the deepened commits are not fetched.

--deepen=<depth>
Similar to --depth, except it specifies the number of commits from the current shallow boundary instead of from the tip of each remote branch history.

--shallow-since=<date>
Deepen or shorten the history of a shallow repository to include all reachable commits after <date>.

--shallow-exclude=<revision>
Deepen or shorten the history of a shallow repository to exclude commits reachable from a specified remote branch or tag. This option can be specified multiple times.

--unshallow
If the source repository is complete, convert a shallow repository to a complete one, removing all the limitations imposed by shallow repositories.

If the source repository is shallow, fetch as much as possible so that the current repository has the same history as the source repository.

--update-shallow
By default when fetching from a shallow repository, git fetch refuses refs that require updating .git/shallow. This option updates .git/shallow and accept such refs.

-f
--force
When git fetch is used with <rbranch>:<lbranch> refspec, it refuses to update the local branch <lbranch> unless the remote branch <rbranch> it fetches is a descendant of <lbranch>. This option overrides that check.

-k
--keep
Keep downloaded pack.

--no-tags
By default, tags that point at objects that are downloaded from the remote repository are fetched and stored locally. This option disables this automatic tag following. The default behavior for a remote may be specified with the remote.<name>.tagOpt setting. See git-config(1).

-u
--update-head-ok
By default git fetch refuses to update the head which corresponds to the current branch. This flag disables the check. This is purely for the internal use for git pull to communicate with git fetch, and unless you are implementing your own Porcelain you are not supposed to use it.

--upload-pack <upload-pack>
When given, and the repository to fetch from is handled by git fetch-pack, --exec=<upload-pack> is passed to the command to specify non-default path for the command run on the other end.

--progress
Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

-4
--ipv4
Use IPv4 addresses only, ignoring IPv6 addresses.

-6
--ipv6
Use IPv6 addresses only, ignoring IPv4 addresses.

<repository>
The "remote" repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section GIT URLS below) or the name of a remote (see the section REMOTES below).

<refspec>
Specifies which refs to fetch and which local refs to update. When no <refspec>s appear on the command line, the refs to fetch are read from remote.<repository>.fetch variables instead (see git-fetch(1)).

The format of a <refspec> parameter is an optional plus +, followed by the source ref <src>, followed by a colon :, followed by the destination ref <dst>. The colon can be omitted when <dst> is empty.

tag <tag> means the same as refs/tags/<tag>:refs/tags/<tag>; it requests fetching everything up to the given tag.

The remote ref that matches <src> is fetched, and if <dst> is not empty string, the local ref that matches it is fast-forwarded using <src>. If the optional plus + is used, the local ref is updated even if it does not result in a fast-forward update.

NOTE
When the remote branch you want to fetch is known to be rewound and rebased regularly, it is expected that its new tip will not be descendant of its previous tip (as stored in your remote-tracking branch the last time you fetched). You would want to use the + sign to indicate non-fast-forward updates will be needed for such branches. There is no way to determine or declare that a branch will be made available in a repository with this behavior; the pulling user simply must know this is the expected usage pattern for a branch.
NOTE
There is a difference between listing multiple <refspec> directly on git pull command line and having multiple remote.<repository>.fetch entries in your configuration for a <repository> and running a git pull command without any explicit <refspec> parameters. <refspec>s listed explicitly on the command line are always merged into the current branch after fetching. In other words, if you list more than one remote ref, git pull will create an Octopus merge. On the other hand, if you do not list any explicit <refspec> parameter on the command line, git pull will fetch all the <refspec>s it finds in the remote.<repository>.fetch configuration and merge only the first <refspec> found into the current branch. This is because making an Octopus from remote refs is rarely done, while keeping track of multiple remote heads in one-go by fetching more than one is often useful.
GIT URLS
In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching, but this is inefficient and deprecated; do not use it).

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

ssh://[user@]host.xz[:port]/path/to/repo.git/

git://host.xz[:port]/path/to/repo.git/

http[s]://host.xz[:port]/path/to/repo.git/

ftp[s]://host.xz[:port]/path/to/repo.git/

An alternative scp-like syntax may also be used with the ssh protocol:

[user@]host.xz:path/to/repo.git/

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path foo:bar could be specified as an absolute path or ./foo:bar to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support ~username expansion:

ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/

git://host.xz[:port]/~[user]/path/to/repo.git/

[user@]host.xz:/~[user]/path/to/repo.git/

For local repositories, also supported by Git natively, the following syntaxes may be used:

/path/to/repo.git/

file:///path/to/repo.git/

These two syntaxes are mostly equivalent, except when cloning, when the former implies --local option. See git-clone(1) for details.

When Git doesn’t know how to handle a certain transport protocol, it attempts to use the remote-<transport> remote helper, if one exists. To explicitly request a remote helper, the following syntax may be used:

<transport>::<address>

where <address> may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being invoked. See gitremote-helpers(1) for details.

If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

	[url "<actual url base>"]
		insteadOf = <other url base>
For example, with this:

	[url "git://git.host.xz/"]
		insteadOf = host.xz:/path/to/
		insteadOf = work:
a URL like "work:repo.git" or like "host.xz:/path/to/repo.git" will be rewritten in any context that takes a URL to be "git://git.host.xz/repo.git".

If you want to rewrite URLs for push only, you can create a configuration section of the form:

	[url "<actual url base>"]
		pushInsteadOf = <other url base>
For example, with this:

	[url "ssh://example.org/"]
		pushInsteadOf = git://example.org/
a URL like "git://example.org/path/to/repo.git" will be rewritten to "ssh://example.org/path/to/repo.git" for pushes, but pulls will still use the original URL.

REMOTES
The name of one of the following can be used instead of a URL as <repository> argument:

a remote in the Git configuration file: $GIT_DIR/config,

a file in the $GIT_DIR/remotes directory, or

a file in the $GIT_DIR/branches directory.

All of these also allow you to omit the refspec from the command line because they each contain a refspec which git will use by default.

Named remote in configuration file
You can choose to provide the name of a remote which you had previously configured using git-remote(1), git-config(1) or even by a manual edit to the $GIT_DIR/config file. The URL of this remote will be used to access the repository. The refspec of this remote will be used by default when you do not provide a refspec on the command line. The entry in the config file would appear like this:

	[remote "<name>"]
		url = <url>
		pushurl = <pushurl>
		push = <refspec>
		fetch = <refspec>
The <pushurl> is used for pushes only. It is optional and defaults to <url>.

Named file in $GIT_DIR/remotes
You can choose to provide the name of a file in $GIT_DIR/remotes. The URL in this file will be used to access the repository. The refspec in this file will be used as default when you do not provide a refspec on the command line. This file should have the following format:

	URL: one of the above URL format
	Push: <refspec>
	Pull: <refspec>
Push: lines are used by git push and Pull: lines are used by git pull and git fetch. Multiple Push: and Pull: lines may be specified for additional branch mappings.

Named file in $GIT_DIR/branches
You can choose to provide the name of a file in $GIT_DIR/branches. The URL in this file will be used to access the repository. This file should have the following format:

	<url>#<head>
<url> is required; #<head> is optional.

Depending on the operation, git will use one of the following refspecs, if you don’t provide one on the command line. <branch> is the name of this file in $GIT_DIR/branches and <head> defaults to master.

git fetch uses:

	refs/heads/<head>:refs/heads/<branch>
git push uses:

	HEAD:refs/heads/<head>
MERGE STRATEGIES
The merge mechanism (git merge and git pull commands) allows the backend merge strategies to be chosen with -s option. Some strategies can also take their own options, which can be passed by giving -X<option> arguments to git merge and/or git pull.

resolve
This can only resolve two heads (i.e. the current branch and another branch you pulled from) using a 3-way merge algorithm. It tries to carefully detect criss-cross merge ambiguities and is considered generally safe and fast.

recursive
This can only resolve two heads using a 3-way merge algorithm. When there is more than one common ancestor that can be used for 3-way merge, it creates a merged tree of the common ancestors and uses that as the reference tree for the 3-way merge. This has been reported to result in fewer merge conflicts without causing mismerges by tests done on actual merge commits taken from Linux 2.6 kernel development history. Additionally this can detect and handle merges involving renames. This is the default merge strategy when pulling or merging one branch.

The recursive strategy can take the following options:

ours
This option forces conflicting hunks to be auto-resolved cleanly by favoring our version. Changes from the other tree that do not conflict with our side are reflected to the merge result. For a binary file, the entire contents are taken from our side.

This should not be confused with the ours merge strategy, which does not even look at what the other tree contains at all. It discards everything the other tree did, declaring our history contains all that happened in it.

theirs
This is the opposite of ours.

patience
With this option, merge-recursive spends a little extra time to avoid mismerges that sometimes occur due to unimportant matching lines (e.g., braces from distinct functions). Use this when the branches to be merged have diverged wildly. See also git-diff(1) --patience.

diff-algorithm=[patience|minimal|histogram|myers]
Tells merge-recursive to use a different diff algorithm, which can help avoid mismerges that occur due to unimportant matching lines (such as braces from distinct functions). See also git-diff(1) --diff-algorithm.

ignore-space-change
ignore-all-space
ignore-space-at-eol
Treats lines with the indicated type of whitespace change as unchanged for the sake of a three-way merge. Whitespace changes mixed with other changes to a line are not ignored. See also git-diff(1) -b, -w, and --ignore-space-at-eol.

If their version only introduces whitespace changes to a line, our version is used;

If our version introduces whitespace changes but their version includes a substantial change, their version is used;

Otherwise, the merge proceeds in the usual way.

renormalize
This runs a virtual check-out and check-in of all three stages of a file when resolving a three-way merge. This option is meant to be used when merging branches with different clean filters or end-of-line normalization rules. See "Merging branches with differing checkin/checkout attributes" in gitattributes(5) for details.

no-renormalize
Disables the renormalize option. This overrides the merge.renormalize configuration variable.

no-renames
Turn off rename detection. See also git-diff(1) --no-renames.

find-renames[=<n>]
Turn on rename detection, optionally setting the similarity threshold. This is the default. See also git-diff(1) --find-renames.

rename-threshold=<n>
Deprecated synonym for find-renames=<n>.

subtree[=<path>]
This option is a more advanced form of subtree strategy, where the strategy makes a guess on how two trees must be shifted to match with each other when merging. Instead, the specified path is prefixed (or stripped from the beginning) to make the shape of two trees to match.
octopus
This resolves cases with more than two heads, but refuses to do a complex merge that needs manual resolution. It is primarily meant to be used for bundling topic branch heads together. This is the default merge strategy when pulling or merging more than one branch.

ours
This resolves any number of heads, but the resulting tree of the merge is always that of the current branch head, effectively ignoring all changes from all other branches. It is meant to be used to supersede old development history of side branches. Note that this is different from the -Xours option to the recursive merge strategy.

subtree
This is a modified recursive strategy. When merging trees A and B, if B corresponds to a subtree of A, B is first adjusted to match the tree structure of A, instead of reading the trees at the same level. This adjustment is also done to the common ancestor tree.
With the strategies that use 3-way merge (including the default, recursive), if a change is made on both branches, but later reverted on one of the branches, that change will be present in the merged result; some people find this behavior confusing. It occurs because only the heads and the merge base are considered when performing a merge, not the individual commits. The merge algorithm therefore considers the reverted change as no change at all, and substitutes the changed version instead.

DEFAULT BEHAVIOUR
Often people use git pull without giving any parameter. Traditionally, this has been equivalent to saying git pull origin. However, when configuration branch.<name>.remote is present while on branch <name>, that value is used instead of origin.

In order to determine what URL to use to fetch from, the value of the configuration remote.<origin>.url is consulted and if there is not any such variable, the value on URL: ` line in `$GIT_DIR/remotes/<origin> file is used.

In order to determine what remote branches to fetch (and optionally store in the remote-tracking branches) when the command is run without any refspec parameters on the command line, values of the configuration variable remote.<origin>.fetch are consulted, and if there aren’t any, $GIT_DIR/remotes/<origin> file is consulted and its `Pull: ` lines are used. In addition to the refspec formats described in the OPTIONS section, you can have a globbing refspec that looks like this:

refs/heads/*:refs/remotes/origin/*
A globbing refspec must have a non-empty RHS (i.e. must store what were fetched in remote-tracking branches), and its LHS and RHS must end with /*. The above specifies that all remote branches are tracked using remote-tracking branches in refs/remotes/origin/ hierarchy under the same name.

The rule to determine which remote branch to merge after fetching is a bit involved, in order not to break backward compatibility.

If explicit refspecs were given on the command line of git pull, they are all merged.

When no refspec was given on the command line, then git pull uses the refspec from the configuration or $GIT_DIR/remotes/<origin>. In such cases, the following rules apply:

If branch.<name>.merge configuration for the current branch <name> exists, that is the name of the branch at the remote site that is merged.

If the refspec is a globbing one, nothing is merged.

Otherwise the remote branch of the first refspec is merged.

EXAMPLES
Update the remote-tracking branches for the repository you cloned from, then merge one of them into your current branch:

$ git pull, git pull origin
Normally the branch merged in is the HEAD of the remote repository, but the choice is determined by the branch.<name>.remote and branch.<name>.merge options; see git-config(1) for details.

Merge into the current branch the remote branch next:

$ git pull origin next
This leaves a copy of next temporarily in FETCH_HEAD, but does not update any remote-tracking branches. Using remote-tracking branches, the same can be done by invoking fetch and merge:

$ git fetch origin
$ git merge origin/next
If you tried a pull which resulted in complex conflicts and would want to start over, you can recover with git reset.

SECURITY
The fetch and push protocols are not designed to prevent one side from stealing data from the other repository that was not intended to be shared. If you have private data that you need to protect from a malicious peer, your best option is to store it in another repository. This applies to both clients and servers. In particular, namespaces on a server are not effective for read access control; you should only grant read access to a namespace to clients that you would trust with read access to the entire repository.

The known attack vectors are as follows:

The victim sends "have" lines advertising the IDs of objects it has that are not explicitly intended to be shared but can be used to optimize the transfer if the peer also has them. The attacker chooses an object ID X to steal and sends a ref to X, but isn’t required to send the content of X because the victim already has it. Now the victim believes that the attacker has X, and it sends the content of X back to the attacker later. (This attack is most straightforward for a client to perform on a server, by creating a ref to X in the namespace the client has access to and then fetching it. The most likely way for a server to perform it on a client is to "merge" X into a public branch and hope that the user does additional work on this branch and pushes it back to the server without noticing the merge.)

As in #1, the attacker chooses an object ID X to steal. The victim sends an object Y that the attacker already has, and the attacker falsely claims to have X and not Y, so the victim sends Y as a delta against X. The delta reveals regions of X that are similar to Y to the attacker.

BUGS
Using --recurse-submodules can only fetch new commits in already checked out submodules right now. When e.g. upstream added a new submodule in the just fetched commits of the superproject the submodule itself can not be fetched, making it impossible to check out that submodule later without having to do a fetch again. This is expected to be fixed in a future Git version.

SEE ALSO
git-fetch(1), git-merge(1), git-config(1)

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```

### git push
```sh
git-push(1) Manual Page
NAME
git-push - Update remote refs along with associated objects

SYNOPSIS
git push [--all | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
	   [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-v | --verbose]
	   [-u | --set-upstream] [--push-option=<string>]
	   [--[no-]signed|--sign=(true|false|if-asked)]
	   [--force-with-lease[=<refname>[:<expect>]]]
	   [--no-verify] [<repository> [<refspec>…​]]
DESCRIPTION
Updates remote refs using local refs, while sending objects necessary to complete the given refs.

You can make interesting things happen to a repository every time you push into it, by setting up hooks there. See documentation for git-receive-pack(1).

When the command line does not specify where to push with the <repository> argument, branch.*.remote configuration for the current branch is consulted to determine where to push. If the configuration is missing, it defaults to origin.

When the command line does not specify what to push with <refspec>... arguments or --all, --mirror, --tags options, the command finds the default <refspec> by consulting remote.*.push configuration, and if it is not found, honors push.default configuration to decide what to push (See git-config(1) for the meaning of push.default).

When neither the command-line nor the configuration specify what to push, the default behavior is used, which corresponds to the simple value for push.default: the current branch is pushed to the corresponding upstream branch, but as a safety measure, the push is aborted if the upstream branch does not have the same name as the local one.

OPTIONS
<repository>
The "remote" repository that is destination of a push operation. This parameter can be either a URL (see the section GIT URLS below) or the name of a remote (see the section REMOTES below).

<refspec>…​
Specify what destination ref to update with what source object. The format of a <refspec> parameter is an optional plus +, followed by the source object <src>, followed by a colon :, followed by the destination ref <dst>.

The <src> is often the name of the branch you would want to push, but it can be any arbitrary "SHA-1 expression", such as master~4 or HEAD (see gitrevisions(7)).

The <dst> tells which ref on the remote side is updated with this push. Arbitrary expressions cannot be used here, an actual ref must be named. If git push [<repository>] without any <refspec> argument is set to update some ref at the destination with <src> with remote.<repository>.push configuration variable, :<dst> part can be omitted—​such a push will update a ref that <src> normally updates without any <refspec> on the command line. Otherwise, missing :<dst> means to update the same ref as the <src>.

The object referenced by <src> is used to update the <dst> reference on the remote side. By default this is only allowed if <dst> is not a tag (annotated or lightweight), and then only if it can fast-forward <dst>. By having the optional leading +, you can tell Git to update the <dst> ref even if it is not allowed by default (e.g., it is not a fast-forward.) This does not attempt to merge <src> into <dst>. See EXAMPLES below for details.

tag <tag> means the same as refs/tags/<tag>:refs/tags/<tag>.

Pushing an empty <src> allows you to delete the <dst> ref from the remote repository.

The special refspec : (or +: to allow non-fast-forward updates) directs Git to push "matching" branches: for every branch that exists on the local side, the remote side is updated if a branch of the same name already exists on the remote side.

--all
Push all branches (i.e. refs under refs/heads/); cannot be used with other <refspec>.

--prune
Remove remote branches that don’t have a local counterpart. For example a remote branch tmp will be removed if a local branch with the same name doesn’t exist any more. This also respects refspecs, e.g. git push --prune remote refs/heads/*:refs/tmp/* would make sure that remote refs/tmp/foo will be removed if refs/heads/foo doesn’t exist.

--mirror
Instead of naming each ref to push, specifies that all refs under refs/ (which includes but is not limited to refs/heads/, refs/remotes/, and refs/tags/) be mirrored to the remote repository. Newly created local refs will be pushed to the remote end, locally updated refs will be force updated on the remote end, and deleted refs will be removed from the remote end. This is the default if the configuration option remote.<remote>.mirror is set.

-n
--dry-run
Do everything except actually send the updates.

--porcelain
Produce machine-readable output. The output status line for each ref will be tab-separated and sent to stdout instead of stderr. The full symbolic names of the refs will be given.

--delete
All listed refs are deleted from the remote repository. This is the same as prefixing all refs with a colon.

--tags
All refs under refs/tags are pushed, in addition to refspecs explicitly listed on the command line.

--follow-tags
Push all the refs that would be pushed without this option, and also push annotated tags in refs/tags that are missing from the remote but are pointing at commit-ish that are reachable from the refs being pushed. This can also be specified with configuration variable push.followTags. For more information, see push.followTags in git-config(1).

--[no-]signed
--sign=(true|false|if-asked)
GPG-sign the push request to update refs on the receiving side, to allow it to be checked by the hooks and/or be logged. If false or --no-signed, no signing will be attempted. If true or --signed, the push will fail if the server does not support signed pushes. If set to if-asked, sign if and only if the server supports signed pushes. The push will also fail if the actual call to gpg --sign fails. See git-receive-pack(1) for the details on the receiving end.

--[no-]atomic
Use an atomic transaction on the remote side if available. Either all refs are updated, or on error, no refs are updated. If the server does not support atomic pushes the push will fail.

-o
--push-option
Transmit the given string to the server, which passes them to the pre-receive as well as the post-receive hook. The given string must not contain a NUL or LF character.

--receive-pack=<git-receive-pack>
--exec=<git-receive-pack>
Path to the git-receive-pack program on the remote end. Sometimes useful when pushing to a remote repository over ssh, and you do not have the program in a directory on the default $PATH.

--[no-]force-with-lease
--force-with-lease=<refname>
--force-with-lease=<refname>:<expect>
Usually, "git push" refuses to update a remote ref that is not an ancestor of the local ref used to overwrite it.

This option overrides this restriction if the current value of the remote ref is the expected value. "git push" fails otherwise.

Imagine that you have to rebase what you have already published. You will have to bypass the "must fast-forward" rule in order to replace the history you originally published with the rebased history. If somebody else built on top of your original history while you are rebasing, the tip of the branch at the remote may advance with her commit, and blindly pushing with --force will lose her work.

This option allows you to say that you expect the history you are updating is what you rebased and want to replace. If the remote ref still points at the commit you specified, you can be sure that no other people did anything to the ref. It is like taking a "lease" on the ref without explicitly locking it, and the remote ref is updated only if the "lease" is still valid.

--force-with-lease alone, without specifying the details, will protect all remote refs that are going to be updated by requiring their current value to be the same as the remote-tracking branch we have for them.

--force-with-lease=<refname>, without specifying the expected value, will protect the named ref (alone), if it is going to be updated, by requiring its current value to be the same as the remote-tracking branch we have for it.

--force-with-lease=<refname>:<expect> will protect the named ref (alone), if it is going to be updated, by requiring its current value to be the same as the specified value <expect> (which is allowed to be different from the remote-tracking branch we have for the refname, or we do not even have to have such a remote-tracking branch when this form is used). If <expect> is the empty string, then the named ref must not already exist.

Note that all forms other than --force-with-lease=<refname>:<expect> that specifies the expected current value of the ref explicitly are still experimental and their semantics may change as we gain experience with this feature.

"--no-force-with-lease" will cancel all the previous --force-with-lease on the command line.

-f
--force
Usually, the command refuses to update a remote ref that is not an ancestor of the local ref used to overwrite it. Also, when --force-with-lease option is used, the command refuses to update a remote ref whose current value does not match what is expected.

This flag disables these checks, and can cause the remote repository to lose commits; use it with care.

Note that --force applies to all the refs that are pushed, hence using it with push.default set to matching or with multiple push destinations configured with remote.*.push may overwrite refs other than the current branch (including local refs that are strictly behind their remote counterpart). To force a push to only one branch, use a + in front of the refspec to push (e.g git push origin +master to force a push to the master branch). See the <refspec>... section above for details.

--repo=<repository>
This option is equivalent to the <repository> argument. If both are specified, the command-line argument takes precedence.

-u
--set-upstream
For every branch that is up to date or successfully pushed, add upstream (tracking) reference, used by argument-less git-pull(1) and other commands. For more information, see branch.<name>.merge in git-config(1).

--[no-]thin
These options are passed to git-send-pack(1). A thin transfer significantly reduces the amount of sent data when the sender and receiver share many of the same objects in common. The default is \--thin.

-q
--quiet
Suppress all output, including the listing of updated refs, unless an error occurs. Progress is not reported to the standard error stream.

-v
--verbose
Run verbosely.

--progress
Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

--no-recurse-submodules
--recurse-submodules=check|on-demand|no
May be used to make sure all submodule commits used by the revisions to be pushed are available on a remote-tracking branch. If check is used Git will verify that all submodule commits that changed in the revisions to be pushed are available on at least one remote of the submodule. If any commits are missing the push will be aborted and exit with non-zero status. If on-demand is used all submodules that changed in the revisions to be pushed will be pushed. If on-demand was not able to push all necessary revisions it will also be aborted and exit with non-zero status. A value of no or using --no-recurse-submodules can be used to override the push.recurseSubmodules configuration variable when no submodule recursion is required.

--[no-]verify
Toggle the pre-push hook (see githooks(5)). The default is --verify, giving the hook a chance to prevent the push. With --no-verify, the hook is bypassed completely.

-4
--ipv4
Use IPv4 addresses only, ignoring IPv6 addresses.

-6
--ipv6
Use IPv6 addresses only, ignoring IPv4 addresses.
GIT URLS
In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching, but this is inefficient and deprecated; do not use it).

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

ssh://[user@]host.xz[:port]/path/to/repo.git/

git://host.xz[:port]/path/to/repo.git/

http[s]://host.xz[:port]/path/to/repo.git/

ftp[s]://host.xz[:port]/path/to/repo.git/

An alternative scp-like syntax may also be used with the ssh protocol:

[user@]host.xz:path/to/repo.git/

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path foo:bar could be specified as an absolute path or ./foo:bar to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support ~username expansion:

ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/

git://host.xz[:port]/~[user]/path/to/repo.git/

[user@]host.xz:/~[user]/path/to/repo.git/

For local repositories, also supported by Git natively, the following syntaxes may be used:

/path/to/repo.git/

file:///path/to/repo.git/

These two syntaxes are mostly equivalent, except when cloning, when the former implies --local option. See git-clone(1) for details.

When Git doesn’t know how to handle a certain transport protocol, it attempts to use the remote-<transport> remote helper, if one exists. To explicitly request a remote helper, the following syntax may be used:

<transport>::<address>

where <address> may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being invoked. See gitremote-helpers(1) for details.

If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

	[url "<actual url base>"]
		insteadOf = <other url base>
For example, with this:

	[url "git://git.host.xz/"]
		insteadOf = host.xz:/path/to/
		insteadOf = work:
a URL like "work:repo.git" or like "host.xz:/path/to/repo.git" will be rewritten in any context that takes a URL to be "git://git.host.xz/repo.git".

If you want to rewrite URLs for push only, you can create a configuration section of the form:

	[url "<actual url base>"]
		pushInsteadOf = <other url base>
For example, with this:

	[url "ssh://example.org/"]
		pushInsteadOf = git://example.org/
a URL like "git://example.org/path/to/repo.git" will be rewritten to "ssh://example.org/path/to/repo.git" for pushes, but pulls will still use the original URL.

REMOTES
The name of one of the following can be used instead of a URL as <repository> argument:

a remote in the Git configuration file: $GIT_DIR/config,

a file in the $GIT_DIR/remotes directory, or

a file in the $GIT_DIR/branches directory.

All of these also allow you to omit the refspec from the command line because they each contain a refspec which git will use by default.

Named remote in configuration file
You can choose to provide the name of a remote which you had previously configured using git-remote(1), git-config(1) or even by a manual edit to the $GIT_DIR/config file. The URL of this remote will be used to access the repository. The refspec of this remote will be used by default when you do not provide a refspec on the command line. The entry in the config file would appear like this:

	[remote "<name>"]
		url = <url>
		pushurl = <pushurl>
		push = <refspec>
		fetch = <refspec>
The <pushurl> is used for pushes only. It is optional and defaults to <url>.

Named file in $GIT_DIR/remotes
You can choose to provide the name of a file in $GIT_DIR/remotes. The URL in this file will be used to access the repository. The refspec in this file will be used as default when you do not provide a refspec on the command line. This file should have the following format:

	URL: one of the above URL format
	Push: <refspec>
	Pull: <refspec>
Push: lines are used by git push and Pull: lines are used by git pull and git fetch. Multiple Push: and Pull: lines may be specified for additional branch mappings.

Named file in $GIT_DIR/branches
You can choose to provide the name of a file in $GIT_DIR/branches. The URL in this file will be used to access the repository. This file should have the following format:

	<url>#<head>
<url> is required; #<head> is optional.

Depending on the operation, git will use one of the following refspecs, if you don’t provide one on the command line. <branch> is the name of this file in $GIT_DIR/branches and <head> defaults to master.

git fetch uses:

	refs/heads/<head>:refs/heads/<branch>
git push uses:

	HEAD:refs/heads/<head>
OUTPUT
The output of "git push" depends on the transport method used; this section describes the output when pushing over the Git protocol (either locally or via ssh).

The status of the push is output in tabular form, with each line representing the status of a single ref. Each line is of the form:

 <flag> <summary> <from> -> <to> (<reason>)
If --porcelain is used, then each line of the output is of the form:

 <flag> \t <from>:<to> \t <summary> (<reason>)
The status of up-to-date refs is shown only if --porcelain or --verbose option is used.

flag
A single character indicating the status of the ref:

(space)
for a successfully pushed fast-forward;

+
for a successful forced update;

-
for a successfully deleted ref;

*
for a successfully pushed new ref;

!
for a ref that was rejected or failed to push; and

=
for a ref that was up to date and did not need pushing.
summary
For a successfully pushed ref, the summary shows the old and new values of the ref in a form suitable for using as an argument to git log (this is <old>..<new> in most cases, and <old>...<new> for forced non-fast-forward updates).

For a failed update, more details are given:

rejected
Git did not try to send the ref at all, typically because it is not a fast-forward and you did not force the update.

remote rejected
The remote end refused the update. Usually caused by a hook on the remote side, or because the remote repository has one of the following safety options in effect: receive.denyCurrentBranch (for pushes to the checked out branch), receive.denyNonFastForwards (for forced non-fast-forward updates), receive.denyDeletes or receive.denyDeleteCurrent. See git-config(1).

remote failure
The remote end did not report the successful update of the ref, perhaps because of a temporary error on the remote side, a break in the network connection, or other transient error.
from
The name of the local ref being pushed, minus its refs/<type>/ prefix. In the case of deletion, the name of the local ref is omitted.

to
The name of the remote ref being updated, minus its refs/<type>/ prefix.

reason
A human-readable explanation. In the case of successfully pushed refs, no explanation is needed. For a failed ref, the reason for failure is described.
Note about fast-forwards
When an update changes a branch (or more in general, a ref) that used to point at commit A to point at another commit B, it is called a fast-forward update if and only if B is a descendant of A.

In a fast-forward update from A to B, the set of commits that the original commit A built on top of is a subset of the commits the new commit B builds on top of. Hence, it does not lose any history.

In contrast, a non-fast-forward update will lose history. For example, suppose you and somebody else started at the same commit X, and you built a history leading to commit B while the other person built a history leading to commit A. The history looks like this:

      B
     /
 ---X---A
Further suppose that the other person already pushed changes leading to A back to the original repository from which you two obtained the original commit X.

The push done by the other person updated the branch that used to point at commit X to point at commit A. It is a fast-forward.

But if you try to push, you will attempt to update the branch (that now points at A) with commit B. This does not fast-forward. If you did so, the changes introduced by commit A will be lost, because everybody will now start building on top of B.

The command by default does not allow an update that is not a fast-forward to prevent such loss of history.

If you do not want to lose your work (history from X to B) or the work by the other person (history from X to A), you would need to first fetch the history from the repository, create a history that contains changes done by both parties, and push the result back.

You can perform "git pull", resolve potential conflicts, and "git push" the result. A "git pull" will create a merge commit C between commits A and B.

      B---C
     /   /
 ---X---A
Updating A with the resulting merge commit will fast-forward and your push will be accepted.

Alternatively, you can rebase your change between X and B on top of A, with "git pull --rebase", and push the result back. The rebase will create a new commit D that builds the change between X and B on top of A.

      B   D
     /   /
 ---X---A
Again, updating A with this commit will fast-forward and your push will be accepted.

There is another common situation where you may encounter non-fast-forward rejection when you try to push, and it is possible even when you are pushing into a repository nobody else pushes into. After you push commit A yourself (in the first picture in this section), replace it with "git commit --amend" to produce commit B, and you try to push it out, because forgot that you have pushed A out already. In such a case, and only if you are certain that nobody in the meantime fetched your earlier commit A (and started building on top of it), you can run "git push --force" to overwrite it. In other words, "git push --force" is a method reserved for a case where you do mean to lose history.

Examples
git push
Works like git push <remote>, where <remote> is the current branch’s remote (or origin, if no remote is configured for the current branch).

git push origin
Without additional configuration, pushes the current branch to the configured upstream (remote.origin.merge configuration variable) if it has the same name as the current branch, and errors out without pushing otherwise.

The default behavior of this command when no <refspec> is given can be configured by setting the push option of the remote, or the push.default configuration variable.

For example, to default to pushing only the current branch to origin use git config remote.origin.push HEAD. Any valid <refspec> (like the ones in the examples below) can be configured as the default for git push origin.

git push origin :
Push "matching" branches to origin. See <refspec> in the OPTIONS section above for a description of "matching" branches.

git push origin master
Find a ref that matches master in the source repository (most likely, it would find refs/heads/master), and update the same ref (e.g. refs/heads/master) in origin repository with it. If master did not exist remotely, it would be created.

git push origin HEAD
A handy way to push the current branch to the same name on the remote.

git push mothership master:satellite/master dev:satellite/dev
Use the source ref that matches master (e.g. refs/heads/master) to update the ref that matches satellite/master (most probably refs/remotes/satellite/master) in the mothership repository; do the same for dev and satellite/dev.

This is to emulate git fetch run on the mothership using git push that is run in the opposite direction in order to integrate the work done on satellite, and is often necessary when you can only make connection in one way (i.e. satellite can ssh into mothership but mothership cannot initiate connection to satellite because the latter is behind a firewall or does not run sshd).

After running this git push on the satellite machine, you would ssh into the mothership and run git merge there to complete the emulation of git pull that were run on mothership to pull changes made on satellite.

git push origin HEAD:master
Push the current branch to the remote ref matching master in the origin repository. This form is convenient to push the current branch without thinking about its local name.

git push origin master:refs/heads/experimental
Create the branch experimental in the origin repository by copying the current master branch. This form is only needed to create a new branch or tag in the remote repository when the local name and the remote name are different; otherwise, the ref name on its own will work.

git push origin :experimental
Find a ref that matches experimental in the origin repository (e.g. refs/heads/experimental), and delete it.

git push origin +dev:master
Update the origin repository’s master branch with the dev branch, allowing non-fast-forward updates. This can leave unreferenced commits dangling in the origin repository. Consider the following situation, where a fast-forward is not possible:

	    o---o---o---A---B  origin/master
		     \
		      X---Y---Z  dev
The above command would change the origin repository to

		      A---B  (unnamed branch)
		     /
	    o---o---o---X---Y---Z  master
Commits A and B would no longer belong to a branch with a symbolic name, and so would be unreachable. As such, these commits would be removed by a git gc command on the origin repository.

SECURITY
The fetch and push protocols are not designed to prevent one side from stealing data from the other repository that was not intended to be shared. If you have private data that you need to protect from a malicious peer, your best option is to store it in another repository. This applies to both clients and servers. In particular, namespaces on a server are not effective for read access control; you should only grant read access to a namespace to clients that you would trust with read access to the entire repository.

The known attack vectors are as follows:

The victim sends "have" lines advertising the IDs of objects it has that are not explicitly intended to be shared but can be used to optimize the transfer if the peer also has them. The attacker chooses an object ID X to steal and sends a ref to X, but isn’t required to send the content of X because the victim already has it. Now the victim believes that the attacker has X, and it sends the content of X back to the attacker later. (This attack is most straightforward for a client to perform on a server, by creating a ref to X in the namespace the client has access to and then fetching it. The most likely way for a server to perform it on a client is to "merge" X into a public branch and hope that the user does additional work on this branch and pushes it back to the server without noticing the merge.)

As in #1, the attacker chooses an object ID X to steal. The victim sends an object Y that the attacker already has, and the attacker falsely claims to have X and not Y, so the victim sends Y as a delta against X. The delta reveals regions of X that are similar to Y to the attacker.

GIT
Part of the git(1) suite

Last updated 2017-02-03 08:41:53 W. Europe Standard Time
```



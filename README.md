# Git & GitHub

- [Git \& GitHub](#git--github)
  - [What is Git?](#what-is-git)
    - [Set up Git](#set-up-git)
    - [Using Git](#using-git)
  - [What is GitHub?](#what-is-github)
  - [Using GitHub](#using-github)
    - [Moving local repo to remote repo with HTTPS](#moving-local-repo-to-remote-repo-with-https)
    - [Moving local repo to remote repo with SSH](#moving-local-repo-to-remote-repo-with-ssh)
    - [Cloning from remote to local](#cloning-from-remote-to-local)
    - [Synchronising local and remote repositories](#synchronising-local-and-remote-repositories)
  - [Git Commands](#git-commands)

## What is Git?

Git is an open-source **version control software** that **tracks and manages changes** made to code base or files. Version control means the Git remembers version updates/changes, provides history of changes, can go back to earlier version, can be done used locally and remotely. To know more read about it on the [Git official page](https://git-scm.com). Discover more with [Atlassian Git tutorials](https://www.atlassian.com/git/tutorials).

To interact with Git use Git Bash terminal (command-line user interface).

Git is an opt-in system, so all files will be controlled by Git unless you explicitly exclude them. To exclude them you must make use of a [`.gitignore`](https://github.com/github/gitignore) file, which you would use to specify files containing sensitive information is not included in repo. File names of files containing non-sensitive information as well as the `.gitignore` file included in the repo can be seen with command [`git ls-files`](https://git-scm.com/docs/git-ls-files) (it will not include the file names/types outlined in your `.gitignore` file).

Git has 3 stages shown below:

Working directory -- git add --> Staging area -- git commit --> Local Repository.

![git staging area](https://git-scm.com/images/about/index1@2x.png)

To treat it as though it does not have 3 stages you can use the command shown in the image below:

![git bypass staging area](https://git-scm.com/images/about/index2@2x.png)

### Set up Git

Download Git from the [Git official page](https://git-scm.com), then run the downloaded file to install and follow the installations steps.

Open the Git Bash terminal and run the following commands to finish configuring Git:

```bash
# verify installation
git --version

# configure Git user name
git config --global user.name "Esther Slabbert"

# configure Git user email
git config --global user.email "super.ejs@gmail.com"

# set the default branch to be main (instead of master)
git config --global init.defaultBranch main

# list configured parameters (may add --show-origin for path to config file)
git config --list
```

The levels for config are: global, system, and local.

### Using Git

Basic steps for setting up a local Git repository and committing to it to keep track of file versions:

1. Navigate to the folder/directory you wish to make a Git repository using `cd <path/to/folder>` in the Bash terminal. To check where you currently are use: `pwd`. To create new directory use: `mkdir <DirectoryName>` To see a list of the items/files in the current directory use: `ls` or `ls -al`  to see more detail and show hidden files.
2. Initialize a repository using `git init`. This creates a `.git` folder in your directory, making it a Git repository.
3. Create a file and write to it or move one into the Git repository (i.e. the folder/directory that you did the `git init` command in).
4. Add the file(s) to staging area (from the working directory) with `git add <file_name.type>`.
5. Commit the files to the Git repository (from the staging area) `git commit -m "<Meaningful message for commit>"`.
6. Write to the file(s) in your working directory or make some changes (e.g. add/remove file(s) from the working directory). (Note: Each time a change you wish to keep/track is made in your working directory (location of repository) you need to add and then commit those changes.)
7. You may use `git status` to check the status of the changes you have made within your working directory at any point (it will tell you if there are unstaged or uncommitted changes or if your repo is clean and up to date).
8. Add all the file(s)/changes to staging area (from the working directory) with `git add .`.
9. Commit the file(s)/changes made to the local Git repository (from the staging area) `git commit -m "<Meaningful message for commit>"`.

## What is GitHub?

[GitHub](https://github.com/) is an online service platform for providing remote repository storage.

## Using GitHub

Create an account by signing up and following the steps (unless you already have one).

Log in if you already have one or after you have created an account.

If you want to remove GitHub credentials from your Windows machine you can do so in the 'Credential Manager'.

Good to know: You must synchronise changes between your local and remote repos. (i.e., You cannot push changes from a local repo until you pull changes from the remote repo.)

### Moving local repo to remote repo with HTTPS

1. Create a new repository on GitHub by clicking the !['New'](./new-repo.png) button in the Repository section or from the Home dashboard. Give your repository a name and choose settings to make the repository public/private and other optional settings.
2. Click HTTPS in the 'Quick setup' section of the page and copy the url. (Note: if there are already files in the repo you can find the HTTPS url by clicking the 'Code' dropdown, being in the 'Local' tab of the dropdown and the 'HTTPS' tab of the 'Local' tab)
3. In your Git Bash terminal you can either create a new repo or upload an existing repo from your local device. (Note: if you do not wish to make a repo on your local device you can just upload the desired files/folders to the GitHub repo by clicking the 'uploading an existing file' link in the 'Quick setup' section or create a new file by clicking  'creating a new file' link. If you already have files/folders in your repo you can add files/create files by clicking the 'Add file' dropdown and selecting what you would like to do.)
   1. Create a new repository on the command line and then push to GitHub:

    ```bash
    # navigate to your desired location for the repo
    cd </path/to/repo> # replace with desired path
    # create a README.md file with the heading of your repo
    echo "# <Repository-Name>" >> README.md # replace <Repository-Name> with actual desired heading/repo name
    # initialize local Git repo
    git init
    # adds README to Staging Area
    git add README.md
    # Commits files/changes from Staging Area to Repo
    git commit -m "first commit"
    # sets main branch name as main
    git branch -M main
    # replace <GitHub-Username>/<Repository-Name> with actual GitHub username and repo name without '<' or '>' or with the entire url from step 2
    git remote add origin https://github.com/<GitHub-Username>/<Repository-Name>.git
    # confirm you have the correct origin added
    git remote -v
    # Pushes local repo to remote repo
    # note that when you do this it may ask for your GitHub username and password - provide what it asks for
    git push -u origin main # runs and shows info for synchronization
    ```

    2. Push an existing up-to-date repository to GitHub from the command line:

    ```bash
    # navigate to the location of your existing repo
    cd </path/to/repo> # replace with actual path
    # replace <GitHub-Username>/<Repository-Name> with actual GitHub username and repo name without '<' or '>' or with the entire url from step 2
    git remote add origin https://github.com/<GitHub-Username>/<Repository-Name>.git
    # confirm you have the correct origin added
    git remote -v
    # sets main branch name as main
    git branch -M main
    # Pushes local repo to remote repo
    # note that when you do this it may ask for your GitHub username and password - provide what it asks for
    git push -u origin main # runs and shows info for synchronization
    ```

Each time you want to update your remote repo from your local repo you will just need to navigate to your repo using a `cd` command and use `git push` to push the changes after you have already added and committed them locally.

Note: You can generate tokens for HTTPS API access to use to grant access instead of using your GitHub password. To set it up go to 'Settings' > 'Developer Settings' > 'Personal access tokens' > 'Tokens (classic)'> 'Generate new token' > 'Generate new token (classic)'. Then specify what you're using it for in the 'Note' block and how long it will be available in the 'Expiration' section. Add the scopes by ticking the appropriate boxes in the 'Select scopes' section. Then click 'Generate token'. Copy the token now as you cannot go back to copy it later. Then when you try to make a push it will ask for your GitHub username and password, for the password use the Personal Access Token (this will happen twice so just fill it in again and it will allow you to interact with GitHub).

### Moving local repo to remote repo with SSH

If you run into trouble or want a more detailed instructions to set up an SSH connection with GitHub check out my other repo [here](https://github.com/EstherSlabbert/tech230_github_ssh).

1. Create a new repository on GitHub by clicking the !['New'](./new-repo.png) button in the Repository section or from the Home dashboard. Give your repository a name and choose settings to make the repository public/private and other optional settings.
2. Click SSH in the 'Quick setup' section of the page and copy the link provided. (Note: if there are already files in the repo you can find the HTTPS url by clicking the 'Code' dropdown, being in the 'Local' tab of the dropdown and the 'SSH' tab of the 'Local' tab)
3. In a Git Bash terminal navigate to the '.ssh' folder (may need to create one) and use tthe following command to generate an SSH key pair: `ssh-keygen -t rsa -b 4096 -C "<email-address-used-to-sign-up-for-GitHub>"`. Note: `-t rsa` = algorithm used & `-b 4096` = length of key. For more details: [generating SSH public key](https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key).
4. 'Enter' to select default (otherwise give the file a name and then hit 'Enter', but if you do this you must replace `id_rsa.pub` with the name you chose).
5. Create passphrase (optional).
6. Copy key to notepad by: `notepad ~/.ssh/id_rsa.pub` or read the contents using `cat ~/.ssh/id_rsa.pub`. Select all the contents shown and copy to clipboard.
7. On GitHub go to 'Settings' > 'SSH and GPG keys'. Then create a new SSH key by clicking 'New SSH key'. Give it a title in the 'Title' box and paste the public SSH key in the 'Key' box, then click 'Add SSH key'.
8. Attempt to SSH to GitHub using `ssh -T git@github.com`. Enter `yes` to continue.
9. Navigate to local repo using a `cd` command.
10. Add origin: `git remote add origin git@github.com:<GitHub-Username>/<Repository-Name>.git`.
11. Confirm you have the correct origin added: `git remote -v`.
12. Push local repo to remote GitHub repo `git push origin main`.

### Cloning from remote to local

When you have everything on GitHub and want it on your local device:

```bash
# shows current location
pwd
# copies remote repo to local repo (new directory) - replace GitHubUsername with actual username and RepoName with name of the repo you want to copy
git clone https://github.com/GitHubUsername/RepoName.git
```

### Synchronising local and remote repositories

Local to Remote:

```bash
# check status of files & repo
git status # optional
# lists the current directory contents
git ls # optional

# Make changes locally
# for example:
# open README.md using notepad, make changes, save and close
notepad README.md

# check status of files & repo - new changes that haven't been staged
git status # optional
# adds all files/changes to staging area
git add .
# check status of files & repo - changes sent to staging area
git status # optional
# commits changes to repo
git commit -m "Added content to README.md"
# check status of files & repo - more local than remote - changes committed locally
git status # optional

# checks correct remote urls for fetching and pushing
git remote -v # optional
# sends local to remote
git push
```

Remote to Local:

```bash
# Make changes on GitHub website (have someone else push to the repo or edit it online)
# syncs changes made to remote repo to local repo
git pull

# check status of files & repo
git status # optional
# lists contents of current directory
ls # optional
# to view what it says in the file (replace file-name.md with name of file and file extension)
cat file-name.md
```

## Git Commands

Commonly used commands:

```bash
# replace <GitHub-Username> and <Repository-Name> with the actual values for each occurance

# correct way to add test.md to repo
git add test.md
git commit -m "updated test.md"

# adds all changes to staging area
git add .

# unstages all changes from staging area
git restore --staged

# commits changes to repository
git commit -m "updated whatever for this purpose"

# adds and commits in one command
git commit -a -m "updated whatever for this purpose"

# current conditions/status of repository
git status

# differences between working files and commits
git diff

# check authentication method and other configs
git config --list

# detailed history of repository changes and who did them + commit ID
git log

# get onelines with commit IDs and commit messages
git log --oneline

# creates new branch
git branch -f <new-branch-name> # replace <new-branch-name> with actual branch name

# creates and switches to new branch
git checkout -b <new-branch-name> # replace <new-branch-name> with actual branch name

# switches over to branch
git checkout <branch-name> # replace <branch-name> with actual branch name

# removes all commits, but does not change the current file state. Can add `--hard` flag to undo all changes made after that commit.
git reset <commit-ID> # Replace <commit-ID> with actual commit ID.

# creates a new commit for the reverted changes.
# a forward-moving undo operation that offers a safe method of undoing changes
git revert <commit-ID> # replace <commit-ID> with actual commit ID.
# If taken into UNIX editor: Press i to enter inline insert mode. Type the description at the very top, press esc to exit insert mode, then type :x! (now the cursor is at the bottom) and hit enter to save and exit. If typing :q! instead, will exit the editor without saving (and commit will be aborted)

## Git-GitHub commands

# updates: local repo to remote repo
git push

# updates: remote repo to local repo
git pull

# clones remote repo locally - replace <repo> with either https or ssh link and <directory> with the location you want to clone to on your device
git clone <repo> <directory>
# makes a copy of remote repo locally with SSH link
git clone git@github.com:<GitHub-Username>/<Repository-Name>.git
# makes a copy of remote repo locally with HTTPS link
git clone https://github.com/<GitHub-Username>/<Repository-Name>.git

# add remote origin
git remote add origin git@github.com:<GitHub-Username>/<Repository-Name>.git

# remove remote origin
git remove remote origin

# checks correct remote urls for fetching and pushing
git remote -v
```

Read more on specific commands:

- [git commit](https://git-scm.com/docs/git-commit)
- [git add](https://git-scm.com/docs/git-add)
- [git log](https://git-scm.com/docs/git-log)
- [git status](https://git-scm.com/docs/git-status)
- [git diff](https://git-scm.com/docs/git-diff)
- [git push](https://git-scm.com/docs/git-push)
- [git pull](https://git-scm.com/docs/git-pull)
- [git clone](https://git-scm.com/docs/git-clone)
- [git revert](https://git-scm.com/docs/git-revert)
- [git reset](https://git-scm.com/docs/git-reset)
- [git restore](https://git-scm.com/docs/git-restore)
- [git checkout](https://git-scm.com/docs/git-checkout)

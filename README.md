Testing creating local file on vscode and uploading it to github


SITUATION A: 
    To create a new Git repository locally using VSCode and then push it to GitHub

1) Open project folder in VSCode
2) Initialize Git in Terminal

    > git init

    Initializes an empty Git repo in local project folder. MAKE SURE you are in the project directory, otherwise,
    
    > cd path
    
    To initialize
    > git init

3) (OPTIONAL) Create a README.md file
    > New-Item -Path "path to project" -Name "README.md" -ItemType "File"

    This creates an empty README.md in the directory

4) Stage and Commit Changes

   Stage the files for initial commit
    > git add .

   Commit the changes
    > git commit -m "Initial commit"

5) Create new repo on github***
    
   NOTE: If you created the README.md locally, DO NOT initialize another on github.

6) Copy repo URL and Push the LOCAL repo to Github

   Adds the github repo as a remote
    > git remote add origin repo URL

7) Push the code to Github

    Check the name of the branch first, it usually is MAIN or MASTER
    > git branch
    
    Pushing
    > git push -u origin branch


SITUATION B:
    You want to use SSH repo link instead of HTTPS as it allows authentication without needing to enter username and password each time you push or pull from repo

1) Set Up SSH Keys (if not yet done)
    
    Check if you already have SSH keys
    > ls -al ~/.ssh

    This will list the files in your .ssh directory. If "id_rsa" and "id_rsa.pub" exists, SSH keys are already set up. Otherwise, generate SSH keys.
    > ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

    Press 'Enter' to accept default location for the keys. Passphrase can be blank.

2) Add SSH key to the SSH agent

    Start the SSH agent
    > eval "$(ssh-agent -s)"

    Add your SSH private key to the SSH agent
    > ssh-add ~/.ssh/id_rsa

3) Add SSH key to Github account

    Copy the ssh publish key to clipboard
    > cat ~/.ssh/id_rsa.pub

   Copy the output, go to "GitHub SSH keys settings" (https://github.com/settings/keys) and click on "New SSH Key"
   Paste SSH key and give it title, ie. "My Laptop"
   Click "Add SSH Key"

4) Refer to earlier steps *** to create repo on Github, from Step 5-6. Copy SSH link of the Github repo.

    Click "Code" button, under "Clone", switch to SSH
    Then look for a link similar to (git@github.com:yourusername/my-project.git)

5) Add Remote URL with SSH

    Go to VSCode terminal, navigate to project directory
    > cd project path

    Add SSH remote URL
    > git remote add origin SSH remote URL

    ie. git remote add origin git@github.com:yourusername/my-project.git

6) Push the Code to Github using SSH

    Pushes local commits to remote Github repo using SSH
    > git push -u origin branch


SITUATION C:
    Edit existing file then save changes to Github Repo

1) STAGE the specific file to prepare it for committing. ie. 'README.md'
    > git add README.md

    OR

    If you made changes to multiple files and want to stage ALL
    > git add .

2) COMMIT the changes
    > git commit -m "your message here"

3) PUSH the changes to the remote repo branch ie. 'main'
    > git push origin main


SITUATION D:
    Error:  ' src refspec main does not match any...'

   Want to use 'main' but it doesn't exist. Create it.
    > git checkout -b main

1. Ensure you have committed changes

    > git log

2. Check Remote URL

    > git remote -v

    To update remote URL
    > git remote set-url origin remote url

SITUATION E:
    To check your branches

1. This will list all local branches
    > git branch -a

2. This will list BOTH local and remote branches
    > git branch -r

SITUATION F:
    To delete a specific branch ie. 'master' branch. Take note that you have to delete the branch locally and remotely.

1. LOCAL
    You can't be on the branch you want to delete, so switch to another branch. In this case, you're currently on 'master' branch, so switch to 'main' branch.
    > git checkout main

    OR
    > git switch main

    Delete local branch (NOTE: This command won't delete the branch if there's unmerged changes)
    > git branch -d master

    To delete forcefully even with unmerged changes
    > git branch -D master

2. REMOTE
    > git push origin --delete master

    OPTIONAL. Clean up references to deleted branch from local repo
    > git fetch --prune

SITUATION G: 
    To push changes from local 'master' branch to remote 'main' branch on GitHub

    OPTIONAL. Fetch latest branches from remote
    > git fetch origin

1. Make sure you are on 'master' branch
    > git checkout master 

2. Push changes to 'main' branch on GitHub
    > git push origin master:main

SITUATION H:
    If there are conflicts due to remote branch having changes that your local branch doesn't

1. Integrate those changes. ie, remote 'main' merge to local 'master' branch (branch you're currently on)
    > git pull origin main

2. Resolve any merge conflicts, if any
    > git add .

    Commit the merge
    > git commit -m "Resolved merge conflicts"

3. Push local changes to remote 'main'
    > git push origin master:main

SITUATION I:
    Error of pushing due to branches refusing to merge unrelated histories

1. This will merge remote 'main' branch into current branch even if they don't share common history
    > git pull origin main --allow-unrelated-histories

2. Stage, commit and push. Refer to Situation C.

Testing creating local file on vscode and uploading it to github


SITUATION: 
    To create a new Git repository locally using VSCode and then push it to GitHub

1) Open project folder in VSCode
2) Initialize Git in Terminal

    > git init

    //initializes an empty Git repo in local project folder. MAKE SURE you are in the project directory, otherwise,
    
    > cd <path>
    > git init

3) (OPTIONAL) Create a README.md file
    > New-Item -Path "path to project" -Name "README.md" -ItemType "File"

    //creates an empty README.md in the directory

4) Stage and Commit Changes

    //stage the files for initial commit
    > git add .

    //commit the changes
    > git commit -m "Initial commit"

5) Create new repo on github***
    
    //if you created the README.md locally, DO NOT initialize another on github

6) Copy repo URL and Push the LOCAL repo to Github

    //adds the github repo as a remote
    > git remote add origin repo URL

7) Push the code to Github

    //check the name of the branch first, it usually is MAIN or MASTER
    > git branch
    
    //pushing
    > git push -u origin branch


SITUATION:
    You want to use SSH repo link instead of HTTPS as it allows authentication without needing to enter username and password each time you push or pull from repo

1) Set Up SSH Keys (if not yet done)
    
    //check if you already have SSH keys
    > ls -al ~/.ssh

    //this will list the files in your .ssh directory. If "id_rsa" and "id_rsa.pub" exists, SSH keys are already set up. Otherwise, generate SSH keys.
    > ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

    //press 'Enter' to accept default location for the keys. Passphrase can be blank.

2) Add SSH key to the SSH agent

    //start the SSH agent
    > eval "$(ssh-agent -s)"

    //add your SSH private key to the SSH agent
    > ssh-add ~/.ssh/id_rsa

3) Add SSH key to Github account

    //copy the ssh publish key to clipboard
    > cat ~/.ssh/id_rsa.pub

    //copy the output, go to "GitHub SSH keys settings (https://github.com/settings/keys)" and click on "New SSH Key"
    //Paste SSH key and give it title, ie. "My Laptop"
    //Click "Add SSH Key"

4) Refer to earlier steps *** to create repo on Github, from Step 5-6. Copy SSH link of the Github repo.

    //Click "Code" button, under "Clone", switch to SSH
    look for a link similar to (git@github.com:yourusername/my-project.git)

5) Add Remote URL with SSH

    //Go to VSCode terminal, navigate to project directory
    > cd project path

    //Add SSH remote URL
    > git remote add origin SSH remote URL

    ie. git remote add origin git@github.com:yourusername/my-project.git

6) Push the Code to Github using SSH

    //Pushes local commits to remote Github repo using SSH
    > git push -u origin branch

    //Verify on Github


SITUATION: 
    Edit existing file then save changes to Github Repo

1) STAGE the file (in this example, you edited the README.md) to prepare it for committing
    > git add README.md

    OR

    if you made changes to multiple files and want to stage ALL, use
    > git add .

2) COMMIT the changes
    > git commit -m "your message here"

3) Push the changes to the remote repo
    > git push origin branch-name


OTHER SITUATIONS:
1. Error:  ' src refspec main does not match any '

    //Want to use 'main' but it doesn't exist. Create it.
    > git checkout -b main

2. Ensure you have committed changes

    > git log

3. Check Remote URL

    > git remote -v

    //to update remote URL
    > git remote set-url origin remote url

4. To delete branch

    LOCAL

    //you can't be on the branch you want to delete, so switch to another branch
    > git checkout branch

    OR
    > git switch branch

    //delete local branch
    > git branch -d branch to be deleted

    (won't delete branch if there's unmerged changes)
    
    //to delete forcefully even with unmerged changes
    > git branch -D branch to be deleted

    REMOTE

    > git push origin --delete branch to be deleted

    //OPTIONAL. Clean up references to deleted branch from local repo
    > git fetch --prune





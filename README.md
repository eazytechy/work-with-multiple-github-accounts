How To Work With Multiple Github Accounts on a single Machine
Let suppose I have two github accounts, https://github.com/sumit-work and https://github.com/sumit-personal. Now i want to setup my mac to easily talk to both the github accounts.

NOTE: This logic can be extended to more than two accounts also. :)

The setup can be done in 5 easy steps:

Steps:
Step 1 : Create SSH keys for all accounts
Step 2 : Add SSH public key to the Github
Step 3 : Create a Config File and Make Host Entries
Step 4 : Cloning GitHub repositories using different accounts

Step 1
Create SSH keys for all accounts
First make sure your current directory is your .ssh folder.

     $ cd ~/.ssh
Syntax for generating unique ssh key:

     ssh-keygen

After entering the command, the terminal will ask for name of the key
For first key, you can enter - key_work
For second key, you can enter - key_personal
In Both the cases, after entering the name of the key, the terminal will ask for passphrase, leave it empty and proceed.

Passphrase Image

Now after adding keys , in your .ssh folder, a public key and a private will get generated.

The public key will have an extention .pub and private key will be there without any extention both having same name which you have passed in the terminal.

Added Key Image


Step 2
Add SSH public key to the Github
For the next step we need to add our public key (that we have generated in our previous step) and add it to corresponding github accounts.

For doing this we need to:

1. Copy the public key

 We can copy the public key either by opening the key_work.pub file in vim and then copying the content of it.
     vim ~/.ssh/key_work.pub
     vim ~/.ssh/key_personal.pub
OR

We can directly copy the content of the public key file in the clipboard.

     pbcopy < ~/.ssh/key_work.pub
     pbcopy < ~/.ssh/key_personal.pub
     
2. Paste the public key on Github

Sign in to Github Account
Goto Settings > SSH and GPG keys > New SSH Key
Paste your copied public key and give it a Title of your choice.
OR

Sign in to Github
Paste this link in your browser (https://github.com/settings/keys) or click here
Click on New SSH Key and paste your copied key.

Step 4
Create a Config File and Make Host Entries
The ~/.ssh/config file allows us specify many config options for SSH.

If config file not already exists then create one (make sure you are in ~/.ssh directory)

     touch config
The commands below opens config in your default editor....Likely TextEdit, VS Code.

     open config
Now we need to add these lines to the file, each block corresponding to each account we created earlier.

     #sumit-work account
     Host github.com-sumit-work
          HostName github.com
          User git
          IdentityFile ~/.ssh/key_work

     #sumit-personal account
     Host github.com-sumit-personal
          HostName github.com
          User git
          IdentityFile ~/.ssh/key_personal

Step 5
Cloning GitHub repositories using different accounts
So we are done with our setups and now its time to see it in action. We will clone a repository using one of the account we have added.

Make a new project folder where you want to clone your repository and go to that directory from your terminal.

For Example: I am making a repository on my personal github account and naming it DemoRepo Now for cloning the repo use the below command:

    git clone git@github.com-{your-username}:{owner-user-name}/{the-repo-name}.git

    [e.g.] git clone git@github.com-sumit-personal:sumit-personal/DemoRepo.git

Finally
From now on, to ensure that our commits and pushes from each repository on the system uses the correct GitHub user — we will have to configure user.email and user.name in every repository freshly cloned or existing before.

To do this use the following commands.

     git config user.email "my_office_email@gmail.com"
     git config user.name "Sumit Jain"
     
     git config user.email "my-personal-email@gmail.com"
     git config user.name "Sumit Jain"

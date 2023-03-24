# DevOps

This file is going to contain the instructions on how to actually setup the environment for the project. 

## Virtual Machine
Use the VM that's associated with the linkblueID, since those should all be pretty much the same.

## Getting Github working on the VM
Git is already pre-installed on the VM (can run `git --version` to verify), but Github is a bit more of a pain since 2021. You can't just use your password, you need an access token.

### Getting the access token
1. Login to Github
2. Click on your profile pic at the top right, click Settings.
3. Scroll down, click Developer Settings, then Personal access tokens, then Tokens (classic).
4. There should be a button for "Generate new token." Click that, then select "Generate new token (classic)". You'll have to set the name and expiration date of the token (I set it for 2 months) as well as the scope (just select repo, which is at the very top). Finally hit Generate at the bottom.
5. It'll pop up with a random string of stuff and a message saying "copy paste this, you won't see it again!" **DON'T LEAVE THE PAGE YET!** 
6. Back on your VM, run `git config --global credential.helper store`.
7. Next, run `git clone https://github.com/CS-498-Suffering/Barter.git`. It'll pop up asking you for your username and then password. Input your Github username, and when it prompts for the password, copy the access token string and paste it in there. If it works, it should successfully clone the repo and you'll have a folder named Barter.
- To make sure it worked entirely, you can run `ls -a` in your home directory and check if you have a folder called `.git-credentials`. This should contain your username as well as your access token, so you don't have to enter username/access token each time you try to push/pull.

## Getting Pip
Pip is a package manager for Python. While the VMs already have Python, they don't have pip. To install it, run `sudo apt-install python3-pip`.

## Getting the `venv` package
This package lets us use virtual environments, another layer of ensuring we all have the same tools available. Unfortunately, again it isn't installed by default on the VM. For me, I had to run first `sudo apt-get update` then `sudo apt install python3.10-venv`. You may get something where a pink screen pops up after the first command saying something like "choose what to restart". Just type Cancel and hit Enter.

## Setting up the virtual environment
This is directly cribbed from the Flask megatutorial, just adapted so it's slightly less confusing (hopefully). 

- Make sure you're in the Barter directory.
- Run `python3 -m venv barter_env`
- This creates a folder called `barter_env` in the top level of the repo. When we commit and push, this folder will be excluded (best practice is to leave environment stuff out of repos and have other ways to standardize that). 

To activate the virtual environment, run `source barter_env/bin/activate`. Your terminal prompt should change to have `barter_env` in parentheses to the left of the prompt. Now the environment is active, all packages installed won't be installed on the entire VM and only for the project.
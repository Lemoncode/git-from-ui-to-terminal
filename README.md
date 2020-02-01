# Basic steps to learn Git using the terminal

In this repo you have a very simple project (a web project that displays a number via the console log), we will provide a guide to recreate it from scratch on a brand new repo.


We will use git terminal commands to setup and work with the repo.

# Creating the repo

You can choose whether to use HTTPS (your standard git login user) or SSH (a more secure approach to treat with your repos but need some additional configuration).

> More info about how to [create an SSH key on your computer](https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html), and [set it up on Git](https://help.github.com/en/enterprise/2.18/user/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)

To create the repo you can just click on the _new repository_ button in Github or your favourite repository cloud provider.

> Is a good idea to check on "creating" a default readme.md file on the repo, just toget already some date in it and an initial commit done.

# Cloning the repo

Now that you have your repo created is time to bring it to your local computer, in order to do that we clone it (download the repo to a local computer folder).

> Ensure you have permissions to access that repositories, and if you are using SSH you have it properly configured.

Choose a folder to download the files, open a terminal window, and execute the following command:

```bash
git clone <repository_address>
```

> Usually your git repo provider display an input where you can copy the url / ssh address of the repo to be cloned.

# Copy

# Basic steps to learn Git using the terminal

In this repo you have a very simple project (a web project that displays a number via the console log), we will provide a guide to recreate it from scratch on a brand new repo.

We will use git terminal commands to setup and work with the repo.

Prerequisites to go through this tutorial:

- Install Git.
- Install nodejs.

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

# Adding a very simple web project

**This is not related with Git, we are just creating a very simple web project to play with**

Let's simulate we add some content to the repository.

We will start by creating a very simple web project (this is not related with Git, just setting up a nodejs project and a simple web project that displays a sentence via console log), let's execute the following command:

```bash
npm init
```

and install a bundler:

```
npm install parcel rimraf --save-dev
```

Let's create the following files under _src_ folder:

_./src/index.js_

```javascript
const sampleNumber = 1;
console.log(`Hello number ${sampleNumber}`);
```

Let's create a HTML entry point:

_./src/index.html_

```html
<html>
  <body>
    <h1>Check the console log</h1>
    <script src="./index.js"></script>
  </body>
</html>
```

Let's add the following command to the existing _package.json_ file:

_./package.json_
```diff
"scripts": {
+    "start": "rimraf dist && parcel ./src/index.html --open",
    "test": "echo \"Error: no test specified\" && exit 1"
},
```

Time to give a quick check that the project is working, from the terminal execute:

```bash
npm start
```

A web browser will be opened and if you open the console log from that browser (e.g. on windows pressing F12) you can check that a message is displayed.

So far so good... now that we have a very simple project to play with, let's go for it !

# Preparing our first commit

Maybe we think we are now ready to make our first commit to master (the default branch has been created in our project).

Before making a commit let's check which files has been modified, open the terminal and type the following command:

```bash
git status
```

Wooooot !!! We have only few files updated, why we get a big ton of files in our list? Well _npm install_ did it, you get under the *node_modules* a ton of files that you don't need in you repository (and you must not upload them), we have to ignore them, create a _.gitignore_ file and include there the following content:

_./.gitignore_
```
node_modules
```

By doing that we are telling to ignore any path that includes *node_modules* to ignore it (do not taking into account in Git), [click here to get more info about how to enter entries and patterns in a .gitIgnore](https://git-scm.com/docs/gitignore).

Now if we execute again a _status_ command we will see that only the files that we have created are pending to be added:

```bash
git status
```

Now if we want to send this change to our git server, we need to perform three steps:
  - First we need to mark that files as ready to be committed (you can do it file by file or you can select all files).
  - Second you need to commit that staged file to your local git database
  - Third now you can push this changes to the server.
  
Let's move the files to staging:

```bash
git add .
```

Now we can commit the files to our local database, we will add _-m_ command to add a commit message:

```bash
git commit -m "initial project setup"
```

> Is a good idea to add some meaningful message

We are reasy to upload the local changes that we have committed to the server:


```bash
git push
```

To check that everything went well, open your browser, navigate to your git provider web client and check that the uploaded content is available.

# Creating and merging branches

Now that we now have taken our first steps using git is time to move forward, we are going to learn the basics of creating branches.


A branch allow us to creating an isolated copy of the master branch (or any other branch) and let us work in that code cut isolated from the rest of the team, this is really useful to:
  - Avoid adding not completed features to our product.
  - Avoid impacting other developers in the team by adding changes into their code base.
  - Reviewing the work done before merging that code into the master branch.
  
We want to implement a new functionallity, display in the console log a second number, to avoid impacting other developers meanwhile we are progressing in our case we are going to create a branch. Let's create a new one:

```
git branch feature/display-number-b
```

> About the naming convention used to define the branch name, we are using gitflow, [click here to get more info about how to name branchs and gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

We can execute the command _git branch_ to check that the branch has been created, this command will indicate us as well the active branch (master):

```bash
git branch
```

Let's switch from our _master_ branch to the _feature/display-number-b_

```bash
git checkout feature/display-number-b
```

> You can switch from a given branch to another if the active branch has no changed pending to be committed (if the active branch has changes pending to be committed, you have to commit them, discard them or stash them, we will check all this later on).

Now we can start working on our branch without impacting users that are working on the master branch.

Let's add some updates in the _.src/index.js_ files:

_./src/index.js_
```diff
const sampleNumber = 1;
+ const sampleNumberB = 2;
- console.log(`Hello number ${sampleNumber}`);
+ console.log(`Hello number ${sampleNumber} {sampleNumberB}`);
```

Save the changes, and add them to staging:

```bash
git add .
```

Commit them to our local database:

```bash
git commit -m "adding one more number"
```

And push them to our remote origin (our remote repository).

```bash
git push
```

Now we could merge this remote branch to master, but we won't do this right away: we will first simulate that in between that time another developer has created another branch and modified the _./src/index.js_ file creating a conflict, we will learn how to sort this out.

> Some good advice: never merge form a given branch to master using the command line, rather raise pull requests and review the code (you can raise pull request from a given branch to master use the web client your favourite repository), on the other hand is a good practice to merge master into your branch just to get your code cut updated to the current branch status.

# Handling conflicts

Before merging our new branch to master, let's simulate that in the mean time another developer (or ourselves) has created a second branch and it's modifying the files we have just updated.

Let's hop in the master branch:

```bash
git checkout master
```

Let's create a new branch from master:

```bash
git branch feature/display-number-b
```

Let's jump into that branch

```bash
git checkout feature/display-number-c
```

Let's update the _index.js_ file and include a _numberC_ to be displayed

_/.src/index.js_

```diff
const sampleNumber = 1;
+ const sampleNumberC = 3;
- console.log(`Hello number ${sampleNumber}`);
+ console.log(`Hello number ${sampleNumber} {sampleNumberC}`);
```

Let add to staging the updated file:

```bash
git add .
```

Let's commit this file

```bash
git commit -m "Adding third number"
```

Let's push the changes

```bash
git push
```

Let's check the list of branches we have available:

```bash
git branch
```

We got three branches: _master_, _feature/display-number-b_, _feature/display-number-c_ and the active one is _feature/display-number-c_

We got the ok from the team to merge branch _feature-display-number-b_ into _master_, let's got for it.

Let's switch to _master_ branch

```bash
git checkout master
```

Let's merge _featute/display-number-b_ it in _master_:

```bash
git merge featute/display-number-b
```

> A good practice before merging with master is to ensure the branch is updated with the latest master cut (merge from master to our branch)

> We can do this because we go the branch available locally, if it's a branch created by another user it may happen that is available in the server but not in our local computer, we have to execute _fetch_ to bring it locally (check Misc section).

In this case there are not conflicts, we are good to go, let's commit this 

# Misc

## Fetch

## Stash

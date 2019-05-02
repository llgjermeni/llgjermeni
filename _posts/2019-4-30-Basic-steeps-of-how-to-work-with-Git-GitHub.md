---
layout: post
title: Basic steeps of how to work with Git & GitHub
---

When you start learning to code in paralel you need to learn how to use some basic tools like Git & GitHub.
In this article, I’ll give you some hints how to get starting with these tools. 

If you read the article until the end I'll get you up and running with the basics. There’s a lot of informations to learn if you want to use Git and GitHub in a professional way, of course but with this article you can get just an introductory!

Let’s get started!

## 1. Starting with Git

### What is Git? 

Git is a version control system (VCS). It is used for tracking changes to files and coordinating changes between multiple people and allow a developer or dev team to work together on a project.

  Git allows you to: 
 - revert files back to a previous state
 - revert the entire project back to a previous state
 - review changes made over time
 - see who last modified 
 - who introduced an issue and when, and more. 
 
 > Using Git also means that if you screw things up or lose files, you can generally recover easily. In addition, you get all this for very little overhead.

To use git you need to install it in your system. It's not complicated:

If you are in **Windows** just go to the Git website and download the official build wich is available and the download will start automatically.  

If you are in **Mac** the easiest way is probably to install the Xcode Command Line Tools. On Mavericks (10.9) or above you can do this simply by trying to run git from the Terminal the very first time.  

`
$ git --version
`

### Basic Git commands
- `git config` - Configure Git with your credentials in a single or globaly
- `git init` - Initialization of your repository
- `git status` - The status of the repository
- `git add` - Adding files to the repository
- `git commit` - Commit changes in repository
- `git push` - Upload files in remote repository
- `git pull` - Pull changes made in repository

## 2. Preparing repository in GitHub

>GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

### Create a repository

You create repository to host a project. Repositories can contain folders and files, images, videos, spreadsheets, and data sets – anything your project needs. Also you can include a README file,  with information and description about your project. 

1. Click `click+ ` in the upper right corner, and then select New repository
2. Enter the name you want for your project
3. Add a description, it is not required
4. Choose between private and public, for most cases like this we use public repository
5. Add a readme file but if not you  can add it later if you want
6. Add .gitignore file. It is used to ignore all kind of file you don't want to be included in your repo
7. Add a licence. You can add it later if you want

![Create repository](/images/GitGithubpost/CreateRepository.png)

## 3. Starting a project

Let's create a sample project with cmd commands.

1. `mkdir SampleProject`  Create a folder with desired name.
2. `cd SampleProject`  Navigate inside the folder.
3. `git init` Add .git folder to initialize git
4. `touch index.html` Create the first file.
5. `git add index.html` Add the file in the local repository
6. `git commit -m "First commit"` First commit
7. `git status` Check the status of the repository

![Starting Project](/images/GitGithubpost/startingProject.png)

8. `code .` Open project with VS Code and put some html code.

```
<!DOCTYPE html>
<html>

<head>
     <title>My Web Page </title>
</head>

<body>
     <p>Welcome this is a paragraph.</p>
     <p> I have add the html code in this page.</p>
     
</body>

</html>
 ```


9. `git commit -m "Second commit"` Second commit  
10. Now you need to connect your local repo with github repository. 
`git remote add origin https://github.com/user/repo.git`
user is your github name and repo is the name of your repository. Add `git push -u origin master` to push your project in github repository   

You can refresh the browser in github and you'll see the folder with the index.html file in the github repository 

Congratulations! You have used Git to tranfer files in an online repository in GitHub. 
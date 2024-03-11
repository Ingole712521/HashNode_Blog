---
title: "CheatSheet of GitHub"
seoTitle: "CheatSheet of GitHub"
datePublished: Mon Mar 11 2024 15:16:19 GMT+0000 (Coordinated Universal Time)
cuid: cltn363ve000009jr6jir8wz5
slug: cheatsheet-of-github
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710169929127/4fd95074-554a-49b2-aef3-0567e23c80a9.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1710170168932/8b20af06-fd7f-4d40-abf1-8d9c614f0963.jpeg
tags: github, githubpages, github-actions-1, learning-journey, learning-in-public, github-copilot

---

## Introduction

GitHub is a powerhouse for collaboration, version control, and project management. Whether you're a seasoned developer or just starting out, having a comprehensive understanding of GitHub commands can significantly enhance your productivity. In this guide, we'll provide you with a complete GitHub cheat sheet, explaining every command in detail to help you navigate GitHub like a pro.

## **git init**

* **Usage**: Initializes a new Git repository in the current directory.
    
* **Example**: `git init`
    
* **Explanation**: This command sets up a new Git repository in the current directory, creating a hidden `.git` folder to store the repository's metadata and configuration.
    

## **git clone**

* **Usage**: Clones a remote repository onto your local machine.
    
* **Example**: `git clone <repository_url>`
    
* **Explanation**: This command creates a copy of the specified remote repository on your local machine, allowing you to work on the project locally.
    

## **git add**

* **Usage**: Adds changes in the working directory to the staging area.
    
* **Example**: `git add <file>`
    
* **Explanation**: Use this command to stage specific files or directories for inclusion in the next commit. You can also use `git add .` to add all changes in the working directory.
    

## **git commit**

* **Usage**: Records changes to the repository.
    
* **Example**: `git commit -m "Commit message"`
    
* **Explanation**: Commits the staged changes to the local repository with a descriptive message explaining the changes made.
    

## **git push**

* **Usage**: Pushes local commits to the remote repository.
    
* **Example**: `git push origin <branch_name>`
    
* **Explanation**: Sends the committed changes from your local repository to the remote repository specified by `<branch_name>`, typically `origin`.
    

## **git pull**

* **Usage**: Fetches changes from the remote repository and merges them into the local branch.
    
* **Example**: `git pull origin <branch_name>`
    
* **Explanation**: Updates your local repository with changes from the remote repository, merging them into your current branch.
    

## **git branch**

* **Usage**: Lists, creates, or deletes branches.
    
* **Example**: `git branch <branch_name>`
    
* **Explanation**: Use this command to manage branches in your repository. Use `git branch` to list all branches, `git branch <branch_name>` to create a new branch, and `git branch -d <branch_name>` to delete a branch.
    

## **git merge**

* **Usage**: Combines changes from one branch into another.
    
* **Example**: `git merge <branch_name>`
    
* **Explanation**: Merges the specified branch into the current branch, incorporating any changes made in `<branch_name>` into your working branch.
    

## **git checkout**

* **Usage**: Switches branches or restores working tree files.
    
* **Example**: `git checkout <branch_name>`
    
* **Explanation**: Use this command to switch between branches or restore files to their state at a specific commit.
    

## **git status**

* **Usage**: Displays the status of the working directory and staging area.
    
* **Example**: `git status`
    
* **Explanation**: Provides information about the current state of the repository, including modified files, staged changes, and untracked files.
    

## **git log**

* **Usage**: Displays commit history.
    
* **Example**: `git log`
    
* **Explanation**: Shows a chronological list of commits in the repository, including commit messages, authors, dates, and commit IDs.
    

## **git remote**

* **Usage**: Manages remote repositories.
    
* **Example**: `git remote -v`
    
* **Explanation**: Lists the remote repositories associated with the current repository, including their URLs.
    

## **git fetch**

* **Usage**: Downloads objects and references from another repository.
    
* **Example**: `git fetch origin`
    
* **Explanation**: Retrieves changes from the remote repository specified by `<remote_name>` and updates the corresponding remote-tracking branches.
    

## **git reset**

* **Usage**: Resets the current HEAD to a specified state.
    
* **Example**: `git reset --hard HEAD`
    
* **Explanation**: Resets the current branch to the specified commit, discarding any changes made after that commit.
    

## **git stash**

* **Usage**: Temporarily shelves changes in the working directory.
    
* **Example**: `git stash save "Work in progress"`
    
* **Explanation**: Stores the current changes in a "stash" and reverts the working directory to its clean state, allowing you to work on other tasks.
    

With this comprehensive GitHub cheat sheet, you'll have the knowledge and confidence to navigate GitHub like a pro. Whether you're collaborating with a team or working on personal projects, mastering these commands will streamline your workflow and enhance your development experience. Happy coding!

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)
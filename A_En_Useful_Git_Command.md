---
title: Useful Git Command
date: 2019-12-25 10:50:59
tags:
- Git
categories:
- 技术
- EnglishNotes
---


## Simple use
In this note I will summarize the simple use of Git. How can we create new folers and upload the local folders to remote. Or after we changes or add new files, how can we update the changes.

### 1. Create new folder locally and push it remote

If we create new local folder  and want to upload it into remote repository. We should cd into the local folder and type 

```bash
git init
```

This will let the local folder prepared to be a github folder. Then connect this folder to the remote folder

```bash
git remote add origin <https://gitxxxx.com/xxxxx/xxxxx.git>
```

The content in the "<>" should be replaced with your own git account link.  Then add all files

```bash
git add .
```

 add description

```bash
git commit -m "<some description here>"
```

Be careful that that `"<>"` double quotation marks are needed. Then  type 

```bash
git push -u origin master
```

When prompted to update the remote repository locally, proceed with the following command

```bash
git pull   
```

Prompt "git pull remote" and so on, continue with the following command

```bash
git pull origin master
```

If history related errors are prompted, continue with the following command

```bash
 git pull origin master --allow-unrelated-histories
```

Then you can push the local folder by typing 

```bash
git push origin master 
```



### 2. Update changes each time 

If the repository has been create in the remote and the local folder has push history. You can fetch changes from remote repository.

```bash
git pull
```

add new files to remote repository

```bash
git add .
git commmit -m "changes"
git push origin master
```
More details will be added if needed.

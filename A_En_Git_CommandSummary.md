# Useful Git Command





## Simple use

In this note I will summarize the simple use of Git. How can we create new repository and upload the local folders to remote？ Or after we changes or add new files, how can we update the changes？



### 1. Create new repository



We should create new repository in the remote.  Then we clone the remote repository into local folder. We can make changes on the folder and update the changes via



```bash

git add .

git commmit -m "changes"

git push -u origin master

```



”-u“ is for the first update.



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


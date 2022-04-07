## Commands:

1. GIT INIT
	```bash
	git init
	```
	
	This will create a new git repository in local and track all the chages you will done.

2. GIT CLONE
	```bash
	git clone repository_url
	```
	
	This will clone that repository in local. It means it will download all the files from that repository. But it will ignore those file which are mentioned in **.gitignore**
	
3. GIT STATUS
	```bash
	git status
	```
	
	This will tell you what things are left to commit or what are the changes made.
	
4. GIT DIFF
	```bash
	git diff file_name
	```
	This command will tell what changes are made in that file.

5. GIT ADD
	```bash
	git add file_name or . (for all files)
	```
	This command is use add the files you have to commit

6. GIT COMMIT
	```bash
	git commit -m "message"
	```
	This command will give commit the changes to the repository  with a message.
	If you don't want to make new commit and add other things in the previous commit then the command is 
	```bash
	git commit --amend
	```
	Then it will open the VI editor press **ESC** and :wq

7. GIT LOG
	```bash
	git log
	```
	This command will give logs what changes happened to this repository till now.
	If you want to see latest 5 logs then you can use **-5**
	
8. GIT SHOW
	```bash
	git show commit_hash
	```
	This will tell you what change happened in that hash.

9. GIT BRANCH
	```bash
	git branch
	```
	This command will tell the current branch of that repository.
	To delete any branch
	**git branch -d branch_name**
10. GIT CHECKOUT
	```bash
	git checkout -b branch_name
	```
	This command will make new branch. 
	You can change the branch also using **git checkout branch_name**

11. GIT PULL
	```bash
	git pull
	```
	This command will sync all the commit from local pc to remote. And it will merge all the changes to the remote repository.  It means it will update your local and remote files both. If anyone has added any file to the repo and in your local pc it is missing then it will download that file in to local pc.

12. GIT PUSH
	  ```bash
	  git push 
	  ```
	  This command will push all the changes you made in local to remote repository. 
## THEORY
* What is staging area and unstage area ?
	> Unstage area means where the changes are not added for commit whereas stage area means the changes are ready to commit in the repository.
	example:
	```bash 
	metaciphar@ashu:~/me/tools/git notes$ git commit
	On branch master
		Initial commit
	Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.obsidian/
	README.md
  nothing added to commit but untracked files present (use "git add" to track)
  ```
  
* How to remove latest commit ?
	> You can use below command to remove the latest commit you have done in the repository. But if you are using --hard then you cannot see the changes you made in that commit. So for this use **--soft**
	```bash 
	git reset --hard HEAD^
	```

* If you want to remove the latest commit but you also have to see the changes you made in that commit ?
> Then you can use 
```bash
git reset --soft commit_hash
```

* If you want to remove any file from stage area ?
> Then you can use below command. This will restore the changes you made in that file.
```bash
git restore --stage file_name
```

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
## STEPS TO ADD DATA IN THE REPOSITORY.
1. git config --global user.email "email@gmail.com"
2. git init
3. git add .
4. git commit -m "message"
5. git branch -M main
6. git remote add origin https://github.com/m3tac1ph4r/repository_url.git
7. git push -u origin main
https://pan.baidu.com/s/1kU5OCOB#path=%252Fpub%252Fgit

launch git bash/ git command
cd repository folder

## 1. create account
git config --global user.name "Mark Zhang"

git config --global user.email "highdream007@163.com"

## 2. create repository
mkdir mygit

## 3. navigate to repository folder
cd mygit/

## 4. initialize git environment
git init

## 5. create some test files under above repository

## 6. add files into stage
git add readme.txt file1.txt file2.txt

## 7. commit files to master repository
git commit -m "add new files"

## 8. check current files status working directory
git status

## 9. compare working directory with stage
 git diff

 compare one file with stage
 git diff HEAD -- file1.txt
 
## 10. compare working directory with master
git diff --cached

## 11. view modify history log
git log
git log --graph

git log --pretty=oneline

## 12. revert to master head version
git reset --hard HEAD

revert to previous version of HEAD
git reset --hard HEAD^

revert to pre-pre version of HEAD
git reset --hard HEAD^^

revert to pre 100 version of HEAD
git reset --hard HEAD~100

## 13. revert to some specified version
git reset --hard (version id)

## 14. view modified log to get specified version id
git reflog

## 15. if file has been modified, but not added into stage, want revert it
git checkout -- file1.txt

## 16. if file has been modified, and added into stage, want revert it
git reset --hard HEAD file1.txt
git checkout --file1.txt

## 17. if file has been modified, added into stage, and commit to master
git reset --hard (version id)

## 18. delete file
#### a. if wanna delete one file
rm file1.txt in working directory
git rm file1.txt
git commit -m "remove file1.txt"

#### b. you already committed file1.txt to master. you delete working directory file1.txt wrongly, and still not commit to master repository, and wanna revert it
rm file1.txt
git checkout -- file1.txt

#### c. you already commited file1.txt to master. you delete it in working directory and commit to master, wanna revert it
rm file1.txt =====> working directory
git rm file1.txt ====> stage
git commit -m "remove it" =====>master repository

***************************************************
git log --pretty=oneline =======> find out specified version id
git reset --hard (version id)

[results:] you will lost what changed or modification in your deleted working directory file.

#### d. if have commited and push to remote server with wrong files, need to remove remote repository
cd working directory
git rm -r \**.**
git commit -m "delete files"
git push


## 19. github remote settings:
#### a. if cannot push in windows machine, need to install below git-credential-manager:
https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.14.0

#### b. connect with github repository:
git remote add origin https://github.com/Mark-Zhang-007/learngit{repository in github} ====>origin means the alias of repository in github server

####  c. push all local git files to remote server
git push -u origin master ====>push all committed files to github server ====>{origin means the alias of repository setting in github when create it} ====>master means the local version will be pushed into github server.

####  d. clone remote repository to local repository
git clone https://github.com/Mark-Zhang-007/learngit{repository}

## 20. modify connection protocol if can't connect with remote repo with ssh in windows machine
git config --local -e
change entry of:

url = git@github.com:username/repo.git

to:

url = https://github.com/username/repo.git

## 21. create branch and switch to branch
git branch dev ====> create branch with name "dev"
git checkout dev ====>switch to branch

=====>git checkout -b dev ===={create branch and switch to branch with name "dev"}

## 22. view current branches, list all branches, and there will be one asterisk(*) before current active branch

git branch

=======> * dev
		  master
		  
## 23. then we can make some change on branch "dev", such as: add/modify file, commit to stage

## 24. switch to master

git checkout master

## 25. merge branch {dev}'s modification to master
git merge dev

## 26. now we can delete dev branch after mergeing finished
git branch -d dev

## 27. view log with graph
git log --graph --pretty=oneline --abbrev-commit

## 28. if need to fix some urgent bugs, can temporarily save current working directory&files in dev branch. then create bug branch, and merge it into master. afte that, back to dev branch, and restore temporary saving working directory.

####  a. save current dev not completed tasks/codes
git stash

####  b. switch to master branch
git checkout master

####  c. create new branch for issue-001
git checkout -b issue-001

####  d. fix the bug, make some change/modification, then add/commit to new branch
git add bug.txt / git add .
git commit -m "fix the bug 001"

####  e. merge into master
git checkout master
git merge --no-ff -m "fix the bug 001" issue-001

####  f. back to dev branch to complete not finished tasks/codes
git checkout dev

####  g. check/view current saved temporary tasks
git stash list

=======>stash@{0}: WIP on dev: 8cca683 commit remote dev

####  h. apply or recover to the saved tasks
###### 1>. git stash apply stash@{0}  ====>{recover it, but the stash still exists}
######   2>. git stash pop ===>{recover it, and then drop the stash}

####   i. check current dev branch
git status

####  j. add/commit modifications
git add .
git commit -m "new feature added"

####  k. merge master and dev
git checkout master
git merge --no-ff -m "add new feature" dev

####  l. push into github server
git push -u origin master

## 29. create tag

####  a. git tag v1.0 ====>add the tag on current branch's head version
####  b. git tag v0.9 {version id} ====>add tag on some specified version
####  c. git tag ====>view current tag list
####  d. git show v1.0  =====> view some specified tag detail information
####  e. git tag -a v0.1 -m "version 0.1 released" 3628164  ======>add some description on some specified version
####  f. git tag -s v0.2 -m "signed version 0.2 released" fec145a ========>add PGP signature with gpg publick key

####  g. how to configure gpg public key

{window 7 按照如下配置后，就可以了。 
1、需到官网www.gnupg.org 下载对应系统的加密软件； 
2、根据http://www.ruanyifeng.com/blog/2013/07/gpg.html 设置好，并生成自己的密钥； 
3、在git上
（1）配置gpg程序位置，先找到GnuPG的安装目录下gpg2.exe的路径，默认是C:\Program Files (x86)\GNU\GnuPG。 配置gpg.program的位置： 在Git Bash中进行配置 $ git config –global gpg.program “C:\Program Files (x86)\GNU\GnuPG\gpg2.exe” （2）配置signingkey： 查看sigingkey，在Windows命令终端下为gpg –list-keys 在Git Bash中进行配置 $ git config user.signingkey F08971B8 F08971B8这个是别人的公钥ID，需替换上自己的

## 30. push current tag
####  a. git push v1.0 =====>push local specified tag to github
####  b. git push --tags =====>push all not pushed local tags to github
####  c. git tag -d v1.0 =====>delete local tag v1.0
####  d. git push origin :refs/tags/<tagname> =====>delete specified tag from github


## 31. create ignore file list

方法一（最直接）：
在资源管理创建文件时，文件命名“.gitignore.”，注意结尾有个.号，回车确认时系统会自动存成.gitignore。

方法二：
打开文本编辑器，保存时文件名输入“.gitignore”，保存类型选“所有文件”、

方法三：
进入cmd命令行，执行 echo > .gitignore 输入空内容并创建文件，或执行 rename somefile .gitignore、copy somefile .gitignore 从已有文件复制、重命名。

##################################################
/Aspect_NLU_backup/Core/bin/Debug
/Aspect_NLU_backup/Core/obj/Debug
/Aspect_NLU_backup/Aspect_NLU.v12.suo
##################################################
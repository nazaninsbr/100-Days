<b>Git: distributed version control system</b>

<p style="color: #D3D3D3">
	Sources:<br>
	[1] This <a href="https://www.youtube.com/watch?v=HVsySz-h9r4">youtube tutorial</a> <br>
	[2] Git <a href="https://git-scm.com/docs">Docs.</a>
	<hr>
</p>


### Basic Commands:
(1) get the version of git you have installed:<br>
```
$ git --version
```
(2) set your name and email (this will be what others see in the author section):<br>
```
$ git config --global user.name "my name"
$ git config --global user.email "myEmail@x.com"
```
(3) see git setting:<br>
```
$ git config --list
```
(4) how to use help in git:<br>
```
$ git help <what you need help with>
$ git <what you need help with> --help
```
(5) create a git project in the directory you are in:<br>
```
$ git init
```
(6) see modified files:<br>
```
$ git status
```
(7) add files to staging area:<br>
```
$ git add --all
$ git add -A
$ git add fileName
```
(8) remove files from the staging area:<br>
```
$ git reset fileName
$ git reset
```
(9) commit the files that are in the staging area:<br>
```
$ git commit -m "something"
```
(10) see the commits:<br>
```
$ git log
```
(11) set the remote repo:<br>
```
$ git remote add origin <url>
```
(12) check the remote repo. url:<br>
```
$ git remote -v
```
(13) see the current branch:<br>
```
$ git branch -a
```
(14) see how the files have changed compared to the commited ones:<br>
```
$ git diff
```
(15) get the changes on the remote:<br>
```
$ git pull
$ git pull origin master
```
(16) push changes to remote:<br>
```
$ git push -u origin master
$ git push 
```
(17) create a branch and go to it:<br>
```
$ git branch <branch name>
$ git checkout <branch name>
```
(18) merge branch with master:<br>
```
$ git checkout master
$ git merge <branch name>
```
(19) see merged branches:<br>
```
$ git branch --merged
```
(20) delete branch:<br>
```
$ git branch -d <branch name>
```
(21) delete branch on remote:<br>
```
$ git push origin --delete <branch name>
```
---
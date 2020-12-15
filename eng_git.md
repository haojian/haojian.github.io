Git commands
===========


@[git | dev]


- [Git LFS](https://git-lfs.github.com/)
- [Serverless Git LFS for Game Development](https://alanedwardes.com/blog/posts/serverless-git-lfs-for-game-dev/)

**merge conflicts**

- [squash the commits in one pull request](http://blog.steveklabnik.com/posts/2012-11-08-how-to-squash-commits-in-a-github-pull-request)
	```
    550  git remote add upstream git@XXXXXXXXXXXXX.git
    551  git fetch upstream
    552  git branch
    553  git rebase -i upstream/master
    554  git status
    555  git add filepath
    556  git rebase --continue
    557  git status
    558  git add  filepath
    559  git rebase --continue
	```
:%s/pick/squash/gc
- [merge conflicts](https://rtcamp.com/tutorials/git/git-resolve-merge-conflicts/) : theirs and ours
- [undo a "git push"](http://stackoverflow.com/questions/1270514/undoing-a-git-push) 
	 ``` 
	 git reset version_code
	 git push -f origin 
	 ```
	 
- [use rebase to squeash commits](http://makandracards.com/makandra/527-squash-several-git-commits-into-a-single-commit)  Recommended!!
	- in case there is a conflict. [git merge](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line/)
- [squeash commits](http://stackoverflow.com/questions/5189560/squash-my-last-x-commits-together-using-git?rq=1)
	- this one works most time, but has an issue about losing some file trackings. The history would be dirtier than the rebase one.
	```
	# Reset the current branch to the commit just before the last 12:
	git reset --hard HEAD~12

	# HEAD@{1} is where the branch was just before the previous command.
	# This command sets the state of the index to be as it would just
	# after a merge from that commit:
	git merge --squash HEAD@{1}

	# Commit those squashed changes.  The commit message will be helpfully
	# prepopulated with the commit messages of all the squashed commits:
	git commit
	```

**version control**
- discard unstaged changes in git: ` git stash save --keep-index` 
- discard local commit: `git reset --hard origin/master`
- change last commit message: `git commit --amend -m "New commit message"`
- get back to most recent version: `git checkout master`
- go back two versions: `git checkout HEAD~2`
- create a temporary branch based on 2 versions back: `git checkout -b temp_branch HEAD~2`

**branch**
- git checkout remote branches (2 steps):
    - fetch a branch: `git fetch origin`
    - get a local copy: `git checkout -b [name] origin/[name]`
- push local branch to remote: `git push origin [name]`
- view remote branches: `git branch -r`
- create a new local branch: `git checkout [name]`
- create a new local branch and switch to it: `git checkout -b [name]`
- delete branch: `git branch -d [name]` only merged branch can be deleted with `-d`. Force delete `-D`
- merge branches: `git merge [name]`  branch [name] would be merged to current branch.
- push local branch to remote: `git push origin [name]`
- delete remote branch: `git push origin :heads/[name]` or `git push origin :[name]`

**code checkin**
- commit a single file/directory: `git commit -m 'my notes' -- path/to/my/file.ext`
- Ignore files that have already been committed to a Git repository:

```
First commit any outstanding code changes, and then, run this command:
	git rm -r --cached .
This removes any changed files from the index(staging area), then just run:
	git add .
Commit it:
	git commit -m ".gitignore is now working"
```

**stash**
- creating a branch from a stash: `git stash branch testchanges`
- list stash: `git stash list`
- apply stash: `git stash apply stash@{2}`
- drop stash: `git stash drop stash@{0}`

**history**
- view the commit history: `git log`
- advanced version: `git log --pretty="%h - %s" --author=gitster --since="2008-10-01" --before="2008-11-01" --no-merges -- t/`
- remove all git files: `find . | grep .git | xargs rm -rf`

**compare**
- compare local git branch with remote branch: `git diff <local branch> <remote-tracking branch>` `git diff master origin/master`
- show statistic: `git diff --stat --color remotes/main/master..origin/master`


**init a git repo with a local directory**


```
git init
git add .
git commit -am "init commit"
ssh -T git@**********     //verify if the access works
git remote add origin address 	//create a repos in the web and get the address there
git remote -v 					//usually we can get two lines (fetch & push)
git pull
git push origin master

[reference](http://my.oschina.net/flan/blog/162189)

```

There is no tracking information for the current branch. 

```
  git pull origin master
  git push -u origin master
```

**Miscs**

recursively remove .DS_Store files on Mac OS X: `find . -name '*.DS_Store' -type f -delete`

remove/delete a large file from commit history in Git repository: `git gc --prune=now --aggressive`

show remote url: `git remote show origin`

Git: “Not currently on any branch.” : 
```
git stash
git checkout some-branch
git stash pop
```
**References**
[Commits didn't show up in the profile page](https://help.github.com/articles/setting-your-email-in-git)


The recommended steps to follow for any contribution are:
```
Fork it
Create your feature branch (git checkout -b my-new-feature)
Commit your changes (git commit -am 'Added some feature')
Push to the branch (git push origin my-new-feature)
Create new Pull Request
```

**fork and pull**

```
假设你fork的项目原始地址是http://github.com/abc/rep.git, 你自己的是http://github.com/you/rep.git 

$ git add remote upstream http://github.com/abc/rep.git # 你本地的origin应该跟了自己的remote，前且假设当前本地branch是master。 
$ git fetch upstream 
$ git merge upstream/master # merge可能会有冲突，手工解决掉并commit 
$ git push origin/master # push到你自己的fork上 

然后向原始项目提交一个pull request。
```


**upload local key to the server**
`scp ~/.ssh/id_rsa xxxxx.corp.gq1.yahoo.com:~/.ssh/id_rsa`


**advanced tricks**

- [How to fork a github repository in bitbucket](https://gist.github.com/jcaraballo/1982605)
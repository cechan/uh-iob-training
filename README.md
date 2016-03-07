Git training:

Git for SVN users:
  * https://git-scm.com/course/svn.html
  * http://www.git-tower.com/blog/git-for-subversion-users-cheat-sheet/

We will NOT be using contrib model, Upstream would be KualiCo, Origin UH-KFS github.  Master will represent KualiCo and not be committed to, uh-master will serve as our master branch.  All devs will have write access to Origin so feature branches, dev, test, and uh-master can all be in Origin.  Devs could do thier own forks if they want and submit pull request per usual.

```
On GitHub - https://github.com/UniversityOfHawaii/uh-iob-training.git
	Change Branch: to test, uh-master, and master.
		Observe how you can see only TEST.txt, UH-MASTER.txt in their respective branches.  Notice that MASTER.TXT is in test and uh-master (as these are branches of master)

Locally:
	git clone https://github.com/UniversityOfHawaii/uh-iob-training.git
	git branch
		Notice how test and uh-master are not listed (only master)
	git branch -a
		Notice how you can see the branches on remotes/origin/
	git checkout uh-master
		Notice that you can now see UH-MASTER.txt
	git checkout test
		Notice that you can now see TEST.txt and not UH-MASTER.txt
	git checkout master
		Notice that you no longer see TEST.txt, and UH-MASTER.txt
	git branch
		Notice how you can now see test, master, and uh-master

General Workflow:
	Create a new branch for your work:
		Create a new file
		Stage your change
		Commit your change (locally)
		Push your local commited changes

	Continue to work on your branch:
		Get changes from uh-master (trainer adds file to uh-master)
			Merging vs Rebase:
				http://stackoverflow.com/questions/33966857/avoiding-merge-commits-in-pull-requests-in-git
			About pull:
				https://coderwall.com/p/jiswdq/let-s-all-take-a-moment-of-silence-git-pull-is-dead	
		Edit MY_BRANCH.txt
		Observe diff
		Stage
		Observe lack of diff
		Observe remote diff
		Commit (locally)
		Observe lack of diff
		Observe remote diff
		Push
		Observe lack of diff
		Edit MY_BRANCH.txt more
		Stage, Commit, Push
		Create new file MY_BRANCH-2.txt
		Stage, Commit, Push		

	Deliver:
		Pull Request to dev-MY_BRANCH from feature branch
		Squashed Pull Request to test from dev-MY_BRANCH
		Squashed Pull Request to uh-master from test
		Cherry pick as required

	Cherry-pick:



CLI Workflow:
	Create a new branch from uh-master your work:
		git checkout -b MY_BRANCH uh-master
		Observe branch only exists locally:
			branch -a
		Create branch remotely:
			git push --set-upstream origin MY_BRANCH
		Create a new file:
			touch MY_BRANCH.txt
		Observe untracted file MY_BRANCH.txt
			git status
		Stage your change:
			git add MY_BRANCH.txt
		Observe newfile MY_BRANCH.txt
			git status
		Commit your change (locally):
			git commit -m 'MY_BRANCH.txt'
		Observe 1 commit note
			git status
		Push your locally commited changes:
			git push

	Continue to work on your branch:	
		Get changes from uh-master (trainer adds file to uh-master)
			Merging vs Rebase:
				http://stackoverflow.com/questions/33966857/avoiding-merge-commits-in-pull-requests-in-git
					git fetch origin
					git checkout uh-master
					git merge --ff origin/uh-master

					git checkout erik0
					git rebase uh-master
					git push -f origin erik0

		Edit MY_BRANCH.txt, Observe diff
			git diff
		Stage:
			git add MY_BRANCH.txt
		Observe lack of diff:
			git diff
		Observe diff:
			git diff origin/MY_BRANCH
		Commit (locally):
			git commit -m 'MY_BRANCH.txt #CONTINUE'
		Observe lack of diff:
			git diff
		Observe diff:
			git diff origin/MY_BRANCH
		Push:
			git push
		Observe lack of diff:
			git diff origin/MY_BRANCH
		Edit MY_BRANCH.txt more, Stage, Commit, Push
			git add MY_BRANCH.txt
			git commit -m 'MY_BRANCH.txt #CONTINUE2'
			git push
		Create MY_BRANCH-2.txt Stage, Commit, Push
			touch MY_BRANCH-2.txt
			git add MY_BRANCH-2.txt
			git commit -m 'MY_BRANCH-2.txt #CONTINUE3'
			git push

	Deliver:
		Pull Request to dev-MY_BRANCH from feature branch:
			git checkout -b dev-MY_BRANCH MY_BRANCH
			git push --set-upstream origin dev-MY_BRANCH
		Squashed Pull Request to test:	
			git checkout test
			git pull --squash origin dev-MY_BRANCH
			git commit -m 'git pull --squash origin dev-MY_BRANCH'
			git push
		Squashed Pull Request to uh-master:
			git checkout uh-master
			git pull --squash origin test
			git commit -m 'MY_BRANCH git pull --squash origin uh-master'
			git push

	Observe your log:
		git log



TODO Desktop version
	Beware GitHub Desktop Sync!
		http://stackoverflow.com/questions/12104513/what-does-github-for-windows-sync-do



TODO Eclipse version



Notes:

Git push from a branch:
git config --global push.default matching
warning: push.default is unset; its implicit value has changed in
Git 2.0 from 'matching' to 'simple'. To squelch this message
and maintain the traditional behavior, use:

  git config --global push.default matching

To squelch this message and adopt the new behavior now, use:

  git config --global push.default simple

When push.default is set to 'matching', git will push local branches
to the remote branches that already exist with the same name.

Since Git 2.0, Git defaults to the more conservative 'simple'
behavior, which only pushes the current branch to the corresponding
remote branch that 'git pull' uses to update the current branch.

See 'git help config' and search for 'push.default' for further information.
(the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
'current' instead of 'simple' if you sometimes use older versions of Git)

fatal: The current branch erik0 has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin MY_BRANCH



Script:

# SETUP
git clone https://github.com/UniversityOfHawaii/uh-iob-training.git
cd uh-iob-training
cp ../Git\ training.txt README.md
git add README.md 
touch MASTER.txt
git add MASTER.txt 
git commit -m 'MASTER.txt and README.md'
git push
git branch uh-master
git checkout uh-master
touch UH-MASTER.txt
git add UH-MASTER.txt 
git commit -m 'UH-MASTER.txt'
git push --set-upstream origin uh-master
git checkout -b test uh-master
touch TEST.txt
git add TEST.txt 
git commit -m 'TEST.txt'
git push --set-upstream origin test


# WORKFLOW
git status
git checkout -b erik0 uh-master
git push
#git checkout erik0
touch erik0.txt
git add erik0.txt 
git commit -m 'erik0.txt #WORKFLOW'
git push --set-upstream origin erik0


# TRAINER adds file to uh-master
git checkout uh-master
touch UH-MASTER-NEW.txt
git add UH-MASTER-NEW.txt
git commit -m 'UH-MASTER-NEW.txt'
git push
git checkout erik0


# CONTINUE
git fetch origin
git checkout uh-master
git merge --ff origin/uh-master

git checkout erik0
git rebase uh-master
git push -f origin erik0

echo "# CONTINUE" > erik0.txt
git add erik0.txt 
git commit -m 'erik0.txt #CONTINUE'
git status
git push

echo "# CONTINUE2" >> erik0.txt
git add erik0.txt 
git commit -m 'erik0.txt #CONTINUE2'
git status
git push

touch erik0-2.txt
git add erik0-2.txt
git commit -m 'erik0-2.txt #CONTINUE3'
git push

# DELIVER using dev-erik0 to test
git checkout -b dev-erik0 erik0
git push --set-upstream origin dev-erik0
git checkout test
git pull --squash origin dev-erik0
git commit -m 'git pull --squash origin dev-erik0'
git push

# test to uh-master
git checkout uh-master
git pull --squash origin test
git commit -m 'git pull --squash origin uh-master'
git push

```

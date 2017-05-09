Git cheatsheet

# Status ..

* `git status -s` or `git status --short` - left side staged, right side modified'

# Diff

* `git diff` diff unstaged vs staged
* `git diff --staged` diff staged vs committed
* `git difftool` for a GUI

# Commit

* `git commit -v` for 

# Remove
* `git rm --cached foo.a`  Remove foo.a from the staging area, but leave it in your working directory

# Log 

* `git log -p` Show the difference included in each commit
* `git log -p -2` As above, but show only the last 2 commits
* `git log -p -2 --stat` As above, but show stats
* `git log --pretty=oneline`
* `git log --pretty=format:"%h - %an, %ar : %s"`
* `git log --since=2.weeks`
* `git log --since="2008-01-15"`
* `git log --since="5 days ago"`
* `git log --graph --all --decorate --oneline` Shows all branches, decorated with names
* `git log --graph --all  --pretty="%C(yellow)%h%Creset %C(blue)%cd%Creset %s"` with colors and times
* `git log --graph --all  --pretty="%C(auto)%h%Creset %C(blue)%cd%Creset %C(auto)%d%Creset %s" --date=local` with refs as well
* `git log --graph --all  --pretty="%C(auto)%h%Creset %C(blue)%cd%Creset %C(auto)%<|(50)%d%Creset %s" --date=local` padding the ref name to col 50

# Undo (Dangerous)

* `git commit --amend`
* `git reset HEAD file` Unstage a staged file - as shown in the output of `git status`
* `git checkout -- file` Unmodify a modified file. __*Dangerous*__

# Remotes 
* `git remote` Show remotes
* `git remote -v` Shows the URLs as well
* `git remote add [shortname] [url]` Add a new remote
* `git remote show origin` 
* `git remote rename pb paul`
* `git push origin :Activate` delete remote branch Activate. Still need to `git branch -d Activate`


# Tags
* `git tag` List all tags
* `git tag -l 'v1.*'` List all tags that start with `v1.`
* `git tag -a v1.4 -m 'my version 1.4'` Create an annotated tag - full commit history, etc.
* `git show v1.4` Show tag v1.4
* `git tag -a v1.2 9fceb02` Tag an existing commit after the fact
* `git push origin --tags` Push all tags to server
* `git checkout -b version2 v2.0.0` Create a new branch at a specific tag


# Aliases
* `git config --global alias.co checkout`
* `git config --global alias.br branch`
* `git config --global alias.ci commit`
* `git config --global alias.st status`
* `git config --global alias.unstage 'reset HEAD --'`
* `git config --global alias.visual "!gitk"`
* `git config --global alias.rmbr branch -d`
* `git config --global alias.rmrbr push origin :`

# Branches
* `git branch -v` Show branches as well as last commit on each branch
* `git branch --merged | --no-merged` Show merged/unmerged branches
* `git branch -d Activate` Delete local branch Activate
* `git push origin :Activate` delete remote branch Activate. Still need to `git branch -d Activate`

# Push
* `git push origin master`
* `git push origin :Activate` delete remote branch Activate. Still need to `git branch -d Activate`
* `git push origin serverfix` is equivalent to `git push origin refs/heads/serverfix:refs/heads/serverfix` and `git push origin serverfix:serverfix`
* `git push origin serverfix:awesomeSauce` Push serverfix to server to as awesomeSauce
* `git push -u myforkRemote featureA` Push branch feature A to a fork remote

# Fetching/Tracking
* The next person can get serverfix by `git fetch origin`. Does not merge. `git pull` merges
* Then, that person can create their own local serverfix branch with `git checkout -b serverfix origin/serverfix`
* Or, he could just do (for short): `git checkout --track origin/serverfix`. This tracks the remote branch.
* Or, as a shortcut to that shortcut: `git checkout serverfix`, since that branch exists on the remote.
* `git branch --set-upstream-to origin/serverfix` to add/change a tracking branch
* `@{upstream}` or `@{u}` is a shorthand for upstream branch. e.g. `git merge @{u}` instead of `git merge origin/master`
* `git branch -vv` show brances with tracking info (ahead/behind).
* But this is not live data. To get live data do `git fetch --all; git branch -vv`
* If you have a local branch and want to create a remote tracking branch: `git push --set-upstream origin BranchName`

# Rebase
#### Steps

                   +- C4 (experiment)
                   v
    C0 <- C1 <- C2 <- C3 (master)

* `git checkout experiment`
* `git rebase master`

Then

                    +- XXX
                    v
     C0 <- C1 <- C2 <- C3 (master) <- C4' (experiment)


* `git checkout master`
* `git merge experiment` (fast-forward)

Then

     C0 <- C1 <- C2 <- C3 <- C4' (experiment) (master)

### __*Do not rebase commits that exist outside your repository.*__

* `git rebase -i` to squash commits. 

# GitHub

#### Pull Request while master has changed

> If you want to merge in the target branch to make your Pull Request mergeable,
you would add the original repository as a new remote, fetch from it, merge
the main branch of that repository into your topic branch, fix any issues and
finally push it back up to the same branch you opened the Pull Request on.

    $ git remote add upstream https://github.com/schacon/blink 1
    
    $ git fetch upstream 2
    remote: Counting objects: 3, done.
    remote: Compressing objects: 100% (3/3), done.
    Unpacking objects: 100% (3/3), done.
    remote: Total 3 (delta 0), reused 0 (delta 0)
    From https://github.com/schacon/blink
     * [new branch]      master     -> upstream/master
    
    $ git merge upstream/master 3
    Auto-merging blink.ino
    CONFLICT (content): Merge conflict in blink.ino
    Automatic merge failed; fix conflicts and then commit the result.
    
    $ vim blink.ino 4
    $ git add blink.ino
    $ git commit
    [slow-blink 3c8d735] Merge remote-tracking branch 'upstream/master' \
        into slower-blink
    
    $ git push origin slow-blink 5
    Counting objects: 6, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (6/6), done.
    Writing objects: 100% (6/6), 682 bytes | 0 bytes/s, done.
    Total 6 (delta 2), reused 0 (delta 0)
    To https://github.com/tonychacon/blink
       ef4725c..3c8d735  slower-blink -> slow-blink
    

1. Add the original repository as a remote named “upstream”
2. Fetch the newest work from that remote
3. Merge the main branch into your topic branch
4. Fix the conflict that occured
5. Push back up to the same topic branch


# References

* `git show HEAD{5}` Show the fifth prior value of HEAD (local data only)
* `git show HEAD^` Show the previous commit
* `git show d921970^` Show the commit previous to `d921970`
* `git show d123^2` Show the second parent of `d123`
* `git show HEAD~3` Same as `git show HEAD^^^` which is "first parent of first parent of first parent"
* `git log master..experiment` Show commits that are in (reachable by) experiment but not in (reachable by) master. 
* `git log refA refB ^refC` == `git log refA refB --not refC` Show commits reachable from refA or refB but not refC

Given: 

    A <- B <- E <- F <- (master)
           ^
           +- C <- D <- (experiment)

Then 

* `git log master...experiment` See what's in `master` or `experiment` but not any common references

Gives us: 

    F
    E
    D
    C

* `git log --left-right master...experiment` See what's in `master` or `experiment` but not any common references

Gives us: 

    < F
    < E
    > D
    > C

# Stashing

* `git stash` Add to stash stack
* `git stash list` Show stash list (with references to `stash@{n}`)
* `git stash apply` Apply most recent stash
* `git stash apply stash@{2}` Apply third most recent stash (counting from zero)
* `git stash apply --index` Apply stash and 'restore' index
* `git stash drop` Drop the stash after applying
* `git stash --keep-index` Don't stash things in the index (assuming you'll commit them)
* `git stash --include-untracked` == `git stash -u` Include untracked files

# Utilities

* `git grep`
* `git log -SZLIB_BUF_MAX --oneline` Show when ZLIB_BUF_MAX was introduced
* `git log -L :drawRect:Slycr/Utilities/SLYCheckerView.m` - Show how drawRect has changed over time


# Rewriting History

* `git commit --amend` Update log or add new files. __*Don't do this if commit is already pushed*__

## Reset (from [here](http://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified))

### Steps

* Move the branch HEAD points to (stop here if --soft)
* Make the Index look like HEAD (stop here unless --hard)
* Make the Working Directory look like the Index

* `git reset --soft COMMIT` essentially undoes the commit - updates the head, but doesn't change the index or wd. Good for squashing commits
* `git reset --mixed COMMIT` undoes the stage
* `git reset --hard COMMIT` __*Dangerous*__ Undoes Everything


### Notes

* `git reset file.txt` effectively unstages the file, by copying HEAD to INDEX. Just the opposite of `git add`


## Checkout

* `git checkout (commit) [file]` replaces Working Directory file with the version in (commit)

Here’s a cheat-sheet for which commands affect which trees. The “HEAD” column
reads “REF” if that command moves the reference (branch) that HEAD points to,
and “HEAD” if it moves HEAD itself. Pay especial attention to the WD Safe?
column – if it says NO, take a second to think before running that command.

                                           Head         Index       Workdir     WD Safe?
    Commit Level

    reset --soft [commit]                  REF          NO          NO          YES
    reset [commit]                         REF          YES         NO          YES
    reset --hard [commit]                  REF          YES         YES         NO
    checkout [commit]                      HEAD         YES         YES         YES

    File Level

    reset (commit) [file]                  NO           YES         NO          YES
    checkout (commit) [file]               NO           YES         YES         NO


# Reverts

Given:

                            +- (master, HEAD)
                            v
    C1 <- C2 <- C5 <- C6 <- M 
             ^              |
             |              | 
             +- C3 <- C4 <--+ 
                       ^
                       +- (topic)

Then, `git reset --hard HEAD~` would reset the branch pointers to give you             

                       +- (master, HEAD)
                       V
    C1 <- C2 <- C5 <- C6 <- M
             ^              |
             |              | 
             +- C3 <- C4 <--+ 
                       ^
                       +- (topic)


But, `git revert -m 1 HEAD` would give you: 

                                  +- (master, HEAD)
                                  v
    C1 <- C2 <- C5 <- C6 <- M <- ^M
             ^              |
             |              | 
             +- C3 <- C4 <--+ 
                       ^
                       +- (topic)

Where the `-m 1` tells it to use the first parent (the old HEAD), the C6 and
not the C4. Now ^M == C6. But C4 is already merged in. If topic has another
commit, Only the new changes will be merged in. That would be a problem
because it would not contain the contents of C3 and C4.

                                        +- (master, HEAD)
                                        v
    C1 <- C2 <- C5 <- C6 <- M <- ^M <- C8
             ^              |           |
             |              |           |
             +- C3 <- C4 <--+--- C7 <---+ 
                       ^
                       +- (topic)

The best way around this is to un-revert the original merge, since now you
want to bring in the changes that were reverted out, then create a new merge
commit:

    $ git revert ^M
    [master 09f0126] Revert "Revert "Merge branch 'topic'""
    $ git merge topic

Which gives us:     

                                               +- (master, HEAD)
                                               v
    C1 <- C2 <- C5 <- C6 <- M <- ^M <- ^^M <- C8
             ^              |                  |
             |              |                  |
             +- C3 <- C4 <--+--- C7 <----------+ 
                       ^
                       +- (topic)

In this example, M and ^M cancel out. ^^M effectively merges in the changes
from C3 and C4, and C8 merges in the changes from C7, so now topic is fully
merged.

# Merges

* `git merge --abort` abort a merge

Useful options: 

* `ignore-all-space`
* `ignore-space-change`
* `-Xours` use ours in conflict
* `-Xtheirs` use theirs in conflict

After a merge: 
 * `git diff --ours` compare merged file with our version
 * `git diff --theirs` compare merged file with their version
 * `git diff --base` compare merged file with base version
 * Use `-w` to strip out whitespace
 * `git co --conflict=[diff3|merge]` Recheckout the file again and replace the merge conflict markers.

# Blame

* `git blame -L 1,200 Vaporstream/AppDelegate.m`

Use -C to show where the line originally came from: 

    $ git blame -C -L 141,153 GITPackUpload.m
    f344f58d GITServerHandler.m (Scott 2009-01-04 141)
    f344f58d GITServerHandler.m (Scott 2009-01-04 142) - (void) gatherObjectShasFromC
    f344f58d GITServerHandler.m (Scott 2009-01-04 143) {
    70befddd GITServerHandler.m (Scott 2009-03-22 144)         //NSLog(@"GATHER COMMI
    ad11ac80 GITPackUpload.m    (Scott 2009-03-24 145)
    ad11ac80 GITPackUpload.m    (Scott 2009-03-24 146)         NSString *parentSha;
    ad11ac80 GITPackUpload.m    (Scott 2009-03-24 147)         GITCommit *commit = [g
    ad11ac80 GITPackUpload.m    (Scott 2009-03-24 148)
    ad11ac80 GITPackUpload.m    (Scott 2009-03-24 149)         //NSLog(@"GATHER COMMI
    ad11ac80 GITPackUpload.m    (Scott 2009-03-24 150)
    56ef2caf GITServerHandler.m (Scott 2009-01-05 151)         if(commit) {
    56ef2caf GITServerHandler.m (Scott 2009-01-05 152)                 [refDict setOb
    56ef2caf GITServerHandler.m (Scott 2009-01-05 153)
    
# Bisect

    $ git bisect start
    $ git bisect bad
    $ git bisect good v1.0
    Bisecting: 6 revisions left to test after this
    [ecb6e1bc347ccecc5f9350d878ce677feb13d3b2] error handling on repo

    $ git bisect good
    Bisecting: 3 revisions left to test after this
    [b047b02ea83310a70fd603dc8cd7a6cd13d15c04] secure this thing
   
    $ git bisect bad
    Bisecting: 1 revisions left to test after this
    [f71ce38690acf49c1f3c9bea38e09d82a5ce6014] drop exceptions table

    $ git bisect good
    b047b02ea83310a70fd603dc8cd7a6cd13d15c04 is first bad commit
    commit b047b02ea83310a70fd603dc8cd7a6cd13d15c04
    Author: PJ Hyett <pjhyett@example.com>
    Date:   Tue Jan 27 14:48:32 2009 -0800
    
        secure this thing
    
    :040000 040000 40ee3e7821b895e52c1695092db9bdc4c61d1730
    f24d3c6ebcfc639b1a3814550e62d60b8e68a8e4 M  config
    

    $ git bisect reset # reset HEAD

    OR: 

    $ git bisect start HEAD v1.0
    $ git bisect run test-error.sh    

# Plumbing
- `git ls-files -s` show index
- `git cat-file -p HEAD` show the tree SHA, parent commit, author & committer and notes for HEAD
- `git ls-tree TREESHA` show the contents of the tree whose SHA is TREESHA


# Errata

* 7.8  anecestor
* 7.13 Line 1: it's

# Git Flow

* `git flow init`
* `git flow feature start`  Makes a branch


# Common Issues

# Show file in previous commit
$ git show HEAD~:fileName

## How to revert a commit
- git revert commitToRevert

## Get an older version of file
- git checkout 88eee6607036223409483069cd80312e0cfcae05 fileName # WILL CLOBBER WORKING DIRECTORY'S COPY!!!!

## How to squash multiple commits into one


## Remove something from staging area that you forgot to put into .gitignore
git rm --cached README

## Change the comment or add a file to the last commit
git commit --amend 

## Unstaging a file
git reset HEAD file

## Unmodifying a modified file
git checkout -- 

## CherryPick just one file from a commit
git checkout commit file
or git cherrypick --nocommit

## Get rid of 2 commits

E-F-G-H-I-J topicA

git rebase (see man page). Danger. I prefer revert

## How to fix diverging branches when git flow is not followed
18:12:14 aijaz@AAA.local test3 master git revert 8bb57aa
[master c40133e] Revert "m2"
 1 file changed, 1 insertion(+), 1 deletion(-)
18:12:24 aijaz@AAA.local test3 master glp
* c40133e Sat Nov 19 18:12:21 2016  (HEAD, master) Revert "m2"
* 8bb57aa Sat Nov 19 18:11:28 2016  m2
* 4351382 Sat Nov 19 18:11:21 2016  m1
| * cf37da3 Sat Nov 19 18:11:00 2016  (develop) d2
| * 999e452 Sat Nov 19 18:10:48 2016  d1
|/
* fe2b44c Sat Nov 19 18:09:51 2016  Initial version
18:12:27 aijaz@AAA.local test3 master git revert 4351382
[master 0dfdd77] Revert "m1"
 1 file changed, 1 insertion(+), 1 deletion(-)
18:12:39 aijaz@AAA.local test3 master gl
* 0dfdd77 Sat Nov 19 18:12:36 2016  (HEAD, master) Revert "m1"
* c40133e Sat Nov 19 18:12:21 2016  Revert "m2"
* 8bb57aa Sat Nov 19 18:11:28 2016  m2
* 4351382 Sat Nov 19 18:11:21 2016  m1
| * cf37da3 Sat Nov 19 18:11:00 2016  (develop) d2
| * 999e452 Sat Nov 19 18:10:48 2016  d1
|/
* fe2b44c Sat Nov 19 18:09:51 2016  Initial version
18:12:40 aijaz@AAA.local test3 master git merge develop
Merge made by the 'recursive' strategy.
 file.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
18:12:51 aijaz@AAA.local test3 master x file.txt
d2
18:12:56 aijaz@AAA.local test3 master


* Then, that person can create their own local serverfix branch with `git checkout -b serverfix origin/serverfix`
* Or, he could just do (for short): `git checkout --track origin/serv
* But this is not live data. To get live data do `git fetch --all; git branch -vv`
* Git revert
* git diff
* man git
* man gitcli
* man giteveryday
* man gitrevisions

## How to work with a private remote

# delete a remote tracking branch

git branch -d -r myfork/branch

# Git hooks

https://www.atlassian.com/git/tutorials/git-hooks/local-hooks

# Pre-commit Hook

```bash
#!/bin/sh

# Check if this is the initial commit
if git rev-parse --verify HEAD >/dev/null 2>&1
then
    echo "pre-commit: About to create a new commit..."
    against=HEAD
else
    echo "pre-commit: About to create the first commit..."
    against=4b825dc642cb6eb9a060e54bf8d69288fbee4904
fi

# Use git diff-index to check for whitespace errors
echo "pre-commit: Testing for whitespace errors..."
if ! git diff-index --check --cached $against
then
    echo "pre-commit: Aborting commit due to whitespace errors"
    exit 1
else
    echo "pre-commit: No whitespace errors :)"
    exit 0
fi
```

# Prepare commit hook

```python
#!/usr/bin/env python

# via https://www.atlassian.com/git/tutorials/git-hooks/local-hooks

import sys, os, re
from subprocess import check_output

# Collect the parameters
commit_msg_filepath = sys.argv[1]
if len(sys.argv) > 2:
    commit_type = sys.argv[2]
else:
    commit_type = ''
if len(sys.argv) > 3:
    commit_hash = sys.argv[3]
else:
    commit_hash = ''

print "prepare-commit-msg: File: %s\nType: %s\nHash: %s" % (commit_msg_filepath, commit_type, commit_hash)

# Figure out which branch we're on
branch = check_output(['git', 'symbolic-ref', '--short', 'HEAD']).strip()
print "prepare-commit-msg: On branch '%s'" % branch

# Populate the commit message with the feature #, if there is one
if branch.startswith('feature/'):
    print "prepare-commit-msg: Oh hey, it's an feature branch."
    result = re.match('feature/(.*)', branch)
    issue_number = result.group(1)

    with open(commit_msg_filepath, 'r+') as f:
        content = f.read()
        f.seek(0, 0)
        f.write("%s %s" % (issue_number, content))
```

# Commit message hook

```python
#!/usr/bin/env python

import sys, os, re
from subprocess import check_output

# Collect the parameters
commit_msg_filepath = sys.argv[1]

# Figure out which branch we're on
branch = check_output(['git', 'symbolic-ref', '--short', 'HEAD']).strip()
print "commit-msg: On branch '%s'" % branch

# Check the commit message if we're on an issue branch
if branch.startswith('issue-'):
    print "commit-msg: Oh hey, it's an issue branch."
    result = re.match('issue-(.*)', branch)
    issue_number = result.group(1)
    required_message = "ISSUE-%s" % issue_number

    with open(commit_msg_filepath, 'r') as f:
        content = f.read()
        if not content.startswith(required_message):
            print "commit-msg: ERROR! The commit message must start with '%s'" % required_message
            sys.exit(1)
```

# Post commit hook

```python
#!/usr/bin/env python

import smtplib
from email.mime.text import MIMEText
from subprocess import check_output

# Get the git log --stat entry of the new commit
log = check_output(['git', 'log', '-1', '--stat', 'HEAD'])

# Create a plaintext email message
msg = MIMEText("Look, I'm actually doing some work:\n\n%s" % log)

msg['Subject'] = 'Git post-commit hook notification'
msg['From'] = 'mary@example.com'
msg['To'] = 'boss@example.com'

# Send the message
SMTP_SERVER = 'smtp.example.com'
SMTP_PORT = 587

session = smtplib.SMTP(SMTP_SERVER, SMTP_PORT)
session.ehlo()
session.starttls()
session.ehlo()
session.login(msg['From'], 'secretPassword')

session.sendmail(msg['From'], msg['To'], msg.as_string())
session.quit()
```


# Post checkout hook

```python
#!/usr/bin/env python

import sys, os, re
from subprocess import check_output

# Collect the parameters
previous_head = sys.argv[1]
new_head = sys.argv[2]
is_branch_checkout = sys.argv[3]

if is_branch_checkout == "0":
    print "post-checkout: This is a file checkout. Nothing to do."
    sys.exit(0)

print "post-checkout: Deleting all '.pyc' files in working directory"
for root, dirs, files in os.walk('.'):
    for filename in files:
        ext = os.path.splitext(filename)[1]
        if ext == '.pyc':
            os.unlink(os.path.join(root, filename))
```


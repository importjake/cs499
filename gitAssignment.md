# Git Assignment

**INDIVIDUAL ASSIGNMENT**

**Deadline**: September 18

**How to submit**: TBD

**Value**: Part of in-class/short assignments grade

## Description

### Understanding the repo

1.  Download [handson.zip](handson.zip) and unzip it. handson is a git repository. Using the commandline change the directory to "handson/"

2.  Draw a diagram of the commits and branches in repository.

    - Use `git branch` to list the branches in this repository.
    - Use `git checkout` to explore each branch.
    - Use `git log --decorate` to explore the structure of commits.

    ```
    $ git branch
    feature-foo
    * master

    $ git checkout feature-foo
    Switched to branch 'feature-foo'

    $ git log --decorate

    commit a70a8e9d3c5390e367028faf033f2a9ef03d2e91 (HEAD -> feature-foo)
    Author: Igor Steinmacher <igorsteinmacher@gmail.com>
    Date:   Fri Aug 24 15:29:22 2018 -0700

        Adding header of method foo()

    commit 309b0d73ff9c2163591c9e96e307fe61b4c8f58a
    Author: Igor Steinmacher <igorsteinmacher@gmail.com>
    Date:   Fri Aug 24 15:27:16 2018 -0700

        Adding class A skeleton

    commit 9c1eeb8901b0926ce7fa13cc6ce0a1876fc4179b
    Author: Igor Steinmacher <igorsteinmacher@gmail.com>
    Date:   Fri Aug 24 15:26:44 2018 -0700

        Creating all files (all empty)

    $ git checkout master
    Switched to branch 'master'
    $ git log --decorate

    commit f67f266cf420735187053f10d32e2c0f7cbc5a43 (HEAD -> master)
    Author: Igor Steinmacher <igorsteinmacher@gmail.com>
    Date:   Fri Aug 24 15:30:05 2018 -0700

        Adding class B skeleton

    commit 309b0d73ff9c2163591c9e96e307fe61b4c8f58a
    Author: Igor Steinmacher <igorsteinmacher@gmail.com>
    Date:   Fri Aug 24 15:27:16 2018 -0700

        Adding class A skeleton

    commit 9c1eeb8901b0926ce7fa13cc6ce0a1876fc4179b
    Author: Igor Steinmacher <igorsteinmacher@gmail.com>
    Date:   Fri Aug 24 15:26:44 2018 -0700

        Creating all files (all empty)
    ```

3.  Try `git log --graph --all` to see the commit tree

4.  Use `git diff BRANCH_NAME` to view the differences from a branch and the current branch.
    Summarize the difference from master to the other branch.

    ```
    diff --git a/A.java b/A.java
    index 674b8ce..3ea227e 100644
    --- a/A.java
    +++ b/A.java
    @@ -1,7 +1,4 @@
     public class A {
    -
    -   public void foo() {
    -
    -   }
    +

     }
    diff --git a/B.java b/B.java
    index e69de29..ae64e6b 100644
    --- a/B.java
    +++ b/B.java
    @@ -0,0 +1,4 @@
    +public class B {
    +
    +
    +}
    ```

5.  Write a command sequence to merge the non-master branch into `master`

    ```
    $ git merge feature-foo
    Merge made by the 'recursive' strategy.
     A.java | 5 ++++-
     1 file changed, 4 insertions(+), 1 deletion(-)
    ```

6.  Write a command (or sequence) to (i) create a new branch called `feature-bar` (from the `master`) and (ii) change to this branch

    ```
    $ git branch feature-bar

    $ git checkout feature-bar
    Switched to branch 'feature-bar'
    ```

7.  Edit B.java adding the following source code inside class B:

    ```
    public void bar(){

    }
    ```

8.  Write a command (or sequence) to commit your changes

    ```
    $ git status
    On branch feature-bar
    Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git checkout -- <file>..." to discard changes in working directory)

     modified:   B.java

    no changes added to commit (use "git add" and/or "git commit -a")

    $ git commit -a -m "add bar method to B.java"
    [feature-bar 61bffe1] add bar method to B.java
     1 file changed, 3 insertions(+)
    ```

9.  Change back to the `master` branch and change B.java adding the following source code (commit your change to `master`):

    ```
    public static void main(){
       System.out.println("Hi")
    }
    ```

10. Write a command sequence to merge the `feature-bar` branch into `master`

```
$ git merge feature-bar
```

11. What happened?

A merge conflict occurred because of the difference in B.java between the two branches

```
Auto-merging B.java
CONFLICT (content): Merge conflict in B.java
Automatic merge failed; fix conflicts and then commit the result.
```

12. Write a set of commands to abort the merge

```
$ git merge --abort
```

13. Now repeat item 10, but proceed with the manual merge (Editing B.java). All implemented methods are needed. Explain your procedure

```
# check the status of the repo
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   B.java

no changes added to commit (use "git add" and/or "git commit -a")

# opening B.java file to edit (with preferred editor neovim)
# to fix the conflicts in B.java

$ nvim B.java

# after fixing the file including both methods, we will add the
# file to the staging area
$ git add B.java

# then we commit the changes
$ git commit -m "resolve merge conflict"
[master d188284] resolve merge conflict
```

14. Write a command (or set of commands) to proceed with the merge and make `master` branch up-to-date

```
$ git merge feature-bar
Already up-to-date
```

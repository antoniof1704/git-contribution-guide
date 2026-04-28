## Want to Make Changes? <a name = 'want_to_make_changes'></a>

### Core Branches

Before making changes, it is important to understand the core branches in the repository and how each should be treated:

* `main` is the original branch and should never be edited directly. Only the `dev` branch should be merged into `main` periodically, to act as a backup of `dev`.
* `dev` is branched off from `main` and acts as the primary working branch that other changes are merged into. It should not be edited directly either.

### Making Changes

If you want to make changes or contribute to the project, please ensure you create a new branch from the `dev` branch (which should contain the most up-to-date code) to make your edits and test their functionality.

This can be done using the following commands in your R terminal. Please run each line one at a time:

```
git branch

git checkout dev

git pull origin dev

git checkout -b <your new branch name>

```

This should create a new local branch with the same code as the `dev` branch (at the point of branching)

If you want to push changes made in your test branch to the repository, please run the following line in your R terminal:

```
git add -a

git commit -m "DESCITPION OF CHANGES"

git push -u origin <your new branch name>

```

Once you are happy with the changes and your test branch has been pushed to the remote repository, you will need to create a merge request by selecting ‘New merge request’ in GitLab.

Ensure that the source branch is set to your test branch and the target branch is set to the dev branch. Assign a reviewer (the person who will be QA‑ing your work), and make sure to select ‘Delete source branch’ so that your test branch is removed after the merge.

If you are unsure how to deal with conflicts or other changes within the merge request, contact a team member who will be able to advise.

Both you and the person QA‑ing the work must complete an entry in the [QA Log template](QA_Log_Template.xlsx), specifically in the ‘Merge Request Log’. Instructions are provided on what information needs to be recorded: the **white** columns are completed by you, and the **yellow** columns by the QA reviewer. If any supporting assumptions or decisions have been made as part of this merge request, these should also be recorded in the ‘Assumptions & Decisions Log’ tab.

Once your code has been independently QA‑ed and all issues have been resolved, select ‘Merge’ and your changes will be merged into the dev branch.


### Rebasing 

Sometimes you will have instances where new updates or changes have been made to the `dev` branch. To prevent your branch from becoming out of date, you will want to rebase it with the most recent commits from `dev`.

Rebasing can be time-consuming if your code has diverged significantly from `dev`. For this reason, it's recommended to rebase your branch whenever a new merge occurs on `dev`. This will allow you to incorporate new changes from `dev` into your branch while preserving your own modifications.

To start the rebase, run the following lines of code in your R terminal. Please run each line one at a time:

```
git branch

git checkout <your new branch name>

git fetch origin

git rebase origin/dev

```

There will lilely be conflicts when you attempt to rebase. When a conflict occurs, your R terminal will look like this:

```
Auto-merging ..........
Auto-merging ..........
CONFLICT (content): Merge conflict in ..........
CONFLICT (modify/delete): .......... deleted in HEAD and modified in .......... (Rebase 1).  Version .......... (Rebase 1) of .......... left in tree.
error: could not apply ............. Rebase 1
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply ............. Rebase 1

```

To resolve the conflicts, you will need to open the scipts in your coding environment that are listed in the terminal and find the conflict within them. In the above example, I have two conflicts denoted by 'CONFLICT'. If I then open the .......... script, I will find the conflicting code, which will be highlighted in the following style:

```
<<<<<<< HEAD
df2V1 <- function(df1v1)

=======
df2V2 <- function(df1v2)
print(df2V2)

>>>>>>> .......... (Rebase 1)
```

You will need to decide which version to keep. If you are unsure which part to keep, contact another team member. 

To do this, remove the unwanted code plus the additional formatting lines with < or =. Again, using the example above, if I wanted to keep the first version of code (underneath the HEAD), I would need to remove all of the other code around it. See below:


```
df2V1 <- function(df1v1)

```

Once all of the scripts with conflicts have been resolved, use the following command to continue with the rebase: 

```
git add .

git rebase --continue
```

After this, your terminal will enter into an interactive shell. To exit this please just type:

```
:q

# and press enter
```

There may be other commits to rebase with conflicts, so you will need to repeat the above process of rebasing until these are all resolved. 

Once all of the commits have been rebased, the following message will appear in your terminal: 

```
Successfully rebased and updated
```

Run the commands below, and you will have successfully rebased your branch and pushed the changes to the remopte repository.

``` 

git commit -m "Successful rebase of my branch"

git push -u origin <your new branch name>

```

If for whatever reason you need to stop the rebase, you can 
use the command below, and this will abandon the rebase, returning your branch to how it was before. 

``` 
git rebase --abort

```

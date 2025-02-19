## Want to Make Changes? <a name = 'want_to_make_changes'></a>

If you want to make changes or contribute to the project, please ensure you create a new branch from the 'main' branch (which should contain the most up-to-date code) to make your edits and test their functionality.

This can be done using the following commands in your R terminal. Please run each line one at a time:

```
git branch

git checkout dev

git pull origin main

git checkout -b <your new branch name>

```

This should create a new local branch with the same code as the main branch (at the point of branching)

If you want to push changes made in your test branch to the repository, please run the following line in your R terminal:

```
git add -a

git commit -m "DESCITPION OF CHANGES"

git push -u origin <your new branch name>

```

Once you are happy with the changes and your test branch has been pushed to the remote repository, please oragnise another team member to peer review your code. 

Once this has been done, get permission to merge your changes onto the main branch.

A merge request can be created by pressing 'New merge request' in the Gitlab.

Ensure that you set the 'source branch' as the name of your test branch and the 'target branch' as the 'main' branch. If you are unsure on how to deal with conflicts or any other changes in the merge request, reach out to a team member who will be able to advise you. Make sure to select 'Delete source branch' to delete your test branch after the merge.

Once everything is ready, press the 'Merge' button, and your changes will appear in the 'main' branch. 


### Rebasing 

Sometimes you will have instances where new updates or changes have been made to the 'main' branch. To prevent your branch from becoming out of date, you will want to rebase it with the most recent commits from 'main'.

Rebasing can be time-consuming if your code has diverged significantly from 'main'. For this reason, it's recommended to rebase your branch whenever a new merge occurs on 'main'. This will allow you to incorporate new changes from 'main' into your branch while preserving your own modifications.

To start the rebase, run the following lines of code in your R terminal. Please run each line one at a time:

```
git branch

git checkout <your new branch name>

git fetch origin

git rebase origin/main

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

To resolve the conflicts, you will need to open the scipts that are listed in the terminal and find the conflict within them. In the above example, I have two conflicts denoted by 'CONFLICT'. If I then open the .......... script, I will find the conflicting code, which will be highlighted in the following style:

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

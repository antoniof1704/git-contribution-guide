# [Insert Project Name]

## Project Description
Provide a high-level summary of the project.

### Purpose and Objectives
Describe the purpose of the project and what it aims to achieve.

### Scope and Key Deliverables
Define what is included and excluded from scope.

List key deliverables, for example:
- Analytical outputs
- Code deliverables
- Documentation

### Expected Timelines
Provide the overall project timeline or key milestones.


## Access & Technology Requirements
List any systems, tools, or permissions required to deliver the project.

| Role / Permission | Description |
|------------------|-------------|
|                  |             |
|                  |             |
|                  |             |


## Information & Data Sources
Details of where relevant files, data, and code are stored.

### Shared File Areas
List and link any shared file areas for the project.

### Data Sources

| Data Source Name | Description |
|------------------|-------------|
|                  |             |
|                  |             |


## Key Outputs
Define the primary deliverables produced by the project.

### Deliverables
- Reports
- Dashboards
- Code repositories
- Documentation


## Key People
List key contacts and contributors.

**Project Lead:**  
Name / role

**Stakeholders:**  
Name / role

**Analysts and Contributors:**  
Name / role


## How to Run Analysis
Provide detailed, step-by-step guidance on how to run the analysis.

Include:
- Script locations
- Naming conventions
- Runtime assumptions
- Dependencies between steps


## Caveats
Provide a brief overview of key assumptions, decisions, or limitations.

More detailed and formal records of assumptions, decisions, and limitations can be found in the **Assumptions, Decisions & Limitations (AD&L) Log**.


## Audit / QA

### Assumptions, Decisions & Limitations Log
- **[AD&L Log Template](AD&L%20Log%20Template.xlsx)**:  Use this log to record all assumptions, decisions, and limitations.

**Guidance:**
- Prior to starting the analysis, record any **starting / baseline assumptions** in the AD&L Log.
- Any new assumptions, decisions, or limitations identified during the analysis must also be recorded in the log.
- Where an assumption, decision, or limitation relates to a code change, the associated **GitLab merge request ID** must be recorded in the log (where prompted).


### Code QA via Merge Requests

Code is QA’d systematically whenever a new merge request is created.

- QA is documented directly in the merge request description using a **standardised template**
- Assumptions, decisions, and limitations relating to a merge request are recorded **only** in the AD&L Log (not in the merge request description)

To review QA on changes made to the codebase:
- Check merge request descriptions, which follow the standard template below:
  - **[QA Merge Request Template](.gitlab/merge_request_templates/QA.md)**

More detail on this process is provided in the next section.


## Want to Make Changes? <a name = 'want_to_make_changes'></a>

### Core Branches

Before making changes, it is important to understand the core branches in the repository and how each should be treated:

- `main` is the original branch and should never be edited directly. Only the `dev` branch should be merged into `main` periodically, to act as a backup of `dev`.
- `dev` is branched off from `main` and acts as the primary working branch that other changes are merged into. It should not be edited directly either.

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

Once your branch has been pushed to the remote repository, create a merge request by selecting **“New merge request”** in GitLab.
Ensure:

- The source branch is your test branch
- The target branch is dev (or whichever branch you are merging into)

On the next screen:

- Select “Choose a template”
- Choose [QA Merge Request Template](.gitlab/merge_request_templates/QA.md), the standardised merge request template referenced in the Audit / QA section
- Complete the sections under **“Analyst”**
- Assign a reviewer (the person who will be QA‑ing your work). The reviewer must complete the sections under **“QA reviewer”**.
- Ensure **“Delete source branch”** is selected so that your test branch is removed once merged.

*NOTE: The merge request description can be edited before the merge is completed, but not after the merge has occurred. All QA must therefore be completed prior to merging.*

Any assumptions, decisions, or limitations arising from the change must be recorded in the AD&L Log (linked in the QA template), including the merge request ID.

If you are unsure how to deal with conflicts or other issues within a merge request, contact a team member who will be able to advise.

Once the code has been independently QA‑ed and all issues resolved, select “Merge” to merge your changes into dev.


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

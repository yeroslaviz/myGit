Git with R
================
AY
12/2/2021

## Creating a HTTPS token

In order to be able to communicate with the git server, it is necessary
to create a so-called Token. this token varify the identity of the
person trying to connect to the server.

Using R libraries such as `usethis` and `gitcreds` make it possible to
do this from within R.

``` r
usethis::create_github_token()
```

will pop-up a new browser windows, where the user can create a new
token.

It is always good to give the token a specific name, which will help
identify, what it is for and why it was created.

After the token was created, **remember to copy it first before
continuing**. It is not possible to see the token again,s once the page
was reloaded.

``` r
gitcreds::gitcreds_set()
```

Without this token, one cannot communicate with the server,
i.e. commiting a `pull` or `push` requests.

The token created for this session is called “happygitwithr.com
tutorial” and is valid for the next 30 days (expires on Sat, Jan 1
2022).

After that I will need to generate an ew token.

When the PAT expires, return to <https://github.com/settings/tokens> and
click on its Note. (You do label your tokens nicely by use case, right?
Right?) At this point, you can optionally adjust scopes and then click
“Regenerate token”. You can optionally modify its Expiration and then
click “Regenerate token” (again). As before, **copy the PAT to the
clipboard**, call `gitcreds::gitcreds_set()`, and paste!

### helpful command for token

``` r
usethis::gh_token_help()

usethis::git_sitrep()
```

# Connect RsStudio to git and Github

Eventhough it is already connected, here aresome steps needed to be done
to achieve this.

## Make a repo on github

First one need to create a repo on the [github
site](https://github.com/). Initialize this repository with “Add a
README file”.

Copy a clone URL to your clipboard. If you’re taking our default advice,
copy the HTTPS URL. But if you’re opting for SSH, then make sure to copy
the SSH URL.

## Clone the repository to your computer via RStudio.

In RStudio, start a new Project:

-   *File* > *New Project* > *Version Control* > *Git*. In “Repository
    URL”, paste the URL of your new GitHub repository. It will be
    something like this.
-   I suggest you check “Open in new session”, as that’s what you’ll
    usually do in real life.
-   Click “Create Project”.

## Make local changes, save, commit

This is mainly just to check if it works, but really necessary, as we
will do many changes.

From RStudio, modify the README.md file, e.g., by adding the line “This
is a line from RStudio”. Save your changes.

Commit these changes to your local repo. How?

From RStudio:

-   Click the “Git” tab in upper right pane.
-   Check “Staged” box for README.md.
-   If you’re not already in the Git pop-up, click “Commit”.
-   Type a message in “Commit message”, such as “Commit from RStudio”.
-   Click “Commit”.

## Push your local changes online to GitHub

Click the green “Push” button to send your local changes to GitHub.

## Confirm the local change propagated to the GitHub remote

Go back to the browser. I assume we’re still viewing your new GitHub
repo.

Refresh.

done

## Clean up

remove the test repo and delete the local file.

## Solving possible problems

If you encounter any problems or even if you have found the appropriate
solution - go [here](https://happygitwithr.com/troubleshooting.html).

# New projects

There are several ways to connect a project with github.

-   It can be a completely new project, which we first create a
    repository on Github and than a running it in RStudio.
-   or it can be an existing project, which we first want to introduce
    it to a new gitHub repo.
-   on the other hand it can be an RStudio project first, which we want
    to add to a github repo (so-called “github last”).

## New project, GitHub first

This is the preferred method.

We create a new Project, with the preferred “GitHub first, then RStudio”
sequence. Why do we prefer this? Because this method of copying the
Project from GitHub to your computer also sets up the local Git
repository for immediate pulling and pushing. Under the hood, we are
doing `git clone`.

1.  Make a repo on GitHub
2.  New RStudio Project via git clone
    -   *File* > *New Project* > *Version Control* > *Git*.
    -   In the “repository URL” paste the URL of your new GitHub
        repository. It will be something like this
        <https://github.com/yeroslaviz/myGit.git>.
3.  make changes and commit them
4.  push to the repo
5.  If changes were make on the github repository online (on Github),
    one needs to `pull` the changes to the local folder.

## Existing project, GitHub first

This is mainly repeating the steps from before for creating the
repository on the github website and cloning it to a local folder. After
cloning the repo one can just copy-paste the files from the existing
projects into the newly created folder.

After the files are copied, one can marked then im the *staged* box and
`commit` -> `push`.

## Existing project, GitHub last

This an explicit workflow for connecting an existing local R project to
GitHub, when for some reason you cannot or don’t want to do a “GitHub
first” workflow.

When does this come up?

Example: it’s an existing project that is already a Git repo with a
history you care about. Then you have to do this properly.

Here we have several methods, depending on the fact if we’re using the
RStudio IDE and/or the `usethis` package. It is a straightforward
process which can be confusing, but if done in the correct order should
cause many problems.

1.  make sure you ahve a local project prepared with RStudio or create
    one using the `usethis::create_project()` command. 2. make and
    verify that you have a git repo with either the RStudio parameters
    or with the command `usethis::git_init()`.
2.  stage and commit
3.  connect the repo with Github. This can be done with either the
    command `usethis::use_github()` or bith the help of the git command,
    after creating a repo online and copying the path to the repo.

``` shell
git remote add origin https://github.com/jennybc/myrepo.git
git push --set-upstream origin main
```

5.  refresh the browser to see, if all went well.

If not, you can read a more detailed description
[here](https://happygitwithr.com/existing-github-last.html).
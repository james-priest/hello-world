# hello-world

My first repo on GitHub

The purpose of this repo is to:

1. Learn GitHub
1. Understand what's involved in creating and managing a repo
1. Connect VSCode, GitKraken, and GitHub Desktop to GitHub
1. Practice with both **GitHub Flow** and **Fork-and-Branch** workflows:
    1. Create second GitHub account (@jpriest-dev) for testing purposes
    1. **GitHub Flow** on a shared repo

        Uses two repos:
        * _Repository on GitHub_ (remote)
        * _Cloned repository_ (local)
    1. **Fork-and-Branch Workflow** (also know as **Fork-and-Pull Request Workflow**)

        Uses three repos:
        * _Original repository_ (remote) - An open source repo on GitHub
        * _Forked repository_ (remote) - my copy of the open source repo on Github
        * _Cloned (local) repository_ (from Forked) - my local copy of my forked repo

## Steps to complete **Fork-and-Branch**

1. Fork a repo
1. Clone to desktop from forked repo

    ```bash
    # Use favorite desktop client or do from command line
    git clone https://github.com/james-priest/hello-world.git
    ```

1. Add **upstream** remote pointing back to the **original** repo

    ```bash
    # By convention this remote is named "upstream"
    git remote add upstream https://github.com/james-priest/hello-world.git
    ```

1. Sync cloned fork with upstream repo

    ```bash
    # fetch from upstream remote
    git fetch upstream

    # view all branches including local ones that represent remote ones (BTW, they are all local branches!)
    git branch -va

    # checkout master
    git checkout master

    # merge upstream (again, this is merging two local branches)
    git merge upstream/master
    ```

1. Create development branch

    ```bash
    # new branch should be based off of master
    git checkout master

    # make it a simple, descriptive name & switch to it
    git branch newfeature
    git checkout newfeatue

    # ALTERNATE OPTION
    # combine previous two lines into one command if desired
    git checkout -b "newfeature"
    ```

1. Develop, test, and commit changes to development branch

    ```bash
    # commit 1
    git commit -m "Add xyz"

    # commit 2
    git commit -m "Update xyz"

    # commit 3
    git commit -m "Expand xyz functionality"
    ```

1. CLEAN-UP BRANCH BEFORE PULL REQUEST:

    If any commits have been made to the upstream master branch, you should rebase your development branch so that merging it will be a simple fast-forward that won't require any conflict resolution work.
    1. Fetch upstream master & merge

        ```bash
        # Fetch upstream master and merge with your repo's master branch
        git fetch upstream
        git checkout master
        git merge upstream/master
        ```

    1. Rebase development branch onto master

        ```bash
        # If there were any new commits, rebase your development branch
        git checkout newfeature
        git rebase master
        ```

    1. Now, it may be desirable to squash some of your smaller commits down into a small number of larger more cohesive commits. You can do this with an interactive rebase:

        ```bash
        # Rebase all commits on your development branch
        git checkout
        git rebase -i master
        ```

1. Push changes to GitHub

    ```bash
    # Pushes development branch to GitHub
    git push origin newfeature
    ```

1. Initiate a Pull Request from development branch
    1. Go to forked repo on GitHub
    1. Select development branch
    1. Click the Pull Request button
1. CLEAN-UP REPOS AFTER INTEGRATION:

    Once maintainer accepts and merges changes into original repositry
    1. Update local clone (git pull upstream master) - This brings down the updated master branch that includes your new developoment changes and merges it with local master

        ```bash
        # Checkout master
        git checkout master

        # Fetch upstream master and merge with local repo's master branch
        git fetch upstream
        git merge upstream/master

        # ALTERNATE OPTION
        # Update local clone (pull does a fetch & merge)
        git pull upstream master
        ```
    1. We can now delete the development branch since changes are already in master branch

        ```bash
        # delete local branch
        git branch -d <branch name>
        ```

    1. Then we can update the master branch in the forked repository

        ```bash
        # push to my fork
        git push origin master
        ```

    1. Lastly, we push the deletion of the development branch to forked repository

        ```bash
        # delete development branch from my fork
        git push --delete origin <branch name>
        ```

## Conclusion

*Finally*, I'm using git like a **PRO**!
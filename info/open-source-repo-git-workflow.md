# Open Source Repo Git Workflow

I have usually contributed only to projects that use git version control system. My Git workflow for contributions has been pretty standard these days so I wanted to capture it down here. This workflow assumes that any and every change to a project goes though Pull Request / Merge Request, with or without review. Most probably with a review, or else there's no point in doing Pull Requests / Merge Requests, but yeah, many projects simply do it too, even if there are no reviews. For example maintainers raise PRs and merge it themselves. Not sure what's the goal there 🤷 I would rather directly push to the default branch without PR. But yeah, follow the "norm" or "processes" to avoid "foul behavior" or any "blaming" of sorts or any other issues that comes with "breaking" / "bypassing" processes!

Now, to the Git Workflow. I usually find projects on GitHub and GitLab. So the steps are -

- Go to the project repository page
- Find a way to clone the repository into my account namespace using the platform features. For example, if the repository is https://github.com/helm/helm , then clone to https://github.com/karuppiah7890/helm . When done through the platform it would just be a `fork`. But if platform doesn't support, I would have to do a lot more. See below [Fork not supported situation](#fork-not-supported) for that

- Once forked, if the fork repository is not there in my local, clone it in my local, assuming development happens locally and not in a cloud environment

```bash
$ git clone git@github.com:karuppiah7890/helm
```

- Add the upstream repository as a remote for pulling in latest changes from upstream / the main repository / main copy of the project

```bash
$ cd helm
$ git remote add upstream git@github.com:karuppiah7890/helm
$ git remote set-url upstream --push no_push
```

- Create a branch from the main / default branch or whatever branch you need for development and on top of which you want to put your code and raise a PR against it

```bash
$ git checkout -b <branch-name>
```

For branch name I usually use `fix-<issue>` or `fix-<issue-number>` or `<feature-name>` and similar

- Make changes to the code. Usually the commands I use at this stage are -

```bash
$ git status
$ git diff
```

- From time and time stage the code to git staging area and commit it -

```bash
$ git add -p
$ git diff --staged
$ git commit -m ""
```

I also use commit amend command

```bash
$ git commit --amend
$ git commit --amend -m ""
$ git commit --amend --no-edit
```

To sign off the commit with `Signed-off-by: ...`

```bash
$ git commit --signoff
```

- Finally check if the list of commits are okay or do a rebase and squash / edit / reword commits or do whatever is needed

```bash
$ git rebase -i head~<a-number-based-on-the-number-of-commits-i-made>
```

I could use a smaller number too if I have to deal with only a fewer number of commits I made recently instead of all the commits I made in the new branch

- Finally push the branch to the fork repository and also track it by setting it as upstream branch

```bash
$ git push -u origin <branch-name>
```

- Finally to raise PR, use the link provided in the `git push` message that the source code hosting website shows. Or else use the Web UI of the source code hosting website ad create PR / MR by following the UI. Create the PR / MR with the source branch as your branch and target branch as whatever branch you want the code to go into, basically the branch on top of which you created the new branch, ideally

- Later if there are changes in the branch, add code and commit using above commands, mainly

```bash
$ git add -p
$ git commit [--amend] [-m "..."]
$ git push
```

- Later if there are breaking changes in the branch, where history of commits are rewritten in such a way that commit SHA itself has changed for one or more commits in the branch, then force push

```bash
$ git push -f
```

History usually gets rewritten when using `git rebase -i head~<number-of-commits-to-choose-for-rewriting-history>`

- Also the branch on top of which you base your new branch could keep moving / getting updated in case new code gets pushed / merged into the branch. And sometimes the PR / MR shows that there are conflicts in merging the PR / MR. Or in some cases, you miss out on the latest code in the main repo branch and also while the merge happens, the merge cannot do fast forward and merge when the branch on top of which you coded has moved off. So, it's best to rebase with the branch on top of which you coded like this

```bash
# first sync the branch that you built on top of. For example main
$ git checkout main
$ git pull --rebase --autostash --verbose upstream main
# or just git pull --rebase --autostash --verbose if main is trakced with upstream/main
# push the new changes to fork
$ git push origin main
# or just git push in case main is already tracked with origin/main
$ git push
# finally, just go to your branch and rebase
$ git checkout <my-branch>
$ git rebase main
```

The branch on top of which you build can be anything and not just `main`. Also, while rebasing, there maybe conflicts. Resolve them using the IDE / text editor by looking at the code that you changed and what code the other branch has changed and ensure only your changes are there / only your branch related changes are there and don't modify anything that others have done, also ensure to keep your changes updated based on whatever changes that are coming from the other branch, say `main`. Usually when conflicts are resolved, you will use -

```bash
$ git add <file>
$ git rebase --continue
```

And keep doing it until all your commits in the branch are rebased on top of the new branch one commit at a time. Finally you would notice that the commit history has been changed due to this and hence the commit SHAs have changed, so check the commits in the branch, ensure all commits are good and then force push

```bash
$ git push -f
```

- Finally when the PR is merged, congratulations!! :D Now you can find the PR code in the other branch that you targeted the PR for, for example `main`. With `main` as example, you can do this to get the latest changes

```bash
$ git checkout main
$ git pull --rebase --autostash --verbose upstream main
$ # and also sync your fork repo main with the latest main
$ git push origin main
$ # or just git push if main is tracked with origin/main
```

- You can also cleanup the branch you created - delete locally and also from the source code hosting site. Usually you can find an option in the PR itself to delete the branch from source code hosting site. If that's done then -

```bash
# assuming main is the other branch where code was targeted in PR
$ git checkout main
# this should remove the tracking of the pr branch as it's deleted from source code hosting site
$ git remote prune origin <pr-branch-name>
$ # to delete the branch locally
$ git branch -D <pr-branch-name>
```

In case the branch wasn't deleted from the source code hosting site's feature, then using git you can do -

```bash
$ git checkout main
$ git push origin :<pr-branch-name>
```

The `:` is to mention that we want to delete the PR branch we created. For deleting locally and to get rid of tracking too, use the previous commands!

## Fork not supported

When source code hosting platform does NOT support the concept of `fork` which is a way to clone git repositories within the platform without using local git or anything, then you can do the following using local git

```bash
$ git clone git@github.com:helm/helm
$ cd helm
$ git remote -v
$ git remote rename origin upstream
# To not be able to push to main copy of the project even if I have push (write) access to repo
$ git remote set-url upstream --push no_push
```

Now create a project called `helm` in your namespace

```
$ git remote add origin git@github.com:karuppiah7890/helm
# for example $ git push origin main
$ git push origin <default-branch>
# or push all branches and references (tags) using $ git push --all
```

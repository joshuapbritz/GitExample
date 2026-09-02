# Git Rebase

Git rebase is a process used to updated divergent git branches by replaying commits on top of new changes to keep divergent branches in sync. Consider a case where you have a main branch and a feature branch. 

<img src="/static/forked_branches.png" alt="Example of forked commit history" />

In this case, we have a main branch and a branch where we are working on a new feature. As you can see, the main branch is ahead of the feature branch by 2 commits, while the feature branch contains 3 commits the main branch does not have. Because we consider the main branch to be the source of truth, we want to make sure that our feature branches are up to date with the main branch to ensure that our code is based on the latest version of main. With rebase, we would update our branch by fetching the latest changes from our repository, pulling them into our branch and then resolving conflicts. The process would look like this, assuming you are currently on the feature branch.

```bash
git fetch origin # get the latest changes from the remote repository

git rebase origin/main # replay your commits on top of the latest changes from main

git push --force-with-lease # push your changes to the remote repository, overwriting the old history
```

When we talking about rebasing, we talk a lot about replaying our commits. What this means is that when we rebase, we move our commits to the latest point in the history of the branch we are rebasing from (for example, the latest point in main) and we then create new commits on top of those changes as if we were starting the branch from scratch. This is really useful because our branch is always fresh and will only ever include the commits you made. It is as if no changes have been made in main since you started. This would look like this.

<img src="/static/rebase_branch.png" alt="Example of branch rebase" />

As you can see, the commits made in the feature branch are moved to branch from the latest commit in main. It is important to note that doing so does edit the commits you have made. For example, these replayed commits would have a new commit time. If the rebase was done by someone other than the original commit author, the commits would also be considered to be co-authored commits. This is fine for feature branches because we the focus of feature branches should be to allow a feature to be developed until ready. This process keeps things nice and clean. Like with merge, this also works the other direction. When we are ready to bring the feature branch changes into main, we can rebase them onto the main branch which means we move them to the top of the main branch commit history as if they had been committed to the main branch. This means that the history of our main branch will always show the order in which commits were added to it. When merged like this, our main branch would look like this.

<img src="/static/rebase_to_main.png" alt="Example of branch rebase into main" />

The neat thing here is that it is really easy to see what commits changed what feature. It is then really easy to move changes from one branch to another, while leaving out specific commits you don't want.

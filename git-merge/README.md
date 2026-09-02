# Git Merge

Git merge is a process used to updated divergent git branches by creating checkpoints in you commit history that keep changes in sync. Consider a case where you have a main branch and a feature branch. 

<img src="/static/forked_branches.png" alt="Example of forked commit history" />

In this case, we have a main branch and a branch where we are working on a new feature. As you can see, the main branch is ahead of the feature branch by 2 commits, while the feature branch contains 3 commits the main branch does not have. Because we consider the main branch to be the source of truth, we want to make sure that our feature branches are up to date with the main branch to ensure that our code is based on the latest version of main. We would normally do something like a `git pull origin main` in our feature branch to update our branch. When we do this, it creates a merge commit. A merge commit is a special checkpoint in our branch where we essentially reconcile the changes that were made in our feature branch to the main branch. A merge commit would look like this.

<img src="/static/merge_commit.png" alt="Merge commit from main" />

We now have a new commit in our feature branch that stems from the main branch. This represents our merge, but both branches remain as they were before the merge took place. We are not bringing commits into our branch, but are rather updating our branch the latest changes in another and can then continue working. The same happens in the other direction. When we are done with our feature branch and we want to bring our changes into our main branch, we create another merge commit into main.

<img src="/static/merge_back_to_main.png" alt="Merge commit to main" />

Once again, we are not bringing new commits into main. Rather, we are bringing changes into main and are then telling git "yo! those changes are from this branch with these commits". This is really powerful if you have a setup where people are all working on the same branch at the same time or if it is critical for you to keep track of when every commit was made on your codebase. The downside is that commits now become very intertwined and cherry picking is much harder to achieve. Even worse, in a large repo, you git history starts to look something like this.

<img src="/static/git_graph.png" alt="Git history graph" />

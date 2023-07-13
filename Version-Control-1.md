# Git Repository Recovery - Fatal: reference is not a tree: 

This repository encountered an issue where some commits were lost and inaccessible through the local Git client. Anyway, I managed to resolve the issue and recover those lost commits with the following steps:

## Background

I ran into a little issue with this repository where I couldn't access certain commits using the [commit-hash]. It was odd because I could see those commits just fine on GitHub, but when I tried to reference them in my local repository using VS Code, I got this annoying error message: fatal: reference is not a tree.

## Solution Steps

1. Checked the remote repository: Verified that the lost commits were still visible on the remote repository on GitHub.
2. Ensure you have a backup before attempting any further actions. This will help ensure that your work is protected in case any unexpected changes occur.
3. Clone the repository into a new directory on your local machine. 
`git clone [repository-url]`
4. cd into the new directory.
5. Checked out the commit in detached HEAD state: 
`git checkout [commit-hash]` to directly check out the commit [commit-hash] in a detached HEAD state.
6. Created a new branch: Created a new branch `debug1` from the detached HEAD state to preserve the changes made in the commit.
7. Switched to the new branch: Switched to the `debug1` branch to continue working with the recovered commit.
<br/><br/>

The next two steps were necessary for me because I had some commits that were ahead, but I didn't want them in the final version of the repository.
1. Ensured consistency across branches: Reset the `main` branch to the same commit as the `debug1` branch to discard any new commits made after the desired commit.
`git switch main`, then `git reset --hard debug1`
2. Force pushed the changes: Force pushed the updated branches to the remote repository to synchronize the changes.
`git push --force origin main`

## Conclusion

By following the steps outlined above, the lost commits were successfully recovered and the repository was brought back to a consistent state. The `debug1` branch contains the desired commit, and the `main` branch has been aligned with it.

It is important to note that force pushing was required to update the branches, which can be a potentially destructive action. Always ensure you have proper backups and communicate with your team before performing force push operations.


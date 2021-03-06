# Git

## Git Commands

- `git --version`
- `git init`
- `git status`
- `git add "file name"`
- `git commit`
- `git config --global user.email "me@gmail.com"`
- `git config --global user.name "First name Last name"`
- `git log`
- `git add .`
- `git commit -m "Messages"`
- `git log --oneline`

## Merging Two Git Repositories Into One Repository Without Losing File History

```
The basic idea is that we follow these steps:

Create a new empty repository New.
Make an initial commit because we need one before we do a merge.
Add a remote to old repository OldA.
Merge OldA/master to New/master.
Make a subdirectory OldA.
Move all files into subdirectory OldA.
Commit all of the file moves.
Repeat 3-6 for OldB.
A Powershell script for these steps might look like this:

# Assume the current directory is where we want the new repository to be created
A Powershell script for these steps might look like this:

# Assume the current directory is where we want the new repository to be created
# Create the new repository
git init

# Before we do a merge, we have to have an initial commit, so we’ll make a dummy commit
dir > deleteme.txt
git add .
git commit -m “Initial dummy commit”

# Add a remote for and fetch the old repo
git remote add -f old_a \<OldA repo URL>

# Merge the files from old_a/master into new/master
git merge old_a/master

# Clean up our dummy file because we don’t need it any more
git rm .\deleteme.txt
git commit -m “Clean up initial file”

# Move the old_a repo files and folders into a subdirectory so they don’t collide with the other repo coming later
mkdir old_a
dir –exclude old_a | %{git mv $_.Name old_a}

# Commit the move
git commit -m “Move old_a files into subdir”

# Do the same thing for old_b
git remote add -f old_b \<OldB repo URL>
  
git merge old_b/main

git merge old_b/main --allow-unrelated-histories

mkdir old_b

dir –exclude old_a,old_b | %{git mv $_.Name old_b}

git commit -m “Move old_b files into subdir”

Very simple.  Now we have all the files from OldA and OldB in repository New, sitting in separate subdirectories, and we have both the commit history and the individual file history for all files.  (Since we did a rename, you have to do “git log –follow <file>” to see that history, but that’s true for any file rename operation, not just for our repo-merge.)

Obviously you could instead merge old_b into old_a (which becomes the new combined repo) if you’d rather do that – modify the script to suit.

If we have in-progress feature branches in the old repositories that also need to come over to the new repository, that’s also quite easy:

# Bring over a feature branch from one of the old repos
git checkout -b feature-in-progress
git merge -s recursive -Xsubtree=old_a old_a/feature-in-progress

This is the only non-obvious part of the whole operation.  We’re doing a normal recursive merge here (the “-s recursive” part isn’t strictly necessary because that’s the default) but we’re passing an argument to the recursive merge that tells Git that we’ve renamed the target and that helps Git line them up correctly.  This is not the same thing as the thing called a “subtree merge“.

So, if you’re simply trying to merge two repositories together into one repository and make it look like it was that way all along, don’t mess with submodules or subtree merges.  Just do a few regular, normal merges and you’ll have what you want.
```

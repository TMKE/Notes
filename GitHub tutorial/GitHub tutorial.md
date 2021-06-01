# GitHub tutorial

## What's GitHub?

GitHub is a ***code hosting platform*** for ***version control*** (buildt on Git) and ***collaboration***. It lets you and others work together on projects from anywhere.

Version control is a system (VCS) that records changes to a file or set of files over time that you can recall specific versions later.
[https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)

CLI

## Repositories

A repository is usually used to organize a single project. Repositories can contain folders and files, images, videos, spreadsheets, and data sets - anything your project needs.

Remember to include a README file

license file

## Branches

Branching is the way to work on different versions of a repository at one time.

By default, your repository has one branch named `main` which is considered to be the definitive branch.

We use branches to experiment and make edits before committing (merging) them to `main`

When you create a branch off the `main` branch, you are making a copy, or snapshot, of `main` as it was at that point in time. If someone else made changes to `main` branch while you were working on your branch, you could pull in those updates.

## Making and committing changes

Saved changes are called ***commits***. Each commit has an associated commit message, which is a description explaining why a particular change was made. Commit messages capture the history of your changes, so other contributors can understand what you've done and why.

## Pull requests

Pull requests are the heart of collaboration on GitHub. When you open a pull request, you're proposing your changes and requesting that someone review and pull in your contribution and merge them into their branch.

Pull requests show differences of the content from both branches. The changes, additions, and subtractions are shown in green and red.

As soon as you make a commit, you can open a pull request and start a discussion, even before the code is finished.

With @mention system, you can ask for feedback from specific people or teams

You can open pull requests in your own repository and merge them yourself

commits → branches
pull requests → main

## Merging pull requests

The final step is to bring changes together — merging a branch into the `main` branch.

Delete branches after you merge pull requests

## Forking projects

fork → clone (with GitHub Desktop or Git) → make a pull request (provide a rational argument for why you're making it in the first place)

# Github flow

GitHub is a branch based workflow that supports teams and projects where deployments are made regularly.

### Create a branch

When you are working on a project, you're going to have a bunch of different features or ideas in progress at any given time — some of which are ready to go, and others which are not. Branching existes to help you manage this workflow.

A branch is an environment where you can try out new ideas. Changes made on a branch don't affect the `main` branch. The branch won't be merged until it's ready to be reviewed by someone you're collaborating with.

Branching is a core concept in Git, and the entire GitHub flow is based upon it. There is only one rule: anything in the `main` branch is always deployable.
Thus, it's extremely important that a new branch is created off of main when working on a feature or a fix. The branch name should be descriptive (e.g. `refactor-authentication`, `user-content-cache-key`, `make-retina-avatar`) so others can see what's beign worked on.

### Add commits

Whenever you add, edit, or delete a file, you're making a commit, and adding them to your branch. This process of adding commits keeps track of your progress as you work on a feature branch.

Commits also create a transparent history of your work that others can follow to understand what you've done and why. Each commit has an associated commit message (a description) explaining why a particular change was made.

Furthermore, each commit is considered a separate unit of change. This lets you roll back if a bug is found, or if you decide to head in different direction.

Commit messages are important, especially since Git tracks your changes and then display them as commits once they're pushed to the server. By writing clear commit messages, you can make it easier for other people to follow along and provide feedback.

### Open a Pull Request

Pull Requests initiate discussion about your commits. Because they're tightly integrated with the underlying Git repository, anyone can see exactly what changes would be merged if they accept your request.

You can open a Pull Request at any point during the development process:

- when you have little or no code but want to share some screenshots or general ideas
- when you're stuck and need help or advice
- when you're ready for someone to review your work

By using GitHub's @mention system in your Pull Request message, you can ask for feedback from specific people or teams, whether they're down the hall or ten time zones away.

If you're using a Fork & Pull Model, Pull Requests provide a way to notify project maintainers about the changes you'd like them to consider. If you're using a Shared Repository Model, Pull Requests help start code review and conversation about proposed changes before they're merged into the main branch.

### Discuss and review your code

Once a Pull request has been opened, the person or team reviewing your changes may have questions or comments. Perhaps the coding style doesn't match project guidelines, the change is missing unit tests, or maybe everything looks great and props are in order. Pull requests are designed to encourage and capture this type of conversation.

You can also continue to push to your branch in light of discussion and feedback about your commits. If someone comments that you forgot to do something or if there is a bug in the code, you can fix it in your branch and push up the change. GitHub will show your new commits and any additional feedback you may receive in the unified Pull Request view.

Pull requests comments are written in Markdown, so you can embed images and emoji, use pre-formatted text blocks, and other lightweight formatting.

### Deploy

Once your pull request has been reviewed and the branch passes your test, you can deploy your changes to verify them in production. If your branch causes issues, you can roll it back by deploying the existing main branch into production.

Different teams may have different deployment strategies. For some, it may be best to deploy to a specially provisioned testing environment. For others, deploying directly to production may be the better choice based on the other elements in their workflow.

### Merge

Now that your changes have been verified in production, it is time to merge your code into the main branch.

Once merged, Pull Requests preserve a record of the historical changes to your code. Because they're searchable, they let anyone go back in time to understand why and how a decision was made.

By incorporating certain keywords into the text of your Pull Request, you can associate issues with code. When your Pull Request is merged, the related issues are also closed. For example, entering the phrase `Closes #32` would close issue number 32 in the repository.

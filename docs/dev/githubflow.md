# Github Flow workflow

GitHub Flow is a lightweight, branching workflow that supports teams and projects where deployments are made regularly. It is centered around a feature and small confined changes.

Some key features of github flow are:

- Master is production ready
- Master is deployed to production
- Development happens on feature branches
- Fast deployment speed
- Requires a verification for each release

## How it works

### Create a branch

![create a branch][createbranch]

When you're working on a project, you're going to have a bunch of different features or ideas in progress at any given time – some of which are ready to go, and others which are not. Branching exists to help you manage this workflow.

When you create a branch in your project, you're creating an environment where you can try out new ideas. Changes you make on a branch don't affect the master branch, so you're free to experiment and commit changes, safe in the knowledge that your branch won't be merged until it's ready to be reviewed by someone you're collaborating with.

```bash
git checkout -b your-awesome-feature
git push --set-upstream origin your-awesome-feature
```

> ProTip
> 
> Branching is a core concept in Git, and the entire GitHub flow is based upon it. There's only one rule: anything in the master branch is always deployable.
> 
> Because of this, it's extremely important that your new branch is created off of master when working on a feature or a fix. Your branch name should be descriptive (e.g., refactor-authentication, user-content-cache-key, make-retina-avatars), so that others can see what is being worked on.
> 

### Add commits

![add commits][commits]

Once your branch has been created, it's time to start making changes. Whenever you add, edit, or delete a file, you're making a commit, and adding them to your branch. This process of adding commits keeps track of your progress as you work on a feature branch.

Make sure you are on the correct branch by listing it and if necessary switching to it:

```bash
git branch
git checkout your-awesome-feature
```

Commits also create a transparent history of your work that others can follow to understand what you've done and why. Each commit has an associated commit message, which is a description explaining why a particular change was made. Furthermore, each commit is considered a separate unit of change. This lets you roll back changes if a bug is found, or if you decide to head in a different direction.


```bash
git add your-awesome-file
git commit
git push
```

> ProTip
> 
> Commit messages are important, especially since Git tracks your changes and then displays them as commits once they're pushed to the server. By writing clear commit messages, you can make it easier for other people to follow along and provide feedback.

{! github/pr.md !}

source: [github guides][github guides]

[createbranch]: createbranch.png
[commits]: commits.png
[deploy]: deploy.png
[github guides]: https://guides.github.com/introduction/flow/
[commit messages]: ../git/commit-message.md

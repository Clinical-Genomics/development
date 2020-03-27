# Branching workflows

Chosing a branching workflow answers the question: how are we branching and merging our features?

Does the workflow 

- scale with team size,
- influence deployment speed,
- provide an easy way to undo mistakes,
- impose unnecessary cognative overhead for its users?

As a team, does the workflow 

- enable me to collaborate unintrusively with my coworkers,
- provide for an easy merge strategy,
- enforce basic coding standards?

Based on the answers of these questions, we are recommending two kinds of branching workflows.

To understand this documentation, knowledge of git and branching is recommended! Why don't you read up on our [git][git] page?

## Shared repository model

Before we dive into how we are using branching workflows, a brief introduction on collaborative development models. An answer to the question: how are we cloning a repository?

There are two main types of collaborative development models. In the _fork and pull model_, anyone can fork an existing repository and push changes to their personal fork without needing access to the source repository. The changes can be pulled into the source repository by the project maintainer. 

In the _shared repository model_, collaborators are granted push access to a single shared repository and feature branches are created when changes need to be made. Pull requests are useful in this model as they initiate code review and general discussion about a set of changes before the changes are merged into the main branch of development.

*We are using the shared repository model.*

## Rolling release (github flow)

![github flow image][githubflow-image]

Some key features of github flow are:

- Master is production ready
- Master is deployed to production
- Development happens on feature branches
- Fast deployment speed
- Requires a verification for each release

When would you use github flow?

- The workflow is great for Continious Integration/Continious Deployment
- Little procedural overhead

Do you want to [know more][githubflow]?

## Distinct release (git flow)

![gitflow-image][gitflow-image]

Some key features of git flow:

- Master is production ready
- Master is deployed to production
- Development happens in a development branch, which in turn has feature branches
- Deploy when the development of a release is finished and validated
- Requires a validation for each release

When would you use git flow?

- The workflow is great for a release-based software development
- The development branch forms a safety barrier between development and production

Do you want to [know more][gitflow]?

[git]: ../../git/
[gitflow]: gitflow.md
[githubflow]: githubflow.md
[githubflow-image]: createbranch.png
[gitflow-image]: 05.svg

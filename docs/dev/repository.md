# Repository Guidelines @clinical-Genomics

This is a list containing all items that need to be set up so that repositories are compatible with AM `1042 Verifications and Validations`.

1. **Add code owners**:
The repository should have at least two code owner in `.github/CODEOWNERS` document according to AM doc #1098. Read up on [codeowners](https://help.github.com/en/articles/about-code-owners)

1. **Choose a branching model**:
The repository should state the branching model used for the repository in the `CONTRIBUTING` doc. Read up on our [branching models](models.md)

1. **Versioning**:
The repository should state the versioning scheme followed e.g. [semantic versioning](https://semver.org/) in the `CONTRIBUTING` doc. For example, bump version on each change on master, e.g. use the [bumpversion package](https://github.com/peritus/bumpversion) to automate bumping and tagging. This should follow the choosen branching model.

1. **Add a pull request template**: 
The repository should have a pull request template in `.github/PULL_REQUEST_TEMPLATE`, e.g [servers](https://github.com/Clinical-Genomics/servers/blob/master/.github/PULL_REQUEST_TEMPLATE), that includes:
    - Description of feature/fix
    - How to test and expected outcome
    - Code review approval
    - This is a major|minor|path version because ...
    - Signoff tickboxes for code review, test status, and 
    - If merging to a branch that will be deployed in production sign off on the merge and deploy, see [approving PRs](../publish/approving-prs.md). 

1. **Labels**: The repository should have these labels:

| Name | Colour | Colour (hex) |
| --- | --- | --- |
| Effort S |  Green | 4dc13c |
| Effort M | Orange | ed851e |
| Effort L | Red | a82330 |
| Gain S | Red | a82330 |
| Gain M | Orange | ed851e |
| Gain L |  Green | 4dc13c |
| Urgency S | Red | a82330 |
| Urgency M | Orange | ed851e |
| Urgency L |  Green | 4dc13c |

### Optional but recommended steps

1. **Add a issue template**:
The repository could have an issue template e.g. [cg](https://github.com/Clinical-Genomics/cg/issues/new?template=user-story.md)

1. **Commit messages**:
Use [conventional commits](https://www.conventionalcommits.org/en/) messages when formulating commit messages to the master branch.

1. **Set up code coverage tracking**:
Only allow -0.1% decrease in test [coverage](https://coveralls.io/) so bug fixes can pass but new code is forced to have a unit test.

1. **Set up automatic linting**:
[Automatically](https://github.com/Clinical-Genomics/cg/blob/master/.travis.yml) apply [standard python coding styles](https://github.com/Clinical-Genomics/cg/blob/master/.gitlint.yaml)  with ease!

1. **Define the public API**:
Without knowing what the public API of your tool is, semantic versioning remains a guessing game. The public API can be e.g. all public functions, the CLI, a REST API.

1. **Set up continous integration**:
Get those unit tests tested [automatically](https://travis-ci.org/) or github actions! See [cg](https://github.com/Clinical-Genomics/cg/blob/master/.travis.yml) for an example.

1. **Create update scripts**:
Read up on how to create an [update script](../publish/update-scripts.md).

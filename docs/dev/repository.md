# Repository Guidelines @clinical-Genomics

## Mandatory
- Add responsible and deputy of the repository to AM doc #1098.
- The repository must state the versioning scheme followed i.e. [semantic versioning](https://semver.org/) in the `CONTRIBUTING` doc.

This is a list containing all items that are **highly** recommended to be set up for Clinical Genomics repositories.

1. **Add code owners**:
The repository should have at least two active contributors that understand the code and help review and sign off on changes (merges to master and releases). You can document this with code owners in the `.github/CODEOWNERS` document (read up on [codeowners](https://help.github.com/en/articles/about-code-owners)), or through GitHub contributions and write permissions. This involves testing and code review. Testing can be done by the user proposing changes, but as with all good peer review, this is not ideal. See also AM doc #1098.

1. **Choose a branching model**:
The repository should state the branching model used for the repository in the `CONTRIBUTING` doc. Here are the ones commonly used at Clinical Genomics [branching models](models.md). Please describe your branching model in this guide. See AM doc #1042.

1. **Versioning**:
Automate version version increments using e.g. the [bumpversion package](https://github.com/peritus/bumpversion) for bumping and tagging. This should follow the choosen branching model. Ensure that archived releases are made of each version you intend to deploy, and ideally all.

1. **Add a pull request template**: 
The repository should have a pull request template in `.github/PULL_REQUEST_TEMPLATE`, e.g [servers](https://github.com/Clinical-Genomics/servers/blob/master/.github/PULL_REQUEST_TEMPLATE), that includes:
    - Description of feature/fix
    - How to test and expected outcome
    - For version bumps, motivate according to your versioning scheme. E.g. in SemVer this is a major|minor|path version because ...
    - Code review approval
    - Signoff tickboxes for code review, test status, and 
    - If merging to a **branch** that will be **deployed** in **production** sign off on deployment and implementation is the person who merges to the production ready branch. Consider using a tickbox for deploy readiness to make it extra clear.
    
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
| Enhancement | Cyan blue | 84b6eb |
| Bug |  Magenta | d60493 |
| Refactor | Light green | 74f79b |


### More recommended features

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

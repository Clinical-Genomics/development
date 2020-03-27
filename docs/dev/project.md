This is a list containing all items that need to be set up so that repositories are compatible with `1042 Verifications and Validations`.

1. **Choose a branching model**.
Read up on our [branching models](models.md).
1. **Update the README.md**. Add on which branching model you are in the README.md of the repo.
1. **Add code owners**. Add `.github/CODEOWNERS`. Please add two people if possible. Read up on [codeowners](https://help.github.com/en/articles/about-code-owners).
1. **Add a pull request template**. Add `.github/PULL_REQUEST_TEMPLATE` that includes a test scenario, a motivation for bump template as well as signoff tickboxes for code review, functional testing, and [sing off for deploy/merge](../publish/sign-off.md). Read up on [pull request templates](https://help.github.com/en/articles/creating-a-pull-request-template-for-your-repository).
1. **Create update scripts**. Read up on how to create an [update script](../publish/update-scripts.md).
1. **Use semantic versioning**. Bump version on each change on master, e.g. use the [bumpversion package](https://github.com/peritus/bumpversion) to automate bumping and tagging.
1. **Define the public API**. Without knowing what the public API of your tool is, semantic versioning remains a guessing game. The public API can be e.g. all public functions, the CLI, a REST API.
1. **Set up TravisCI**. Get those unit tests tested [automatically](https://travis-ci.org/)! In doubt, check out [cg](https://github.com/Clinical-Genomics/cg/blob/master/.travis.yml).

### Optional but recommended steps

1. **Commit messages**. Use [conventional commits](https://www.conventionalcommits.org/en/) messages when formulating commit messages to the master branch.
1. **Set up coveralls**. Only allow -0.1% decrease in test [coverage](https://coveralls.io/) so bug fixes can pass but new code is forced to have a unit test.
1. **Set up automatic linting**. [Automatically](https://github.com/Clinical-Genomics/cg/blob/master/.travis.yml) apply [standard python coding styles](https://github.com/Clinical-Genomics/cg/blob/master/.gitlint.yaml)  with ease!

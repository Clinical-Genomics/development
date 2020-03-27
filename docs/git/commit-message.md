# On the importance of commit messages

We chose [conventional commits][conventional commits] for its readability and its ability to automate our [semantic versioning][semantic versioning] & changelog.

Conventional commits are structured as `<type>(<scope>):<subject>`. Adhering to this structure with detailed subjects and message bodies when appropriate allows us to create a truly meaningful history. When browsing this history we can really see the progression of development, and when reviewing PRs we have a brief summary of changes right in front of us. However, the real value of a meaningful commit message may not come for months down the road.

## Format of the commit message:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Message subject (first line)

First line cannot be longer than 70 characters, second line is always blank and other lines should be wrapped at 80 characters.
These are the <type> values:

 - **fix**: the commit patches a bug in your codebase (this correlates with PATCH in semantic versioning).
 - **feat**: the commit introduces a new feature to the codebase (this correlates with MINOR in semantic versioning).
 - **BREAKING CHANGE**: a commit that has the text "BREAKING CHANGE" at the beginning of its optional body or footer section introduces a breaking API change (correlating with MAJOR in semantic versioning). A breaking change can be part of commits of any type. e.g., a fix:, feat: & chore: types would all be valid, in addition to any other type.
 - Others: commit types other than fix: and feat: are allowed, for example recommends chore:, docs:, style:, refactor:, and test:. We also recommend improvement for commits that improve a current implementation without adding a new feature or fixing a bug.
 - A scope may be provided to a commit’s type, to provide additional contextual information and is contained within parenthesis, e.g., feat(parser): add ability to parse arrays.

Example <scope> values:

 - cli
 - build
 - frontend
 - tests
 - config
 - web

The `<scope>` can be empty (eg. if the change is a global or difficult to assign to a single component), in which case the parentheses are omitted.

### Message body

 - uses the imperative, present tense: “change” not “changed” nor “changes”
 - includes description for the change and contrasts with previous behavior

*This description must include the motivation for the chosen version increment.*

## When to use conventional commits?

During the work on a feature branch commit messages are reflecting the work in progress. Only after a feature is approved to be merged, does the commit message become important and conventional commits should be followed. The commit messages that ends up in the tools master branch is following the conventional commits standard.

> ProTip
>
> Squashing commits of a pull request reduces the clutter introduced in the commit history. It enables to push early and often to the feature branch and to merge a feature as a unit.

## Why Use Conventional Commits

 - Automatically generating CHANGELOGs.
 - Automatically determining a semantic version bump.
 - Communicating the nature of changes to teammates, the public, and other stakeholders.
 - Triggering build and publish processes.
 - Making it easier for people to contribute to your projects, by allowing them to explore a more structured commit history.

## Examples

Commit message with description and breaking change in body

```text
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

Commit message with no body

```text
docs: correct spelling of CHANGELOG
```

Commit message with scope

```text
feat(lang): added polish language
```

Commit message for a fix using an (optional) issue number.

```text
fix: minor typos in code

see the issue for details on the typos fixed

fixes issue #12
```

Sources:

- [conventional commits][Conventional commits]
- [karma][karma]

[conventional commits]: https://www.conventionalcommits.org/en/v1.0.0-beta.2
[semantic versioning]: https://semver.org/
[karma]: http://karma-runner.github.io/0.10/dev/git-commit-msg.html

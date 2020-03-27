# Code review

Code reviews exist to spot mistakes that were overlooked during initial development. They are also an excellent opportunity for spreading knowledge and best practices among your team members.

I've basically stolen all of this from Thoughbot's guide on [Code Review][thoughtbot].

- Establish the idea that *everybody* gets reviewed. No one stands above the rest. Every patch gets reviewed. However small, there is no valid argument to not review it.
- As far as possible, code should be reviewed before it gets merged.
- Make liberal use of GitHub and pull requests; use line-specific comments for example.
- For bigger patches, don't be afraid to ask to separate them into smaller units.
- Document code review practices.

## Role: Reviewer

The reviewer should focus on things in this order:

1. Intent (why)
1. Design (how)
1. Implementation
1. Grammar

Collect the suggested changes in TODO lists, questions for the code author, and suggested follow-ups for later patches.

## Workflow

The code needs to be reviewed and approved by a code owner. They are automatically assigned when you create the pull request.

The person reviewing the code [signs off][sign-off] on the pull request with a "👍" or similar.

> Hot fixes are excluded from code reviews and can be merged by the author herself.

## Automate the automatable

Aim to discover mistakes as early as possible. This includes running lints, checking for conformance to style guide, etc. Encourage team members to run these tools locally as well as considering them as part of your continuous integration flow. It can also be worth mentioning that it's often easier to take criticism from computers rather than your peers.

[thoughtbot]: https://github.com/thoughtbot/guides/tree/master/code-review
[sign-off]: ../publish/sign-off.md

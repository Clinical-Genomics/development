# When do you need a sign-off and who can sign off on tests, code reviews and deploys?


All tools developed at clinical genomics need to be tested, reviewed and deployed according to a specific routine which is generally outlined under ["How to publish your tool"][prod]. These three things also need a sign-off by an authorized person. For tools used in production this is especially important. There are two development models used at Clinical Genomics and depending on which you use the sign-offs happen at slightly different steps in the update process.

## Github flow
In this model the sign-offs all happen in the pull request. The developer will as part of the initial pull request add two check boxes to the description; one for code review and one for functional testing. The authorized person(s) doing the test and review then ticks the boxes as the code has been checked and tested on stage according to the test case described in the pull request. The person ticking the last box also approves the pull request. Only when the boxes are ticked, the authorized person(s) have added their thumbs up and the pull request has been approved the decision to merge and deploy is made. The person(s) authorized to sign-off on this then adds the go-ahead as a comment in the pull request and merges the branch to master (or other source). This process is better described in ["How to publish your tool"][prod].

### People authorized to sign-off on code reviews
* Code owner(s) of the specific repository

### People authorized to sign-off on functional tests
* Clinical Genomics employee

### People authorized to sign-off on merge and deploy
* Tools in production - Team leader IT (see AM document `1047 Functions and signature list`)
* Tools in development - Code owner(s) of the specific repository

## Git flow
In this model several pull requests are bunched in the same release and it is therefore necessary to do the sign-offs in three steps:

1. First pull request to add changes to the feature branch - sign-offs needed are on code review, functional testing and merge as described under Github flow.
2. AM Test specification and implementation plan - sign-offs needed on system testing (testing of the whole development or release branch to be deployed) and decision to merge to master and deploy the code. Test specifications and implementation plan templates are available in AM (`1249 Test Specification - Template` and `1187 Implementation plan - template`)
3. Second pull request to merge into master - confirm the sign-offs in the AM test specification and implementation plan.

### People authorized to sign-off on code reviews
* Code owner(s) of the specific repository

### People authorized to sign-off on functional tests
* Test specification and implementation plan - Management team member, Facility manager and Quality control manager (see AM document `1047  Functions and signature list`)
* Pull request - Code owner(s) to confirm test specification and implementation plan

### People authorized to sign-off on merge and deploy
* Tools in production - Team leader IT (see AM document `1047 Functions and signature list`)
* Tools in development - Code owner(s) of the specific repository

[prod]: prod.md

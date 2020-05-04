# How to install your tool in production (deployment)?

## Rules
1. Always get code review approval from a code owner or responsible in AM #1098 of the tool that you are deploying
1. Announce the change and document the change in behaviour in AM or github accordingly
1. Merge and deploy together with a code owner of the repository you are pushing changes to
1. Use an [update script][update-script] (recommended) or an otherwise well documented installation process in AM

## Hasta
Prerequisuites:

- All update scripts are in `/home/proj/production/servers/resources/hasta.scilifelab.se`
- Your intended conda env must exist before using an update script as they will not create a new one

- Create a [pull request][pr] from your branch
- Make changes on your branch as needed. Your pull request will update automatically when you push to github
- Ask for a [pull request review][pr-review]
- Test the PR on stage by deploying your branch on a Hasta:
    - Login to Hasta using ssh <YOUR_USER_NAME>@hasta.scilifelab.se
    - Switch to stage: `us`
    - Install with the tool's update script: `bash /home/proj/production/servers/resources/hasta.scilifelab.se/update-<YOUR-TOOL>-stage.sh <YOUR-BRANCH>`
    - Perform the tests you have described in the PR header and record the results accordingly (e.g. by taking a screenshot)
- If the tests passes and you have an approved code review, merge the PR into master
    - If applicable - add a small risk assessment to the merge message describing the potential impact on existing functionality
    - Remove or rewrite any nonsense in the merge message into descriptive text
- Merge the branch to master on github
- Delete `<YOUR-BRANCH>` on github after merging (recommended to be automated in Github Settings)
- Bump the version on master (by code-owner):
    - Cloning the master branch locally or pull master into local existing clone
    - Run: `bumpversion patch|minor|major` if applicable
    - Push version bump: `git push && git push --tags` if applicable
- Test that the merged PR is installable on stage:
    - `bash /home/proj/production/servers/resources/hasta.scilifelab.se/update-<YOUR-TOOL>-stage.sh master`
- If it passes, deploy in production:
    - Check with the production team that it is a good time to modify production
    - Announce the deploy to all who should be informed
    - Switch to production: `up`
    - Install with the tool's update script: `bash /home/proj/production/servers/resources/hasta.scilifelab.se/update-<YOUR-TOOL>.sh master`
    
Installing the tool an update script will log the deploy.

[update-script]: update-scripts.md
[pr]: ../../github/pr
[pr-review]: ../../github/pr-request

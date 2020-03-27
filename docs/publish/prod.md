# How to install your tool in production?

Your code is ready for deployment. Well done bucko! Now what do I do?

(all scripts are in `${PRODUCTION_HOME}/servers/resources`)

- Kick off a discussion by sending a [pull request][pr] from your branch.
- Make changes on your branch as needed. Your pull request will update automatically.
- Ask for a [pull request review][pr-review]
- Test the PR on stage by deploying your branch
    - Do this with your reviewer
    - Announce on TTNs daily standup
    - Delete current stage
    - Clone prod to stage: `condacopy-prod-to-stage.sh`
    - Switch to stage: `usestage`
    - Install branch into stage with the tool's update script: `update-tool-stage.sh`
- If it passes, merge the PR into master
    - Add a small risk assessment to the merge message describing the potential impact on existing functionality
    - Remove or rewrite any nonsense in the merge message into descriptive text
- Delete the branch
- Delete the development branch in conda
- Bumpversion on master
- Test the installation of the new master on stage
    - But only test that the installation succeeds
- If it passes, deploy on prod!
    - Announce on stand up
    - Take backup of prod: e.g. `savetheconda prod170926`
    - Install with the tool's update script: `update-tool-prod.sh`
    
Installing the tool an update script will log the deploy.

[pr]: ../../github/pr
[pr-review]: ../../github/pr-request

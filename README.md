# GithubActionTesting

## Learnings

### Status checks
* Name the jobs in workflows so they can be referenced easier
* Workflow jobs won't automatically appear in the status check list, you need to search by the name and then an auto-complete prompt will appear where you can select the job as a status check: ![Example](https://i.imgur.com/IPQnuhE.png)
* Status checks "on push" only wont trigger if a PR is made from a forked repo so to support that you also need "on pull_request" setup

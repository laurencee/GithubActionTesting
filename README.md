# GithubActionTesting

## Learnings

### Status checks
* Name the jobs in workflows so they can be referenced easier
* Workflow jobs won't automatically appear in the status check list, you need to search by the name and then an auto-complete prompt will appear where you can select the job as a status check: ![Example](https://i.imgur.com/IPQnuhE.png)
* Skip required status checks for non-code changes by [following this guide](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/troubleshooting-required-status-checks#handling-skipped-but-required-checks)
* Status checks "on push" only wont trigger if a PR is made from a forked repo so to support that you also need "on pull_request" setup
  - When doing both `on push` and `on pull_request` you will trigger double builds if you don't specify branch filters for `on push`. 
  As `on pull_request` by default will pickup all commits pushed as part of the "synchronize" event, so as long as you leave `on pull_request` as the default state or specify `synchronize` in the types argument then every commit will result in a new build (along with opening/reopening the PR).
  - **TLDR; Recommendation is**
  ```yml
  on:
  pull_request:

  push:
    branches: 
      - main
  ```

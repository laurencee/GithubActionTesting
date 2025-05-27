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

### CSpell GHA

Apparently [this GHA](https://github.com/streetsidesoftware/cspell-action) [doesn't require any permissions to function](https://github.com/laurencee/GithubActionTesting/pull/17/files#diff-616593396de2fd1a651a07cd6e58919c62943ce8b34d237b85adbdd4ce2438d1L11) despite what [this issue indicated](https://github.com/streetsidesoftware/cspell-action/issues/712).

For my purposes, it was important to set the following on the CSpell github action if you want it to check your whole repo everytime.

This is particularly useful if you have an existing larger repo and want your initial main builds to highlight issues that you can fix later.

The other surprise was you must set the `use_cspell_files` field or your cspell files input will be ignored.

```yaml
  - uses: streetsidesoftware/cspell-action@v7
    with: 
      incremental_files_only: false
      use_cspell_files: true
```

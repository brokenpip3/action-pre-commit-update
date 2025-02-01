# Pre-commit auto-update action

A GitHub Action that will automatically update your pre-commit hooks version and create a PR

## How to use it

``` yaml
jobs:
   pre-commit-update:
     runs-on: ubuntu-latest
     name:
     steps:
       - name: Checkout
         uses: actions/checkout@v3
       - name: Update pre-commit hooks
         uses: brokenpip3/action-pre-commit-update@0.0.2
         with:
           github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Key              | Default                               | Required | Description                                                                                 |
|------------------|---------------------------------------|----------|---------------------------------------------------------------------------------------------|
| pr-create        | `true`                                | false    | Specify if you want to create the PR or not                                                 |
| pr-title         | `chore(pre-commit): auto update hooks`| false    | PR Title                                                                                    |
| pr-branch        | `auto-update-pre-commit-hooks`        | false    | PR Branch                                                                                   |
| pr-targetbranch  | `main`                                | false    | PR Target branch                                                                            |
| github-token     |                                       | false    | Github Token, required if PR create is true                                                 |
| update-latest    | `false`                               | false    | Instead of using the latest tag use the latest commit, equals to run with '--bleeding-edge' |
| update-freeze    | `true`                                | false    | Store hashes in rev instead of tag names, equals to run with '--freeze'                     |
| update-repo      |                                       | false    | Only update a specifi repository, equals to run with '--repo'                               |
| update-allfiles  | `false`                               | false    | Run hooks vs all the files of the repo                                                      |


## Outputs

| Key              | Description                                                  |
|------------------|--------------------------------------------------------------|
| update-hit       | True/False if changes in .pre-commit-config.yaml are present |
| options          | Options used in pre-commit update command                    |


## Notes

During the process of writing this action, I came across a similar one authored by [browniebroke](https://github.com/browniebroke/pre-commit-autoupdate-action). However, unlike that one, this action is built as a single package without the need for any additional dependency actions. It should be noted that this approach may not be suitable for all contexts, such as different Python versions. Additionally, this action offers more options, with the most important one for me being the ability to not run pre-commit on all files.

# GitHub Activity in Readme

Updates a GitHub user's `README.md` with the recent GitHub activity.

<img width="735" alt="profile-repo" src="https://user-images.githubusercontent.com/25279263/87703301-3aa4a500-c7b8-11ea-8eb6-245121997a7b.png">

> **Remember that using this fork will commit your updated README as the [Recap TIme Bot](https://github.com/RecapTimeBot).**
> That account is managed by [the Pins team](https://madebythepins.tk) and will count it as an contribution to your README repo.
> If you want, add that account to your collaborators to allow us debug issues.

---

## Instructions

**NOTE**:We recommend to have an `your-username/your-username` repo on your personal GitHub account and not on your org (they're unsupported yet).

- Add the comment `<!--START_SECTION:activity-->` (entry point) within `README.md`. You can find an example
[here](https://github.com/AndreiJirohHaliliDev2006/AndreiJirohHaliliDev2006/blob/master/README.md).

- It's the time to create a workflow file called `.github/workflows/update-readme.yml`. The above job runs every half an hour, you can change it as you
wish based on the [cron syntax](https://jasonet.co/posts/scheduled-actions/#the-cron-syntax).
You can find an example [here](https://github.com/AndreiJirohHaliliDev2006/AndreiJirohHaliliDev2006/blob/master/.github/workflows/update-readme.yml).


```yml
name: Update README

on:
  schedule:
    - cron: '*/30 * * * *'

jobs:
  build:
    runs-on: ubuntu-latest
    name: Update this repo's README with recent activity

    steps:
      - uses: actions/checkout@v2

      # Pin the version to the latest stable version.
      # If you want to live on edge, use 'master' branch.
      - uses: MadeByThePinsHub/github-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

The above job runs every half an hour, you can change it as you wish based on the [cron syntax](https://jasonet.co/posts/scheduled-actions/#the-cron-syntax).

Please note that only those public events that belong to the following list show up:

- `IssueEvent`
- `IssueCommentEvent`
- `PullRequestEvent`

You can find an example [here](https://github.com/jamesgeorge007/jamesgeorge007/blob/master/.github/workflows/update-readme.yml).

### Custom commit message

Specify a custom commit message with the `COMMIT_MSG` input param.

```yml
name: Update README

on:
  schedule:
    - cron: '*/30 * * * *'
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    name: Update this repo's README with recent activity

    steps:
      - uses: actions/checkout@v2
      - uses: jamesgeorge007/github-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          COMMIT_MSG: 'Specify a custom commit message'
```

_Inspired by [JasonEtco/activity-box](https://github.com/JasonEtco/activity-box)_

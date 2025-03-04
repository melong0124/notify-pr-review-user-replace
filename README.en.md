# notify-pr-review

🌏 [**한국어**](README.md) | English

GitHub Actions to notify on Slack when a PR review is requested.

<img src="https://user-images.githubusercontent.com/13075245/279234262-cbe5c159-e103-49eb-bf1f-b50116f98984.png" width="500" alt="intro">

## Usage

1. Set up a secret named `SLACK_BOT_TOKEN` to send the message.

> Go to the Repo > Settings > Secrets > New repository secret

For the value, use a Slack token that starts with `xoxb-`.

2. Create a `.github/workflow/notify-pr-review.yml` file:

```yml
name: notify pr review

on:
  pull_request:
    types: [review_requested]
    
jobs:
  notify:
    runs-on: [ubuntu-latest]
    steps:
      - name: Notify PR Review
        uses: melong0124/notify-pr-review-user-replace@v1.0.0
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          slackBotToken: ${{ secrets.SLACK_BOT_TOKEN }}
          emailToSlackMap: "user@sample.com:replace_slack_user_name,user2@sample.com:replace_slack_user_name2"
          ignoreUsers: "github_user_login1,github_user_login2"

```

## Inputs

### `token`

**Required** GitHub token

### `slackBotToken`

**Required** Slack bot token to send messages

e.g. `xoxb-798572638592-435243279588-9aCaWNnzVYelK9NzMMqa1yxz`

### `emailToSlackMap`

**Required** emailToSlackMap maps email addresses to custom Slack usernames for notifications

### `user@sample.com:replace_slack_user_name,user2@sample.com:replace_slack_user_name2`

**Required** ignoreUsers is a comma-separated list of GitHub login usernames to be ignored

e.g. `github_user_login1,github_user_login2`

## License

```text
Copyright (c) 2023-present NAVER Corp.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

---

### Modifications
This software is based on the original work by NAVER Corp., licensed under the Apache License 2.0.
Additional features have been implemented in this version, including:

- Ignore User List feature added
- Email Replace feature added

These modifications are distributed under the same Apache License 2.0.

---

### Notice
This software includes modifications and enhancements that are not part of the original NAVER Corp. project. Any use of this software must comply with the Apache License 2.0.

The names, trademarks, and logos of NAVER Corp. are not included in this license. Usage of NAVER Corp.'s branding in any form requires separate permission.
```

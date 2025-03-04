# notify-pr-review

🌏 한국어 | [**English**](README.en.md)

PR 리뷰 요청을 받으면 Slack으로 알리는 Github Actions

<img src="https://user-images.githubusercontent.com/13075245/279234262-cbe5c159-e103-49eb-bf1f-b50116f98984.png" width="500" alt="intro">

## Usage

1. 메시지 전달을 위해 `SLACK_BOT_TOKEN` 이름의 secret을 세팅하세요.

> 세팅할 Repo > Settings > Secrets > New repository secret

이때, Value는 슬랙에서 제공하는 `xoxb-` 형태의 토큰이어야 합니다.

2. `.github/workflow/notify-pr-review.yml` 파일을 만드세요:

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

**Required** GitHub에서 제공하는 토큰

### `slackBotToken`

**Required** Slack bot을 통해 메시지를 보내기 위한 토큰

e.g. `xoxb-798572638592-435243279588-9aCaWNnzVYelK9NzMMqa1yxz`

### `emailToSlackMap`

**Required** GitHub 이메일 주소를 특정 Slack 사용자 이름으로 매핑하는 값입니다. 값이 제공되지 않을 경우, 이메일 주소에서 @ 앞 부분이 Slack 사용자 이름으로 사용됩니다.

### `user@sample.com:replace_slack_user_name,user2@sample.com:replace_slack_user_name2`

**Required** ignoreUsers는 무시할 GitHub 로그인 사용자 이름의 쉼표로 구분된 목록입니다.

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

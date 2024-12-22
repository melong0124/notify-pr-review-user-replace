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
        uses: naver/notify-pr-review@v1.2.1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          slackBotToken: ${{ secrets.SLACK_BOT_TOKEN }}
          emailToSlackMap: 'user_1@example.com:slack_user_1;user_2@example.com:slack_user_2'
```

## Inputs

### `token`

**Required** GitHub에서 제공하는 토큰

### `slackBotToken`

**Required** Slack bot을 통해 메시지를 보내기 위한 토큰

e.g. `xoxb-798572638592-435243279588-9aCaWNnzVYelK9NzMMqa1yxz`

### `emailToSlackMap`

**Optional** GitHub 이메일 주소를 특정 Slack 사용자 이름으로 매핑하는 값입니다. 값이 제공되지 않을 경우, 이메일 주소에서 @ 앞 부분이 Slack 사용자 이름으로 사용됩니다.

e.g. `user_1@example.com:slack_user_1;user_2@example.com:slack_user_2`

## License
```
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
```

name: Update README Time

on:
  schedule:
    - cron: '*/1 * * * *'  # 每分钟运行一次
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Update time in README
        run: |
          CURRENT_TIME=$(TZ='Asia/Shanghai' date '+%Y-%m-%d %H:%M:%S')
          sed -i "s/<!-- TIME -->.*<!-- TIME -->/<!-- TIME --> $CURRENT_TIME <!-- TIME -->/" README.md
      - uses: actions/commit-and-push@v3
        with:
          commit-message: "Update current time"

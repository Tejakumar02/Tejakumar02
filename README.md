name: Generate GitHub Stats

on:
  schedule:
    - cron: "0 */6 * * *"   # runs every 6 hours
  workflow_dispatch:          # also lets you trigger manually

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Generate Stats SVGs
        uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: Tejakumar02
          template: classic
          base: header, activity, community, repositories
          config_timezone: Asia/Kolkata
          plugin_languages: yes
          plugin_languages_limit: 6
          filename: assets/stats.svg

      - name: Generate Langs SVG
        uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: Tejakumar02
          template: classic
          base: ""
          plugin_languages: yes
          plugin_languages_details: lines, percentage
          plugin_languages_limit: 8
          filename: assets/langs.svg

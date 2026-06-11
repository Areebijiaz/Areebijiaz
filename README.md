name: Metrics
 
on:
  schedule:
    - cron: "0 0 * * *"   # runs every day at midnight UTC
  workflow_dispatch:       # allows manual trigger from GitHub Actions tab
  push:
    branches: [main]
 
jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: Areebijiaz
          template: classic
          base: header, activity, community, repositories
          base_indepth: yes
          filename: github-metrics.svg
 
          # Languages breakdown
          plugin_languages: yes
          plugin_languages_limit: 8
          plugin_languages_threshold: 0%
          plugin_languages_details: lines, percentage
 
          # Repository highlights
          plugin_repositories: yes
          plugin_repositories_featured: Areebijiaz/streamflix, Areebijiaz/AutoDesk-DSA, Areebijiaz/gamingcafe
 
          # Activity feed
          plugin_activity: yes
          plugin_activity_limit: 5
          plugin_activity_days: 14
          plugin_activity_filter: all
 
          # Contribution calendar
          plugin_isocalendar: yes
          plugin_isocalendar_duration: full-year
 
          # Topics
          plugin_topics: yes
          plugin_topics_limit: 12
          plugin_topics_mode: mastered
 

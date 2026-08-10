name: metrics
on:
  workflow_dispatch:
  schedule:
    - cron: "0 0 * * *"   # regenerates once a day

jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: cuervo0102
          template: classic
          base: header, activity, community, repositories, metadata

          # Language breakdown bars
          plugin_languages: yes
          plugin_languages_analysis_timeout: 15
          plugin_languages_categories: markup, programming
          plugin_languages_recent_categories: markup, programming
          plugin_languages_details: bytes-size, percentage

          # Coding habits + activity per day
          plugin_habits: yes
          plugin_habits_charts_type: classic
          plugin_habits_days: 14
          plugin_habits_facts: yes

          # Isometric commit calendar cube
          plugin_isocalendar: yes
          plugin_isocalendar_duration: full-year

          # Achievements ranks (the colored badges)
          plugin_achievements: yes
          plugin_achievements_display: compact
          plugin_achievements_secrets: yes

          # Most used topics/technologies
          plugin_topics: yes
          plugin_topics_mode: icons

          # Contribution calendar + streaks
          plugin_calendar: yes
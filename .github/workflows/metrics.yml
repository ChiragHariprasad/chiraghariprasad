# Generates metrics.svg using lowlighter/metrics and commits it to this repo.
# Docs: https://github.com/lowlighter/metrics
#
# Setup (see the step-by-step guide in chat):
#   1. Create a classic GitHub PAT (scopes: public_repo, read:user)
#   2. Add it as a repo secret named METRICS_TOKEN
#   3. Commit this file to .github/workflows/metrics.yml in your profile repo
#   4. Run it once manually from the Actions tab, then it refreshes daily

name: Metrics

on:
  schedule:
    - cron: "0 3 * * *"   # daily at 03:00 UTC (~8:30 AM IST) — change or remove if you don't want daily updates
  workflow_dispatch:       # lets you trigger a run manually from the Actions tab
  push:
    branches: ["main"]     # change to "master" if that's this repo's default branch

jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Generate metrics
        uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          filename: metrics.svg

          # --- what to render ---
          base: header, activity, community, repositories
          config_timezone: Asia/Kolkata
          config_display: large
          config_animations: yes

          # --- isometric contribution calendar ---
          plugin_isocalendar: yes
          plugin_isocalendar_duration: full-year

          # --- most-used languages ---
          plugin_languages: yes
          plugin_languages_limit: 8
          plugin_languages_threshold: 2%
          plugin_languages_analysis_timeout: 15

          # --- achievements + lines of code changed ---
          plugin_achievements: yes
          plugin_achievements_threshold: C
          plugin_lines: yes

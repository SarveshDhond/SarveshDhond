- 👋 Hi, I’m @SarveshDhond
- 👀 I’m interested in Data Analysis and Data Science
- 🌱 I’m currently learning Python programming language
- 💞️ I’m looking to collaborate on developing Python projects and apps
- 😄 Pronouns: He/Him
- ⚡ Hot take: Data Science is just a glorified version of astrology  

name: Generate pacman animation

on:
  schedule: # execute every 12 hours
    - cron: "* */12 * * *"

  workflow_dispatch:

  push:
    branches:
    - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: generate pacman-contribution-graph.svg
        uses: abozanona/pacman-contribution-graph@main
        with:
          github_user_name: ${{ github.repository_owner }}


      - name: push pacman-contribution-graph.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

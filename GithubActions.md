# About - 
- PLatform to automate developer workflows
# GitHUB events - 
- When something happens IN ot TO your REPOSITORY
- PR created
- Issue Created
- PR merged
- Contributor Joined
# How Github actions Work
- Listen to an event - > Trigger Workflow (Workflow is nothing but a set of GitHub actions)
# What was the need of Just another CI/CD tool when we already have Jenkins/ArgoCD etc
- Simple reason - use same tool instead of third party integration
- Setup pipeline easily becuase specifically designed for developers
# How to create GitHUB actions - 
- GitHUb acions tab is by default integrated with every repository on GitHUB
- Go to Github actions choose a workflow
- .github/worflows/workflow.yml
# Sample File
- Create a giyhub actions workflow file in which whenever I commit code to my repo or create a PR then automatically a line is added in the readme.md file that a commit or pr has been created on date - with current data and time
```
# .github/workflows/update-readme.yml
name: Update README with Commit/PR Info

on:
  push:
    branches:
      - main  # Trigger on commits to the main branch
  pull_request:
    types: [opened, closed]  # Trigger on PR creation and closing

jobs:
  update-readme:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Git
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "github-actions[bot]@users.noreply.github.com"

      - name: Update README with Commit/PR Info
        run: |
          echo "A commit or PR was created on $(date)" >> README.md
          git add README.md
          git commit -m "Auto-update README with commit/PR info"

      - name: Push changes
        run: |
          git push
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```

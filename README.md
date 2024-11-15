# Introduction 
This repository contains all configuration files and Github actions to run the Renovate bot periodically to update the dependencies in all configured repositories. 

# Getting Started
## What is Renovate?
Renovate automates dependency updates. Multi-platform and multi-language.

This bot frequently updates the dependencies of all linked repositories. It then creates PRs or automatically merges new versions of those dependencies depending on the corresponding configuration. Each repository can have its own configuration.

## Adding a new repository to be automatically updated by Renovate
1. Modify `renovate-config.json` file in this repository. In this file there is an array `repositories`. Append your repository at the end of the existing array. \
Use the syntax `'PROJECT_NAME/REPOSITORY_NAME'`\
Example: `'gisktzh/gb3-web_ui'`
2. Push your commit
3. (Optional) Run the Github action manually to immediately run Renovate

Now, if the bot is running for the first time after adding your repository it will scan the repository for the `renovate.json` configuration. It will automatically create a pull request containing an initial configuration if none is found. You have to approve and merge this PR manually before Renovate will start updating your dependencies.

> **Note:** To enable automerge to work the following repository settings must be set:
> - `Settings` -> `General` -> `Pull Requests` -> `Allow auto-merge Loading`
> - `Settings` -> `Rules` -> `Rulesets` -> `Branch Rules` -> `Require merge queue`
> - The account that runs `Renovate` must have the permission to bypass required reviews

## How does it work?
There is an Github action based on `.github/workflows/main.yml` that runs the Renovate bot daily. The bot will operate according to the configuration written in `renovate-config.js` file. This file contains a list of all repositories that will be checked/updated automatically.

Each checked repository contains its own rules on how to process dependency updates. The goal should be that the updates run mostly silent and the project should be as up-to-date as possible.

More information: https://docs.renovatebot.com/modules/platform/github/

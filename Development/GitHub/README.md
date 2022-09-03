## Commands
- Create new empty branch
  - https://jira.atlassian.com/browse/SRCTREEWIN-8976
  - ```
    #Local Project Folder connection to Git
    git init
    git add .
    git commit -m "<commit message>"
    git remote add origin <Remote repository URL>
    #git branch -m <branch name>
    git push origin <branch name>
    
    #branch delete
    git push origin --delete <branch name>
    ```
---
## Actions

- cron scheduler

- https://github.com/nektos/act
  - test workflow in local environment
  - `curl https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash`
  - ```yaml
    # ./github/workflows/sample.yml
    name: release
    on:
      push:
        tags:
          - v*
    jobs:
      build:
        runs-on: ubuntu-latest
        strategy:
          matrix:
            python-version: [ 3.9 ]

    steps:
      - uses: actions/checkout@v2
      - name: Set up python ${{ matrix.python-version }}
        uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}

      - name: Install python package
        run: |
          pip install requests

      - name: Run!
        run: |
          python sample.py
    ```
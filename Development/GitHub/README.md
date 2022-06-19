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
# Sample Pipeline for python

```yaml
name: Python CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  python-ci:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.8, 3.9, 3.10]
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          pip install flake8 pytest

      - name: Run Flake8 (Python linter)
        run: |
          flake8 .

      - name: Run Python tests
        run: |
          pytest --junitxml=tests/results/test-results.xml

      - name: Upload test results
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: pytest-results
          path: tests/results/test-results.xml
```

## Explanation:

- **Checkout code**: Uses the actions/checkout@v3 action to pull the code from the repository.
- **Set up Python**: The setup-python@v4 action sets up the specified Python version from the matrix.
- **Install dependencies**: This command installs the necessary Python packages from requirements.txt, upgrades pip, and also installs flake8 (linter) and pytest (unit testing framework).
- **Run Flake8**: This step runs flake8, which checks the Python code for style and formatting errors. If there are issues, the pipeline will fail.
- **Run Python tests**: This runs the unit tests using pytest. The --junitxml flag generates an XML report of the test results, which is useful for viewing test results in CI environments.
- **Upload test results**: This uploads the pytest test results as an artifact so they can be reviewed later.

### Why is this important?

    Flake8 ensures code quality by checking for linting and style issues before running tests.
    Pytest ensures that your code works as expected and detects bugs early.
    Matrix testing ensures that your code works across different Python versions, improving compatibility.

```py
# Python function and unit test
def add(x, y):
    return x + y

def test_add():
    assert add(1, 2) == 3
    assert add(-1, 1) == 0
    assert add(0, 0) == 0
```
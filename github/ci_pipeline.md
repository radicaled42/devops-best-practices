# CI Pipeline

```
name: CI Pipeline

# Trigger the pipeline on pushes and pull requests to the main branch
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    # Checkout the latest code from the repository
    - name: Checkout code
      uses: actions/checkout@v3

    # Set up Python environment
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.9'

    # Install dependencies
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    # Lint the code using flake8
    - name: Run Linting
      run: |
        pip install flake8
        flake8 .

    # Run unit tests using pytest
    - name: Run Unit Tests
      run: |
        pip install pytest
        pytest

    # Build a Docker image
    - name: Build Docker image
      run: |
        docker build -t myapp:latest .

    # (Optional) Deploy the Docker image to a container registry (e.g., Docker Hub)
    # - name: Log in to Docker Hub
    #   run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

    # - name: Push Docker image to Docker Hub
    #   run: docker push myapp:latest

    # (Optional) Deploy the Docker image to a server
    # - name: Deploy to server
    #   run: |
    #     ssh user@your-server 'docker pull myapp:latest && docker run -d -p 80:80 myapp:latest'

    # Notify the team (using a hypothetical action)
    - name: Notify team
      if: failure()
      run: echo "Build failed! Check the logs."
```
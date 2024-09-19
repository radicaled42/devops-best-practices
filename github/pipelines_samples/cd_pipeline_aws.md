# Sample AWS CD

```yaml
name: CD Pipeline

on:
  push:
    branches:
      - main  # Trigger on push to the main branch

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    # Step 1: Checkout the code from the repository
    - name: Checkout code
      uses: actions/checkout@v2

    # Step 2: Set up AWS credentials
    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v2
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: ${{ secrets.AWS_REGION }}

    # Step 3: Log in to Amazon ECR
    - name: Log in to Amazon ECR
      id: login-ecr
      uses: aws-actions/amazon-ecr-login@v1

    # Step 4: Build the Docker image
    - name: Build Docker image
      run: |
        docker build -t my-app:${{ github.sha }} .

    # Step 5: Tag the Docker image with the ECR repository URI
    - name: Tag Docker image
      run: |
        ECR_REPO_URI=123456789012.dkr.ecr.$AWS_REGION.amazonaws.com/my-repo
        docker tag my-app:${{ github.sha }} $ECR_REPO_URI:latest

    # Step 6: Push Docker image to Amazon ECR
    - name: Push Docker image to ECR
      run: |
        ECR_REPO_URI=123456789012.dkr.ecr.$AWS_REGION.amazonaws.com/my-repo
        docker push $ECR_REPO_URI:latest
```
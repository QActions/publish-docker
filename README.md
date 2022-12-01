# Publish service image

Used to publish a service Docker image to AWS ECR.

**This step expects a Docker image to be available with the name: `service`.**

Expected environment variables:
```sh
# Project info, set by QActions/expose-project-info
PROJECT_NAME=my-service
PROJECT_VERSION=1.0.0

# AWS credentials
AWS_ACCESS_KEY_ID=......
AWS_SECRET_ACCESS_KEY=......
```

Example usage:
```yml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      # Exposes PROJECT_VERSION and PROJECT_NAME
      - name: Expose project info
        uses: QActions/expose-project-info@1.0.0

      # Build Docker image
      # Should result in an image named `service`
      - name: Build Docker image
        uses: .........

      - name: Publish Docker image to AWS ECR
        uses: QActions/publish-service-image@1.2.0
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

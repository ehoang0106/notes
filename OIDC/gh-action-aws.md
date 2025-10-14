
### Setup OIDC for GitHub Action and AWS

## 1. AWS Configure

### a. Create IAM Identity Providers

Go to AWS IAM -> Identity Providers -> Add provider

Select OpenID Connect

Provider URL:

```
https://token.actions.githubusercontent.com
```

Audience:

```
sts.amazonaws.com
```

### b. Create IAM Role

AWS IAM -> Roles -> Create role -> Web identity -> `token.actions.githubusercontent.com` (the identity provider just created above)

Fill out the GitHub organization. Usually it is your github accunt ID or organization

GitHub repo and GitHub branch

Create a custom policy or a existing aws permission. This is for permissions the role can do on AWS account

Enter Role name and done

## 2. GitHub Action

Create folder `.github\workflows`

Create `deploy.yml`

`deploy.yml` example:

```yml
name: Push code to earnesti.com
#tringger when push code to master branch
on:
  push:
    branches:
      - master
  workflow_dispatch:
  
permissions:
  contents: read # This is required for actions/checkout
  id-token: write   # This is required for requesting the JWT

jobs:
  Deploy-to-S3:
    runs-on: ubuntu-latest
    steps:
      #config aws
      - name: Configure aws credentials
        uses: aws-actions/configure-aws-credentials@v1.7.0
        with:
          role-to-assume: ${{ secrets.AWS_ROLE_TO_ASSUME }}
          role-session-name: 'GitHub_OIDC_earnesti'
          aws-region: us-west-1

      #checkout code
      - name: Checkout code
        uses: actions/checkout@v4
        
      #copy to s3
      - name: Sync S3 bucket
        run: aws s3 sync . s3://${{ secrets.AWS_BUCKET_NAME}}
```

`role-to-assume`: the arn of the role
`role-session-name`: the name of the role

Done
## CICD React TS

Neat React starter with TypeScript and Github Actions. Sets up hosting using Amazon S3 and Amazon CloudFront.

### Prerequisites

- [OIDC set up between Github and your AWS account](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services)
- Manually set the OIDC_ROLE environment variable in `.github/workflows/backend.yml` and `.github/workflows/backend.yml` to the role created using the tutorial above.
- [Install AWS SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)

### How to deploy the project manually (without pushing a commit triggering Github Workflows)

##### Backend

Make sure you're in the backend folder. Then, run the following.

```
$ sam build
$ sam deploy --stack-name <CLOUDFORMATION STACK NAME> \
            --parameter-overrides GithubRepoName=<INSERT REPO NAME> \
            --resolve-s3 \
            --region <INSERT REGION> \
            --no-fail-on-empty-changeset \
            --tags project=<INSERT TAGS [OPTIONAL]>
```

##### Frontend

Make sure you're in the frontend folder. Then, run the following commands. You may find the S3 hositng bucket ssm parameter name among the CloudFormation outputs.

```
$ npm run build
$ aws s3 cp ./build s3://$(aws ssm get-parameter --name <S3 HOSTING BUCKET SSM PARAMETER NAME> --query "Parameter.Value" --output text)/ --recursive
```

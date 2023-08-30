## CICD React TS

Neat React starter with TypeScript and Github Actions. Sets up hosting using Amazon S3 and Amazon CloudFront.

### Prerequisites

-   [OIDC set up between Github and your AWS account](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services)
-   Replace the OIDC_ROLE environment variable in `.github/workflows/backend.yml` and `.github/workflows/backend.yml` with the role created using the tutorial above.

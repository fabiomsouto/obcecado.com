# AWS setup

The site is served by the existing CloudFront distribution in front of a
private S3 bucket. `.github/workflows/deploy.yaml` builds with Hugo, syncs
`public/` to the bucket and invalidates CloudFront on every push to `main`.
It authenticates with an IAM role over GitHub's OIDC, so no AWS keys are
stored in GitHub.

One-time setup:

1. **Check the bucket.** The deploy runs `aws s3 sync --delete`, which removes
   every object in the bucket that isn't part of the built site. Move anything
   else you want to keep somewhere else first.

2. **Create the stack.** In CloudFormation, create a stack from
   `site-deploy.yaml` with the bucket name and distribution ID. Set
   `CreateOIDCProvider` to `false` if the account already has the
   `token.actions.githubusercontent.com` identity provider (IAM → Identity
   providers). It creates:
   - the `obcecado-site-deploy` role, which only `main` of this repository can
     assume, and which can only write to the bucket and invalidate the
     distribution;
   - the `obcecado-index-rewrite` CloudFront Function.

3. **Attach the function.** CloudFront → the distribution → Behaviors →
   Default (*) → Edit → Function associations → Viewer request → CloudFront
   Functions → `obcecado-index-rewrite`. Without it, `/phonkyo/` returns 403.

4. **Show the 404 page.** CloudFront → the distribution → Error pages →
   Create custom error response: HTTP error code 403, response page path
   `/404.html`, HTTP response code 404. (A private bucket answers 403 for
   missing keys, not 404.)

5. **Set the repository variables** (Settings → Secrets and variables →
   Actions → Variables, or with `gh variable set`):

   | Variable | Value |
   |---|---|
   | `AWS_ROLE_ARN` | the stack's `RoleArn` output |
   | `S3_BUCKET` | the bucket name |
   | `CLOUDFRONT_DISTRIBUTION_ID` | the distribution ID |
   | `AWS_REGION` | the bucket's region (defaults to `eu-west-1`) |

   Until `AWS_ROLE_ARN` is set, the workflow only builds the site.

6. Re-run the latest workflow run on `main`, or push to `main`.

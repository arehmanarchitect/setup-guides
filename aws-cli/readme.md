### AWS CLI – Quick Reference

| Task                                    | Command                                                   |
| --------------------------------------- | --------------------------------------------------------- |
| Check AWS CLI version                   | `aws --version`                                           |
| Create/configure profile                | `aws configure --profile sift`                            |
| Configure another profile               | `aws configure --profile dev`                             |
| Configure SSO profile                   | `aws configure sso --profile sift`                        |
| Login using SSO                         | `aws sso login --profile sift`                            |
| List all profiles                       | `aws configure list-profiles`                             |
| View profile configuration              | `aws configure list --profile sift`                       |
| Get profile region                      | `aws configure get region --profile sift`                 |
| Set profile region                      | `aws configure set region us-east-2 --profile sift`       |
| Set default output format               | `aws configure set output json --profile sift`            |
| Activate profile in current terminal    | `export AWS_PROFILE=sift`                                 |
| Switch profile                          | `export AWS_PROFILE=dev`                                  |
| Remove active profile selection         | `unset AWS_PROFILE`                                       |
| Show active profile variable            | `echo $AWS_PROFILE`                                       |
| Check effective AWS configuration       | `aws configure list`                                      |
| Verify AWS identity/account             | `aws sts get-caller-identity`                             |
| Verify a specific profile               | `aws sts get-caller-identity --profile sift`              |
| List S3 buckets                         | `aws s3 ls --profile sift`                                |
| List EKS clusters                       | `aws eks list-clusters --region us-east-2 --profile sift` |
| List KMS keys                           | `aws kms list-keys --region us-east-2 --profile sift`     |
| Set default region for current terminal | `export AWS_DEFAULT_REGION=us-east-2`                     |
| Remove a profile                        | `aws configure remove-profile sift`                       |

### AWS credential files

| File                 | Purpose                                                |
| -------------------- | ------------------------------------------------------ |
| `~/.aws/config`      | Profiles, regions, output format and SSO configuration |
| `~/.aws/credentials` | Access keys and secret keys                            |

### Troubleshooting

| Task                           | Command                                      |
| ------------------------------ | -------------------------------------------- |
| List AWS environment variables | `env \\| grep '^AWS_'`                       |
| Remove access key override     | `unset AWS_ACCESS_KEY_ID`                    |
| Remove secret key override     | `unset AWS_SECRET_ACCESS_KEY`                |
| Remove session token override  | `unset AWS_SESSION_TOKEN`                    |
| Refresh SSO login              | `aws sso login --profile sift`               |
| Verify credentials             | `aws sts get-caller-identity --profile sift` |



# AWS Deployment using Beanstalk and CodePipeline


- Beanstalk:
  - Follow the normal flow of the setup. Always select the default options.
  - When asked to deploy code, always remeber to use **.zip** format, **DO NOT USE .rar FORMAT**.

- CodePipeline
  - Follow the normal flow of the setup. Always select the default options.
  - The CodePipeline would create an ARN policy to access all the resources. This is very important.
  - There must be a **buildspec.yml** file to activate 

    ```
    version: 0.2
    phases:
      pre_build:
        commands:
          - echo Installing source NPM dependencies.
          - npm install
      build:
        commands:
          - echo Build started on `date`
          - echo Compiling the Node.js code
          - npm run build
      post_build:
        commands:
          - echo Build completed on `date`
    artifacts:
      files:
        - '**/*'
      discard-paths: no
      base-directory : ./
    ```
  - Now the ARN policy does not include KMS key policy, which you would have to include in the IAM policy. Go to IAM policy, open the policy that is attached with CodePipeline and edit the policy by adding theses new policies.
    ```
    {
    "Effect": "Allow",
    "Action": [
        "kms:Encrypt",
        "kms:DescribeKey",
        "kms:Decrypt"
    ],
    "Resource": "*"
    },
    {
    "Effect": "Allow",
    "Action": [
        "ssm:GetParametersByPath",
        "ssm:GetParameters",
        "ssm:GetParameter"
    ],
    "Resource": "*"
    }
    ```

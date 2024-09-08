# CloudFormation CI/CD Pipeline with GitHub Actions

This project demonstrates the creation of a Continuous Integration/Continuous Deployment (CI/CD) pipeline that validates and deploys CloudFormation test stacks using GitHub Actions. The workflow is triggered by a Pull Request (PR) and ensures that CloudFormation templates are tested and validated before being merged into the main branch.

## Architecture Overview

This workflow utilizes GitHub Actions to automate the validation and testing of AWS CloudFormation stacks on every pull request.

![2024-09-09_00h59_15](https://github.com/user-attachments/assets/640ab093-d0ab-4b93-8fe6-167ba2f715f3)



### Workflow Steps:

1. **GitHub Secrets**:  
   AWS credentials are stored securely in GitHub Secrets.

2. **PR Creation**:  
   The user pushes code and creates a pull request.

3. **GitHub Actions Runner**:  
   A runner checks out the code and sets up AWS credentials using the AWS CLI.

4. **CloudFormation Validation**:  
   The CloudFormation template is validated to ensure correctness.

5. **Test Stack Deployment**:  
   A CloudFormation stack is deployed in AWS (S3 bucket in this case).

6. **PR Comment**:  
   GitHub Actions adds a comment to the PR with the results of the deployment.

7. **Merge PR**:  
   If everything looks good, the PR is merged.

8. **Stack Deletion**:  
   The test stack is deleted automatically after the PR is merged.



## CloudFormation Template

The CloudFormation template defines the creation of an S3 bucket. The bucket is dynamically named based on the environment parameter (test, staging, or production) and includes tagging for the environment.



## GitHub Actions Workflow

The GitHub Actions workflow automates several key tasks during the PR lifecycle:

1. **Trigger**:  
   The workflow is triggered by pull request events, such as when a PR is opened, updated, or reopened, specifically for changes in the `cloudformation/` directory.

2. **AWS Credentials**:  
   GitHub Secrets are used to securely configure AWS credentials to interact with AWS services.

3. **CloudFormation Validation**:  
   The template is validated to ensure it is correctly structured and deployable.

4. **Test Stack Deployment**:  
   A CloudFormation stack (S3 bucket) is deployed in the AWS environment as a test.

5. **PR Comment**:  
   Once the test stack is deployed, a comment is automatically added to the pull request detailing the stack name and status of the deployment.

6. **Cleanup on Merge**:  
   Once the PR is merged, the test CloudFormation stack is automatically deleted to clean up resources.



## Requirements

- **AWS Account**: Ensure you have access to an AWS account.
- **GitHub Secrets**: You need to store your AWS credentials as GitHub Secrets (`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`).
- **CloudFormation Template**: The CloudFormation template must be available in the `cloudformation/` directory.



## Usage

### Set Up GitHub Secrets:

1. In your GitHub repository, go to **Settings -> Secrets -> Actions**.
2. Add `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.

### Push Code:

1. Create a new branch and add your CloudFormation template to the `cloudformation/` directory.
2. Open a pull request.

### Review Pull Request:

- The GitHub Actions workflow will validate and deploy the stack.
- A comment will be added to the pull request with the deployment result.

### Merge PR:

- Once validated, merge the pull request.
- The workflow will delete the test stack after merging.

## Conclusion

This CI/CD pipeline automates the validation and deployment of AWS CloudFormation templates using GitHub Actions. By integrating this pipeline with your pull request workflow, you ensure that changes are tested and validated before being merged into your main branch. This enhances code quality, prevents misconfigurations, and ensures that your infrastructure is consistent and reliable.

   

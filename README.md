# Basic Jenkins Pipeline with Terraform Deployment Using S3

This guide walks through setting up a basic Jenkins pipeline for deploying infrastructure with Terraform and AWS.

## Steps

### 1. Deploy Jenkins
- **Option 1: Locally with Docker**
  - You can deploy Jenkins locally using Docker. This method is simple and quick for local development.
    - Example command:
      ```bash
      docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
      ```
  - Access Jenkins at `http://localhost:8080` and unlock it using the initial password printed in the terminal.

- **Option 2: Deploy on EC2 with a Marketplace AMI**
  - Launch an EC2 instance with a pre-configured Jenkins AMI from the AWS Marketplace.
  - Follow AWS documentation for setting up the instance and accessing Jenkins via the public IP.

### 2. Create an IAM User with Key Pair
- In the AWS Management Console, go to **IAM > Users** and create a new user with programmatic access.
- Generate a key pair for this user and download the `.csv` file containing the access and secret keys.
- Attach appropriate IAM policies to allow Terraform to manage AWS resources (e.g., `AdministratorAccess` for testing purposes).

### 3. Set Up Repository with Basic Terraform Configuration
- Create a Git repository (GitHub, GitLab, etc.) and clone it to your local machine.
- Initialize a basic Terraform configuration

### 4. Modify `Jenkinsfile` with Repo Name
- Create a `Jenkinsfile` in the root of your repository to define the pipeline. 
- Modify the pipeline steps to fit your specific repo name, Terraform configuration, and environment.

### 5. Add AWS Credentials to Jenkins
- Go to **Jenkins > Manage Jenkins > Manage Credentials**.
- Add a new set of credentials for AWS access (`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`).
- Make sure to reference these credentials in your `Jenkinsfile` as shown in the example.

### 6. Create Pipeline in Jenkins
- In Jenkins, go to **New Item**, select **Pipeline**, and provide a name for the job.
- Under **Pipeline Configuration**, point to your repository and specify the location of the `Jenkinsfile`.
- Save the pipeline job.

### 7. Run Pipeline
- Trigger the pipeline manually or set it to trigger on code pushes (via webhooks, GitHub/GitLab integration, etc.).
- Monitor the pipeline execution in Jenkins and confirm that the Terraform steps (init, plan, apply) are executed properly.
- After the pipeline completes, check your AWS S3 bucket and verify the creation of resources.

## Conclusion
You now have a working Jenkins pipeline that automates the deployment of Terraform-managed infrastructure, using S3 as the backend for storing the state. 


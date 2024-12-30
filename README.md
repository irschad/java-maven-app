# Configure Webhook to trigger CI Pipeline automatically on every change

## Overview
This project demonstrates how to configure a GitHub webhook to automatically trigger a Jenkins Continuous Integration (CI) pipeline whenever a code change is pushed to a GitHub repository.

## Key Technologies
- Jenkins
- GitHub
- Git
- Docker
- Java
- Maven

## Project Setup and Configuration

### 1. Install GitHub Plugin in Jenkins
1. In Jenkins, navigate to **Dashboard** > **Manage Jenkins** > **Manage Plugins**.
2. Search for the **GitHub** plugin in the **Available plugins** tab.
3. Select the plugin and click **Install without restart**.
Note: This should be already installed as part of recommended plugins during initial setup. 

### 2. Set Up GitHub Webhook
1. Open your GitHub project repository.
2. Go to **Settings** > **Webhooks** and click **Add webhook**.
3. In the **Payload URL** field, enter the Jenkins webhook URL: `http://<jenkins-ip>:8080/github-webhook/`.
4. Set the **Content type** to **application/json** and choose **Just the push event** under events.
5. Save the webhook.

### 3. Configure Jenkins to Connect with GitHub
1. In Jenkins, go to **Dashboard** > **Manage Jenkins** > **Configure System**.
2. In the **GitHub** section, click **Add GitHub Server**.
3. Enter a name for the connection and paste the GitHub access token.
4. Test the connection and click **Save**.

### 4. Trigger CI Pipeline on GitHub Push
1. In your Jenkins pipeline, go to **Build Triggers** and enable the option **GitHub hook trigger for GITScm polling**.
2. Save the pipeline configuration.

Now, Jenkins will automatically trigger the CI pipeline each time changes are pushed to the connected GitHub repository.

## Configuring Multibranch Pipelines

### 1. Install Multibranch Scan Webhook Trigger Plugin
1. Go to **Dashboard** > **Manage Jenkins** > **Manage Plugins** > **Available plugins**.
2. Search for and install the **Multibranch Scan Webhook Trigger** plugin.

### 2. Set Up Multibranch Pipeline Trigger
1. In the Jenkins multibranch pipeline project, go to **Configure**.
2. Under **Scan Multibranch Pipeline Triggers**, enable **Scan by webhook**.
3. Set a custom trigger token, such as `gittoken`.
4. Save the configuration.

### 3. Configure GitHub Webhook for Multibranch Pipeline
1. In GitHub, go to your repository **Settings** > **Webhooks** and click **Add webhook**.
2. In the **Payload URL**, enter `http://<jenkins-ip>:8080/multibranch-webhook-trigger/invoke?token=gittoken`.
3. Save the webhook.

With this setup, Jenkins will trigger the multibranch pipeline for any code changes pushed to GitHub.

## Summary
This project shows how to integrate Jenkins with GitHub via webhooks, enabling automatic triggers for CI pipeline execution. The setup covers both basic and multibranch pipeline configurations to accommodate various development workflows.

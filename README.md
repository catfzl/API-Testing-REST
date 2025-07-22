> [!Note] API-Automation-Testing-REST
> This repository showcases example automated API testing using industry standard tools and techniques, demonstrating how to effectively test RESTful APIs, ensuring functionality, reliability, and performance.
---
[![Chat in Slack #<slack-channel>](https://img.shields.io/badge/chat-%23<slack--channel>-FF4C00.svg?logo=slack)](
https://<company--domain>.slack.com/archives/CL8MM972P)
[![Code owners](https://img.shields.io/badge/Code%20Owners-%40<company--domain>%2Fidentity--access--management-FF4C00?)](
./CODEOWNERS)

# IAM Automation Testing
This repository houses automated end-to-end (E2E) tests for the services owned by an IAM (Identity and Access Management) team. It integrates with a CI/CD pipeline that automatically runs tests on code pushes and a daily schedule. By reporting status to Slack, and pushing detailed results to TestRail, this offers a comprehensive Postman automation solution; facilitating API testing, performance validation, and streamlined collection execution for robust regression testing and quality assurance.

- [1. Features](#1-features)
  - [1.1. Postman Collection](#11-postman-collection)
  - [1.2. CI/CD Integration](#12-cicd-integration)
  - [1.3. Scheduled Runs](#13-scheduled-runs)
  - [1.4. Slack Notifications](#14-slack-notifications)
  - [1.5. TestRail Integration](#15-testrail-integration)
  - [1.6. HTML Test Reports](#16-html-test-reports)
- [2. Prerequisites](#2-prerequisites)
- [3. Monitoring & Reporting](#3-monitoring--reporting)
  - [3.1. Jira Project](#31-jira-project)
  - [3.2. TestRail](#32-testrail)
- [4. Local Development](#4-local-development)
  - [4.1. Prerequisites (Local)](#41-prerequisites-local)
  - [4.2. Environment Setup](#42-environment-setup)
  - [4.3. Running Tests Locally](#43-running-tests-locally)
  - [4.4. Authoring Automated Tests](#44-authoring-automated-tests)
- [5. CI/CD Pipeline & Automation](#5-cicd-pipeline--automation)
  - [5.1. GitHub Repository Secrets](#51-github-repository-secrets)
  - [5.2. Workflow File & Triggers](#52-workflow-file--triggers)
  - [5.3. Slack Integration](#53-slack-integration)
  - [5.4. TestRail Integration](#54-testrail-integration)
  - [5.5. Accessing CI/CD Reports](#55-accessing-cicd-reports)
- [6. Other Useful Resources](#6-other-useful-resources)
- [7. Troubleshooting](#7-troubleshooting)
- [8. Contributing](#8-contributing)

## 1. Features

### 1.1. Postman Collection
A Postman collection within the <team-specific> Postman Workspace dedicated to Automated API Testing. More specifically, End-to-End tests for IAM owned services.

### 1.2 CI/CD Integration
Tests that are automatically run via GitHub Actions whenever a branch is merged to the `main` branch.

### 1.3 Scheduled Runs
Automated test execution is completed daily for continuous monitoring.

### 1.4 Slack Notifications
Real-time alerting for test run status (Pass/Fail) visibility to a designated Slack channel, <slack-channel> with links to run/detailed reports.

### 1.5 TestRail Integration
Allows for clear mapping of test cases to automated tests. This ensures comprehensive coverage and easy tracking of test results.
Automated upload of detailed test results to <designated-testrail-project-name> TestRail Suite.

### 1.6 HTML Test Reports
HTML Test Reports: HTML reports generated for easy viewing and sharing of test results.

## 2. Prerequisites
Before you begin, ensure you have the following general prerequisites:
- **GitHub Account**: A GitHub account is needed to access the <`repo-name`> repository and contribute to the codebase.
- **Postman**: Ensure you have Postman installed with access to the <team-specific> workspace to run and develop the collections locally. For detailed instructions of installing Postman and gaining access to the workspace, please refer to the <specific-team-documentation> article in Confluence.
- **Slack App**: For receiving notifications (for CI/CD setup).
- **TestRail Access**: <company-name>'s test case management tool used to manage, track, and organize testing efforts. Access to the <designated-testrail-project-name> TestRail Suite for viewing test results. You can find detailed instructions on how to access TestRail in the <specific-access-documentation> in Confluence.
- **<password-manager> Account**: Access to <password-manager>, <company-name>'s Password Manager, and the `IAM Test Automation` vault in <password-manager>. This is needed for managing secrets, credentials, and variables used in the tests. The application can be requested by creating a ticket through <specific-request-portal>.

## 3. Monitoring & Reporting
This section outlines how the test results contribute to overall system monitoring and where to find related information, including Jira, TestRail, and other monitoring tools.

### 3.1. Jira Project
Automation work can be found in the <team-name> Jira Project, with dedicated quarterly epics. Each epic will contain tickets related to IAM QA automation efforts. (e.g. Planned automation, bugs, etc.)

### 3.2. TestRail
Every workflow and endpoint within the `IAM Automated Smoke Tests` collection of Postman is mapped 1:1 to a TestRail case in the <designated-testrail-project-name> in TestRail. Whenever a run agains the `main` branch is triggered via GitHub Actions, results are reported to the TestRail suite. When the `IAM Test Automation` vault is shared with you in <password-manager> you will be able to find the credentials for the user account dedicated to IAM automation.

## 4. Local Development
This section provides instructions for setting up, authoring, and running the automated Postman tests on your local development machine.

### 4.1. Prerequisites (Local)
- **Node.js & npm**: Ensure you have Node.js and npm installed on your local machine. You can download them from Node.js official website.
- **Newman CLI**: This is the command-line collection runner for Postman. Install Newman globally using npm:
  ```bash
  npm install -g newman
  npm install -g newman-reporter-htmlextra
  ```

### 4.2. Environment Setup

This covers getting the test environment ready, including cloning the repo and configuring test data/secrets.

#### 4.2.1. Clone the Repository:

```bash
cd ~/path/to/repos
git clone <iam-automation-testing-repo-url>
```

#### 4.2.2. Postman Collection & Environment

The Postman collection and environment files are located in the `postman-tests/` directory of the repository.

  - **Collection**: Contains the automated tests for IAM services. Within the Postman UI, this collection is titled `IAM Automation Smoke Tests`.
      - `postman-tests/iamAutomationSmokeTests.postman_collection.json`
  - **Environment**: Contains the environment variables and configurations needed to run the tests.
      - `postman-tests/staging.postman_environment.json`
        In the [Prerequisites](https://www.google.com/search?q=%232-prerequisites) section, you should have received access to the `IAM Test Automation` vault in <password-manager>. This will also contain sensitive variables, such as OAuth client ID and secrets used for our various users. While the secrets are saved in the repository for the CI/CD integration, you will need to set up the following environment variables in your local Postman environment:
  - `exampleSmokeId`: The OAuth client ID for Workflows that require a machine client token.
  - `exampleSmokeSecret`: The OAuth client secret for Workflows that require a machine client token.

> Note: Should you create or update a new variable, please add it to the `IAM Test Automation` vault in <password-manager>, in addition to other locations mentioned in this article.

#### 4.3 Running Tests Locally

You can run the tests directly from your command line, or by using the Postman Desktop Client (application UI).

##### 4.3.1. Using Newman CLI

To run the tests using Newman, navigate to the `postman-tests/` directory by using the following command:

```bash
cd ~/path/to/repos/<iam-automation-testing-repo-url>/postman-tests
```

Then execute the tests with the following:

```bash
newman run iamAutomationSmokeTests.postman_collection.json \
  --environment staging.postman_environment.json \
  --env-var="exampleSmokeId=YOUR_LOCAL_EXAMPLE_SMOKE_ID" \
  --env-var="exampleSmokeSecret=YOUR_LOCAL_EXAMPLE_SMOKE_SECRET" \
  --reporters cli,htmlextra,junit \
  --reporter-htmlextra-export newman/report.html \
  --reporter-junit-export newman/junit-report.xml
```

  - Replace `YOUR_LOCAL_EXAMPLE_SMOKE_ID` and `YOUR_LOCAL_EXAMPLE_SMOKE_SECRET` with the actual values from your <password-manager> vault.
  - The `--reporters` flag specifies the reporters to use. In this case, we are using `cli`, `htmlextra`, and `junit` reporters.

#### 4.3.2. Using Postman UI

To run the tests using the Postman UI first ensure you are in the <team-specific> Workspace. You will then need to set the local environment variables for `exampleSmokeId`, `exampleSmokeSecret`, in your Postman `staging` environment. Only update the current value. Once you have set the environment variables, you can run the tests by following these steps:

1.  Select the `IAM Automation Smoke Tests` collection.
2.  Select the Overflow button and click on `Run`.
3.  All workflows within the colletion are automatically selected. If you want to run a specific workflow, you can uncheck the ones you do not want to run.
4.  Click on the `Run IAM Automation Smoke Tests` button.
5.  Once the tests are complete, you can view the results in the Postman UI.
6.  If there are any failures, you can click on the failed test to view the details and debug the issue. For more detailed debugging, you can select Console to view the Request and Response details for each endpoint.

### 4.4. Authoring Automated Tests

This section provides guidelines for creating and maintaining automated tests within this repository. You can create new workflows and tests using the Postman UI (Desktop Client).

#### 4.4.1. Test Structure

The tests are organized within the `postman-tests/` directory. Each test is structured as follows:

  - **Collection**: Contains the Postman collection file (`iamAutomationSmokeTests.postman_collection.json`) that defines the tests, and is where you will author new tests.
      - The collection is then organized into folders or `Worfklows`.
  - **Workflows**: Each workflow within the collection represents a specific e2e workflow or scenario being tested, and consists of multiple endpoints. These workflows are grouped logically based on the features or services they test, and should be listed in the corresponding JIRA ticket.
      - Each Workflow can be customised with its own Authorization and scripts, allowing for environment setup and execution, that is specific to that workflow.
          - *Example Pre-request scripts setting an environment variable for the entire workflow*:

```javascript
pm.environment.set("locationGuid", "<locationGuid>");
pm.environment.set("emailSuffix", "<company-domain.com")
```

*Setting the email domain is useful for flows that require calling an endpoint with a mandatory email field when creating a user/ customer.*

> To *create a new workflow*, you can select the IAM Automation Smoke Tests Collection, select the overflow button and click on `Add Folder`.

  - **Test Cases**: Each workflow contains individual test cases that validate specific functionalities or scenarios. These test cases are defined using Postman's scripting capabilities, allowing for assertions and validations against the API responses.
      - **Assertions**: Each test case includes assertions to verify the expected behavior of the API. These assertions are written in JavaScript using Postman's `pm` library, allowing for validation of API responses.
      - **Environment Variables**: The tests utilize environment variables to manage configuration settings, such as API endpoints, authentication tokens, and other parameters. This allows for easy customization and reuse of tests across different environments as we scale our automation efforts (e.g., development, staging, production).
      - **Pre-request Scripts**: Each test case should include pre-request scripts to set up any necessary conditions or data before the test is executed. This allows for dynamic test execution based on the current state of the system or environment.
      - **Test (Post-response) Scripts**: Each test case includes test scripts that run after the API request is executed. These scripts should validate the response data, check for errors, and perform any necessary cleanup or setup for subsequent tests. *Depending on the version of Postman you have, this may be a tab called `Tests` or `Test Scripts`, OR `Post-response Scripts` within the Scripts tab.*
      - **Logging**: Use `console.log()` statements within the pre-request and/or test (post-response) scripts to log important information, such as request and response data, for debugging purposes. This can help identify issues during test execution and provide insights into the test flow.

#### 4.4.2. Test Naming Conventions

  - Use descriptive names for each test to clearly indicate its purpose.
  - Follow a consistent naming convention, such as `workflow number - <TestFeature> - <Scenario>`, to ensure clarity and maintainability. Each endpiint within the workflow should also be named descriptively, such as `workflow number.x - <endpoint>`.

#### 4.4.3. Test Documentation

  - Each Workflow should include documentation to explain its purpose, endpoints called, expected outcomes, and any prerequisites.
  - Use the `Overview` field in Workflow Folder to provide detailed information about each test case.

#### 4.4.4. Test Data Management

  - We should use environment variables to manage test data and secrets, ensuring sensitive information is not hard-coded in the tests.
  - Store test data in a separate file or database if needed, and reference it in the tests using environment variables or Postman data files.
  - Ensure that test data is representative of real-world scenarios to provide meaningful test results.
  - Use the `Pre-request Script` and `Tests` tabs in Postman to set up and validate test data as needed.
      - For example, you can use the `Pre-request Script` tab to set up any necessary headers, authentication tokens, or  before running the test, and the `Tests/Post-response script` to validate the response data against expected values.
  - Ensure that test data is cleaned up after the test run to avoid interference with subsequent tests.
  - Use the `Tests` tab to perform assertions on the response data, such as checking for specific values or status codes.
  - Use the `pm.expect()` function to perform assertions on the response data, such as checking for specific values or status codes.
      - *For example, you can use the following code to check if the response status code is 200*:

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

  - Use the `pm.response.json()` function to parse the response data as JSON and perform assertions on specific fields.
      - *For example, you can use the following code to check if the response contains a specific field*:

```javascript
pm.test("Response contains field", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("fieldName");
});
```

  - Save changes regularly to ensure test files stay up-to-date. (e.g., `staging.postman_environment.json`for new test variables and `iamAutomationSmokeTests.postman_collection.json` for new tests or workflows).

#### 4.4.5 Verifying Locally

  - After creating new tests or updating existing, always run them locally using the Postman UI or Newman CLI to ensure they work as expected.
  - Check the test results in the Postman UI or the Newman CLI output to verify that all assertions pass and there are no errors.
  - If any tests fail, debug the issues by checking the request and response details in the Postman Console or the Newman CLI output. Add logging statements as needed to help identify the root cause of the failure in the pre-request and/or post-request scripts.
  - If you encounter issues, refer to the [Troubleshooting](https://www.google.com/search?q=%237-troubleshooting) section for guidance on common problems and solutions.

#### 4.4.6 Exporting for Automation

  - Once you have verified your tests are passing locally, you will need to **export the updated** Postman collection and environment files **back into the** `postman-tests/` **directory** in this repo by doing the following:

1.  **Collection**: Right-click on the `IAM Automation Smoke Tests` collection in the Postman UI and select `Export`. Save the file as `iamAutomationSmokeTests.postman_collection.json`.
2.  **Environment**: Right-click on the `staging` environment in the Postman UI and select `Export`. Save the file as `staging.postman_environment.json`.
3.  **Copy the files** to the `postman-tests/` directory in your local clone of the <`repo-name`> repository:


```bash
cp ~/Downloads/iamAutomationSmokeTests.postman_collection.json ~/path/to/repo/<repo-name>/postman-tests/
```

```bash
cp ~/Downloads/staging.postman_environment.json ~/path/to/repo/<repo-name>/postman-tests/
```

4.  **Commit and Push**: Commit the changes to your local repository and push them to the remote repository.
5.  **Verify Automation Run**: After pushing the changes, verify that the CI/CD pipeline runs successfully and that the new tests are executed as part of the automated workflow. This should be completed after [Github Secrets](https://www.google.com/search?q=%2351-github-repository-secrets) are set up, and the workflow file is configured correctly. Steps to complete this are lsted in [Manual Trigger](https://www.google.com/search?q=%2352-workflow-file--triggers).

### 5. CI/CD Pipeline & Automation

This section provides an overview of the CI/CD pipeline setup, including GitHub repository secrets, workflow files, triggers, and integration with Slack and TestRail.

#### 5.1. GitHub Repository Secrets

For the CI/CD pipeline to function securely, any newly created, or updated secrets must be configured in the `<repo-name>` repository. These secrets are required for the CI/CD pipeline to run successfully. These secrets are used to authenticate with external services, such as TestRail and Slack, and to manage sensitive information like API keys and OAuth credentials.

1.  Go to the `<repo-name>` repository on GitHub.
2.  Navigate to `Settings` \>`Secrets and variables` \> `Actions`.
3.  Click on `New repository secret` to add a new secret, where the name of the secret is the key and the value is the secret itself. The key should be in all-caps to follow the typical convention for contants of environment variables.

> *Examples of existing secrets include*:
>
>   - `EXAMPLE_SMOKE_ID`: The OAuth machine client ID for the IAM Smoke tests.
>   - `EXAMPLE_SMOKE_SECRET`: The OAuth machine client secret for the IAM Smoke tests.
>   - `TESTRAIL_USERNAME`: The username for the TestRail account used to upload test results.
>   - `TESTRAIL_API_KEY`: The API key for the TestRail account used to upload test results.
>   - `TESTRAIL_URL`: The URL for the TestRail instance used to upload test results.
>   - `TESTRAIL_PROJECT_NAME`: The name of the TestRail project where test results will be uploaded.
>   - `SLACK_WEBHOOK_URL`: The webhook URL for the Slack channel where test results will be posted.

4.  Add the required secret to the `.github/workflows/github-actions-cicd-pipeline.yml` file under Run Postman tests job.

#### 5.2. Workflow File & Triggers

The CI/CD pipeline is defined in the `.github/workflows/github-actions-cicd-pipeline.yml` file.

This file contains the configuration for the GitHub Actions workflow that checks out the code, installs dependencies, runs the automated tests, integrates & uploads results to TestRail and Slack.

The workflow is configured to run automatically:

  - **On Push**: Whenever code is pushed to the `main` branch, the workflow will be triggered.
  - **Daily Scheduled Runs**: The workflow is also set to run daily at 7:00 AM UTC.
  - **Manual Trigger**: The workflow can be manually triggered from the GitHub Actions tab in the repository. This should be completed, with tests passing before your JIRA ticket is submitted for code review.

1.  Go to "Actions" tab in the `<repo-name> ` repository on GitHub.
2.  Select "IAM Postman API Automated Tests" from the `Workflows` list.
3.  Click "Run workflow" on the right sidebar.
4.  In the dialog, you can select the target\_branch to run the tests against under the `Use worfklow from` dropdown.

#### 5.3. Slack Integration

The CI/CD pipeline integrates with Slack to provide real-time notifications about the status of test runs. This integration is configured in the `.github/workflows/github-actions-cicd-pipeline.yml` file, and uses a Slack webhook URL stored as a GitHub secret (`SLACK_WEBHOOK_URL`).
The workflow sends notifications to Slack using the slackapi/slack-github-action. No updates should be needed for this integration, as it is already configured to send notifications to the <slack-channel> channel in the <comapnay-name> Slack workspace.

  - **Webhook**: Ensure `SLACK_WEBHOOK_URL` is correctly set as a GitHub secret.
  - **Message Format**: The Slack message provides the test status, repository/branch details, a link to the GitHub Actions run, and a link to download the HTML test report artifact.
  - **Branch Filtering**: Slack alerts are currently configured to *only* trigger when the workflow runs *against the `main` branch*.

> Note: To view the configuration for setting up the Slack integration, determining the Test Run Status and posting the Slack notification, refer to the Slack-related jobs section in the `.github/workflows/github-actions-cicd-pipeline.yml` file.

#### 5.4. TestRail Integration

The CI/CD pipeline integrates with TestRail to upload test results automatically. This integration is configured in the `.github/workflows/github-actions-cicd-pipeline.yml` file, and uses TestRail credentials stored as GitHub secrets using the `trcli` (TestRail Command Line Interface).
No updates should be needed for this integration, as it is already configured to upload test results to the `<designated-testrail-project-name>` TestRail suite.

  - **Credentials**: Ensure `TESTRAIL_USERNAME`, `TESTRAIL_API_KEY`, and `TESTRAIL_URL` are correctly set as GitHub secrets.
  - **Suite ID**: Suite ID: The `trcli` command is configured to upload results to a specific TestRail suite using `--suite-id <suite-id>`.

> Note: To view the configuration for setting up the TestRail integration, installing the TestRail CLI, and Uploading test results to TestRail, refer to the TestRail-related jobs section in the `.github/workflows/github-actions-cicd-pipeline.yml` file.

#### 5.5. Accessing CI/CD Reports

After the CI/CD pipeline runs, you can access the test reports and results in the following ways:

  - **GitHub Actions Run**: Click on any workflow run in the "Actions" tab to see detailed logs for each step.
  - **HTML Test Report**: After a workflow run completes, you can download the postman-report artifact from the run summary page. This contains the detailed HTML report generated by Newman. A direct link is also provided in the Slack notification.
  - **TestRail**: Navigate to the <designated-testrail-project-name>  Project wihtin the <testRail-suite> Suite (<suite-ID>). You will find new Test Runs created with titles like "IAM Automated Postman Tests - main Run XXXXXX".
  - **Slack**: Test status notifications are posted to your configured Slack channel.

## 6. Other Useful Resources

  - Postman Test Script Examples
  - How to Write and Automate API Tests in Postman with Proven Strategies
  - Newman Documentation
  - GitHub Actions Documentation
  - TestRail Documentation
  - Automatic Postman Testing Examples
  - Example JIRA Automation Epic for Project

## 7. Troubleshooting

This section provides solutions to common issues encountered during local development, CI/CD pipeline execution, and test runs.

### 7.1. GitHub Actions Issues:

  - `Error: Process completed with exit code 1.` during automation run with GitHub Actions:
      - This error indicates that one or more tests have failed. Check the logs in the GitHub Actions run to identify which tests failed and why.

### 7.2. Debugging Tests

When tests are failing during development, or you need more insight into their execution, follow these steps:

1.  **Run Tests Locally First**:
    Always begin by running the tests on your local machine using Newman (as described in [4.3. Running Tests Locally](https://www.google.com/search?q=%2343-running-tests-locally)). This provides immediate feedback and a faster debugging cycle than waiting for CI/CD.
2.  **Check Postman Console**:
    If a test is consistently failing, try to reproduce the exact request and its conditions directly within the Postman Desktop client. This allows you to step through assertions, inspect responses, and manually tweak parameters.
      - Use the Postman Console to view request and response details, including headers, body, and status codes. This can help identify issues with the API calls.
      - Open the console by clicking on the "Console" button at the bottom left of the Postman UI.
3.  **Add Logging in Postman Scripts**:
    You can insert console.log() statements directly into your Postman Pre-request and Test(Post-Response) scripts to print variable values, response data, or execution flow markers. This is particularly useful when a workflow requires getting and setting variable across multiple requests in a workflow.

> *Example of logging in a Postman Pre-request script*:
>
> ```javascript
> // Debugging
> console.log("Pre-request (Add access with job):");
> console.log("  userGuid:", userGuid);
> console.log("  requesterUserGuid:", requesterUserGuid);
> ```

> *Example of logging in a Postman Post-response script*:
>
> ```javascript
> //debugging
> console.log("Retrieved User GUID: ", retrievedGuid);
> console.log("Expected User GUID: ", expectedGuid);
> ```

4.  **Viewing Logs**: When you run the collection in the Postman Desktop CLient, Newman locally, or in CI/CD, these console.log() outputs will be visible in the terminal/workflow logs, and can help you trace the execution flow and identify where things might be going wrong.
5.  **Check Environment Variables/Secrets**: Ensure that the environment variables (especially sensitive ones like `exampleSmokeId`, `exampleSmokeSecret`) are correctly populated and accessible, both locally and in the CI/CD environment (via GitHub Secrets).

## 8. Contributing
Feel free to contribute to this test suite. Please follow the existing coding standards and submit Pull Requests for review.

# Chaos Onboarding Pipeline Documentation

## Overview
The `chaos-onboarding-pipeline` is designed to onboard chaos in a structured and automated manner. The pipeline consists of multiple stages and steps that deploy, configure, and validate the required components for chaos engineering in a Kubernetes environment.

## Pipeline Details

### Pipeline Configuration
- **Name**: chaos-onboarding-pipeline
- **Identifier**: chaosonboardingpipeline
- **Project Identifier**: ChaosDev
- **Organization Identifier**: default
- **Tags**: None

### Stages and Steps

#### Stage: Onboard Chaos
- **Identifier**: onboard_chaos
- **Type**: Custom
- **Description**: This stage encompasses several steps to deploy and configure the necessary components for chaos engineering.

  1. **Step: Create Onboard Util Pod**
     - Executes a shell script to create a utility pod for onboarding.
     - Validates the necessary environment variables before proceeding.
     - Deploys a Kubernetes pod and waits until it's ready.
     - Sets up AWS credentials within the pod for further AWS related actions.

  2. **Step: Create Project**
     - Executes a command to create a new project using the onboard utility.

  3. **Step: Create App Dev and Staging Chaos Infrastructure**
     - Executes commands to create chaos infrastructure for both development and staging environments.

  4. **Step: Annotate App Dev and Staging Infra With Role ARN**
     - Executes commands to annotate the chaos infrastructures with AWS IAM role ARN for permissions.

  5. **Step: Create Experiments**
     - Executes a script to convert hub templates to JSON and create chaos experiments.

  6. **Step: Delete Onboard Util Pod**
     - Deletes the onboard utility pod to clean up the resources.

### Environment Variables

| Variable Name                      | Description                                                   | Type                         | Default Value                 |
|------------------------------------|---------------------------------------------------------------|------------------------------|-------------------------------|
| HARNESS_API_KEY                    | Provide the harness api token.                                | Secret                       | harness_pat_token_secret      |
| ORGANISATION_ID                    | Provide the target organisation id.                           | String                       |                               |
| ACCOUNT_ID                         | Provide the target account id.                                 | String                       |                               |
| PROJECT_ID                         | Provide the target project id to be created by the pipeline and used further. | String (Runtime Input)       | ChaosDev                      |
| INFRA_NAMESPACE_DEV                | Infra namespace for dev.                                       | String                       | app1-dev                      |
| INFRA_NAME_DEV                     | Infra name for dev.                                            | String                       | app1-dev                      |
| INFRA_NAME_STAGING                 | Infra name for staging.                                        | String                       | app1-stg                      |
| INFRA_NAMESPACE_STAGING            | Infra namespace for staging.                                   | String                       | app1-stg                      |
| ONBOARDING_NAMESPACE               | Onboarding namespace.                                          | String                       | default                       |
| ONBOARDING_SERVICE_ACCOUNT_NAME    | Onboarding service account name.                               | String                       | chaos-onboard-util            |
| AWS_ACCESS_KEY_ID                  | The access key id for the AWS account.                        | Secret                       | Should be created via secret. |
| AWS_SECRET_ACCESS_KEY              | The secret access key for the AWS account.                     | Secret                       | Should be created via secret. |
| CHAOSHUB_NAME                      | Name of the chaoshub that has the target experiment.          | String (Runtime Input)       | Enterprise ChaosHub           |
| EXPERIMENT_NAME                    | Target experiment name from the given chaoshub.               | String (Runtime Input)       | nginx-pod-delete              |

The table above provides the description for each environment variable, its type, and default value where applicable. Please note that some of the variables require a runtime input or should be created as secrets prior to executing the pipeline. You can modify any String variable to Runtime Variable as per the requirement.

## Conclusion
The `chaos-onboarding-pipeline` is structured to facilitate the onboarding process of harness chaos engineering within a Kubernetes environment. Through the defined stages and steps, the pipeline automates the deployment, configuration, and validation of necessary components, ensuring a streamlined onboarding process.

`gh-actions-example1.yaml`

# Overview
This GitHub actions workflow file has been written to build cloud resources with Terraform. It is ready to go and fundamentally only requires one edit to make it work which is the target working directory of the Terraform code against which it will work.

**TL;DR**
> Ensure the workflow is located in your own GitHub repository

> Edit the `working-directory` path to match your code working directory

> Execute the workflow by either a  `push` `pull request` or `manually`

## What the workflow does

**Triggers**

There are multiple triggers for this workflow to execute. The automatic execution occurs on either a `push` or `pull request`. You can choose to run the workflow manually and then choose Terraform `Apply` or `Destroy`.


**Working directory**

The workflow expects Terraform code to be in the given working directory. This workflow has succeeded when the working directory is setup as follows. So your working directory value woud be `codefolder1/` if using the structure exactly as below.

```
.
{GitHub account}
|_{GitHub repository}
|__/codefolder1
|   |main.tf
|   |providers.tf
|   |variables.tf
|   |terraform.tfvars
```

**Runner**

This workflow relies on using GitHub provisioned runners. It declares a standard Ubuntu version.

**Authentication**

GitHub actions secrets need to be populated with the `ARM_*` environment variables that has the service principal credentials with permissions required to CRUD cloud resources.

```
ARM_CLIENT_ID: ${{secrets.ARM_CLIENT_ID}}
ARM_CLIENT_SECRET: ${{secrets.ARM_CLIENT_SECRET}}
ARM_TENANT_ID: ${{secrets.ARM_TENANT_ID}}
ARM_SUBSCRIPTION_ID: ${{secrets.ARM_SUBSCRIPTION_ID}}
``` 

**Terraform actions**

The workflow processes the following Terraform actions:

**If triggered automatically by a `push` or `pull reqeust`**

1. Checkout the current configuration from the working-directory
2. Installs the Terraform CLI used in the GitHub action workflow
3. Checks whether the configuration has been properly formatted. If the configuration isn't properly formatted this step will produce an error.
4. Initializes the configuration used in the GitHub action workflow
5. Validates the configuration used in the GitHub action workflow
6. Generates a Terraform plan
7. **ONLY if a pull request** adds a comment to the pull request with the results of the format, init and plan steps.
8. Returns whether a plan was successfully generated or not. This step highlights whenever a plan fails because the "Terraform Plan" step continues on error
9. Applies the configuration

**If triggered `manually`**
It runs the same steps as the automated process aside from writing the `plan` to the comments of the `pull request`.

Depending on the choice you select either `terrform apply` or `terraform destroy` commands will be executed.

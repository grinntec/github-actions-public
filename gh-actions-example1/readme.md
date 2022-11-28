`gh-actions-example1.yaml`

# Overview
This GitHub actions workflow file has been written to use building cloud resources with Terraform. It is ready to go and fundamentally only requires one edit to make it work which is the target working directory of the Terraform code against which it will work.

**TL;DR**
> Ensure the workflow is located in your own GitHub repository

> Edit the `working-directory` path to match your code working directory

> Execute the workflow by either a  `push` `pull request` or `manually`

## What the workflow does

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

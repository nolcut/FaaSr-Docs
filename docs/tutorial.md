# Tutorial

This document guides you through a simple tutorial that uses GitHub Actions and a free S3 data store (Minio Play). The pre-requisite for this tutorial is a GitHub account.

## Configure your FaaSr-workflow repository

This is a one-time step you go through to set up your [workflow repository] to host all your workflows, including the tutorial.

- Navigate to the [FaaSr organization workflow repo](https://github.com/FaaSr/FaaSr-workflow)
- Fork the repository to your own GitHub account, keeping the FaaSr-workflow name
- In your forked repository, click on _Actions_ and click on _I understand my workflows, go ahead and enable them_ to allow FaaSr register/invoke actions to execute

## Configure your GitHub PAT

You need a personal access token in your repository secrets to run this tutorial. 

Follow the steps outlined in the [credentials] documentation to obtain your PAT. Copy this PAT so you can paste it as a secret in the next step

## Configure your repository secrets

Before you can register and invoke workflows, you need to create secrets storing credentials for the cloud providers you will use. The following assumes that you already have obtained [cloud credentials] for those.

- In the _FaaSr-workflow_ repo you just forked, click on the _Settings_ tab (top of the page, to the right)
- Scroll down; on the left pane, click on the pull-down _Secrets and variables_ and select _Actions_
- Click on the green _New repository secret_ to enter a new secret
- Enter the proper _Name_ for each of the three secrets below (one for GitHub actions, two for Minio Play) and past the secret itself in the _Secret_ text box:
- Click on _Add secret_ and add a secret named `GH_PAT`, pasting your GitHub PAT created in the previous step
- Click on _Add secret_ and add a secret named `S3_ACCESSKEY`, pasting the following text: `Q3AM3UQ867SPQQA43P2F`
- Click on _Add secret_ and add a secret named `S3_SECRETKEY`, pasting the following text: `zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG`

## Edit the tutorial JSON file

The tutorial.json file comes by default in the repository you forked; however, you still need to configure it with your GitHub account name. This can be done in either of two ways:

### Option 1: Edit tutorial.json in GitHub

- Edit the tutorial, json file in GitHub
- Search for _myusername_, and replace that with your GitHub account name
- Commit the file

### Option 2: Edit tutorial.json in the Web UI

- Browse to the [FaaSr Workflow Builder Web UI]
- Click on Upload (top left)
- To import the tutorial file from GitHub, enter in text box: `https://github.com/FaaSr/FaaSr-workflow/blob/main/tutorial.json`
- Click on _Edit Compute Servers_, click on _GH_, replace the UserName with your GitHub account name
- Download tutorial.json to your computer
- Upload tutorial.json to your repository (replacing the original file)

## Register the workflow

- You first need to [register the workflow] before it can be invoked
- Click on _Actions_
- Click on `(FAASR REGISTER)` (left)
- Click on the `Run workflow` drop-down; enter `tutorial.json` and click on `Run workflow`
- This will take a few seconds to complete; wait until the action completes before proceeding

## Invoke the workflow

- After register, you can [invoke the workflow] 
- Click on _Actions_
- Click on `(FAASR INVOKE)` (left)
- Click on the `Run workflow` drop-down; enter `tutorial.json` and click on `Run workflow`
- This will take a few seconds to complete; wait until the action completes before proceeding

## Check outputs

The workflow outputs are stored in the Minio Play S3 bucket. There are different ways you can access it, with different S3 clients (e.g. Minio client); we will use the Minio Play console in this tutorial:

- Browse to [minio play web UI](https://play.min.io:9443/login)
- For user name, enter `Q3AM3UQ867SPQQA43P2F`
- For password, enter `zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG`
- Browse to faasr/tutorial to see the output files

## Another example

The tutorial.json workflow is based on two R functions (start, compute_sum). Another example is found in tutorialRpy.json that uses an R function (start) followed by a Python function (compute_sum). If you'd like to test this out, repeat the edit, register, and invoke workflow steps as above for this workflow 


[workflow repository]: workflow_repo.md
[credentials]: credentials.md
[FaaSr Workflow Builder Web UI]: workflows.md
[register the workflow]: register_workflow.md
[invoke the workflow]: invoke_workflow.md

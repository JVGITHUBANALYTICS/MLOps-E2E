# MLOps End to End Workshop

https://github.com/davew-msft/MLOps-E2E

## Branches

There are multiple branches of this workshop

* `master` is currently set to `gh`
* `azdo` is the original version, using Azure DevOps
* `gh` has github actions instructions vs AzDO instructions


## What Technologies are Covered

* Databricks (dbx)
* Azure Machine Learning Service (AMLS)
* Azure Container Instances (ACI)
* Azure Kubernetes Service (AKS)
* Azure DevOps (AzDO) or GitHub (and gh actions)
* JupyterLab Notebooks using vscode and AMLS Compute targets

## Target audience

-   Data Scientists
-   App Developers
-   AI Engineers
-   DevOps Engineers 
-   Anyone wanting to learn to think like a Data Scientist and take their analytics to the next level

The solution will look something like this:  

![End-to-end Custom AI Solution](images/e2e.png)

## Business Case Background

Our company sells bikes.  We have data about who does and does not buy bikes.  We'd like to use that data to build a predictive model to determine who will buy bikes in the future.  

On Day 2 of the workshop we'll look at the second part of the business use case...we want to look at our specifications documents and determine if they are compliant or not with bicycle industry regulations (work with me on this use case).  We are going to build an MLOps solution that uses Deep Learning against the specifications text to determine if we are in compliance.  

## Workshop Objectives

In this workshop, you will learn how to:

* use the az cli to deploy resources to Azure
* setup and configure Azure Databricks for analytics
* setup and configure Azure ML Services to integrate your data science work into your DevOps pipelines.  
* *Think Like a Data Scientist*


## Workshop Agenda

1. [Lab 1:  Setup the resources needed for this workshop](Lab1/README.md)
1. [Lab 2:  Learn about Azure Machine Learning Services](Lab2/README.md)
1. [Lab 2a: Getting Databricks Ready for DevOps/MLOps](Lab2a/README.md)
1. [Lab 3:  Build and Deploy an ML Model](Lab3/README.md)  

Alternate Labs:  

1. Load data to ADLS2 with ADF and Databricks



## Day 2 Agenda - DevOps/MLOps in Depth

We are going to build the DL/NLP model to look at their specification documents.  We'll use Jupyter notebooks, AMLS, and AzDO to manage the MLOps pipelines.  This will build on Day 1 by adding in AzDO Pipelines concepts.  We'll determine how to retrieve the best model, package it with a WebApp, and deploy an inferencing web service.  Then we'll figure out how to monitor the model's performance after it is deployed (on AKS).  Our model will be deployed as ONNX format, which means it can be run on the Edge or anywhere else.  

We are going to build something that looks similar to this:  

![stuffs](images/architecture-overview.png 'Solution Architecture')

The overall approach used in this lab is to orchestrate continuous integration and continuous delivery Azure Pipelines from Azure DevOps. These pipelines are triggered by changes to artifacts that describe a machine learning pipeline, that is created with the Azure Machine Learning SDK. In the lab, you make a change to the model training script that executes the Azure Pipelines Build Pipeline, which trains the model and creates the container image. Then this triggers an Azure Pipelines Release pipeline that deploys the model as a web service to AKS, by using the Docker image that was created in the Build pipeline. Once in production, the scoring web service is monitored using a combination of Application Insights and Azure Storage.

**Day 2 has only a few dependencies on Day 1 workshop.  Make sure you run Lab 1 above and you should be fine**

These labs can be divided between data scientists and DevOps engineers.  


These tasks are geared toward data scientists:  

1. [Lab10:  Setup](Lab10/README.md)
1. [Lab11:  Create a Classifier Model](Lab11/README.md)
1. [Lab12:  Register the Model](Lab12/README.md)

We can now do our MLOps/DevOps processes using either Azure DevOps Pipelines or GitHub Actions.  

### Azure DevOps 

These tasks are geared toward **Azure DevOps** engineers and can be done in parallel with the tasks above, if desired.  If you are using **GitHub Actions** please see Labs 30-34.  

1. [Lab20:  Setup AzDO](./Lab20/README.md)

This task should be done by both the data scientist and DevOps engineer **when using Azure DevOps**:  

1. [Lab21:  Setup and Run a Build Pipeline](Lab21/README.md)
1. [Lab22:  Setup and Run a Release Pipeline](Lab22/README.md)
1. [Lab23:  Test Our Pipelines](Lab23/README.md)
1. [Lab24:  Monitoring Model Performance](Lab24/README.md)

### GitHub Actions

These tasks are geared toward **GitHub Actions** engineers and can be done in parallel with the tasks above, if desired.  If you are using **Azure DevOps** please see Labs 20-24.  

1. [Lab30: Setup GitHub](./Lab20/README-gh.md):  this is an alternate lab if you'd rather use github for git repos and CI/CD pipelines

This task should be done by both the data scientist and DevOps engineer **when using GitHub Actions**:  

**TODO:  these labs are wip**

1. [Lab31:  Setup and Run a Build Workflow](./Lab21/README-gh.md)
1. [Lab32:  Setup and Run a Release Pipeline](Lab22/README-gh.md)
1. [Lab33:  Test Our Pipelines](Lab23/README-gh.md)
1. [Lab34:  Monitoring Model Performance](Lab24/README-gh.md)

## AutoML Labs

These labs aren't specific to automl but they build upon each other.  In these labs we'll look at employee attrition using a dataset provided by IBM.  

1. [Lab40: Using Datasets and Datastores in AMLS](./Lab40/README.md):  we'll first get the data into a dataset and explore the data
1. [Lab41: Automated Machine Learning (automl)](./Lab41/README.md):  we'll use the IBM dataset to look at the causes of employee attrition, using the AMLS GUI.  
1. [Lab42: automl from a python notebook](./samples/automl-forecast-model.ipynb) :  We will look at running automl from within a python notebook using automl API calls.  We'll forecast energy demand using NYCs open dataset.  **Please see the [sample notebooks area](./samples/README.md) for other approaches using ARIMA and deep learning.**

## Other Labs

1. [Lab80: Batch inferencing](./samples/batch-inferencing.ipynb) :  generally most ML models are deployed for real-time inferencing and therefore are deployed on something like AKS as a container.  But this pattern doesn't work well for batch inferencing.  In this notebook we look at one possible pattern for batch inferencing by leveraging AMLS Pipelines feature. 
1. [Lab85: Batch Scoring Videos Using Deep Learning Models With Azure Machine Learning](./Lab85/README.md) 
  * demonstrates batch inferencing using NNs by doing _neural style transfer_ to an uploaded video.  
  * Upload a video file to storage.
  * The video file will trigger Logic App to send a request to the AML pipeline published endpoint.
  * The pipeline will then process the video, apply style transfer with MPI, and postprocess the video.
The output will be saved back to blob storage once the pipeline is completed.
  * _we can also do this using AKS_
1. [Lab90: Time Series Analysis](./Lab90/README.md) :  we specifically look at time series analytics in these labs with a focus on how AMLS can help.  


## Kubeflow Labs

MLOps currently has very few industry-wide best practices to improve time-to-market.  Obviously, we like MLOps using AMLS, but Kubeflow is an excellent alternative that we can integrate into AMLS.  We'll build a solution using Kubeflow in these labs.  

>>The [kubeflow project](https://github.com/kubeflow/kubeflow) is dedicated to making deployments of machine learning (ML) workflows on Kubernetes simple, portable and scalable. Our goal is not to recreate other services, but to provide a straightforward way to deploy best-of-breed open-source systems for ML to diverse infrastructures. Anywhere you are running Kubernetes, you should be able to run Kubeflow.

Kubeflow is really the following:
* [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/), which allows you to request an instance of a dedicated Jupyter Notebook.  We recommend using AMLS compute instances, but this is an excellent alternative.  The problem is it's harder to control costs by spinning down Jupyter container instances with kubernetes HPA (horizontal pod autoscaler).  
* Training controllers:  this component makes training jobs deployment easier.  We will only deploy training controllers for tf jobs in this workshop, but there are controllers for PyTorch and others.  The AMLS analog is training compute instances, again the benefit being these are able to be better autoscaled when not in use.  
* a model serving component:  this isn't much different from AMLS inference clusters.  

### MLFlow vs Kubeflow
Kubeflow is meant to build E2E workflow pipelines, MLFlow is used to track metrics and deploy models.  AMLS experiments and pipelines are really a superset of MLFlow and you can use the MLFlow APIs to talk to AMLS, essentially making AMLS a PaaS offering for an MLFlow server.  Kubeflow is its own thing that you deploy into an AKS/k8s cluster.  

1. [Lab100: Kubeflow Prerequisites, Background, and Motivation](./Lab100/README.md)
1. [Lab101: Containerizing a TensorFlow Model](./Lab101/README.md)
1. [Lab102: Kubeflow Installation](./Lab102/README.md)
1. [Lab103: Running JupyterHub with Kubeflow on AKS](./Lab103/README.md)
1. [Lab104: Using tfjob to run training jobs](./Lab104/README.md)

## AMLS Deeper Dive Labs

These labs will get you a little more intimate with the AMLS service.  You may want to start here on your journey with AMLS. Most of these are ipynb files and can be run either from your local workstation (vscode, pycharm, whatever) or using the JupyterLab notebooks on the AMLS compute engines (or anywhere else supporting .ipynb files)

**Remember, we do all of these labs in code, but much of it can be examined using the AMLS workspace.**

1. [Lab200: The Azure ML SDK](./Lab200/200-intro.ipynb) :  basic calls
1. [Lab201: Running Experiments](./Lab200/201-experiments.ipynb) 
  * running experiments using the diabetes sample data set
  * creating .py files from a Jupyter notebook and executing those with logged experiments
1. [Lab202: Working with conda and python envs using Jupyter notebooks](./Lab200/202-envs.ipynb)
  * all about python environments
  * When you run a Python script as an experiment in Azure Machine Learning, a Conda environment is created to define the execution context for the script
  * we also create some AMLS datasets
1. [Lab203: Working with Pipelines](./Lab200/203-pipelines.ipynb)
  * Pipelines consist of one or more _steps_, which can be Python scripts, or specialized steps like an Auto ML training estimator or a data transfer step that copies data from one location to another. Each step can run in its own compute context.
  * Pipelines are a good start on the automation journey, it also separates work so various team members can focus on particular areas in your solution. 
1. [Lab204: Model Interpretability and Explainability with AMLS](./Lab200/204-interpret.ipynb)
  * we use features of AMLS and LIME
1. [Lab205: Monitoring a Model](./Lab200/205-monitor.ipynb)
  * we quickly train and deploy a model for inferencing
  * we monitor it using the service and AppInsights
  * also sets up conda envs using yaml
  * inference deployment uses ACI and not AKS
1. [Lab206: Monitor Data Drift](./Lab200/206-drift.ipynb)
  * Over time, models can become less effective at predicting accurately due to changing trends in feature data. This phenomenon is known as data drift, and it's important to monitor your machine learning solution to detect it so you can retrain your models if necessary.
## WrapUp

1. **Remove the RG you created to prevent incurring Azure costs**


## Reference Material

* [Microsoft's MLOpsPython repo](https://github.com/microsoft/MLOpsPython)
* [MLOps on Azure](https://github.com/microsoft/MLOps)
* [My Sample Notebooks](./samples/README.md)



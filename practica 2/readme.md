# Face Recognition Function Deployment using OpenFaaS on Kubernetes

## Overview
This document outlines the process of setting up Kubernetes and OpenFaaS, deploying pre-existing face recognition functions, developing a custom face detection function, and alternatives for other applications. This practice aims to implement scalable face detection functionalities that can serve as a component for biometric identification.

## Table of Contents
- [Installation Setup](#installation-setup)
  - [Kubernetes](#kubernetes)
  - [OpenFaaS](#openfaas)
- [Function Deployment](#function-deployment)
  - [Deploying Existing Functions](#deploying-existing-functions)
  - [Testing Functions](#testing-functions)
- [Developing Custom Functions](#developing-custom-functions)
  - [Development Environment](#development-environment)
  - [Face Detection Logic](#face-detection-logic)
  - [Deployment and Testing](#deployment-and-testing)
- [Alternative Applications](#alternative-applications)
- [Documentation and Submission](#documentation-and-submission)
- [Conclusion](#conclusion)
- [References](#references)

## Installation Setup

### Kubernetes
- **Installation**: Detail the steps taken to install Minikube along with any configurations applied.
- **Verification**: Describe how you verified the successful installation and operation of Minikube.

### OpenFaaS
- **Installation**: Outline the process followed to install OpenFaaS using Helm on Kubernetes.
- **Configuration**: Explain any specific configurations used for OpenFaaS, including setting up `faas-cli`.

## Function Deployment

### Deploying Existing Functions
- **Function Selection**: Discuss the functions chosen from the OpenFaaS store (`face-detect-pigo` and `face-detect-opencv`).
- **Deployment Commands**: Provide the commands used to deploy these functions along with any output or verification steps.

### Testing Functions
- **Test Images**: List the URLs of test images used.
- **Function Invocation**: Show how the functions were invoked both via the OpenFaaS UI and CLI.
- **Results**: Include screenshots or descriptions of the outputs.

## Developing Custom Functions

### Development Environment
- **Setup**: Describe how you set up the development environment using `faas-cli`.
- **Files Created**: List the files created by the setup process and their purposes.

### Face Detection Logic
- **Code Implementation**: Include the code snippet used for detecting faces using OpenCV.
- **Dependencies**: List any additional dependencies required for your function.

### Deployment and Testing
- **Deployment Steps**: Provide detailed steps on how to build, push, and deploy the custom function.
- **Testing**: Detail how the function was tested and any results or modifications made.

## Alternative Applications
- **Suggestions**: Describe any alternative applications considered or developed.
- **Approval**: Note any discussions with the instructor regarding these alternatives.

## Documentation and Submission
- **Document Preparation**: Outline how the documentation was prepared and organized.
- **Submission Package**: Describe the contents of the submission package.

## Conclusion
Summarize the experience, the outcomes of the deployment, and any lessons learned.

## References
- Include all external references used in this project.

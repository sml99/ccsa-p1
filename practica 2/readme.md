# Face Recognition Function Deployment using OpenFaaS on Kubernetes

## Overview
This document outlines the process of setting up Kubernetes and OpenFaaS, deploying pre-existing face recognition functions, developing a custom face detection function, and alternatives for other applications. This practice aims to implement scalable face detection functionalities that can serve as a component for biometric identification.

## Table of Contents
- [Setup](#setup)
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

## Setup

### Kubernetes
**Installation**:
1. **Minikube**:
   - **Minikube** is a tool that lets us run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a VM.
   Installation using Powershell on Windows 11:
   - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/196c6129-6149-498f-91b5-676d5bb6cd50)
   - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/dcdebed8-1e7d-495f-a0c7-0f61b7140cfe)


2. **Start Minikube**:
   - **Starting Minikube** sets up the Kubernetes cluster managed by Minikube.
   - `minikube start`
   - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/03f94502-f15f-432a-ac8e-d2a369b39c1b)
   - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/d8c79ac6-a113-4f68-b891-07eedb1d9041)

3. **Install kubectl**:
   - **kubectl** is the Kubernetes command-line tool, allowing us to run commands against Kubernetes clusters. It is used for deploying applications, inspecting and managing cluster resources, and viewing logs.
   - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/10b63693-86da-48a7-aab5-96a42be0c633)



### OpenFaaS
- **Installation**: Install OpenFaaS using Arkade.
1. **Arkade**:
    - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/d180cd1f-1e28-46a5-a14e-1ed46ab509b5)

2. **Openfaas**:
    - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/492b2b75-2168-42fd-823a-bcee6ab3a476)

3. **Openfaas cli**:
    - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/ddafa89f-a9f8-4d68-beb9-61025e340767)

- **Configuration**: 
    - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/d9a1363e-bcd3-432d-b408-e80e236d598a)
    - ![image](https://github.com/sml99/ccsa-p1/assets/29798184/3aa9a33a-f40f-4ba6-a294-ab3d631c9550)


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

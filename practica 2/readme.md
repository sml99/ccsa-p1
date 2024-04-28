# Funciones como servicio

## Overview
This document outlines the process of setting up Kubernetes and OpenFaaS, deploying pre-existing face recognition functions, developing a custom face detection function.

## Table of Contents
- [Setup](#setup)
  - [Kubernetes](#kubernetes)
  - [OpenFaaS](#openfaas)
- [Function Deployment](#function-deployment)
  - [Deploying Existing Functions](#deploying-existing-functions)
  - [Testing Functions](#testing-functions)

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

### Deploying Existing Functions from store
- **Function Selection**: We have 2 face detection functions 
- ![image](https://github.com/sml99/ccsa-p1/assets/29798184/5888dfab-766a-4daa-97b9-79315d9311ef)
- **Deployment Commands**:
- ![image](https://github.com/sml99/ccsa-p1/assets/29798184/e6f89582-d10d-4aad-9a6f-2ac7609f2c3e)

### Testing Functions
- **Test Images**: ![image](https://github.com/sml99/ccsa-p1/assets/29798184/b510bf22-a551-4431-9a33-d22fa2230fda)
- **Function Invocation**: ![image](https://github.com/sml99/ccsa-p1/assets/29798184/29b1cdc2-a8d2-40c8-ae60-242a14ca4849)
- **Results**: ![face](https://github.com/sml99/ccsa-p1/assets/29798184/766b5d1c-1690-4a45-aa44-4726e943eb74)

## Building Custom Functions

### Development Environment
- **Setup**: first We clone https://github.com/esimov/pigo-openfaas
- **Build&Deploy**: 
- ![image](https://github.com/sml99/ccsa-p1/assets/29798184/61a8da40-2206-47a7-95dd-06723cd94e48)
- ![image](https://github.com/sml99/ccsa-p1/assets/29798184/d64f2d64-bb65-4455-9515-c8ca6ab8755c)
- ![image](https://github.com/sml99/ccsa-p1/assets/29798184/97293c4d-8387-4843-aaf0-8779eb4c8754)

### Face Detection Logic
- **Code Implementation**: ![code](https://github.com/sml99/ccsa-p1/assets/29798184/77f26a4d-b187-4a25-9318-c1b034f82cf6)
- **Invocation**: ![image](https://github.com/sml99/ccsa-p1/assets/29798184/c324369c-1ab4-46de-8c28-1f6e586b5091)
- **Results**: ![output](https://github.com/sml99/ccsa-p1/assets/29798184/1fde9a31-4b18-4494-9264-1917d95c0878)



# Kubernetes for DevOps

This repository contains my hands-on learning and practical implementation of **Kubernetes** concepts as part of my DevOps journey.

The goal of this repository is to understand how Kubernetes is used to deploy, manage, scale, and expose containerized applications.

## 🛠️ Technologies & Tools

* Kubernetes
* Docker
* YAML
* kubectl
* Linux
* Git & GitHub

## 📚 Topics Covered

### 1. Pods

* Understanding Kubernetes Pods
* Creating and managing Pods
* Pod lifecycle
* Running containers inside Pods

### 2. Deployments

* Creating Kubernetes Deployments
* Replica management
* Rolling updates
* Application scaling

### 3. Services

* Understanding Kubernetes Services
* ClusterIP
* NodePort
* LoadBalancer
* Exposing applications

### 4. ConfigMaps & Secrets

* Managing application configuration
* Using ConfigMaps
* Managing sensitive configuration using Secrets

### 5. Kubernetes Networking

* Pod-to-Pod communication
* Service discovery
* Basic Kubernetes networking concepts

### 6. Ingress

* Understanding Ingress
* Routing external traffic to applications
* Host and path-based routing

### 7. Scaling

* Scaling Deployments
* Replica management
* Introduction to Horizontal Pod Autoscaling

### 8. Application Deployment

A containerized **Inventory Management Spring Boot application** will be deployed to Kubernetes using Kubernetes manifests.

## 📂 Repository Structure

```text
kubernetes-for-devops/
│
├── 01-pods/
│   ├── pod.yaml
│   └── README.md
│
├── 02-deployments/
│   ├── deployment.yaml
│   └── README.md
│
├── 03-services/
│   ├── service.yaml
│   └── README.md
│
├── 04-configmaps-secrets/
│   ├── configmap.yaml
│   └── secret.yaml
│
├── 05-ingress/
│   └── ingress.yaml
│
├── 06-scaling/
│   └── deployment.yaml
│
└── 07-inventory-management/
    ├── deployment.yaml
    └── service.yaml
```

## 🎯 Objectives

* Understand Kubernetes architecture and core components
* Deploy containerized applications using Kubernetes
* Manage application replicas and scaling
* Understand Kubernetes networking and service discovery
* Manage application configuration and secrets
* Gain hands-on experience with `kubectl`
* Deploy a real-world Spring Boot application on Kubernetes

## 🚀 Learning Approach

This repository focuses on **hands-on implementation rather than theory alone**.

Each topic contains Kubernetes YAML manifests and documentation explaining:

1. What the Kubernetes resource does
2. Why it is used
3. How the configuration works
4. Commands used to deploy and manage it
5. Expected output

## 📌 Project

As part of this repository, the **Inventory Management Spring Boot application** will be containerized using Docker and deployed to Kubernetes.

```text
Spring Boot Application
        ↓
      Maven
        ↓
      Docker
        ↓
  Container Image
        ↓
    Kubernetes
        ↓
    Deployment
        ↓
     Service
        ↓
 Running Application
```

## 👩‍💻 Author

**Arfa Fathima**

This repository is part of my hands-on **DevOps learning journey**, focusing on containerization, orchestration, cloud infrastructure, and automation.

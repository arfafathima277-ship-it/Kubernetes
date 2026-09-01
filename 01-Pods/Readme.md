# Kubernetes Pods

## What is a Pod?

A **Pod** is the smallest deployable unit in Kubernetes.

A Pod represents one or more containers that are deployed together and share the same network and storage resources.

In most common applications, a Pod contains a single application container.

## Why are Pods used?

Kubernetes does not directly manage individual containers. Instead, containers run inside Pods.

The basic relationship is:

```text
Kubernetes
    |
   Pod
    |
Container
```

For example:

```text
Pod
 |
 +---- Spring Boot Container
```

A Pod provides the environment in which the application container runs.

## Key Characteristics

* A Pod can contain one or more containers.
* Containers inside the same Pod share the Pod's network namespace.
* Containers in the same Pod can communicate with each other using `localhost`.
* Pods can share storage volumes.
* Pods are designed to be relatively short-lived.
* Kubernetes can create, terminate, and replace Pods as required.

## Pod IP Address

Each Pod normally receives its own IP address.

However, Pod IPs are not considered permanent. If a Pod is deleted and recreated, the new Pod can receive a different IP address.

This is one reason Kubernetes uses **Services** to provide stable network access to applications.

## Pod vs Container

| Container                       | Pod                                      |
| ------------------------------- | ---------------------------------------- |
| Runs the application            | Provides the environment for containers  |
| Managed by a container runtime  | Managed by Kubernetes                    |
| Can run independently           | Contains one or more containers          |
| Has its own process environment | Containers can share network and storage |

## Single-Container Pod

A common Kubernetes architecture is:

```text
Pod
 |
 +---- Application Container
```

For example, a Spring Boot application can run inside a container, and that container can run inside a Kubernetes Pod.

## Multi-Container Pod

A Pod can also contain multiple containers when the containers need to work closely together.

```text
Pod
 |
 +---- Application Container
 |
 +---- Supporting Container
```

Containers inside the same Pod share networking and can communicate using `localhost`.

## Important Interview Questions

### 1. What is a Pod?

A Pod is the smallest deployable unit in Kubernetes and provides an environment for running one or more containers.

### 2. Can a Pod contain multiple containers?

Yes. A Pod can contain multiple containers that share networking and storage.

### 3. Is a Pod the same as a container?

No. A container runs the application, while a Pod is the Kubernetes unit that encapsulates one or more containers.

### 4. Are Pod IP addresses permanent?

No. Pods are replaceable, so their IP addresses can change.

### 5. Why do we need Services if Pods have IP addresses?

Because Pod IP addresses can change. A Service provides a stable way to access a group of Pods.

## Summary

```text
Kubernetes
     |
    Pod
     |
 Container
     |
Application
```

**Pod = Kubernetes' smallest deployable unit for running containers.**

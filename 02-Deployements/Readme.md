# Kubernetes Deployments

## 1. What is a Kubernetes Deployment?

A Deployment is a Kubernetes resource used to manage and maintain a set of identical Pods.

It ensures that the desired number of Pod replicas are running and helps manage application updates.

For example, if an application requires 3 replicas, the Deployment ensures that Kubernetes maintains 3 Pods.

## 2. Why Do We Use Deployments?

* Automatically maintains the desired number of Pods.
* Recreates Pods if they fail or are deleted.
* Supports scaling applications.
* Supports rolling updates without taking down the entire application.
* Allows rollback to a previous application version.
* Simplifies application management.

## 3. How Does a Deployment Work?

Deployment → ReplicaSet → Pods

* Deployment manages the ReplicaSet.
* ReplicaSet ensures the desired number of Pods are running.
* Pods run the actual application containers.

If a Pod fails, the ReplicaSet creates a replacement Pod to maintain the desired replica count.

## 4. Deployment YAML Example

Create a file named `deployment.yaml`.

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

### Explanation

* `apiVersion`: API version used for Deployments.
* `kind`: Defines the Kubernetes resource type.
* `metadata`: Contains the Deployment name.
* `replicas`: Number of desired Pods.
* `selector`: Identifies the Pods managed by the Deployment.
* `template`: Defines the Pod configuration.
* `image`: Container image used to run the application.
* `containerPort`: Port exposed by the container.

Note: The selector's labels must match the Pod template's labels.

## 5. Create a Deployment

```bash
kubectl apply -f deployment.yaml
```

This creates the Deployment using the YAML configuration.

## 6. Verify the Deployment

Check Deployments:

```bash
kubectl get deployments
```

Check ReplicaSets:

```bash
kubectl get replicasets
```

Check Pods:

```bash
kubectl get pods
```

Describe a Deployment:

```bash
kubectl describe deployment nginx-deployment
```

## 7. Scaling a Deployment

Scaling means increasing or decreasing the number of application replicas.

Scale to 5 replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Verify:

```bash
kubectl get pods
```

Kubernetes adjusts the number of Pods to match the desired replica count.

## 8. Rolling Updates

A rolling update gradually replaces old Pods with new Pods when an application version changes.

Update the container image:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.26
```

Check rollout status:

```bash
kubectl rollout status deployment/nginx-deployment
```

Check rollout history:

```bash
kubectl rollout history deployment/nginx-deployment
```

Rolling updates help minimize application downtime during deployments.

## 9. Rollback a Deployment

If a new application version causes issues, Kubernetes allows you to roll back to a previous revision.

Rollback:

```bash
kubectl rollout undo deployment/nginx-deployment
```

Verify the rollout:

```bash
kubectl rollout status deployment/nginx-deployment
```

## 10. Delete a Deployment

```bash
kubectl delete deployment nginx-deployment
```

This deletes the Deployment and its managed resources, including its ReplicaSet and Pods.

## 11. Deployment vs Pod

| Pod                                               | Deployment                                          |
| ------------------------------------------------- | --------------------------------------------------- |
| Runs one or more containers                       | Manages replicated Pods                             |
| Does not automatically recreate itself if deleted | Maintains the desired number of Pods                |
| Does not provide rollout management               | Supports rolling updates and rollbacks              |
| Used to run application containers                | Used to manage application availability and updates |

## 12. DevOps Interview Questions

### Q1. What is a Kubernetes Deployment?

A Deployment is a Kubernetes resource that manages application Pods and ensures the desired number of replicas are running.

### Q2. What is the difference between a Deployment and a ReplicaSet?

A ReplicaSet maintains the desired number of Pod replicas. A Deployment manages ReplicaSets and provides features such as rolling updates and rollbacks.

### Q3. What happens if a Pod managed by a Deployment gets deleted?

The ReplicaSet detects that the actual number of Pods is below the desired count and creates a replacement Pod.

### Q4. What is a rolling update?

A rolling update gradually replaces old application Pods with new ones to minimize downtime during application updates.

### Q5. How do you roll back a Deployment?

Use:

`kubectl rollout undo deployment/<deployment-name>`

### Q6. How do you scale a Deployment?

Use:

`kubectl scale deployment <deployment-name> --replicas=<count>`

## Key Takeaway

Kubernetes Deployments simplify application management by maintaining Pod replicas, supporting scaling, enabling rolling updates, and allowing rollbacks when application updates fail.

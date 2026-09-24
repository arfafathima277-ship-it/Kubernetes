# Kubernetes Services

## 1. What is a Kubernetes Service?

A Kubernetes Service is an object that exposes a group of Pods over a network.

Pods are temporary and can be recreated with different IP addresses. A Service provides a stable IP address and DNS name to access the application.

Services help applications communicate with other applications inside or outside the Kubernetes cluster.

## 2. Why Do We Use Services?

* Provides stable network access to Pods.
* Enables communication between application components.
* Distributes traffic across matching Pods.
* Allows applications to be exposed outside the cluster.
* Supports service discovery using DNS.

## 3. Types of Kubernetes Services

### ClusterIP

ClusterIP is the default Service type.

It exposes an application using an internal IP address that is accessible within the Kubernetes cluster.

Use case: Communication between frontend and backend applications inside the cluster.

### NodePort

NodePort exposes an application on a specific port on each node in the cluster.

The application can be accessed using:

`<NodeIP>:<NodePort>`

Use case: Basic external access to an application, commonly in development or testing environments.

### LoadBalancer

LoadBalancer exposes an application externally using a cloud provider's load balancer integration.

Use case: Exposing applications to external users in supported cloud environments.

Note: A working external load balancer depends on the cluster environment and its infrastructure configuration.

## 4. Kubernetes Service YAML Example

Create a file named `service.yaml`.

```yaml
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  type: ClusterIP

  selector:
    app: nginx

  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

### Explanation

* `apiVersion`: Kubernetes API version.
* `kind`: Defines the resource type.
* `metadata.name`: Name of the Service.
* `type`: Service type.
* `selector`: Identifies the Pods that receive traffic.
* `port`: Port exposed by the Service.
* `targetPort`: Port on the target Pod to which traffic is forwarded.

The Service selector must match the labels on the target Pods.

## 5. Create a Service

```bash
kubectl apply -f service.yaml
```

## 6. Verify the Service

List Services:

```bash
kubectl get services
```

Describe a Service:

```bash
kubectl describe service nginx-service
```

Check Service endpoints:

```bash
kubectl get endpoints nginx-service
```

In newer Kubernetes environments, EndpointSlices are the preferred API for representing backend endpoints.

```bash
kubectl get endpointslices
```

## 7. Expose a Deployment

You can create a Service directly from an existing Deployment.

```bash
kubectl expose deployment nginx-deployment --type=ClusterIP --port=80 --target-port=80
```

This creates a Service that routes traffic to the Pods managed by the Deployment.

## 8. Port Forwarding

Port forwarding allows you to access a Service locally for testing.

```bash
kubectl port-forward service/nginx-service 8080:80
```

Now access the application at:

`http://localhost:8080`

Port forwarding is useful for local testing and debugging. It does not make the application publicly accessible.

## 9. Service vs Deployment

| Deployment                               | Service                                 |
| ---------------------------------------- | --------------------------------------- |
| Manages application Pods                 | Provides network access to Pods         |
| Maintains the desired number of replicas | Routes traffic to matching Pods         |
| Supports rolling updates and rollbacks   | Provides a stable network endpoint      |
| Focuses on application lifecycle         | Focuses on networking and communication |

## 10. DevOps Interview Questions

### Q1. What is a Kubernetes Service?

A Service provides a stable network endpoint to access a group of Pods.

### Q2. Why do we need a Service if Pods already have IP addresses?

Pod IP addresses can change when Pods are recreated. A Service provides a stable endpoint and routes traffic to matching Pods.

### Q3. What are the main types of Kubernetes Services?

ClusterIP, NodePort, and LoadBalancer.

### Q4. What is the default Service type?

ClusterIP.

### Q5. What is the difference between port and targetPort?

`port` is the port exposed by the Service, while `targetPort` is the port on the backend Pod where traffic is sent.

### Q6. How does a Service identify Pods?

A Service uses label selectors to identify the Pods that should receive traffic.

## Key Takeaway

Kubernetes Services provide stable networking and enable communication with application Pods. They are essential for exposing applications and connecting components in a Kubernetes environment.

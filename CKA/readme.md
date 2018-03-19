# CKA

Certified Kubernetes Administrator (CKA) 

## syllabus

### 5% - Scheduling

#### Use label selectors to schedule Pods.
[ref here](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

one usage scenario：

```shell
kubectl label node 127.0.0.1 accelerator=nvidia-tesla-p100
```
some label limits:


```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cuda-test
spec:
  containers:
    - name: cuda-test
      image: "k8s.gcr.io/cuda-vector-add:v0.1"
      resources:
        limits:
          nvidia.com/gpu: 1
  nodeSelector:
    accelerator: nvidia-tesla-p100
```

#### Understand the role of DaemonSets.
A DaemonSet ensures that all (or some) Nodes run a copy of a Pod.
[ref here](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: busybox-apps-v1
  labels:
    app: busybox-apps-v1  # important
spec:
  selector:
    matchLabels:
      name: busybox-apps-v1  # important
  template:
    metadata:
      labels:
        name: busybox-apps-v1
    spec:
      containers:
      - name: busybox-apps-v1
        image: busybox
        imagePullPolicy: IfNotPresent
```


#### Understand how resource limits can affect Pod scheduling.
[ref here](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)

When you create a Pod, the Kubernetes scheduler selects a node for the Pod to run on. Each node has a maximum capacity for each of the resource types: the amount of CPU and memory it can provide for Pods. The scheduler ensures that, for each resource type, the sum of the resource requests of the scheduled Containers is less than the capacity of the node. Note that although actual memory or CPU resource usage on nodes is very low, the scheduler still refuses to place a Pod on a node if the capacity check fails. This protects against a resource shortage on a node when resource usage later increases, for example, during a daily peak in request rate.

actual memory or CPU resource = maximum allocable capacity - sum of all requested resources.
It doest not care the really actual usage.


#### Understand how to run multiple schedulers and how to configure Pods to use them.


Manually schedule a pod without a scheduler.

Display scheduler events.

Know how to configure the
Kubernetes scheduler.

### 5% - Logging/Monitoring

Understand how to monitor all
cluster components.

Understand how to monitor applications.

Manage cluster component logs.

Manage application logs.

### 8% - Application Lifecycle Management

Understand Deployments and how to
perform rolling updates and rollbacks.

Know various ways to configure applications.
Know how to scale applications.

Understand the primitives necessary to
create a self-healing application.

### 11% - Cluster Maintenance

Understand Kubernetes cluster
upgrade process.

Facilitate operating system upgrades.

Implement backup and restore methodologies.

12% - Security

Know how to configure authentication
and authorization.

Understand Kubernetes security primitives.
Know to configure network policies.

Create and manage TLS certificates for
cluster components.

Work with images securely.

Define security contexts.

Secure persistent key value store.

Work with role-based access control.

7% - Storage

Understand persistent volumes and know how
to create them.

Understand access modes for volumes.

Understand persistent volume claims primitive.

Understand Kubernetes storage objects.

Know how to configure applications with persistent storage.

### 10% - Troubleshooting

Troubleshoot application failure.

Troubleshoot control plane failure.

Troubleshoot worker node failure.

Troubleshoot networking.

19% - Core Concepts

Understand the Kubernetes API primitives.

Understand the Kubernetes cluster architecture.

Understand Services and other network primitives.

### 11% - Networking

Understand the networking configuration on the cluster nodes.

Understand Pod networking concepts.

Understand service networking.

Deploy and configure network load balancer.

Know how to use Ingress rules.

Know how to configure and use the cluster DNS.

Understand CNI.

### 12% - Installation, Configuration & Validation

Design a Kubernetes cluster.

Install Kubernetes masters and nodes, including the use of TLS bootstrapping.

Configure secure cluster communications.

Configure a Highly-Available Kubernetes cluster.

Know where to get the Kubernetes release binaries.

Provision underlying infrastructure to deploy a Kubernetes cluster.

Choose a network solution.

Choose your Kubernetes infrastructure configuration.

Run end-to-end tests on your cluster.

Analyse end-to-end tests results.

Run Node end-to-end tests.
# Kubernetes Architecture for CKAD Examination

Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. Understanding its architecture is critical for the CKAD examination.

## Key Components of Kubernetes

### 1. Control Plane

The control plane manages the Kubernetes cluster and is responsible for maintaining the desired state of the system.

#### Components:

- **API Server (kube-apiserver):**

  - Serves as the front-end for the Kubernetes control plane.
  - Handles REST requests from users, command-line tools (kubectl), and other components.
  - Validates and processes API objects (e.g., Pods, Services).

- **Controller Manager (kube-controller-manager):**

  - Runs various controllers (e.g., Node Controller, Deployment Controller) to ensure the cluster's state matches the desired state.

- **Scheduler (kube-scheduler):**

  - Assigns Pods to Nodes based on resource requirements, constraints, and scheduling policies.

- **etcd:**

  - A distributed key-value store that serves as Kubernetes' backing store.
  - Stores all cluster data, including configuration and state.

### 2. Nodes (Worker Nodes)

Nodes are the machines (virtual or physical) where Kubernetes deploys application workloads.

#### Components:

- **kubelet:**

  - The primary agent on a Node.
  - Ensures that containers in a Pod are running and healthy.

- **kube-proxy:**

  - Manages networking for Pods.
  - Handles Service discovery and load balancing.

- **Container Runtime:**

  - Software responsible for running containers (e.g., Docker, containerd, CRI-O).

### 3. Add-Ons

Add-ons extend the functionality of Kubernetes. Common examples include:

- **DNS (CoreDNS):** Internal DNS server for service discovery.
- **Dashboard:** Web-based UI for managing the cluster.
- **Monitoring and Logging:** Tools like Prometheus and Grafana for monitoring and Fluentd for logging.

## Kubernetes Object Model

### Core Objects:

- **Pods:** The smallest deployable units in Kubernetes, encapsulating containers.
- **Services:** Expose Pods to the network.
- **Deployments:** Manage stateless applications and ensure a desired number of replicas.
- **ConfigMaps and Secrets:** Store configuration and sensitive data.

### Workloads:

- **DaemonSets:** Ensure one Pod per Node.
- **StatefulSets:** Manage stateful applications.
- **Jobs and CronJobs:** Run tasks and scheduled jobs.

## Cluster Communication

- **API Server as the Single Entry Point:** All communication between components goes through the API Server.
- **Networking:** Kubernetes uses a flat network model, enabling Pods to communicate directly with one another.

## Summary Diagram

```plaintext
+----------------------------+             +-----------------------------+
|        Control Plane       |             |         Worker Nodes        |
|----------------------------|             |-----------------------------|
| - API Server               |             | - kubelet                   |
| - Controller Manager       | <----------> | - kube-proxy                |
| - Scheduler                |             | - Container Runtime         |
| - etcd                     |             |                             |
+----------------------------+             +-----------------------------+
```

This architecture ensures high availability, scalability, and robust management of containerized applications.


# Kubernetes Components

An overview of the key components that make up a Kubernetes cluster.

![componenets-of-kubernetes](./files/kubernetes_components/components-of-kubernetes.svg "Components of Kubernetes")

## Core Components

A Kubernetes cluster consists of a control plane and one or more worker nodes. Here's a brief overview of the main components:

### Control Plane Components

The control plane is really the brain of your cluster, and it’s composed of:

- API Server: is responsible for exposing the K8s API, which is how users interact with the cluster.
- etcd: is a key-value datastore responsible for storing specifications, state, and configurations of the cluster.
- Scheduler: It selects which node will host a specific pod, taking into consideration the available resources of each node and its state.
- Controller Manager: ensures that your cluster is running with the last state specified in the etcd. For example, keeping the specified number of replicas of a pod.

### Node Components

Run on every node, maintaining running pods and providing the Kubernetes runtime environment:

- Kubelet: It’s an agent placed inside the nodes responsible for managing the pods according to Controller instructions.
- Kube-proxy: It’s a network proxy running in your worker nodes responsible for the node network and for routing requisitions to pods.
- Container Runtime: manages the execution and lifecycle of containers inside the nodes.

### Bibliography

- https://kubernetes.io/docs/concepts/overview/components/
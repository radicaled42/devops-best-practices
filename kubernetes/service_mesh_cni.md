# Service Mesh and CNI

<p align="center">
  <img src="./files/service_mesh_cni/1_tDsSyEtZBnZmhBD070beiQ.png" alt="Kubernetes Networks" />
</p>

## Kubernetes Networks

It is important to understand that there are four types of networks in a Kubernetes cluster:

1. **Host Network**

   This network connects all the hosts running as Kubernetes Nodes. IP addresses allocated within this network are defined within your Virtual Private Cloud (VPC).

2. **Cluster Network**

   This network connects all the Pods together seamlessly. Kubernetes requires that all Pods can communicate with one another without any Network Address Translation (NAT). 
   
   Effectively, this makes Pods behave like virtual machines on a virtual network, sharing a subnet among all Pods.

3. **Service Network**

   Since Pods are ephemeral, they can be terminated and rescheduled at any time, potentially on different Nodes with different IP addresses. To ensure consistent access, Kubernetes introduces the concept of a Service.
   
   A Service provides persistent access even if the underlying Pods change. Each Service is assigned an IP address from the Service Network when created.

4. **Container Network**

   When multiple containers exist in a Pod, they share the same network, similar to how processes share the same network on a virtual machine. Containers in the same Pod have access to the same Pod IP address and can communicate via the localhost loopback network, but they must operate on different ports.

## Container Network Interface (CNI)

Kubernetes requires all Pods to communicate over the Cluster network. This means that each Node and Pod must be configured to implement the cluster subnet. This is where the **Container Network Interface (CNI)** comes in.

When Kubernetes schedules a Pod, the **kubelet** (Kubernetes agent) on the Node calls the CNI, which assigns an IP address and configures network interfaces to ensure the required connectivity.

The CNI itself is an interface, and its implementation is provided by a plugin, such as **Flannel** or **Calico**. These plugins implement the CNI in different ways and provide various layers of security within the cluster.

## Service Mesh

A **Service Mesh** is a layer that sits on top of the Cluster Network. It is designed to secure and manage communications between specific Pods, rather than allowing open access between all Pods.

A Service Mesh operates as a **sidecar** to the main application container, providing network connectivity as a proxy. Communication between the proxy and the application occurs over the localhost network.

## Do I Need Both a Service Mesh and a CNI Plugin?

- A **CNI plugin** is **required** for Kubernetes to function as it ensures connectivity between Pods on the cluster network.
- A **Service Mesh** is **optional** but can be beneficial.

### Need for CNI Plugin

Kubernetes requires the CNI interface for connectivity between Pods across the cluster network. This is mandatory.

### Need for Service Mesh

A Service Mesh is optional but provides several advantages:

- **Security**: Implements routing rules and mutual Transport Layer Security (mTLS) between Pods.
- **Load Balancing**: Defines how traffic is distributed between Pods.
- **Monitoring**: Provides metrics and logs on connections and traffic.
- **Separation of Concerns**: Abstracts network management from the application, allowing for consistent implementation and making the application technology-agnostic. It also supports namespace separation.
- **Reliability**: Enables automatic retries for failed requests.

These benefits make a strong case for implementing a Service Mesh on top of the CNI plugin.

### Options for Service Mesh

There are several technologies available for implementing a Service Mesh:

- **Istio**
- **Linkerd**
- **Cilium**
- **Consul Connect**
- **Cloud-Specific Solutions** (e.g., GCP Anthos, AWS App Mesh, Azure Open Service Mesh - deprecated)

Many of these services are now paid solutions. Istio remains a free, open-source option but can be complex to set up and debug.


**Bibliography**:
- https://medium.com/@martin.hodges/why-do-i-need-a-service-mesh-as-well-as-a-cni-829b492398b7
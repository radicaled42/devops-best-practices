# Kubernetes Networking

The Kubernetes networking model allows the different parts of a Kubernetes cluster, such as Nodes, Pods, Services, and outside traffic, to communicate with each other. For the most part, Kubernetes networking is seamless, with traffic moving automatically across your Nodes to reach your resources.

Nonetheless, understanding how Kubernetes networking works is important so you can properly configure your environment and set up more complex networking scenarios. In this article, we’ll cover the different parts of the Kubernetes networking architecture, explore how it differs from conventional networking solutions, and explain how Kubernetes networking handles the main cluster communication types. 

## What is Kubernetes networking?

Kubernetes networking is the mechanism by which different resources within and outside your cluster are able to communicate with each other. Networking handles several different scenarios which we’ll explore below, but some key ones include communication between Pods, communication between Kubernetes Services, and handling external traffic to the cluster.

Because Kubernetes is a distributed system, the network plane spans across your cluster’s physical Nodes. It uses a virtual overlay network that provides a flat structure for your cluster resources to connect to.

Below is an example of a Kubernetes networking diagram:

<p aling="center">
  <img src="./files/kubernetes_networking/kubernetes-networking-diagram-example.png" alt="Kubernetes Networking" />
</p>

The Kubernetes networking implementation allocates IP addresses, assigns DNS names, and maps ports to your Pods and Services. This process is generally automatic—when using Kubernetes, you won’t normally have to manage these tasks on your network infrastructure or Node hosts.

At a high level, the Kubernetes network model works by allocating each Pod a unique IP address that resolves within your cluster. Pods can then communicate using their IP addresses, without requiring NAT or any other configuration.

This basic architecture is enhanced by the Service model, which allows traffic to route to any one of a set of Pods, as well as control methods, including network policies that prevent undesirable Pod-to-Pod communications.

## What is the difference between physical/VM networking and Kubernetes networking?

Kubernetes networking takes familiar networking principles and applies them to Kubernetes cluster environments. Kubernetes networking is simpler, more consistent, and more automated when compared to traditional networking models used for physical devices and VMs.

Whereas you’d previously have to manually configure new endpoints with IP addresses, firewall port openings, and DNS routes, Kubernetes provides all this functionality for your cluster’s workloads.

Developers and operators don’t need to understand how the network is implemented to successfully deploy resources and make them accessible to others. This simplifies setup, maintenance, and continual enforcement of security requirements by allowing all management to be performed within Kubernetes itself.

## What is the difference between Docker networking and Kubernetes networking?

Kubernetes uses a flat networking model that’s designed to accommodate distributed systems. All Pods can communicate with each other, even when they’re deployed to different physical Nodes.

As a single-host containerization solution, Docker takes a different approach to networking. It defaults to joining all your containers into a bridge network that connects to your host. You can create other networks for your containers using a variety of network types, including bridge, host (direct sharing of your host’s network stack), and overlay (distributed networking across Nodes, required for Swarm environments).

Once they’re in a shared network, Docker containers can communicate with each other. Each container is assigned a network-internal IP address and DNS name that allows other network members to reach it. However, Docker does not automatically create port mappings from your host to your containers—you must configure these when you start your containers.

In summary, Docker and Kubernetes networking have similarities, but each is adapted to its use case. Docker is primarily concerned with single-node networking, which the bridged mode helps to simplify, whereas Kubernetes is a naturally distributed system that requires overlay networking.

This difference is apparent in how you prevent containers from communicating with each other: to stop Docker containers from interacting, you must ensure they’re in different networks. This contrasts with Kubernetes, where all Pods are automatically part of one overlay network, and traffic through the network is controlled using policy-based methods.

## Kubernetes networking architecture

As we’ve mentioned, Kubernetes networking has a fundamentally flat structure with the following characteristics:

- All Pods are assigned their own IP addresses.
- Nodes run a root network namespace that bridges between the Pod interfaces. This allows all Pods to communicate with each other using their IP addresses, regardless of the Node they’re scheduled to.
- Communication does not depend on Network Address Translation (NAT), reducing complexity and improving portability.
- Pods are assigned their own network namespaces and interfaces. All communications with Pods go through their assigned interfaces.
- The cluster-level network layer maps the Node-level namespaces, allowing traffic to be correctly routed across Nodes.
- There’s no need to manually bind Pod ports to Nodes, although this is possible when required by assigning Pods a hostPort.

These concepts make Kubernetes networking predictable and consistent for both cluster users and administrators. The model imposed by Kubernetes ensures that all Pods can reliably access network connectivity without requiring any manual configuration.
How Kubernetes allocates pod IP addresses

Kubernetes allocates IP addresses to Pods using the Classless Inter-Domain Routing (CIDR) system. This notation defines the subnet of IP addresses that will be available for use by your Pods. Each Pod is allocated an address from the CIDR range that applies to your cluster. You’ll need to specify the permitted CIDR range when you configure a new cluster’s networking layer.

Many Kubernetes networking plugins also support IP Address Management (IPAM) functions, so you can manually assign IP addresses, prefixes, and pools. This facilitates advanced management of IP addresses in more complex networking scenarios

## How DNS works in Kubernetes clusters

Kubernetes clusters include built-in DNS support. CoreDNS is one of the most popular Kubernetes DNS providers; it comes enabled by default in many Kubernetes distributions.

Kubernetes automatically assigns DNS names to Pods and Services in the following format:

```
    Pod – pod-ip-address.pod-namespace-name.pod.cluster-domain.example (e.g. 10.244.0.1.my-app.svc.cluster.local)
    Service – service-name.service-namespace-name.svc.cluster-domain.example (e.g. database.my-app.svc.cluster.local)
```

The applications running in your Pods should usually be configured to communicate with Services using their DNS names. Names are predictable, whereas a Service’s IP address will change if the Service is deleted and then replaced.

## Kubernetes network isolation with Network Policies

Kubernetes defaults to allowing all Pods to communicate with each other. This is a security risk for clusters used for several independent apps, environments, teams, or customers.

Kubernetes Network Policies are API objects that let you define the permitted ingress and egress routes for your Pods.

## How Kubernetes networking is implemented

Kubernetes defines the networking functionality that a cluster requires, but it doesn’t include a built-in implementation. All the features discussed above are provided by Container Network Interface (CNI) plugins. You have to manually install a CNI plugin when you set up a new Kubernetes cluster from scratch using Kubeadm.

The CNI model improves modularity in the Kubernetes ecosystem. Different plugins offer unique combinations of features to accommodate a wide range of use cases and environments. Any CNI plugin will provide the standard set of Kubernetes networking features but can also expand on them, such as by integrating with other network technologies and services.

## Key Points

Kubernetes networking consists of a flat overlay network that all Pods automatically join. Pods can communicate with each other using their auto-assigned in-cluster addresses and DNS names.

For practical use, Pods that run network services should be exposed using a Kubernetes Service, which provides a single IP address and DNS name to route traffic to multiple Pods. This ensures the service can be scaled up with additional replicas while also providing the possibility of external access.

In this article, we’ve covered the fundamental Kubernetes networking architecture, how it’s implemented, and how the main cluster networking scenarios are achieved. You should now understand more about how Kubernetes networking works and what happens behind the scenes when you create a new Pod or Service.

Need a way to visualize your Kubernetes networking services and enforce guard rails? Check out Spacelift, our CI/CD-driven IaC management platform with Kubernetes environment support. Spacelift lets you apply policies, approval flows, and rules that prevent infrastructure misconfigurations, such as by requiring that all Kubernetes Pods are network-isolated using a Network Policy

**Bibliography**:
- https://spacelift.io/blog/kubernetes-networking
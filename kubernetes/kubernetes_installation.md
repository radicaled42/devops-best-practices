# Installing Kubernetes On-Premise

Installing Kubernetes on-premise involves setting up a cluster of machines (physical or virtual) that work together to run Kubernetes. Here’s a high-level guide to install Kubernetes on-premise:

## Step 1: Prerequisites
Before you start, make sure you have:

- **Machines**: At least one machine for the master node (control plane) and one or more worker nodes. You can use physical servers or virtual machines (VMs).
- **Operating System**: Linux-based OS (Ubuntu, CentOS, Debian, etc.). This guide assumes Ubuntu as the OS.
- **Hardware**: Each machine should meet the minimum requirements (2 CPU, 2GB RAM for testing, more for production).
- **Network**: The nodes should be able to communicate over a network.
- **Container Runtime**: Kubernetes requires a container runtime (like Docker, containerd, or CRI-O).
- **Access to Internet**: For downloading Kubernetes binaries and container images.

## Step 2: Prepare the Environment

1. **Set up SSH Access**:  
   Ensure you can SSH into each node from your master node for easy management.

2. **Update Packages**:  
   Run the following commands on all nodes (master and workers):

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

3. **Disable Swap**:
   Kubernetes doesn’t work well with swap enabled. Disable it by editing the /etc/fstab file and commenting out any swap entries:

```bash
sudo swapoff -a
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```

4. **Set Hostnames**:
   Assign unique hostnames to your master and worker nodes:

```bash
sudo hostnamectl set-hostname master-node  # On the master
sudo hostnamectl set-hostname worker-node  # On worker nodes
```

5. **Install Container Runtime (Docker)**:
On each node (master and workers), install Docker or another container runtime:

```bash
sudo apt-get update
sudo apt-get install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
```

## Step 3: Install Kubernetes Components

1. Add Kubernetes Repository:
    Run these commands on all nodes to add the Kubernetes repository:

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo bash -c 'cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF'
sudo apt-get update
```

2. Install `kubeadm`, `kubelet`, and `kubectl`:
On all nodes, install Kubernetes components:

```bash
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

3. Check kubelet status:
Ensure kubelet is running on each node:

```bash
    sudo systemctl enable kubelet
    sudo systemctl start kubelet
```

## Step 4: Initialize the Kubernetes Master

1. Initialize the Master Node:
On the master node only, initialize the Kubernetes cluster using `kubeadm`:

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

- The `--pod-network-cidr` flag specifies the CIDR for the Pod network. Make sure this matches your Pod network configuration (e.g., Calico, Flannel).

2. Set Up `kubectl` for the Master:
After initializing, set up `kubectl` for the `root` or user running the commands:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

3. Join Worker Nodes:
After initialization, `kubeadm` will output a command like this to join worker nodes to the cluster. Save it, and run it on all worker nodes:

```bash
    kubeadm join <master-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

## Step 5: Install a Pod Network Add-on

Kubernetes needs a Pod network add-on to enable communication between pods on different nodes. Install a network plugin like Calico or Flannel. For example, to install Calico:

```bash
kubectl apply -f https://docs.projectcalico.org/v3.14/manifests/calico.yaml
```

## Step 6: Join Worker Nodes to the Cluster

1. Run the Join Command on Worker Nodes:
On each worker node, run the `kubeadm join` command you saved from the master initialization:

```bash
sudo kubeadm join <master-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

2. Verify Worker Nodes:
On the master node, verify that the worker nodes have joined the cluster:

```bash
    kubectl get nodes
```

    You should see both the master and worker nodes listed.

## Step 7: Test Your Kubernetes Cluster

1. Test the Cluster:
Deploy a simple application to ensure everything is working. For example, deploy Nginx:

```bash
kubectl create deployment nginx --image=nginx
```

2. Expose the Deployment:
Expose the Nginx deployment to access it:

```bash
kubectl expose deployment nginx --port=80 --type=NodePort
```

3. Check Pods and Services:
Check if the Nginx pod is running and the service is accessible:

```bash
    kubectl get pods
    kubectl get svc
```

## Step 8: Set Up Optional Add-ons (Optional)

- Kubernetes Dashboard: You can install the Kubernetes Dashboard for an easy-to-use GUI to manage your cluster.

    ```bash
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.2.0/aio/deploy/recommended.yaml
    ```

- Monitoring and Logging: Set up tools like Prometheus, Grafana, and EFK (Elasticsearch, Fluentd, Kibana) for cluster monitoring and logging.

## Step 9: Manage the Cluster

1. kubectl: Use kubectl to manage your cluster, deploy applications, and monitor system status.
        For example, to scale your deployment:

    ```bash
    kubectl scale deployment nginx --replicas=3
    ```

2. Upgrading Kubernetes:
You can upgrade the Kubernetes cluster components (`kubeadm`, `kubelet`, `kubectl`) following the official Kubernetes upgrade documentation.
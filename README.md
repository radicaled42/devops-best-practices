# DevOps tips and best practices

This repository is a collection of essential tips, troubleshooting guides, and best practices for DevOps engineers. Whether you're working with Docker, Kubernetes, GitHub CI/CD, or Linux, this repo provides valuable insights to help streamline your workflow and enhance your productivity.

## DevOps Essentials

<p align="center">
  <img src="./files/devops-essentials.png" alt="DevOps Essentials" />
</p>

- https://sysxplore.com/
- https://twitter.com/sysxplore/status/1831934837730767250

## Docker

Explore best practices, troubleshooting techniques, and detailed Dockerfile instructions to optimize your containerized applications.

- [Docker Troubleshooting](./docker/docker_troubleshooting.md)
- [Best Practices](./docker/docker_best_practices.md)
- [Dockerfile Instructions](./docker/dockerfile_instructions.md)
- [Securing Docker Containers](./docker/docker_security.md)
- [Docker Monitoring](./docker/docker_monitoring.md)
- [Docker Performance Tuning](./docker/docker_performance.md)

## Kubernetes

Gain insights into best practices for Kubernetes, along with troubleshooting tips to handle deployment issues effectively.

#### Installation and Upgrade
- [Standard Kubernetes Installation](./)
- [HA Kuberenetes Installation](./kubernetes/ha_kubernetes_installation.md)

#### Troubleshooting
- [General Kubernetes Troubleshooting Steps](./kubernetes/general_troubleshooting.md)
  - [Troubleshoot a deployment](./kubernetes/troubleshooting_deployments.md)

#### Components
- [Kubernetes Components](./kubernetes/kubernetes_components.md)
- [Kubernetes Cheat Sheet](./kubernetes/kubernetes_cheat_sheet.md)
- [ReplicaSet vs Deployments vs StatefulSet vs DemonSet](./kubernetes/rs_dp_ds_ss.md)
- [Service Mesh and CNI](./kubernetes/service_mesh_cni.md)

#### Security
- [Kubernetes Security Best Practices](./kubernetes/kubernetes_security.md)

#### Observability
- [Kubernetes Logging](./kubernetes/kubernetes_logging.md)

#### Misc
- [Best Practices](./kubernetes/best_practices.md)
- [Kubernetes Plugins Resources](./kubernetes/kubernetes_resources.md)
- [Kubernetes Performance Optimization](./kubernetes/kubernetes_performance.md)
- [ArgoCD](./kubernetes/misc/argocd.md)

## Networking
- [How a DNS Works](./networking/how_dns_works.md)
- [Kubernetes Networking](./kubernetes/kubernetes_networking.md)
- [TCP/UPD](./networking/tcp_udp.md)
- [SSL Protocol](./networking/ssl_protocol.md)

## Github CI/CD

Learn how to implement continuous integration and continuous deployment (CI/CD) workflows using GitHub Actions.

- [Git Commands](./github/git_commands.md)
- [CI/CD](./github/cicd.md)
  - [Sample Python Pipeline](./github/piplines_sample/ci_pipeline_python.md)
  - [Sample Typescript Pipeline](/github/piplines_sample/ci_pipeline_typescript.md)
  - [Sample AWS CD Pipeline](/github/pipelines_samples/cd_pipeline_aws.md)
- [CI/CD Security](./github/cicd_security.md)

## Linux

Discover a range of useful Linux commands that can help improve your efficiency and effectiveness on the command line.

- [Useful commands](./linux/useful_commands.md)

## Infrastructure as Code (IaC)

Best practices and tips for managing infrastructure using code.

  - [Best Practices for IaC](./iac/best_practices.md)
  - [Terraform]
    - [Terraform Best Practices](./iac/terraform_best_practices.md)
    - [Terraform Key Conepts](./iac/terraform_key_concepts.md)
    - [Terraform Code Structure](./iac/terraform_code.md)
  - [Ansible](./iac/whats_ansible.md)
    - [Ansible Playbooks](./iac/ansible_playbooks.md)
    - [Ansible Command Line](./iac/ansible_command_line.md)
  - [Jenkins Best Practices](./iac/jenkins_best_practices.md)

## Misc

- [SDLC](./AWS/sdlc.md)
- [Devops and Cloud Certifications](./misc/devops_cloud_certifications.md)
- [Observability](./misc/observability.md)

----

## DevOps Roadmap

https://roadmap.sh/devops

----

<p float="left">
  <img src="./files/docker.png" alt="Docker" width="100" />
  <img src="./files/kubernetes.png" alt="Kubernetes" width="100" />
  <img src="./files/github.png" alt="GitHub" width="100" />
  <img src="./files/4923041_aws_icon.png" alt="AWS" width="100" />
  <img src="./files/icons8-ansible-240.png" alt="Ansible" width="100" />
  <img src="./files/icons8-terraform-240.png" alt="Terraform" width="100" />
</p>

----
----

By @radicaled42
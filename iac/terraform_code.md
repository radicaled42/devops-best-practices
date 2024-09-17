# Code Structure

Questions related to Terraform code structure are by far the most common in the community. At some point, everyone considers the best way to structure their Terraform project.

## How should I structure my Terraform configurations?

There are many possible solutions for structuring Terraform code, and it can be challenging to provide universal advice. Let's start by understanding the key factors to consider when deciding on your structure:

- **Project complexity**:
  - Number of related resources
  - Number of Terraform providers (see the note below about "logical providers")
- **Frequency of infrastructure changes**:
  - **From**: once a month/week/day
  - **To**: continuously (with every new commit)
- **Code change initiators**:
  - Do you allow the CI server to update the repository when a new artifact is built?
  - Only developers can push to the infrastructure repository
  - Everyone can propose changes by opening a PR (including automated tasks running on the CI server)
- **Deployment platform or service**:
  - AWS CodeDeploy, Kubernetes, or OpenShift might require different approaches
- **How environments are grouped**:
  - By environment, region, or project

{% hint style="info" %}
_Logical providers_ work entirely within Terraform's logic and often don't interact with external services, so their complexity is generally O(1). Common logical providers include [random](https://registry.terraform.io/providers/hashicorp/random/latest/docs), [local](https://registry.terraform.io/providers/hashicorp/local/latest/docs), [terraform](https://www.terraform.io/docs/providers/terraform/index.html), [null](https://registry.terraform.io/providers/hashicorp/null/latest/docs), and [time](https://registry.terraform.io/providers/hashicorp/time/latest).
{% endhint %}

---

## Getting Started with Structuring Terraform Configurations

When starting with Terraform, placing all code in `main.tf` is acceptable, especially when writing example code. However, as your project grows, splitting your code into multiple files based on their purpose is recommended:

- **`main.tf`**: Calls modules, locals, and data sources to create all resources
- **`variables.tf`**: Contains declarations of variables used in `main.tf`
- **`outputs.tf`**: Contains output values from the resources created in `main.tf`
- **`versions.tf`**: Contains version requirements for Terraform and providers

It's important to note that `terraform.tfvars` should only be used in the context of [composition].

---

## How to Think About Terraform Configuration Structure

{% hint style="info" %}
Please ensure that you understand the key concepts of [resource module], [infrastructure module], and [composition], as they will be used in the following examples.
{% endhint %}

---

### Common Recommendations for Structuring Code

- **Work with fewer resources**: 
  - Fewer resources make `terraform plan` and `terraform apply` faster since they involve fewer cloud API calls.
  - Having your entire infrastructure in one composition may cause delays in these processes.
- **Minimize blast radius**: 
  - Placing unrelated resources in separate compositions reduces the potential impact of errors or security breaches.
- **Start with remote state**:
  - Your local machine should not hold the source of truth for your infrastructure.
  - Managing a `tfstate` file in Git is challenging and can become a nightmare as your project scales.
- **Maintain consistent structure and naming conventions**:
  - Just like procedural code, Terraform should be written with readability in mind. This is crucial when returning to the code months later.
  - Moving resources between states is possible but much easier with consistent structure and naming.
- **Keep resource modules simple**.
- **Avoid hardcoding**: Use variables and data sources to dynamically retrieve values.
- **Use `terraform_remote_state`** as the glue between modules within the same composition.

In this book, example projects are grouped by _complexity_ — from small to very large infrastructures. This separation is not strict, so be sure to review other structures as well.

---

### Orchestration of Infrastructure Modules and Compositions

As your infrastructure grows, managing the orchestration of Terraform configurations, connecting infrastructure modules, and passing values across compositions becomes necessary. There are several orchestration tools and methods that teams use:

1. **Terraform-only**: 
   - Simple and requires only knowledge of Terraform.
2. **Terragrunt**: 
   - A dedicated orchestration tool that manages infrastructure modules and handles dependencies. It reduces code duplication and simplifies infrastructure management.
3. **In-house scripts**: 
   - Often used as a starting point before switching to a tool like Terragrunt.
4. **Ansible or similar tools**: 
   - General-purpose automation tools that can orchestrate Terraform. This method is common when teams adopt Terraform after using Ansible.
5. **Kubernetes-inspired solutions like Crossplane**: 
   - For teams leveraging the Kubernetes ecosystem, tools like Crossplane can offer reconciliation loops to achieve the desired state for your Terraform configurations. Watch the [Crossplane vs Terraform](https://www.youtube.com/watch?v=ELhVbSdcqSY) video for more details.


Bibliography:
- https://www.terraform-best-practices.com/code-structure
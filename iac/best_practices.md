# IaC Best Practices

Some fundamental best practices that apply to all Infrastructure as Code projects. These should be used in your processes regardless of your tool to manage your cloud infrastructure. 

1. Use version control and prevent manual changes

This seems like an obvious statement in 2024, but it’s the basis of everything else. We should treat our infrastructure configurations as application code and apply the same best practices for managing, testing, reviewing, and bringing it to production. We should embrace a GitOps approach that fits our use case and implement an automated CI/CD workflow for applying changes. See: How to Use Terraform with GitOps.

2. Shift your culture to Collaborative IaC

Keeping your infrastructure in version-controlled repositories is the first step to improving your manual infrastructure management. Next, we should strive to enable usage across teams with self-service infrastructure, apply policies and compliance according to our organization’s standards, and access relevant insights and information. Thankfully, Spacelift can assist you along the way to achieving these.

**Bibliography**:
- https://spacelift.io/blog/terraform-best-practices
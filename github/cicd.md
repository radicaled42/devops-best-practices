# Github - Development

## Continuous Integration (CI):

Continuous Integration (CI) is a development practice where developers frequently merge their code changes into a shared repository, often several times a day. Each merge **triggers an automated build and testing process**, allowing teams to detect and address issues early in the development cycle. The primary goal of CI is to ensure that new code integrates seamlessly with the existing codebase, preventing integration problems and reducing the time it takes to deliver features or fixes.

## Continuous Delivery (CD):

Continuous Delivery (CD) is an extension of Continuous Integration that focuses on ensuring that code is always in a deployable state. After code changes pass the CI process, they are automatically **staged** for **deployment**, often to a testing or staging environment. CD enables teams to release updates to production at any time with minimal manual intervention, by automating the entire software release process from integration to deployment readiness.

## Continuous Deployment:

Continuous Deployment takes Continuous Delivery one step further by automatically deploying every change that passes the CI and CD processes directly to **production**. In this approach, there are no manual deployment steps, and every successful build that passes all tests is automatically released to users. Continuous Deployment ensures that new features, improvements, and bug fixes reach users as quickly as possible, providing a continuous flow of updates without human intervention in the deployment process.
**The difference between continuous delivery and continuous deployment is the presence of a manual approval to update to production**

## CI vs CD: What is the Difference Between Continuous Integration and Continuous Delivery?

### Continuous Integration (CI):

CI, as its name suggests, is the practice of frequently integrating code changes into a shared repository. Every integration triggers automated builds and tests to quickly identify issues. This process reduces the complexity and cost of fixing problems later in the development cycle, ensuring that code is always in a good state and preventing the "works on my machine" issue.

### Continuous Delivery (CD):

CD automates the software release process, enabling teams to deliver new code to users as quickly and safely as possible. After passing the CI stage, the code is automatically prepared for production. The key here is automation—ensuring the code can be deployed at any time with confidence.

### Key Differences Between Continuous Integration and Continuous Delivery:

While CI and CD often work in sync, their scope is different:

- **Continuous Integration** focuses on integrating code frequently into a shared repository, followed by automated testing to catch defects early.
- **Continuous Delivery** focuses on automating the release pipeline so that any change passing through CI is ready for deployment.

Sometimes, CD is also used to refer to Continuous Deployment. Continuous Deployment is similar to Continuous Delivery, but the releases happen automatically without manual approval.

Here's a table summarizing the differences between Continuous Integration and Continuous Delivery:

| **Continuous Integration** | **Continuous Delivery** |
|----------------------------|-------------------------|
| Integrates code into the shared repository frequently. | Automates the process after CI, preparing code for deployment to production. |
| Main focus is on catching issues early by frequently testing integrated code. | Main focus is ensuring code is always in a deployable state. |
| Uses automation to quickly detect issues before they become larger problems. | Uses automation to release code to staging or production environments. |
| Reduces integration issues, speeds up the development process, and improves code quality. | Ensures quick, safe releases, reduces risks, and delivers new features faster. |
| Less complex and costly compared to CD. | More complex, involving deployment automation and multiple environments (e.g., staging, production). |

### Conclusion:

- **CI** ensures code integration is smooth and defect-free.
- **CD** ensures code is always ready for deployment.
- **Continuous Deployment** goes a step further and automates the entire process, pushing code into production with no manual intervention.

### Bibliography

- [Atlassian: Continuous Integration and Continuous Delivery](https://www.atlassian.com/continuous-delivery/continuous-integration)

# Github - Development

## Continuous Integration (CI):

Continuous Integration is a development practice where developers frequently merge their code changes into a shared repository, often several times a day. Each merge triggers an automated build and testing process, allowing teams to detect and address issues early in the development cycle. The primary goal of CI is to ensure that new code integrates seamlessly with the existing codebase, preventing integration problems and reducing the time it takes to deliver features or fixes.

## Continuous Delivery (CD):

Continuous Delivery is an extension of Continuous Integration that focuses on automatically preparing code for release. After code changes pass the CI process, they are automatically staged for deployment, often to a testing or staging environment. CD ensures that the code is always in a deployable state, enabling teams to release updates to production at any time with minimal manual intervention. The emphasis is on automating the entire software release process, from integration to deployment readiness.

## Continuous Deployment:

Continuous Deployment takes Continuous Delivery a step further by automatically deploying every change that passes the CI and CD processes directly to production. In this approach, there are no manual deployment steps, and every successful build that passes all tests is released to users. Continuous Deployment ensures that new features, improvements, and bug fixes reach users as quickly as possible, providing a continuous flow of updates without the need for human intervention in the deployment process.


## CI vs CD: Difference between Continuous Integration and Continuous Delivery?

### What is Continuous Integration (CI)

CI, as its name suggests, is a process that occurs prior to a build in which code is tested. It demands developers to regularly integrate or merge code into a shared repository. It often results in greater long-term cost savings, as it is more expensive to repair problems in high-level design uncovered later in the process. It is regarded as a superior method of developing software since it minimises the number of defects when features are merged and resolves the issue of “works on my machine.”

### What is Continuous Delivery (CD)

CD, as its name implies, is a technique that leverages automation to expedite the delivery of new code. Teams build, test, and release software as quickly as feasible in short cycles. It generally assures that any modification made is releasable by automating the entire release process. One is capable of delivering to production. The most significant aspect is the thoroughness of checks.

### The Difference Between Continuous Integration and Continuous Delivery

Since CI and CD often function in sync, it is easy to be confused as to the scope of their activities. The below diagram can help in obtaining a clear understanding of what this does.

Since CI and CD often function in sync, it is easy to be confused as to the scope of their activities. The below diagram can help in obtaining a clear understanding of what this does.

Sometimes CD is also used to refer to Continuous Deployment. Continuous deployment is similar to continuous delivery with the exception that releases occur automatically.

While not the direct scope of this article, the difference between Continuous Integration and Deployment is shown as below.

The main points of difference between Continuous Integration and Continuous Delivery are tabulated as below:

| **Continuous Integration** | **Continuous Delivery** |
|----------------------------|-------------------------|
| It is the integration of code into the mainstream code base. | It is the process of testing, staging, and deploying code that occurs after code integration in order to deliver app updates to users. |
| It is specifically built to incorporate code changes into a shared repository on a regular basis. | It is specifically built to incorporate code changes into a shared repository on a regular basis. |
| Its primary objective is to offer timely feedback so that any flaw in the code base may be quickly discovered and fixed. | Its primary objective is to ensure that the code base is always deployable to the production environment. |
| It employs automation to quickly discover issues and validate the accuracy of new code prior to integration. | Automation is used to expedite the release of new code. |
| It is crucial because it enables greater transparency and foresight in the software development and delivery process. | That is crucial because it makes our release processes as efficient and repeatable as feasible. |
| It often decreases expenses, instils confidence, ensures a consistent construction process, mitigates hazards, improves team communication, etc. | It generally reduces risk, delivers software with fewer problems, responds rapidly to market conditions, and releases new products more regularly, among other benefits. |
| It offers additional benefits to developers because it enables code to be tested automatically and integrated continually with the code of other developers and the current code base. | As soon as code is accepted successfully in the CI stage and its logical functionality can be tested, it is made available to business users. |
| This procedure is less complicated and less expensive than CD. | This procedure is more complicated and expensive than CI. |


### Bibliography

- https://www.atlassian.com/continuous-delivery/continuous-integration
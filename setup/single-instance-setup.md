---
description: >-
  Single Instance Setup is the aggregation of all the internal environments like
  QA, DEV, UAT, and STAGING.
---

# Single Instance Setup



## Pre-read:

* Know about EKS: [https://www.youtube.com/watch?v=SsUnPWp5ilc](https://www.youtube.com/watch?v=SsUnPWp5ilc)
* Know what is terraform: [https://youtu.be/h970ZBgKINg](https://youtu.be/h970ZBgKINg)

## Prerequisites <a href="#prerequisites" id="prerequisites"></a>

* [**AWS account**](https://portal.aws.amazon.com/billing/signup?nc2=h\_ct\&src=default\&redirect\_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) with the admin access to provision EKS Service, you can always subscribe to free AWS account to learn the basics and try, but there is a limit to [**what is offered as free**](https://aws.amazon.com/free/), for this demo you need to have a commercial subscription to the EKS service, if you want to try out for a day or two, it might cost you about Rs 500 - 1000. **(Note: Post the Demo, for the internal folks, eGov will provide a 2-3 hrs time bound access to eGov's AWS account based on the request and available number of slots per day)**
* Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine that helps you interact with the kubernetes cluster
* Install [**Helm**](https://helm.sh/docs/intro/install/) that helps you package the services along with the configurations, envs, secrets, etc into a \*\*\*\*[**kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)
* Install [**terraform**](https://releases.hashicorp.com/terraform/0.14.10/) version (0.14.10) for the Infra-as-code (IaC) to provision cloud resources as code and with desired resource graph and also it helps to destroy the cluster at one go.
* \*\*\*\*[**Install AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) \*\*\*\*on your local machine so that you can use aws cli commands to provision and manage the cloud resources on your account.
* Install [**AWS IAM Authenticator**](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html) that helps you authenticate your connection from your local machine so that you should be able to deploy DIGIT services.
*   Use the [**AWS IAM User**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_users\_create.html) **credentials provided** for the Terraform ([**Infra-as-code**](https://devops.digit.org/devops-general/infra-as-code)) to connect with your AWS account and provision the cloud resources.

    1. You'll get a **Secret Access Key** and **Access Key ID**. **Save them safely.**
    2. Open the terminal and Run the following command you have already installed the AWS CLI and you have the credentials saved. (Provide the credentials and you can leave the region and output format as blank)




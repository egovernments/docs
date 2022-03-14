---
description: >-
  Single Instance Setup is the aggregation of all the internal environments like
  QA, DEV, UAT, and STAGING.
---

# Single Instance Setup

### **Objectives:** <a href="#objectives" id="objectives"></a>

* Provision cluster with an individual node pool and affinity according to each environment.
* Prepare the respective \<env>.yaml files. [https://github.com/egovernments/DIGIT-DevOps/tree/singleinstance/deploy-as-code/helm/environments](https://github.com/egovernments/DIGIT-DevOps/tree/singleinstance/deploy-as-code/helm/environments)
* Prepare the [product-release-charts](https://github.com/egovernments/DIGIT-DevOps/tree/singleinstance/deploy-as-code/helm/product-release-charts)
* Deploy the backbone(Kafka, Zookeeper, ES, etc) services and cluster-configs (RBAC, network-policy, namespaces, etc)
* Deploy the specific services to each environment specific namespace.



&#x20;   ****   &#x20;

### Pre-read:

* Know about EKS: [https://www.youtube.com/watch?v=SsUnPWp5ilc](https://www.youtube.com/watch?v=SsUnPWp5ilc)
* Know what is terraform: [https://youtu.be/h970ZBgKINg](https://youtu.be/h970ZBgKINg)
* Know sops to secure your keys/creds: [https://www.youtube.com/watch?v=DWzJ87KbwxA](https://www.youtube.com/watch?v=DWzJ87KbwxA)
* Know the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes\_kubectl\_commands.htm) commands.
* Know how to manage env values, secrets of any service deployed in kubernetes [https://www.youtube.com/watch?v=OW244LxB4oI](https://www.youtube.com/watch?v=OW244LxB4oI)



## Prerequisites <a href="#prerequisites" id="prerequisites"></a>

* [**AWS account**](https://portal.aws.amazon.com/billing/signup?nc2=h\_ct\&src=default\&redirect\_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) with admin access to provision EKS Service, you can always subscribe to a free AWS account to learn the basics and try.
* Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine that helps you interact with the kubernetes cluster
* Install [**Helm**](https://helm.sh/docs/intro/install/) that helps you package the services along with the configurations, envs, secrets, etc into a \*\*\*\*[**kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)
* Install [**terraform**](https://releases.hashicorp.com/terraform/0.14.10/) version (0.14.10) for the Infra-as-code (IaC) to provision cloud resources as code and with desired resource graph and also it helps to destroy the cluster at one go.
* Install [**Mozilla Sops**](https://github.com/mozilla/sops#:\~:text=SOPS%20has%20the%20ability%20to,to%20the%20least%20secure%20one) **** is an editor of encrypted files that supports YAML, JSON, ENV, INI and BINARY formats and encrypts with AWS KMS, GCP KMS, Azure Key Vault, age, and PGP.
* Domain.
* [**Go lang** ](https://golang.org/doc/install)(v. 1.13) that helps you to deploy helm manifests.
* \*\*\*\*[**Install AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) \*\*\*\*on your local machine so that you can use aws cli commands to provision and manage the cloud resources on your account.
* Install [**AWS IAM Authenticator**](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html) that helps you authenticate your connection from your local machine so that you should be able to deploy DIGIT services.
*   Use the [**AWS IAM User**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_users\_create.html) **credentials provided** for the Terraform ([**Infra-as-code**](https://devops.digit.org/devops-general/infra-as-code)) to connect with your AWS account and provision the cloud resources.

    1. You'll get a **Secret Access Key** and **Access Key ID**. **Save them safely.**
    2. Open the terminal and Run the following command you have already installed the AWS CLI and you have the credentials saved. (Provide the credentials and you can leave the region and output format as blank)

    &#x20;

```
aws configure --profile egov-workshop-account 

AWS Access Key ID []:<Your access key>
AWS Secret Access Key []:<Your secret key>
Default region name []: ap-south-1
Default output format []: text
```

The above will create the following file In your machine as /Users/\<your username>/.aws/credentials

```
[egov-test-account] 
aws_access_key_id=*********** 
aws_secret_access_key=****************************
```

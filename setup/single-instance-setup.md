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

## Single Instance with  Multi-Tenancy:

Kubernetes clusters are typically used by several teams. In other cases, Kubernetes can be used to deliver applications to end users requiring segmentation and isolation of resources across users from different environments. Secure sharing of Kubernetes control plane and node pools resources allows maximizing productivity and saving costs in both cases.

![Multitenancy](<../.gitbook/assets/image (307).png>)

### Namespaces as a Service:    <a href="#namespaces-as-a-service" id="namespaces-as-a-service"></a>

With the _namespaces-as-a-service_ model, tenants share a cluster, and tenant workloads are restricted to a set of Namespaces assigned to the tenant. The cluster control plane resources like the API server and scheduler, and worker node resources like CPU, memory, etc. are available for use across all tenants.

To isolate tenant workloads, We do the following configuration to each namespace:

* [**role bindings**](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding)**:** for controlling access to the namespace
* [**network policies**](https://kubernetes.io/docs/concepts/services-networking/network-policies/)**:** to prevent network traffic across tenants

## Single Instance Setup:

[**Terraform**](https://www.terraform.io/intro/index.html) helps you build a graph of all your resources, and parallelizes the creation and modification of any non-dependent resources. Because of this, Terraform builds infrastructure as efficiently as possible, and operators get insight into dependencies in their infrastructure.

Before we provision the cloud resources, we need to understand and be sure about what resources need to be provisioned by terraform. The following picture shows the various key components. (EKS, Worker Nodes, node pool, Postgres DB, EBS Volumes, Load Balancer)     &#x20;



The following is the resource graph that we are going to provision using terraform in a standard way so that every time and for every env, it'll have the same infra.

* EKS Control Plane (Kubernetes Master)
* Work node group (VMs with the estimated number of vCPUs, Memory)
* Node pools (VMs with the estimated number of vCPUs, Memory ,and taints)
* Auto Scaling Group
* EBS Volumes (Persistent Volumes)
* RDS (PostGres)
* VPCs (Private network)
* Users to access, deploy ,and read-only

## Understand the **Resource Graph in** Terraform script: <a href="#set-up-and-initialize-your-terraform-workspace" id="set-up-and-initialize-your-terraform-workspace"></a>

* Ideally, one would write the terraform script from the scratch using this [doc](https://learn.hashicorp.com/collections/terraform/modules).
* Here we have already written the terraform script that provisions the production-grade DIGIT Infra and can be customized with the specified configuration.
* Let's Clone the DIGIT-DevOps GitHub repo where the terraform script to provision EKS cluster is available.

```
root@ip:/# git clone -b singleinstance https://github.com/egovernments/DIGIT-DevOps 
```

```
cd /DIGIT-DevOps/infra-as-code/terraform/single-instance-tf

└── modules
    ├── db
    │   └── aws
    │       ├── main.tf
    │       ├── outputs.tf
    │       └── variables.tf
    ├── kubernetes
    │   └── aws
    │       ├── eks-cluster
    │       │   ├── main.tf
    │       │   ├── outputs.tf
    │       │   └── variables.tf
    │       ├── network
    │       │   ├── main.tf
    │       │   ├── outputs.tf
    │       │   └── variables.tf
    │       └── workers
    │           ├── main.tf
    │           ├── outputs.tf
    │           └── variables.tf
    └── storage
    |    └── aws
    |       ├── main.tf
    |       ├── outputs.tf
    |       └── variables.tf
    └── node-pool
        └── aws
        |    ├── main.tf
        |    ├── outputs.tf
        |    └── variables.tf
        └── azure
            ├── main.tf
            ├── outputs.tf
            └── variables.tf    
               
                    
            
```



In here, you will find the **main.tf** under each of the modules that has the provisioning definition for resources like EKS cluster, RDS, and Storage, etc. All these are modularized and react as per the customized options provided.

**Example:**

* **VPC Resources:**
  * VPC
  * Subnets
  * Internet Gateway
  * Route Table
* **EKS Cluster Resources:**
  * IAM Role to allow EKS service to manage other AWS services
  * EC2 Security Group to allow networking traffic with EKS cluster
  * EKS Cluster
* **EKS Worker Nodes Resources:**
  * IAM role allowing Kubernetes actions to access other AWS services
  * EC2 Security Group to allow networking traffic
  * Data source to fetch latest EKS worker AMI
  * AutoScaling Launch Configuration to configure worker instances
  * AutoScaling Group to launch worker instances
* **Database**
  * Configuration in this directory creates set of RDS resources including DB instance, DB subnet group, and DB parameter group.
* **Storage Module**
  * Configuration in this directory creates EBS volume and attaches it together.
* **Node Pool**

&#x20;                &#x20;



****



****

&#x20; &#x20;

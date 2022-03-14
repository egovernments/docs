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

## Taints and Tolerations

[_Node affinity_](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) is a property of [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) that _attracts_ them to a set of [nodes](https://kubernetes.io/docs/concepts/architecture/nodes/) (either as a preference or a hard requirement). _Taints_ are the opposite -- they allow a node to repel a set of pods.

_Tolerations_ are applied to pods, and allow (but do not require) the pods to schedule onto nodes with matching taints.

Taints and tolerations work together to ensure that pods are not scheduled onto inappropriate nodes. One or more taints are applied to a node; this marks that the node should not accept any pods that do not tolerate the taints.

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
cd /DIGIT-DevOps/infra-as-code/terraform/

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

****

1. The following main.tf with create s3 bucket to store all the state of the execution to keep track.

```
DIGIT-DevOps/infra-as-code/terraform/single-instance-tf/remote-state
```

```
provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "terraform_state" {
  bucket = "single-instance-terraform-state"

  lifecycle {
    prevent_destroy = true
  }
}

resource "aws_s3_bucket_versioning" "versioning" {
  bucket = aws_s3_bucket.terraform_state.id
  versioning_configuration {
    status = "Enabled"
  }
}


resource "aws_dynamodb_table" "terraform_state_lock" {
  name           = "single-instance-terraform-state"
  read_capacity  = 1
  write_capacity = 1
  hash_key       = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

&#x20;2\. The following main.tf contains the detailed resource definitions that need to be provisioned, please have a look at it.

```
DIGIT-DevOps/infra-as-code/terraform/single-instance-tf
```

****[**main.tf**](https://github.com/egovernments/DIGIT-DevOps/blob/singleinstance/infra-as-code/terraform/single-instance-tf/main.tf)

```
terraform {
  backend "s3" {
    bucket = "single-instance-terraform-state"
    key = "terraform"
    region = "ap-south-1"
  }
}

module "network" {
  source             = "../modules/kubernetes/aws/network"
  vpc_cidr_block     = "${var.vpc_cidr_block}"
  cluster_name       = "${var.cluster_name}"
  availability_zones = "${var.network_availability_zones}"
}


module "iam_user_deployer" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-deployer"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "egovterraform" has uploaded his public key here - https://keybase.io/egovterraform/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

module "iam_user_admin" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-admin"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "egovterraform" has uploaded his public key here - https://keybase.io/egovterraform/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

module "iam_user_user" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-user"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "test" has uploaded his public key here - https://keybase.io/test/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

data "aws_eks_cluster" "cluster" {
  name = "${module.eks.cluster_id}"
}

data "aws_eks_cluster_auth" "cluster" {
  name = "${module.eks.cluster_id}"
}

provider "kubernetes" {
  host                   = "${data.aws_eks_cluster.cluster.endpoint}"
  cluster_ca_certificate = "${base64decode(data.aws_eks_cluster.cluster.certificate_authority.0.data)}"
  token                  = "${data.aws_eks_cluster_auth.cluster.token}"
  #load_config_file       = false
}

module "eks" {
  source          = "terraform-aws-modules/eks/aws"
  version         = "17.24.0"
  cluster_name    = "${var.cluster_name}"
  vpc_id          = "${module.network.vpc_id}"
  cluster_version = "${var.kubernetes_version}"
  subnets         = "${concat(module.network.private_subnets, module.network.public_subnets)}"

  worker_groups = [
    {
      name                          = "spot"
      subnets                       = "${concat(slice(module.network.private_subnets, 0, length(var.availability_zones)))}"
      override_instance_types       = "${var.override_instance_types}"
      kubelet_extra_args            = "--node-labels=node.kubernetes.io/lifecycle=spot"
      additional_security_group_ids = ["${module.network.worker_nodes_sg_id}"]
      asg_max_size                  = 1
      asg_desired_capacity          = 1
      spot_allocation_strategy      = "capacity-optimized"
      spot_instance_pools           = null
    }
  ]
  tags = "${
    tomap({
      "kubernetes.io/cluster/${var.cluster_name}" = "owned",
      "KubernetesCluster" = "${var.cluster_name}"
    })
  }"
  map_users    = [
    {
      userarn  = "${module.iam_user_deployer.iam_user_arn}"
      username = "${module.iam_user_deployer.iam_user_name}"
      groups   = ["system:masters"]
    },
    {
      userarn  = "${module.iam_user_admin.iam_user_arn}"
      username = "${module.iam_user_admin.iam_user_name}"
      groups   = ["global-readonly", "digit-user"]
    },
    {
      userarn  = "${module.iam_user_user.iam_user_arn}"
      username = "${module.iam_user_user.iam_user_name}"
      groups   = ["global-readonly"]
    },    
  ]
 
}

module "es-master" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "es-master"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "10"
  
}
module "es-data-v1" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "es-data-v1"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "100"
  
}

module "zookeeper" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "zookeeper"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "10"
  
}

module "kafka" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "kafka"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "100"
  
}

data "aws_security_group" "node_sg" {
 tags = {
    Name = "${var.cluster_name}-eks_worker_sg"
  }
  depends_on = [
   module.eks
  ]
}

module "node-group" {    // Node Pool
  for_each = toset(["qa", "dev", "uat", "staging" ])  // Define respective environments
  source = "../modules/node-pool/aws"

  cluster_name        = "${var.cluster_name}"
  node_group_name     = "${each.key}-ng"
  kubernetes_version  = "${var.kubernetes_version}"
  security_groups     =  ["${module.network.worker_nodes_sg_id}", "${data.aws_security_group.node_sg.id}"]
  subnet              = "${concat(slice(module.network.private_subnets, 0, length(var.availability_zones)))}"
  node_group_max_size = 1
  node_group_desired_size = 1

  depends_on = [
    module.network , module.eks
  ]  
}
```

## Custom variables/configurations: <a href="#set-up-an-environment" id="set-up-an-environment"></a>

You can define your configurations in **variables.tf** and provide the env specific cloud requirements so that using the same terraform template you can customize the configurations.

```
├── single-instance-tf
│   ├── main.tf 
│   ├── outputs.tf
│   ├── providers.tf
│   ├── remote-state
│   │   └── main.tf
│   └── variables.tf
```

Following are the values that you need to mention in the following files, the blank ones will be prompted for inputs while execution.

\*\*\*\*[**variables.tf**](https://github.com/egovernments/DIGIT-DevOps/blob/singleinstance/infra-as-code/terraform/single-instance-tf/variables.tf)****

```
#
# Variables Configuration
#

variable "cluster_name" {                   // Define Cluster Name
  default = "single-instance"
}

variable "vpc_cidr_block" {                 // Define CIDR Block
  default = "192.168.0.0/16"
}

variable "network_availability_zones" {     // Define Availability Zones
  default = ["ap-south-1b", "ap-south-1a"]
}

variable "availability_zones" {
  default = ["ap-south-1b"]
}

variable "kubernetes_version" {              // Define Kubernetes Vserion
  default = "1.20"
}

variable "instance_type" {
  default = "m4.xlarge"
}

variable "override_instance_types" {         
  default = ["r5a.large", "r5ad.large", "r5d.large", "m4.xlarge"]
  
}

variable "number_of_worker_nodes" {
  default = "2"
}

variable "ssh_key_name" {
  default = "test-singleinstance"
}
variable "iam_keybase_user" {
 default = "keybase:egovterraform"
}


```



### **Important: Create your own keybase key before you run the terraform**

* Use this URL [https://keybase.io/](https://keybase.io) to [create your own PGP key](https://pgpkeygen.com), this will create both public and private key in your machine, upload the public key into the [keybase](https://keybase.io) account that you have just created, and give a name to it and ensure that you mention that in your terraform. This allows to encrypt all the sensitive information.
  * Example user keybase user in eGov case is "_egovterraform_" needs to be created and has to uploaded his public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp\_keys.asc)
  * you can use this [portal](https://8gwifi.org/pgpencdec.jsp) to Decrypt your secret key. To decrypt PGP Message, Upload the PGP Message, PGP Private Key and Passphrase.

## Run terraform

Now that we know what the terraform script does, the resources graph that it provisions and what custom values should be given with respect to your env.

Let's begin to run the terraform scripts to provision infra required to Deploy DIGIT on AWS.

1. First CD into the following directory and run the following command 1-by-1 and watch the output closely.

```
cd DIGIT-DevOps/infra-as-code/terraform/single-instance-tf/remote-state
terraform init
terraform plan
terraform apply


cd DIGIT-DevOps/infra-as-code/terraform/single-instance-tf
terraform init
terraform plan
terraform apply
```

Upon Successful execution following resources gets created which can be verified by the command "terraform output"

* **s3 bucket:** to store terraform state.
* **Network:** VPC, security groups.
* **IAM users auth:** using keybase to create admin, deployer, the user. Use this URL [https://keybase.io/](https://keybase.io) to [create your own PGP key](https://pgpkeygen.com), this will create both public and private key in your machine, upload the public key into the [keybase](https://keybase.io) account that you have just created, and give a name to it and ensure that you mention that in your terraform. This allows to encrypt all the sensitive information.
  * Example user keybase user in eGov case is "_egovterraform_" needs to be created and has to uploaded his public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp\_keys.asc)
  * you can use this [portal](https://8gwifi.org/pgpencdec.jsp) to Decrypt your secret key. To decrypt PGP Message, Upload the PGP Message, PGP Private Key and Passphrase.
* **EKS cluster:** with master(s) & worker node(s).
* **Node Pools:** with worker nodes and taints.
* **Storage(s):** for es-master, es-data-v1, es-master-infra, es-data-infra-v1, zookeeper, kafka, kafka-infra.

1. Use this link to [get the kubeconfig from EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html) to get the kubeconfig file and being able to connect to the cluster from your local machine so that you should be able to deploy DIGIT services to the cluster.

```
aws sts get-caller-identity

# Run the below command and give the respective region-code and the cluster name
aws eks --region <region-code> update-kubeconfig --name <cluster_name>
```

1. Finally, Verify that you are able to connect to the cluster by running the following command and list taints on node group nodes.

```
kubectl config use-context <your cluster name>

kubectl get nodes

NAME                                            STATUS   ROLES    AGE   VERSION
ip-192-168-74-92.ap-south-1.compute.internal    Ready    <none>   20d   v1.20.11-eks-f17b81
ip-192-168-81-18.ap-south-1.compute.internal    Ready    <none>   21d   v1.20.11-eks-f17b81
ip-192-168-85-104.ap-south-1.compute.internal   Ready    <none>   21d   v1.20.11-eks-f17b81
ip-192-168-89-128.ap-south-1.compute.internal   Ready    <none>   21d   v1.20.11-eks-f17b81
ip-192-168-90-245.ap-south-1.compute.internal   Ready    <none>   20d   v1.20.11-eks-f17b81
```

```
kubectl get nodes -o json | jq '.items[].spec.taints'

[
  {
    "effect": "NoSchedule",
    "key": "dedicated",
    "value": "staging-ng"
  }
]
null
null
[
  {
    "effect": "NoSchedule",
    "key": "dedicated",
    "value": "dev-ng"
  }
]
[
  {
    "effect": "NoSchedule",
    "key": "dedicated",
    "value": "qa-ng"
  }
]
[
  {
    "effect": "NoSchedule",
    "key": "dedicated",
    "value": "uat-ng"
  }
]
```

---
description: Provision infra for DIGIT on AWS using Terraform
layout: landing
---

# On AWS

The [**Amazon Elastic Kubernetes Service (EKS)**](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html) is one of the AWS services for deploying, managing, and scaling any distributed and containerized workloads, here we can provision the EKS cluster on AWS from ground up and using an automated way (infra-as-code) using [**terraform**](https://www.terraform.io/intro/index.html) and then deploy the DIGIT Services config-as-code using [**Helm**](https://helm.sh/docs/).

## Pre-reads

* Know about EKS: [https://www.youtube.com/watch?v=SsUnPWp5ilc](https://www.youtube.com/watch?v=SsUnPWp5ilc)
* Know what is terraform: [https://youtu.be/h970ZBgKINg](https://youtu.be/h970ZBgKINg)

## Installation Steps

{% content-ref url="1.-pre-requisites.md" %}
[1.-pre-requisites.md](1.-pre-requisites.md)
{% endcontent-ref %}

{% content-ref url="2.-understanding-eks.md" %}
[2.-understanding-eks.md](2.-understanding-eks.md)
{% endcontent-ref %}

{% content-ref url="3.-setup-aws-account.md" %}
[3.-setup-aws-account.md](3.-setup-aws-account.md)
{% endcontent-ref %}

{% content-ref url="4.-infra-as-code-terraform.md" %}
[4.-infra-as-code-terraform.md](4.-infra-as-code-terraform.md)
{% endcontent-ref %}

{% content-ref url="5.-prepare-deployment-config.md" %}
[5.-prepare-deployment-config.md](5.-prepare-deployment-config.md)
{% endcontent-ref %}

{% content-ref url="6.-deploy-digit.md" %}
[6.-deploy-digit.md](6.-deploy-digit.md)
{% endcontent-ref %}

{% content-ref url="7.-bootstrap-digit.md" %}
[7.-bootstrap-digit.md](7.-bootstrap-digit.md)
{% endcontent-ref %}

{% content-ref url="faq.md" %}
[faq.md](faq.md)
{% endcontent-ref %}

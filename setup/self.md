---
description: Deployments made easy
---

# Self Provision

The Deployment to the Kubernetes cluster is made very simple and easy. We have a single Jenkins Job which does everything for you.&#x20;

### **Prerequisites**

1. **Create/Update the Product Charts with the relevant version and its dependency modules in the  below directory,**
2. **Create/Update respective environment file**

{% embed url="https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/product-release-charts" %}
**Product release Charts**&#x20;
{% endembed %}

{% embed url="https://github.com/egovernments/DIGIT-DevOps/tree/singleinstance/deploy-as-code/helm/environments" %}
**environment files**
{% endembed %}

## Preparation of Environment files

[Here](https://github.com/egovernments/DIGIT-DevOps/tree/singleinstance/deploy-as-code/helm/environments), We have each project wise and environments specific files like **digit** and **urban-dev, urban-qa, urban-uat, urban-staging,** etc.

### Namespace structure

The namespace structure is quite different from the existing setup, Here we have the below mentioned namespaces and each would contain the respective services.

**DIGIT**:- This namespace would contain all backbone services and core services.

**QA**:- It'd contain each project wise QA environment specific services.

**DEV**:- It'd contain project wise Dev environment specific services.

**UAT**:- It'd contain project wise Uat environment specific services.

**STAGING**:- It'd contain project wise Staging environment specific services.



![NameSpace Structure](<../.gitbook/assets/Untitled Diagram.drawio.png>)

## **Deployment**

**Deployment Job's:** [**https://builds.digit.org/job/singledeployments/**](https://builds.digit.org/job/singledeployments/)****

**Self Provision Job:** [**https://builds.digit.org/job/self-provision/job/deploy/**](https://builds.digit.org/job/self-provision/job/deploy/)****

The Self Provision Jenkins Job gives the flexibility for you to select/configure the following fields,

**Environments** - Displays the K8s cluster environment which you want to deploy your Services/Modules.

**Project** - Displays the Project that you want to deploy.

**Release-Version** - Displays the Version that you want to deploy.

**Core-Platform** - Displays the Core Platforms of the Project selected.

**Feature-Modules** - Displays the modules available in your selected platform.

**Cluster-Configs** - When checked deploys the cluster configs along with your selected services/modules.

**Print\_Manifest** - When checked prints the Manifest that got rendered so that you can review it before deployment.

![Jenkins Self Provision Job](<../.gitbook/assets/Screenshot 2022-03-28 at 11.26.38 AM.png>)

Once the above fields are filled up, we are done with our work. Now a single click on the build button will provision the whole product for you in the Kubernetes Cluster.\

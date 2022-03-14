---
description: Deployments made easy
---

# Self Provision

The Deployment to the Kubernetes cluster is made very simple and easy. We have a single Jenkins Job which does everything for you.&#x20;

### **Prerequisites**

**Create/Update the Product Charts with the relevant version and its dependency modules in the  below directory,**

****[**https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/product-release-charts**](https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/product-release-charts)****

### **Deployment**

The Self Provision Jenkins Job gives the flexibility for you to select/configure the following fields,

**Environments** - Displays the K8s cluster environment which you want to deploy your Services/Modules.

**Project** - Displays the Project that you want to deploy.

**Release-Version** - Displays the Version that you want to deploy.

**Core-Platform** - Displays the Core Platforms of the Project selected.

**Feature-Modules** - Displays the modules available in your selected platform.

**Cluster-Configs** - When checked deploys the cluster configs along with your selected services/modules.

**Print\_Manifest** - When checked prints the Manifest that got rendered so that you can review it before deployment.

![Jenkins Self Provision Job](<../.gitbook/assets/image (309).png>)

Once the above fields are filled up, we are done with our work. Now a single click on the build button will provision the whole product for you in the Kubernetes Cluster.\

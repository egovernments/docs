# Single Instance Deployment

### **Prerequisites**

**Create/Update project respective environment files**



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



![NameSpace Structure](<../../.gitbook/assets/Untitled Diagram.drawio (1).png>)

## **Deployment**

**Deployment Job's:** [**https://builds.digit.org/job/singledeployments/**](https://builds.digit.org/job/singledeployments/)****

![Single Instance Deploment Jobs](<../../.gitbook/assets/Screenshot 2022-04-08 at 4.07.30 PM.png>)

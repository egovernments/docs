# Install on Cloud

Quickstart setup would have helped you to get your hands dirty and build the kubernetes cluster on a local or single VM instance,  However, DIGIT is built as cloud native at the same time cloud agnostic, running **DIGIT on production** requires an advance capabilities like HA, DRS, autoscaling, resiliency, etc.. all these capabilities are provided out of the box by the commercial clouds like **AWS, Google, Azure, VMware, OpenStack** and also private clouds like **NIC and few SDCs**, all these cloud providers provide the **kubernetes-as-a-managed-service** that makes the entire infra setup and management seamless and automated, like **infra-as-code**. 

## 1. Choose the Cloud:

* \*\*\*\*[**AWS**](on-aws.md)\*\*\*\*
* \*\*\*\*[**Azure**](on-azure.md)\*\*\*\*
* \*\*\*\*[**GCP**](on-gcp.md)\*\*\*\*
* \*\*\*\*[**NIC**](on-nic.md)\*\*\*\*
* \*\*\*\*[**SDC**](on-sdc.md)\*\*\*\*

## 2. Deploy DIGIT

Post infra setup, DIGIT Deployment has 2 stages and 2 modes. We can see the stages first and then the modes.

### 2 Stage Process

1. Prepare a **&lt;**[**env.yaml&gt; master config file**](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/dev.yaml) ****per env like dev, qa or prod, which will have following configurations, this env file need to be inline with your cluster name. 
   * service env value overrides
   * credentials, secrets \(You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a **&lt;env&gt;-secret.yaml** separately\)
   * Number of replicas of individual services
   * mdms, config repos
   * sms g/w, email g/w
   * GMap key
   * S3 Bucket for Filestore
   * DNS on which the DIGIT will be exposed
   * SSL Certificate
   * End-points configs
2. Run the digit\_setup deployment script and simply answer the questions that it asks.

```text
cd DIGIT-DevOps/deploy-as-code/egov-deployer

go run digit_setup.go

#Be prepared for the following questions
1. Do you have the Kubernetes Setup?
2. Provide the path of the intented env kubeconfig file
3. Which version of the DIGIT that you want to install
4. What DIGIT Modules that you choose to install
5. All, done, Now do you want to preview the deployment manifests 
6. Are you good to proceed with the DIGIT Installation

All Done.
```

 Done, wait and watch for 10 min, you'll have the DIGIT setup completed and the application will be running on the given DNS.

### 2 Modes of Deployment

1. From local machine
2. From CI/CD System like jenkins














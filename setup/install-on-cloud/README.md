---
description: >-
  Complete DIGIT Installation step-by-step Instructions across various Infra
  types like Public & Private Clouds
---

# Full Installation

While [**Quickstart Guide**](../quickstart.md) ****would have helped you to get your hands dirty and build the Kubernetes cluster on a local/single VM instance, which you can consider for either local development, or to understand the details involved in infra and deployment.

 However, DIGIT is a [**cloud-native**](https://www.appdynamics.com/topics/what-is-cloud-native-architecture#~3-challenges) platform at the same time [**cloud agnostic**](https://looker.com/definitions/cloud-agnostic#:~:text=Cloud%2Dagnostic%20platforms%20are%20environments,different%20features%20and%20price%20structures.), depending on the scale and performance running **DIGIT on production** requires advanced capabilities like HA, DRS, autoscaling, resiliency, etc.. all these capabilities are provided out of the box by the commercial clouds like **AWS, Google, Azure, VMware, OpenStack, etc..** and also the private clouds like **NIC** and **few SDCs implemented clouds**, all these cloud providers provide the **kubernetes-as-a-managed-service** that makes the entire infra setup and management seamless and automated, like **infra-as-code, config-as-code**. 

## 1. Choose the Cloud

Choose you cloud and follow the Instruction to setup a Kubernetes cluster before moving on to the Deployment.

{% page-ref page="on-aws.md" %}

{% page-ref page="on-azure.md" %}

{% page-ref page="on-gcp.md" %}

{% page-ref page="on-nic.md" %}

{% page-ref page="on-sdc.md" %}

## 2. Deploy DIGIT

Post infra setup \(Kubernetes Cluster\), the deployment has got 2 stages and 2 modes. We can see the stages first and then the modes. As part of a sample exercise we can deploy PGR, however deployment steps are similar, just that the prerequisites will have to be configured accordingly.    

### The 2 Stages

**Stage 1: Prepare an &lt;**[**env.yaml&gt; master config file**](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/dev.yaml)**, you can name this file as you wish which will have the following configurations, this env file need to be in line with your cluster name.** 

* each service global, local env variables 
* credentials, secrets \(You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a **&lt;env&gt;-secret.yaml** separately\)
* Number of replicas/scale of individual services  \(Depending on whether dev or prod\)
* mdms, config repos \(Master Data, ULB, Tenant details, Users, etc\)
* sms g/w, email g/w, payment g/w
* GMap key \(In case you are using Google Map services in your PGR, PT, TL, etc\)
* S3 Bucket for Filestore
* URL/DNS on which the DIGIT will be exposed
* SSL Certificate for the above URL
* End-points configs \(Internal/external\)

**Stage 2: Run the digit\_setup deployment script and simply answer the questions that it asks.**

```text
cd DIGIT-DevOps/deploy-as-code/egov-deployer

go run digit_setup.go

#Be prepared for the following questions
1. Do you have the Kubernetes Setup?
2. Provide the path of the intented env kubeconfig file
3. Which version of the DIGIT that you want to install
4. What DIGIT Modules that you choose to install (Choose PGR)
5. All, done, Now do you want to preview the deployment manifests 
6. Are you good to proceed with the DIGIT Installation

All Done.
```

All Done, wait and watch for 10 min, you'll have the DIGIT setup completed and the application will be running on the given URL.

### The 2 Modes of Deployment

Essentially, DIGIT deployment means that we need to generate Kubernetes manifests for each individual service. We use the tool called helm, which is an easy, effective and customizable packaging and deployment solution. So depending on where and which env you initiate the deployment there are 2 modes that you can deploy.

1. From local machine - whatever we are trying in this sample exercise so far. 
2. Advanced: From CI/CD System like Jenkins - Depending on how you want to setup your CI/CD and the expertise the steps will vary, however [here](../more-deploy-docs/deployment-key-concepts/cicd.md) you can find how we have setup CI/CD on Jenkins and the pipelines are created automatically without any manual intervention.

## 3. Post Deployment Steps

### 1. Role Action Mapping

Post deployment, now the application will be accessible from the configured domain.

To try out PGR employee login, Lets create a sample tenant, city, user to login and assign LME employee role.

1. To map the roles to a user, we have to do the [kubectl port-forwarding](https://phoenixnap.com/kb/kubectl-port-forward) of the **egov-user** service running from kubernetes cluster to your localhost, this will now give you access to egov-user service directly and interact with the api directly.

```text
kubectl port-forward svc/egov-user 8080:8080 -n egov
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080

```

2. Execute the below API Request either from postman or curl to perform the role mapping.

```text
curl --location --request POST 'http://localhost:8080/user/users/_createnovalidate' \
--header 'Content-Type: application/json' \
--data-raw '{
    "requestInfo": {
        "apiId": "Rainmaker",
        "ver": ".01",
        "ts": null,
        "action": "_update",
        "did": "1",
        "key": "",
        "msgId": "20170310130900|en_IN",
        "authToken": "ec6a2db1-c000-4927-af21-f4ce13c1d75f",
        "userInfo": {
            "id": 23287,
            "uuid": "4632c941-cb1e-4b83-b2d4-200022c1a137",
            "userName": "eGovEmp",
            "name": "eGovTest Employee",
            "mobileNumber": "1234567890",
            "emailId": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "superuser",
                    "code": "SUPERUSER",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "PGR Last Mile Employee",
                    "code": "PGR_LME",
                    "tenantId": "pg.citya"
                },
                {
                    "name": "superuser",
                    "code": "SUPERUSER",
                    "tenantId": "pg"
                }
            ],
            "tenantId": "pg.citya"
        }
    },
    "user": {
        "userName": "PGRLME1",
        "name": "PGRLME",
        "gender": null,
        "mobileNumber": "1234567890",
        "type": "EMPLOYEE",
        "active": true,
        "password": "eGov@4321",
        "roles": [
            {
                "name": "Employee",
                "code": "EMPLOYEE",
                "tenantId": "pg"
            },
            {
                "name": "PGR LME",
                "code": "PGR_LME",
                "tenantId": "pg.citya"
            },
            {
                "name": "superuser",
                "code": "SUPERUSER",
                "tenantId": "pg"
            }
        ],
        "tenantId": "pg.citya"
    }
}'
```

## 4. Assessment of the DIGIT Deployment

By now we have successfully completed the digit setup on cloud, use the URL that you mentioned in your env.yaml Eg: https://mysetup.digit.org and create a grievance to ensure the PGR module deployed is working fine. Refer the below product documentation for the steps. 

**Credentials:**

1. Citizen: You can use your mobile number to signup using the Mobile OTP.
2. Employee: Username: **PGRLME1** and password: **eGov@4321** 

{% page-ref page="../../modules/public-grievances-and-redressal/pgr-user-manual/" %}

##  5. Destroy the Cluster

Post validating the PGR functionality share the API response of the following request to assess the correctness of successful DIGIT PGR Deployment. 

Finally, cleanup the DIGIT Setup if you wish, using the following command. This will delete the entire cluster and other cloud resources that were provisioned for the DIGIT Setup.

```text
cd DIGIT-DevOps/infra-as-code/terraform/my-digit-eks
terraform destroy

```

## Conclusion:

All Done, we have successfully Created infra on Cloud, Deployed Digit, Bootstrapped DIGIT, Performed a Transaction on PGR and Finally Destroyed the cluster.


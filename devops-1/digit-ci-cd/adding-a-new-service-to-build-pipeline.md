# Adding New Service to build Pipeline

**As a developer -** To integrate any new service/app to the CI/CD below is the starting point:

Once the desired service is ready for the integration: decide the service name, type of service, whether DB migration is required or not. While you commit the source code of the service to the git repository, the following file should be added with the relevant details which are mentioned as below:

**Build-config.yml** –It is present under build directory in each repository

Eg: [https://github.com/egovernments/core-services/blob/master/build/build-config.yml](https://github.com/egovernments/core-services/blob/master/build/build-config.yml)

This file contains the below details which are used for creating the automated Jenkins pipeline job for your newly created service.

\# **config:**  
\#   **-** **name:** &lt; Name of the job, foo/bar would create job named bar inside folder foo &gt;  
\#     **build:**  
\#     **- work-dir:** &lt; Working directory of the app to be built &gt;  
\#       **dockerfile:** &lt; Path to the dockerfile, optional, assumes dockerfile in working directory if not provided&gt;                                                  
\#       **image-name:** &lt; Docker image name &gt;

While integrating a new service/app, the above content needs to be added in the build-config.yml file of that app repository. For example: If we are on-boarding a new service called **egov-test,** then the build-config.yml should be added as mentioned below.

_**config:  
   - name: core-services/egov-test  
     build:  
     - work-dir: egov-test  
       dockerfile: build/maven/Dockerfile  
       image-name: egov-test**_

If a job requires multiple images to be created \(DB Migration\) then it should be added as below,

_**config:  
   - name: core-services/egov-test  
     build:  
     - work-dir: egov-test  
       dockerfile: build/maven/Dockerfile  
       image-name: egov-test  
     - work-dir: egov-test/src/main/resources/db  
       dockerfile: build/maven/Dockerfile  
       image-name: egov-test-db**_

‌

**Note -** **If a new repository is created then the build-config.yml should be created under build folder and then the config values are added to it.**

‌

**The git repository URL is then added to the Job Builder parameters**

When the Jenkins Job =&gt; job builder is executed the CI Pipeline gets created automatically based on the above details in build-config.yml. Eg: **egov-test** job will be created under **core-services** folder in Jenkins because the “build-config was edited under core-services” And it should be the “master” branch only. Once the pipeline job is created, it can be executed for any feature branch with build parameters \(Specifying which branch to be built – master or any feature branch\).

‌

As a result of the pipeline execution the respective app/service docker image will be built and pushed to the docker repository.

‌

**Continuous Integration \(CI\)**

The Jenkins CI pipeline is configured and managed 'as code'. [New Service Integration - Example](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/111673399/New+Service+Integration+-+Example)

URL - [https://builds.egovernments.org/](https://builds.egovernments.org/)

**Job Builder** – Job Builder is a Generic Jenkins job which creates the Jenkins pipeline automatically which are then used to build the application, create the docker image of it and push the image to docker repository. The Job Builder job require the git repository URL as a parameter. It clones the respective git repository and reads the **build/**[**build-config.yml**](https://github.com/egovernments/core-services/blob/master/build/build-config.yml) file for each git repository and uses it to create the service build job.

‌

**Check git repository URL is available in** [**ci.yaml**](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/ci.yaml)[‌](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/ci.yaml)‌

![](../../.gitbook/assets/0%20%281%29.png)

If git repository URL is available build the Job-Builder Job

![](../../.gitbook/assets/1%20%281%29.png)

If git repository URL is not available ask devops team to add.

\*\*\*\*

**Continuous Deployment \(CD\):**‌

The services deployed and managed **on a Kubernetes cluster** in cloud platforms like **AWS, Azure, GCP, OpenStack, etc.** Here, we use **helm charts** to manage and generate the **Kubernetes manifest files** and use them for further deployment to respective **Kubernetes cluster**. Each service is created as charts which will have the below-mentioned files in it.

For Eg:

       ****_billing-service/           \# Directory – name of the service/app  
       Chart.yaml              \# A YAML file containing information about the chart  
       LICENSE                \# OPTIONAL: A plain text file containing the license for the chart  
       README.md          \# OPTIONAL: A human-readable README file  
       values.yaml            \# The default configuration values for this chart  
       templates/              \# A directory of templates that, when combined with values, will generate valid Kubernetes manifest files._

To deploy a new service, we need to create the helm chart for it. The chart should be created under the **charts/helm** directory in **eGov-infraOps** repository.

Github repository URL: ****[**https://github.com/egovernments/eGov-infraOps**](https://github.com/egovernments/eGov-infraOps) ****OR [**https://github.com/egovernments/Train-InfraOps**](https://github.com/egovernments/Train-InfraOps)\*\*\*\*

We have an automatic helm chart generator utility which needs to be installed on local machine, the utility will prompt for user inputs about the newly developed service\( app specifications\) for creating the helm chart. The requested chart with the configuration values \(created based on the inputs provided\) will be created for the user.

‌                       _**Name of the service?  test-service  
                       Application Type? NA  
                       Kubernetes health checks to be enabled ? Yes  
                       Flyway DB migration container necessary? No  
                       Expose service to the internet? Yes  
                       Route through API gateway \[zuul\] ? No  
                       Context path ? hello**_‌

The generated chart will have the following files.

                           **create Chart.yaml  
                           create values.yaml  
                           create templates/deployment.yaml  
                           create templates/service.yaml  
                           create templates/ingress.yaml**

This chart can also be modified further based on the user requirements.

The Deployment of manifests to the Kubernetes cluster is made very simple and easy. We have Jenkins Jobs for each state and environment specific. We need to provide the image name or the service name in the respective Jenkins deployment job.

![](../../.gitbook/assets/2%20%281%29.png)

Enter a caption for this image \(optional\)

![](../../.gitbook/assets/3%20%281%29.png)

Enter a caption for this image \(optional\)

‌

The deployment Jenkins job internally performs the following operations,‌

* Reads the image name or the service name given and finds the chart that is specific to it.
* Generates the Kubernetes manifests files from the chart using helm template engine.
* Execute the deployment manifest with the specified docker image\(s\) to the Kubernetes cluster


---
description: >-
  Quickstart Installation helps you jump start with the DIGIT basic installation
  steps with the limited functionalities.
---

# Quickstart

DIGIT is a distributed microservice-based platform that comprises many services which are containerized, depending upon the required features we can run only those services on any container supported orchestration platform like docker compose, Kubernetes, etc.

Here in this Quickstart guide we'll install basic services to get the platform up and running along with the PGR module, before we setup DIGIT, we'll create a lightweight Kubernetes cluster called [k3d](https://github.com/rancher/k3d) on a local machine with specified H/W requirement. The H/W requirements are listed below to ensure before we proceed further.

## **1. Infra Setup**

**To provision a lightweight Kubernetes cluster, please follow the instructions below in context to your OS and install the k3d on your machine.**&#x20;

### **H/W  or VM Size**

* min 4 vCPUs (recommended 8)
* min 8GiB of RAM (recommended 16)
* min 30GiB of HDD (recommended 30+)

### **Tools**

*   **Linux distribution running in a VM or bare metal**

    * Ubuntu 18.04 or Debian 10 (VM or bare metal)
    * Install [Docker](https://docs.docker.com/engine/install/ubuntu/)
    * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) on Linux
    * Open terminal and Install k3d on Linux using the below command

    ```
    wget -q -O - https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash       
    ```
*   **OSX or Mac**

    * [Docker Desktop](https://docs.docker.com/docker-for-mac/install/) local Kubernetes cluster enabled
    * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/) on Mac
    * Install k3d on Mac, on terminal use [Homebrew](https://brew.sh) (Homebrew is available for MacOS) using the below command

    ```
    brew install k3d  
    ```
*   **Windows 10 or above**

    * [Docker Desktop for windows](https://docs.docker.com/docker-for-windows/install/#system-requirements-for-wsl-2-backend) need to be installed
    * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/) on Windows
    * [Install Chocolatey](https://chocolatey.org) package manager for windows&#x20;
    * Install [GitBash](https://git-scm.com/download/win) as an alternative command prompt that allows most of the Linux commands on windows.
    * Now open gitbash and Install k3d on Windows using the below command

    ```
    choco install k3d
    ```

### **Infra (Kubernetes Cluster) Creation**

**Once the above prerequisites are met, run the following tasks depending upon your OS.**

* [ ] &#x20;**** login/ssh into the machine, go to terminal/command prompt and run the following commands as an admin user.
* [ ] Create /Kube directory and change permission. To use this directory for persistent data mount. This means all the container logs, data will be stored here.

```
 mkdir /kube
 chmod 777 /kube
 
 #if you are unable to create the /kube folder in the root
 # you can create it your user directory and provide the absolue path below
```

* [ ] Create a cluster with a single master node and 2 agents (Worker Nodes) and mount the pre**-**created directory (for data persistence).&#x20;

```
k3d cluster create --k3s-arg "--no-deploy=traefik@server:0" --agents 2 -v "/kube:/kube@agent:0,1" -v "/kube:/kube@server:0"  --port "80:80@loadbalancer"
```

* [ ] When cluster creation is successful, Get the kubeconfig file, which will allow you to connect the to the cluster at any time.

```
k3d kubeconfig get k3s-default > k3dconfig
kubectl config use-context k3d-k3s-default --kubeconfig=k3dconfig
```

* [ ] Verify the Cluster creation by running the following commands from your local machine where the kubectl is installed. It gives you the sample output as below

```
root@ip:/# kubectl cluster-info

OutPut:
Kubernetes control plane is running at https://0.0.0.0:33931
CoreDNS is running at https://0.0.0.0:33931/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://0.0.0.0:33931/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy
 
 
 
root@ip:/# k3d cluster list
NAME          SERVERS   AGENTS   LOADBALANCER
k3s-default   1/1       2/2      true
```

* [ ] You can verify the workers' nodes created by using the following command.

```
kubectl get nodes
 
Output:
NAME                       STATUS   ROLES                  AGE     VERSION
k3d-k3s-default-agent-0    Ready    <none>                 3d18h   v1.21.1+k3s1
k3d-k3s-default-agent-1    Ready    <none>                 3d18h   v1.21.1+k3s1
k3d-k3s-default-server-0   Ready    control-plane,master   3d18h   v1.21.1+k3s1
 
 
kubectl top nodes

Output:
W0625 07:56:24.588781   12810 top_node.go:119] Using json format to get metrics. Next release will switch to protocol-buffers, switch early by passing --use-protocol-buffers flag
NAME                       CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
k3d-k3s-default-agent-0    547m         6%     1505Mi          9%        
k3d-k3s-default-agent-1    40m          0%     2175Mi          13%       
k3d-k3s-default-server-0   59m          0%     2286Mi          14%  
 
```

If the above steps are completed successfully, your Cluster is now up and running ready to proceed with the DIGIT Deployment.

## **2. DIGIT Setup**

Now that we have the Infra setup to proceed with the DIGIT Deployment. Following are the tools that need to be installed on the machine before proceeding with the DIGIT Services deployment.

**What we'll deploy in Quickstart:**

* DIGIT's core platform services
* PGR

### **Prerequisites**

1. DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds on to Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
2. All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
3. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine
4. Install [CURL](https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux) for making api calls
5. [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
6. All the DIGIT services deployment configurations are in [GitRepo](https://github.com/egovernments/DIGIT-DevOps) which you would need to [install git](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) and then [git clone](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) it to your local.
7. [Install Postman](https://www.postman.com/downloads/) to run some digit bootstrap scripts

```
root@ip:/# git clone -b quickstart https://github.com/egovernments/DIGIT-DevOps 
```

&#x20; 6\. After cloning the repo CD into the folder DIGIT-DevOps and type the "code ." command that will open the visual editor and opens all the files from the repo DIGIT-DevOps

```
root@ip:/# cd DIGIT-DevOps
root@ip:DIGIT-DevOps# code .
```

&#x20; 7\. Have look at the [sample deployment config file](https://github.com/egovernments/DIGIT-DevOps/blob/quickstart/deploy-as-code/helm/environments/quickstart-config.yaml) that needs to be configured as per any specific values according to your needs. (For a quick start you can run as it is)

```
https://github.com/egovernments/DIGIT-DevOps/blob/quickstart/deploy-as-code/helm/environments/quickstart-config.yaml
```

&#x20;8\. Add the following entries in your host file /etc/hosts depending on your OS, instructions can be found [here](https://phoenixnap.com/kb/how-to-edit-hosts-file-in-windows-mac-or-linux).&#x20;

```
127.0.0.1 quickstart.local.digit
```

### Deployment

Once all the prerequisites set up is complete, go to the following repo, run the command and follow the instructions.

```
root@ip:# cd DIGIT-DevOps/deploy-as-code/egov-deployer

root@ip:# go run digit_setup.go

#Be prepared for the following questions
1. Do you have the Kubernetes Setup?
2. Provide the path of the intented env kubeconfig file
3. Which version of the DIGIT that you want to install - Choose "Quickstart"
4. What DIGIT Modules that you choose to install
5. All, done, Now do you want to preview the deployment manifests 
6. Are you good to proceed with the DIGIT Installation

All Done.
```

You can now test the Digit application status in command prompt/terminal by using the below command.

```
curl -Is http://quickstart.local.digit/employee/login |  head -n 1
HTTP/2 200
```

## 3. Post Deployment Steps

Post deployment, now the application will be accessible from the configured domain.

To try out PGR employee login, Lets create a sample tenant, city, user to login and assign LME employee role through the seed script

1. We have to do the [kubectl port-forwarding](https://phoenixnap.com/kb/kubectl-port-forward) of the **egov-user** service running from kubernetes cluster to your localhost, this will now give you access to egov-user service directly and interact with the api directly.

```
kubectl port-forward svc/egov-user 8080:8080 -n egov
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```



2\. Seed the sample data

* Ensure you have the postman to run the following seed data api, if not [Install postman](https://www.postman.com/downloads/canary/) on your local
* Import the following postman collection into the postman and run it, this will have the seed data that enable sample test users and localisation data.
  * [DIGIT Bootstrap](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/quickstart/deploy-as-code/bootstrap\_scripts/seed\_data.json)

![](<../.gitbook/assets/image (112).png>)

![](<../.gitbook/assets/image (113).png>)



To test the kubernetes operations through kubectl from you local machine, please execute the below commands.

```bash
#get the pods running in the cluster
kubectl get pods -n egov

Output:

NAME                                                    READY   STATUS    RESTARTS   AGE
citizen-79cf89659c-8glf4                                1/1     Running   0          14d
egov-accesscontrol-78b78dddb9-tfbkf                     1/1     Running   0          21d
egov-enc-service-574cd7b5b5-hmhh4                       1/1     Running   0          36d
egov-idgen-84954b565b-xsnqj                             1/1     Running   0          45d
egov-indexer-5f5fbb6f4b-58rtm                           1/1     Running   0          43d
egov-localization-6cc5977bb9-gm7f9                      1/1     Running   0          27d
egov-mdms-service-65d6d65d8c-t85d9                      1/1     Running   0          21d
egov-user-6676968d76-8n6t6                              1/1     Running   0          29d
egov-workflow-v2-5cdb96bcf5-dcgmf                       1/1     Running   0          36d
employee-749464fbfb-tptlh                               1/1     Running   0          14d
nginx-ingress-controller-b9678869c-mkslb                1/1     Running   0          49d
pgr-services-b9f4ffdbf-5h5kd                            1/1     Running   0          38d
zuul-788bf8cd8b-9nxfl                                   1/1     Running   0          41d


#Delete the pods so that it gets restarted automatically

kubectl delete pods zuul-788bf8cd8b-9nxfl nginx-ingress-controller-b9678869c-mkslb -n egov

Output:

pod "zuul-788bf8cd8b-9nxfl" deleted
pod "nginx-ingress-controller-b9678869c-mkslb" deleted
```

You have successfully completed the DIGIT application setup. You can now experience the DIGIT platform - PGR module.&#x20;

{% hint style="info" %}
You can try experimenting the different DIGIT modules by installing them in your cluster with your H/W or VM complying to higher level machine configuration of increased number of vCPUs. RAM and storage size.
{% endhint %}

# DigitalOcean-Kubernetes-Challenge
### Deploying an internal container registry
Since kubernetes does not provide an internal container registry but having one would be really useful, therefore we are going to deploy a container registry to our kubernetes using [Harbour](https://goharbor.io/docs/2.4.0/install-config/).
### Before proceeding to our challenge lets understand some keywords:
#### [Container image](https://kubernetes.io/docs/concepts/containers/):
A container image is a ready-to-run software package, containing everything needed to run an application: the code and any runtime it requires, application and system libraries, and default values for any essential settings.
#### [Container registry](https://www.redhat.com/en/topics/cloud-native-apps/what-is-a-container-registry):
A container registry is a repository, or collection of repositories, used to store container images for Kubernetes, DevOps,  and container-based application development.
#### [Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/):
Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available. <br><br>
The image shows container evolution, Kubernetes helps in orchestration of modern containers.
![container-evolution](https://i.ibb.co/n0w1TcK/container-evolution.png)
#### [HELM](https://www.bmc.com/blogs/kubernetes-helm-charts/)
Helm helps us to manage Kubernetes applications — Helm Charts help us define, install, and upgrade even the most complex Kubernetes application.
### Continuing with the challenge:
I am going to use my local Linux terminal to deploy clusters and etc. check out [this](https://docs.digitalocean.com/reference/doctl/how-to/install/) to install DigitalOcean CLI and authenticate your local terminal with its API. { I have already authenticated my terminal, so before going to step 1, refer the above link and auth. your digitalocean CLI }
#### Step 1 : Setting up kubernetes cluster on [DigitalOcean](https://docs.digitalocean.com/reference/doctl/reference/kubernetes/cluster/create/)
Go to your local terminal and type in the following command and set the flags according to your requirement. This could take few minutes for the kubernetes cluster to get provisioned and get running. <br>
`doctl kubernetes cluster create kube-challenge --version 1.21.5-do.0 --count 3 --size s-1vcpu-2gb --region blr1` <br>
![Spinning up cluster](https://i.ibb.co/m8Q1TqN/Screenshot-from-2021-12-25-18-53-34.png) <br>
Now install also install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) which helps as to operate over our kubernetes cluster in later part. <br>Also install HELM using the this [link](https://helm.sh/docs/intro/install/). { you can follow the steps in link to install helm through a script }. 
#### Step 2 : Installing Harbour using HELM chart:
I am using [Bitnami helm chart](https://bitnami.com/stack/harbor/helm) to install harbour registry. { you can refer the link for more details or can follow the sub steps below }
- add bitnami repo to helm `helm repo add bitnami https://charts.bitnami.com/bitnami`
- before directly installing we need to edit the harbor-values.yml file [you can find in the current directory once you run this command] to change external url to our external one and change harbour admin password `helm show values bitnami/harbor > harbor-values.yaml`
- Now install using `helm install harbor bitnami/harbor --values harbor-values.yaml -n harbor --create-namespace`
![install-harbor](https://i.ibb.co/fxWNgsh/Screenshot-from-2021-12-25-18-55-22.png)
#### Step 3 : Waiting for harbor loadbalancer's external IP to be activated
Now lets wait for the loadbalancer's external IP to be activated, we can check the progress using the following commands
- for checking out the pods status `kubectl get pod -n harbor` <br>
![pod-status](https://i.ibb.co/Prqmdnv/Screenshot-from-2021-12-25-18-56-28.png)
- for checking services status `kubectl get svc -n harbor` <br>
![svc-status](https://i.ibb.co/vPGTcFm/Screenshot-from-2021-12-25-19-04-05.png)
- Once the external IP is ready we can access our private registry. <br>
![ip-access](https://i.ibb.co/5Y5jVmf/Screenshot-from-2021-12-25-19-05-00.png)
<br>we can login through username admin and password that we mentioned in our harbor-values.yaml
![login-page](https://i.ibb.co/Xy8CB80/Screenshot-from-2021-12-25-19-07-11.png)
#### Thank you

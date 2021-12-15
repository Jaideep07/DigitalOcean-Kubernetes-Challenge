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
### Continuing with the challenge:
#### Step 1 : Setting up kubernetes cluster on [DigitalOcean](https://docs.digitalocean.com/products/kubernetes/quickstart/)

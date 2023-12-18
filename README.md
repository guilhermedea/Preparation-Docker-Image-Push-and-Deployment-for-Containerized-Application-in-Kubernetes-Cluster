# Preparation, Docker Image Push and Deployment for Containerized Voting Application in Kubernetes Cluster using Docker, Azure Container Registry (ACR) and Azure Kubernetes Service (AKS)

In another project based on a real world scenario, I had to act as a DevOps Engineer, and show a new team member how to deploy an application on a Kubernetes cluster.

This cluster is part of The Cloud Bootcamp project, and I prepared this new team member to deploy the voting application that was developed for the MultiCloud Experience,
an online event where participants had the opportunity to learn about Cloud technologies.

I deployed it to Microsoft Azure cloud, where I first pushed the application’s Docker image to Azure Container Registry (ACR) and then used the Azure Kubernetes Service 
(AKS) service to deploy a cluster managed by Microsoft Azure.

![picture with the words Cloud Project and icons of the services used](https://miro.medium.com/v2/resize:fit:720/format:webp/0*qWIDV-WqVOsOVY-G.jpg)

First I set up a virtual machine, using a SSH connection to install the necessary apps for the operation, including unzip, Docker and Docker Compose. With the app folder downloaded,
I made a quick test, using Docker to generate the app’s containers.

With the first test done, I installed Azure CLI to use provisioning commands. First I create a registry on Azure Container Registry (ACR) to host the app image. Next I used Docker 
to apply a tag to the app image using the newly created registry. With the tag done, I uploaded it to Azure.

Next I created a cluster on Azure Kubernetes Service (AKS). To interact with the cluster, I installed Kubectl on the virtual machine. With the machine ready, I edited the app’s YAML 
file an altered a path, pointing the file to the hosted image on ACR. With everything in place, I deployed it.

![Terminal running the kubectl commands](https://miro.medium.com/v2/format:webp/1*-9yEXqtLmPvcmwP25EeuvQ.png)

For some unknown reason, my Azure account sometimes has login problems. After the deploy I came across an “ImagePullBackOff” error on the app front-end, which is the image that should
be downloaded from the registry on ACR. After some research and using Microsoft documentation, I activated the “Admin Access” option on ACR, creating a user and password to use with Docker.
I created a Secret on kubectl with those informations, and on the YAML file I added the line “imagePullSecrets” on the Specs section of the front-end pod, pointing to the Secret I had just
created. After making those alterations, the image was correctly pulled, and the app was live, accessible trough a public IP from Kubernetes.

Azure Container Registry and Azure Kubernetes Service allow the deployment of containered app quickly and securely, and are fundamental functions for any DevOps today. Azure Services have 
rich and detailed interfaces, helping a lot with troubleshooting should they occur.

![Picture showing the voting app used on the project](https://miro.medium.com/v2/format:webp/1*PqptBA_p0TvTe1rPavJwQA.png)

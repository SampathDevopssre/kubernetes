### EKS : Elastic Kubernetes Cluster

EKS is a managed kubernetes solution on AWS. Which is very powerful, available and robust service on AWS.

EKS Cluster can be created in any of the following ways of your choice :

    1) Sign in to EKS Console and do all the steps manually ( which is really lengthy )
    2) EKSCTL
    3) Terraform

### TERRAFORM are the most convinient ways.

EKSCTL: This is an official CLI Tool for AWS EKS from Weaveworks.
Let's see how can we use EKSCTL to provision the ELS CLuster

1) Install EKSCTL on your Linux Server 
    
    * Ref: https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html

2) Once EKSCTL is installed, you need to ensure that EKSCTL has the required authentication and authorization to your AWS Cloud Account.
   Only in that situation EKSCTL can create the EKS Cluster on your behalf.

3) This Authentication can be done by either suppling Access,Secret Key or attach the IAM Role created in the training to your linux server.

4) Now use `eksctl create cluster --help` command to see the list of options and proceed accordingly

   Here is how the final command should look like

    $ eksctl create cluster --name clusterName --version 1.22 --region us-east-1 --nodegroup-name k8-ng --node-type t3.micro --nodes 2

    $ kubectl get nodes 

    $ aws eks update-kubeconfig --name clusterName

    How to Delete the created cluster ?
EKS is a chargeable managed service. Ensure you delete them once you practice them. Use the below command to delete the cluster

$ eksctl delete cluster clusterName --region us-east-1


### Do we have any control of the master node on EKS ?

 NO!

    You don't have any visibility or control on Master Node or Control Pane when you're using Managed Service.

### What happends if the master node is down ???

$ Will the existing workloads going to fail or going to be impacted ?

        * No ! If the master is not reachable or fails, all the workloads will operate normally. But you cannot connect to the cluster or schedule new workloads. Existing workloads will run as usual. 

        * That's why for production based workloads, we typically go with 3 Master nodes in 3 different zones.

### What is kubectl and why we need that ?
    kubectl is a kubernetes client that needs to be installed on the top of the computer where you wish to connect to the kubernetes cluster.

### What is the smallest resource that you can create on Kubernetes ?
POD

### What is a POD in Kubernetes ?

 In Kubernetes, we don't run containers directly. Instead, we run pods and pods will have the containers.
    POD is a just a wrapper to our conainer.

    Kubernetes has solved lot of challenges using pods and below are the major aspects :
        1) Shared Storage 
        2) Shared Network NameSpace.


### How can we authenticat to kubernetes cluster ?
    $ aws eks update-kubeconfig --name clusterName

### What is the structued of Kubernetes Commands ?

kubectl get resourceTypeYOuWant 

Ex:
        $ kubectl get pods     # This will list all the pods 
        $ kubectl get nodes    # This will list all the nodes in the cluster


How can we create resources using kubectl when using delcarative manifest files ?
    $ kubectl create -f fileName.yml 

    $ kubectl update -f fileName.yml 

### create vs update ?

create : creates the resources if the resource is not available. ( cannot update the values if the resource is already there .)

apply  : apply can create the resouce and at the same time if the resource is already available, then it's going to upadte the value if you want.

### We create pods using SETS!!!

What is a set and why we need set's and type of sets.

    1) Replica Sets 
    2) Deployment Sets
    3) Daemon Sets
    4) Stateful Sets

### Why we create pods using sets ?

    1) Sets helps in in ensuring the specific number of pods running all the time
    2) For any reason if any of the pod fails or crashed, scheduler is going to schedule the pods on the node with enough resources.
    3) Based on the requirement, we would have to use one among the sets.

### Services In Kubernetes

Services in kubernetes are used to pass the requests to the backend pods using the service discovery mechanism.

Service Types In Kubernetes : 

        1) Cluster IP       [ Often Used ] : This is accessible with in the cluster only, we use this for service-service communication
        2) Load Balancer    [ Need basis ] : This is used when you want to expose service to the PUBLIC / External Network.
        3) Node Port        [ Need Basis ]
        4) External Name    [ Need Basis ]

### What is a deemon set and why we need that ?

Typically we use this for Monitoring Agents!!!

    Whenever you were landed in to a situation where you want to run a single POD on the top of each and eevery node of the cluster irrespective of the scale-out or scale-in.


### How can we create kubernetes resources using manifest files ???

$ kubectl apply -f nameOfTheFile.yml       
            [ apply is going to create resource is not available or updates the values of the resources if the resource already exits]

    $ kubectl create -f nameOfTheFile.yml 
             [ create is going to create resource ]
    
    $ kubectl delete -f nameOfTheFile.yml 
             [delete is going to delete all the kubernetes resources created by this manifest]


How to create a Kubernetes Cluster on AWS ?
We can use a Managed Service called EKS : Elastic Kubernetes Service

Ensure you have VPC In Place ( network )
Create the cluster
Create Nodepools




# How to Install minikube

Minikube is used as the local kubernetes cluster. It fetches the images from the Google Cloud Registry and create a container on the local system.
So it can be used for testing the application on the local system and then can be deployed on the production.

Let see how to install minikube. I have used the RHEL8 virtual machine. You can use your local system or cloud instance or the VM

1- Installing minikube on RHEL8 server. You need atleast 2 VCPU and 2 GB of RAM.

2- Install the docker first on the system. Foollow below steps:

==> Create docker repository as below and install docker package

~]# dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

]# dnf install docker-ce 

==> Enable the docker service so even after reboot of the system the docker service will start

~]# systemctl enable docker --now

I have referred the below link for installing docker on RHEL8:

https://www.linuxtechi.com/install-docker-ce-centos-8-rhel-8/

3- Once the docker is installed then start installing the minikube. Download the minikube as below and start the minikube cluster. I have referred the k8s documentation for the same. Below is the link

https://minikube.sigs.k8s.io/docs/start/

=================

$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube

]# minikube start

😄  minikube v1.30.1 on Redhat 8.7

✨  Automatically selected the docker driver. Other choices: none, ssh

🛑  The "docker" driver should not be used with root privileges. If you wish to continue as root, use --force.

💡  If you are running minikube within a VM, consider using --driver=none:

📘    https://minikube.sigs.k8s.io/docs/reference/drivers/none/

   Exiting due to DRV_AS_ROOT: The "docker" driver should not be used with root privileges.

=================

4- minikube was refusing to start as I was working as root user, so I gave --force to use as root user.

=================

]# minikube start --force

😄  minikube v1.30.1 on Redhat 8.7

❗  minikube skips various validations when --force is supplied; this may lead to unexpected behavior

✨  Automatically selected the docker driver. Other choices: none, ssh

🛑  The "docker" driver should not be used with root privileges. If you wish to continue as root, use --force.

💡  If you are running minikube within a VM, consider using --driver=none:

📘    https://minikube.sigs.k8s.io/docs/reference/drivers/none/

📌  Using Docker driver with root privileges

👍  Starting control plane node minikube in cluster minikube

🚜  Pulling base image ...

💾  Downloading Kubernetes v1.26.3 preload ...

    > preloaded-images-k8s-v18-v1...:  397.02 MiB / 397.02 MiB  100.00% 102.95 
    
    > gcr.io/k8s-minikube/kicbase...:  373.53 MiB / 373.53 MiB  100.00% 16.47 M
    
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...

🐳  Preparing Kubernetes v1.26.3 on Docker 23.0.2 ...

    ▪ Generating certificates and keys ...
    
    ▪ Booting up control plane ...
    
    ▪ Configuring RBAC rules ...
    
🔗  Configuring bridge CNI (Container Networking Interface) ...

    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
    
🔎  Verifying Kubernetes components...

🌟  Enabled addons: storage-provisioner, default-storageclass

💡  kubectl not found. If you need it, try: 'minikube kubectl -- get pods -A'

🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default


=================

5- It downloads the kubernetes images from the GCP-Google Cloud Registry and create a container

=================


]# docker ps

CONTAINER ID   IMAGE                                 COMMAND                  CREATED              STATUS              PORTS                                                                                                                                  NAMES
62ac99228292   gcr.io/k8s-minikube/kicbase:v0.0.39   "/usr/local/bin/entr…"   About a minute ago   Up About a minute   127.0.0.1:32772->22/tcp, 127.0.0.1:32771->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32769->8443/tcp, 127.0.0.1:32768->32443/tcp   minikube

=================

6- Check minikube status:

=================

]# minikube status

minikube

type: Control Plane

host: Running

kubelet: Running

apiserver: Running

kubeconfig: Configured

=================

7- Now we need to install kubectl. I have referred the official documentation of the kubernetes. Below is the link for the document. 

https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/


]# kubectl version --client --output=yaml

clientVersion:

  buildDate: "2023-05-17T14:20:07Z"
  
  compiler: gc
  
  gitCommit: 7f6f68fdabc4df88cfea2dcf9a19b2b830f1e647
  
  gitTreeState: clean
  
  gitVersion: v1.27.2
  
  goVersion: go1.20.4
  
  major: "1"
  
  minor: "27"
  
  platform: linux/amd64
  
kustomizeVersion: v5.0.1

8- Now out minikube cluster is running and kubectl is also installed. We can use it to deploy containers and get to know how kubernetes works and it's various components.



# Task 2: Create your first pod on Kubernetes through minikube.

1- Created the nginx pod by using below pod.yml file

=====================

]# cat pod.yml 

apiVerison: v1

kind: pod

metadata:

    name: ngnix-pod
 
spec:

  containers:
  
      - name: ngnix-container-pod
      
        image: divya422/nginx:latest
        
        ports:
        
           - ContainerPort:  80

=====================

- But while running, it created below error message. So cross check your yml syntax for maniest files.

]# kubectl apply -f pod.yml 

Error from server (BadRequest): error when creating "pod.yml": pod in version "v1" cannot be handled as a Pod: no kind "pod" is registered for version "v1" in scheme "pkg/api/legacyscheme/scheme.go:30"


- Above error was pointing to the "kind: pod". In pod P should be capital, "kind: Pod".
-
=====================

]# cat pod.yml 

apiVersion: v1

kind: Pod

metadata:

   name: ngnix-pod
   
 
spec:

  containers:
  
       - name: ngnix-container-pod
        
         image: divya422/nginx:latest
        
         ports:
        
            - containerPort:  80

=====================
           
 - ]# kubectl apply -f pod.yml 
 - 
pod/ngnix-pod created


- ]# kubectl get pods
- 
NAME        READY   STATUS             RESTARTS   AGE

ngnix-pod   0/1     ImagePullBackOff   0          47s


- You can check if the container is created by going in minikube.

]# minikube ssh

docker@minikube:~$ 

Below you can see container is created for nginx:

docker@minikube:~$ docker ps

CONTAINER ID   IMAGE     
COMMAND                  CREATED              STATUS              PORTS     NAMES
9dcc78042931   registry.k8s.io/pause:3.9      "/pause"                 About a minute ago   Up About a minute             k8s_POD_ngnix-pod_default_176648a3-0f39-424d-8600-920ddc0aaeac_0


**Services in Kubernetes

==> Service is required in kubernetes to access the pods in the network. Deployment will create pods and its replicas, but those will not be accessible outside cluster. 
So to make it accessible we create service file mentioning the ports and the service types.

1- Below is the service file which applies to the namespace "todo" andhaving label "todo-app".

~~~~~~~~~~

# cat services.yml 

apiVersion: v1

kind: Service

metadata:

   name: todo-service
   
   namespace: todo
   
spec:

  selector:
  
     app: todo-app
     
  ports:
  
    - protocol: TCP
    
      port: 8000
      
      targetPort: 8000
      
  type: NodePort
~~~~~~~~~~

==> Below is deployment file:

~~~~~~~~~~

# cat deployment-namespace.yml 

apiVersion: apps/v1

kind: Deployment

metadata:

    name: deploy-namespace-test
    
    namespace: todo
    
    labels:
    
   
      app: todo-app
      
spec:

  replicas: 2
  
  selector:
  
    matchLabels:
    
       app: todo-app
       

  template:
  
     metadata:
     
         labels:
         
            app: todo-app

     spec: 
     
       containers:
       
         - name: todo-container
         
           image: divya422/todo-image
           
           ports:
           
              - containerPort: 8000
~~~~~~~~~~

==> Using below command to get the service created and to access it inside the cluster:

$ kubectl get service --namespace todo

NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE

todo-service   ClusterIP   10.101.50.146   <none>        8000/TCP   23s

$ minikube service todo-service -n todo
  
|-----------|--------------|-------------|---------------------------|
| NAMESPACE |     NAME     | TARGET PORT |            URL            |
|-----------|--------------|-------------|---------------------------|
| todo      | todo-service |        8000 | http://192.168.49.2:30302 |
|-----------|--------------|-------------|---------------------------|

  
$ minikube service todo-service -n todo --url
  
http://192.168.49.2:30302

$ curl -L  http://192.168.49.2:30302

  <!DOCTYPE html>

<html>

    <head>
        <title>My shaandaar todolist</title>
        <style>
            a {
                text-decoration: none;
                color: black;
            }

        </style>
    </head>
   
   
   
   **Types of services:
   
   1- ClusterIP: Using this tyoe the pod is not accessible outside cluster. It will only accessible inside. So one podd can comminicate with another within cluster.
   
   2- NodePort: To access the application outside the cluster we use this type of service. It assign the port to the node so application can on that port.
   
   3- Loadbalancing: It uses LB from cloud providers to send the traffic from external to the pod. It is used whrn we want to expose service to the outside world.
   
   
   **Endpoint:
   
   Endpoints that keep the list of IP addresses up to date for the service to forward its traffic.
   
~~~~~~~~~~~~~~
$ kubectl describe services todo-service -n todo
   
Name:                     todo-service
Namespace:                todo
Labels:                   <none>
Annotations:              <none>
Selector:                 app=todo-app
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.101.50.146
IPs:                      10.101.50.146
Port:                     <unset>  8000/TCP
TargetPort:               8000/TCP
NodePort:                 <unset>  32027/TCP
Endpoints:                10.244.0.12:8000,10.244.0.13:8000     <<<== List of IP of the pods
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
~~~~~~~~~~~~~~



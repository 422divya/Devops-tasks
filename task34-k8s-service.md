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

# kubectl get service --namespace todo

NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE

todo-service   ClusterIP   10.101.50.146   <none>        8000/TCP   23s

  # minikube service todo-service -n todo
  
|-----------|--------------|-------------|---------------------------|
| NAMESPACE |     NAME     | TARGET PORT |            URL            |
|-----------|--------------|-------------|---------------------------|
| todo      | todo-service |        8000 | http://192.168.49.2:30302 |
|-----------|--------------|-------------|---------------------------|

  
  # minikube service todo-service -n todo --url
  
http://192.168.49.2:30302

# curl -L  http://192.168.49.2:30302

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


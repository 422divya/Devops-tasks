**ConfigMap:

Refer below document:

https://matthewpalmer.net/kubernetes-app-developer/articles/ultimate-configmap-guide-kubernetes.html



**Task1: Created ConfigMap as below :

~~~~~~~~~~~~~~~

]# cat configmap.yml 
apiVersion: v1
kind: ConfigMap
metadata:
  name: todo-config
  namespace: todo

data: 
  name: TODO
  app1.properties: |
      environment: production
      message: Hello

~~~~~~~~~~~~~~~

      
==> Then mapped the config map in below deployment:

~~~~~~~~~~~~~~~

]# cat deployment-namespace.yml 
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
           env:
              - name: ENVIRONMENT
                valueFrom:
                   configMapKeyRef: 
                     name: todo-config
                     key: name

           volumeMounts:
              - name: config
                mountPath: /tmp/text.txt
       volumes:
         - name: config
           configMap:
              name: todo-config
              
              
~~~~~~~~~~~~~~~


==> While applying pods failed to create:

]# kubectl get pod -n todo
NAME                                     READY   STATUS                       RESTARTS   AGE
deploy-namespace-test-5bc6bccbb7-j8vx6   0/1     CreateContainerConfigError   0          8m9s
deploy-namespace-test-6c57cc56f7-kqjdg   0/1     ContainerCreating            0          2s

==> Checked the logs as below and found the error was while finding for key environment. So as it was mention in properties in configmap I changed the env varaiable to map content to data.

]# kubectl describe pod -n todo deploy-namespace-test-5bc6bccbb7-j8vx6
Name:             deploy-namespace-test-5bc6bccbb7-j8vx6
Namespace:        todo
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Sun, 04 Jun 2023 12:16:46 +0530
Labels:           app=todo-app
                  pod-template-hash=5bc6bccbb7
Annotations:      <none>
Status:           Pending
IP:               10.244.0.18
IPs:
  IP:           10.244.0.18
Controlled By:  ReplicaSet/deploy-namespace-test-5bc6bccbb7
Containers:
  todo-container:
    Container ID:   
    Image:          divya422/todo-image
    Image ID:       
    Port:           8000/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       CreateContainerConfigError
    Ready:          False
    Restart Count:  0
    Environment:
      ENVIRONMENT:  <set to the key 'environment' of config map 'todo-config'>  Optional: false
    Mounts:
      /tmp/text.txt from config (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-rjdht (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             False 
  ContainersReady   False 
  PodScheduled      True 
Volumes:
  config:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      todo-config
    Optional:  false
  kube-api-access-rjdht:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                    From               Message
  ----     ------     ----                   ----               -------
  Normal   Scheduled  6m33s                  default-scheduler  Successfully assigned todo/deploy-namespace-test-5bc6bccbb7-j8vx6 to minikube
  Normal   Pulled     6m31s                  kubelet            Successfully pulled image "divya422/todo-image" in 1.970084941s (1.970193575s including waiting)
  Normal   Pulled     6m27s                  kubelet            Successfully pulled image "divya422/todo-image" in 1.914522034s (2.791608208s including waiting)
  Normal   Pulled     6m12s                  kubelet            Successfully pulled image "divya422/todo-image" in 1.952344104s (1.952359079s including waiting)
  Normal   Pulled     5m57s                  kubelet            Successfully pulled image "divya422/todo-image" in 1.902320443s (1.902328363s including waiting)
  Normal   Pulled     5m42s                  kubelet            Successfully pulled image "divya422/todo-image" in 1.93095243s (1.930961041s including waiting)
  Normal   Pulled     5m25s                  kubelet            Successfully pulled image "divya422/todo-image" in 1.90873206s (1.908740655s including waiting)
  Normal   Pulled     5m11s                  kubelet            Successfully pulled image "divya422/todo-image" in 1.954575967s (1.95458589s including waiting)
  Warning  Failed     4m57s (x8 over 6m31s)  kubelet            Error: couldn't find key environment in ConfigMap todo/todo-config
  Normal   Pulled     4m57s                  kubelet            Successfully pulled image "divya422/todo-image" in 1.93730101s (2.841299364s including waiting)
  Normal   Pulling    84s (x22 over 6m33s)   kubelet            Pulling image "divya422/todo-image"

  
  ==> After mapping the env to the data in configmap pods got created successfully.
  
  ~~~~~~~~~~~~~~~~
  
  ]# kubectl exec -it deploy-namespace-test-6c57cc56f7-kqjdg sh -n todo
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
/project # 
/project # env
TODO_SERVICE_SERVICE_HOST=10.101.50.146
KUBERNETES_PORT=tcp://10.96.0.1:443
KUBERNETES_SERVICE_PORT=443
NODE_VERSION=12.2.0
HOSTNAME=deploy-namespace-test-6c57cc56f7-kqjdg
TODO_SERVICE_PORT_8000_TCP=tcp://10.101.50.146:8000
YARN_VERSION=1.15.2
SHLVL=1
HOME=/root
ENVIRONMENT=TODO
TODO_SERVICE_SERVICE_PORT=8000
TODO_SERVICE_PORT=tcp://10.101.50.146:8000
TERM=xterm
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
TODO_SERVICE_PORT_8000_TCP_ADDR=10.101.50.146
KUBERNETES_SERVICE_HOST=10.96.0.1
PWD=/project
TODO_SERVICE_PORT_8000_TCP_PORT=8000
TODO_SERVICE_PORT_8000_TCP_PROTO=tcp
/project # ls -lrth /tmp
total 0
drwxrwxrwx    3 root     root          95 Jun  4 06:54 text.txt
~~~~~~~~~~~~~~~~
  
  
  
  **Secrets:
  
  - I have created the mysql database by fetching the image from dockerhub. I have encoded password and created secret yaml file to store password and use it in deployment file.
  
  ~~~~~~~~~~~~~~~~
  
  # cat deployment-db.yml 
apiVersion: apps/v1
kind: Deployment
metadata:
   name: database-pod
   namespace: database
   labels:
      app: db
spec:

  replicas: 2
  selector:
    matchLabels:
      app: db
  template:
    metadata:
       labels:
         app: db
    spec:
      containers:
       - name: db-container
         image: mysql:latest
         ports:
          - containerPort: 3306 
         env:
           - name: mysql_password
             valueFrom:
               secretKeyRef:
                 name: secret
                 key: root_password 
  
  ~~~~~~~~~~~~~~~~
  
  Secret file
  
  ~~~~~~~~~~~~~~~~
  Encoded password as below:
  
  ]# echo -n "test@123" |base64
dGVzdEAxMjM=

  
  ]# cat secret.yml 
apiVersion: v1
kind: Secret
metadata:
   name: secretpass
   namespace: database
type: Opaque
data:
  root_password: dGVzdEAxMjM=
  
  ~~~~~~~~~~~~~~~~

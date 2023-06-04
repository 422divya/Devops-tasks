**Created persistent volume and persistent volume claim


~~~~~~~~~~~~~~~

]# cat persistentvol.yml 
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-volume
  namespace: todo
spec:
  capacity:
     storage: 1Gi
  accessModes:
      - ReadWriteOnce
  hostPath:
      path: "/tmp/app"

]# cat pvc.yml 
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-claim
  namespace: todo
spec:
  accessModes:
     - ReadWriteOnce
  resources:
    requests:
       storage: 1Gi

~~~~~~~~~~~~~~~


==> Using the volumes in the pods:

~~~~~~~~~~~~~~

]# cat deployment-namespace.yml 
apiVersion:  apps/v1
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
              - mountPath: /tmp/app
                name: persistent
           volumeMounts:
               - mountPath: /tmp/test.txt
                 name: config


       volumes:
           - name: persistent 

             persistentVolumeClaim:
                 claimName: my-claim  
       volumes:
         - name: config
           configMap:
              name: todo-config


~~~~~~~~~~~~~~

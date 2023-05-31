**Namespace in K8S

It is use to isolate the resources in same cluster. If there are multiple team using same cluster then it is better to create the separate namespace. So the conflict in namng for kubernetes resources like 
deployments, services and other object can be avoided.

So team can use the same resource names in different namscpace without creating conflict. We can set resource limit on namespcaes by defining resource quotas as below:

apiVersion: v1
kind: ResourceQuota
metadata:
  name: test-cpu-quota
  namespace: demo
  spec:
    hard:
       requests.cpu: "200m"  
       limits.cpu: "300m"  
       
       
 Above creates quota for the demo namespace, so pods created and running inside demo namespace will be limited to above limit. If cpu limit is reached mentioned abive then no more pods created in that namespace.
 
 

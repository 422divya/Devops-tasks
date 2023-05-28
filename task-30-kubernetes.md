#Kubernetes

1- What is Kubernetes? Write in your own words and why do we call it k8s?

==> Kubernetes is an container orchestartion tool. It is used to manage a group of containers, monitor containers fr maintaining its uptime, scaling, managing traffic on containers.

If any of the container gets crashed kubernetes creates new container and maintain the uptime of the applications. It also add more number of instances and create containers if the traffic flow is high on the application.
Also it will reduce the idle containers when the traffic flow becomes low. Performs health check of the container and heals its automatically by restarting it or replacing it by creating new container.

In short kubernetes is also called k8s as in between k and s there are 8 characters.

2- Kubernetes API Server:

==> It is in Control plane on K8S cluster. It si responsible for communicating with the cluster components. When we want to make any changes in the containers or create containers we use kubectl CLI tool
to pass the yml file. It is then being taken care by API server. So any component in cluster need to make changes on the node it ha to make interaction with nodes using API server.



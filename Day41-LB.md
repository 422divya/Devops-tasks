**Elastic Load Balancers**

AWS provides Elastic LB as service. It is used to manage the traffic across the instances, containers across the AZ. Using it can help to distribute traffic 
among the instances so our application can run smoothly.

It has 3 types:

1- Application LB: Used to redirect particular path to the servers. Suppose if we have instance were images or videos stored , so client request the content by provising path like abc.jpg. On LB we can
apply the rule that is path is abc.jpg then redirect it to particular Target group. Can use http and https rule.

2- Network LB: Use for TCP and UDP protocol. Can apply rule for the ports.

3- Classic: Classic one where we cannot apply rules.

Tasks:

Created 2 instances with apache installed using user data. Then created ALB and target group. Added 2 instances in TG and associated TG with LB. 
Then applied rules that if request is index.html then forward request to particular TG so instance in that can be accesses.

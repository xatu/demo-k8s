# demo-k8s

Demo hello-world application in nodejs to be built in an docker image, pushed to dockerhub as public and deployed in kubernetes cluster as 3 replicas and 1 small load balance service. 

### Pre-requirements

In order to run this demo you need the following: 

- Add id dockerhub-credentials on jenkins
- Add config file hosts_k8s on jenkins
- Setup ssh-keys between jenkins and k8s cluster

### Diagram

![image](https://user-images.githubusercontent.com/6520725/58902677-90f87680-86d1-11e9-8d75-a96f59ac0396.png)

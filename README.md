# Kubernetes


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#kubernetes-locally">Host kubernetes locally</a>
      <ul>
        <li><a href="#minikube">Minikube</a></li>
      </ul>
      <ul>
        <li><a href="#docker-desktop">Docker Desktop</a></li>
      </ul>
      <ul>
        <li><a href="#config-context">Config Context</a></li>
      </ul>
    </li>
  </ol>
  <ol>
    <li>
      <a href="#pods">Pods</a>
      <ul>
        <li><a href="#pods">Kubernetes pods</a></li>
      </ul>
      <ul>
        <li><a href="#pods-ip-and-ports">Pods ip and ports</a></li>
      </ul>
       <ul>
        <li><a href="#multi-container-pod">Multi Container Pod</a></li>
      </ul>
       <ul>
        <li><a href="#pods-api-imperative">Pods command</a></li>
      </ul>
    </li>
  </ol>
  <ol>
    <li>
      <a href="#yaml-declarative">Kubernetes declarative YAML</a>
    </li>
  </ol>
    <ol>
    <li>
      <a href="#monitor">Monitor & Manage</a>
      <ul>
        <li><a href="#describe">Describe</a></li>
      </ul>
    </li>
  </ol>
    <ol>
    <li>
      <a href="#probe">Probe</a>
      <ul>
        <li> <a href="#liveness-and-readiness-probe">Liveness and Readiness probe</a></li>
        <ul>
        <li> <a href="#liveness-configuration">Liveness Configuration</a></li>
      </ul>
      </ul>
    </li>
    <li>
      <a href="#deployment-and-replicaset">ReplicaSets & Deployments</a>
      <ul>
        <li> <a href="#replicaset">Replicasets</a></li>
      </ul>
      <ul>
        <li> <a href="#deployments">deployments</a></li>
      </ul>
      <ul>
        <li> <a href="#replicaset-commands">Replicaset Commands</a></li>
      </ul>
      <ul>
        <li> <a href="#deployment-commands">Deployment Commands</a></li>
      </ul>
    </li>
     <li>
      <a href="#namespace">Namespaces</a>
      <ul>
        <li> <a href="#namespace-commands">Namespace commands</a></li>
      </ul>
    </li>
</details>

## Kubernetes Locally

### Minikube

Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing only one node
OBS: We dont use minikube anymore

![image](https://user-images.githubusercontent.com/29054168/218310245-a686301f-7fad-4a6c-b896-9a63321d835e.png)


### Docker Desktop

- **Recommeded way**
- Set alias Set-Alias -Name k -Value kubectl

Use docker desktop with kubernetes enabled. The ip address will be localhost instead of minikube ip address

![image](https://user-images.githubusercontent.com/29054168/218310611-e4901125-2990-43ef-920f-f11db306beaf.png)


### Config context
```
kubectl config get-contexts
kubectl config use-context docker-desktop
```


## Pods

* Pods are the smallest unit in kubernetes
* We can have several pods in a node
* One pod can have several containers, but that is very rarlely used 

![image](https://user-images.githubusercontent.com/29054168/218312449-58a92932-c4f4-459b-8aca-5e07b2d9d461.png)

### Pods ip and ports

* Pods get unique ip addresses in a node
* Containers in a pod need to have unique ports. But containers in 2 different pods can have same port

![image](https://user-images.githubusercontent.com/29054168/218312679-cfc26b24-cc37-4775-849f-e070338103e8.png)


### Multi container pod

![image](https://user-images.githubusercontent.com/29054168/218438569-5f8c167b-d014-4e54-abfd-032154097a7d.png)

* Resources can communicate through localhost


### Pods api Imperative
```
Create pods nginx image Imperative:             kubectl run <pod name> image=nginx:latest
Get pods:                                       kubectl get pods -o wide
Port forward, expose pod to external:           kubectl port-forward <pod-name> 8080:80
Access -it  of a container:                     kubectl exec <pod-name> it sh
```

## YAML Declarative
```
Run Yaml file:                       kubectl --apply -f <podfile>.yml --validate=true
Delete resources from yaml file:     kubectl delete -f <podfile>.yml
```


## Monitor

### Describe

```
Describe pod: kubectl describe pod <pod-name>
```

![image](https://user-images.githubusercontent.com/29054168/218318499-a4dafa41-b6f3-48c7-8d8d-56560d1200e5.png)


## Probe

## Liveness and Readiness probe

![image](https://user-images.githubusercontent.com/29054168/218322682-c0db390a-28c5-44cf-be04-dcb09f920771.png)

  ### Liveness configuration
  
  If the liveness check fails it will kill the container and restart it. 
  
![image](https://user-images.githubusercontent.com/29054168/218324176-9d3c94ca-0cff-4477-adff-3a65392a47e3.png)

  * periodSeconds: Specifies that the kubelet should perform a liveness probe every 5 seconds.
  * initialDelaySeconds: Tells the kubelet that it should wait 5 seconds before performing the first probe.
  
  

## Deployment and ReplicaSet
  
### Replicaset
  
  ![image](https://user-images.githubusercontent.com/29054168/218337634-7f0d7bee-0a9a-4f80-b5a5-fc55895fd962.png)
  
  
### Deployments
  
  ![image](https://user-images.githubusercontent.com/29054168/218337803-0e8abd53-6a1e-4c5e-a52c-99f40b1d8375.png)
  
  
  * Declarative updates for Pods and ReplicaSets.
  * Declare desire state  

### Replicaset Commands
```
Edit: kubectl edit replicasets <name>
Run: kubectl apply -f 
Scale manually: kubectl scale --replicas=3 rs/my-replicaset
Delete: kubectl delete rs <name>
```


### Deployment Commands
```
Edit: kubectl edit deployment <name>
Run: kubectl apply -f 
Scale manually: kubectl scale --replicas=3 rs/my-replicaset
Delete: kubectl delete deployment <name>
```
  
  
##Namespace

 * Default namespace: default
 
### Namespace Commands
```
Edit: kubectl edit namespace <name>
Run: kubectl apply -f 
Delete: kubectl delete namespace <name>
Get namespaces: kubectl get namespaces
Get pods for namespace: kubeclt get pods --namespace development
Create namespace: kubectl create namespace <name>
Get pods in all namespaces: kubectl get pods --all-namespaces
Set default namespace
FQDN name service in another namespace: <service-name>.<Namespace>.svc.cluster.local
```

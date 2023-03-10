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
    </li>
     <li>
      <a href="#args-and-commands">Args and Commands</a>
      <ul>
        <li> <a href="#args">args</a></li>
      </ul>
      <ul>
        <li> <a href="#command">command</a></li>
      </ul>
      <ul>
        <li> <a href="#describe-pod-command-and-args">Describe Pod command and args</a></li>
      </ul>
       <ul>
        <li> <a href="#run-image-with-arguments">Run image with arguments</a></li>
      </ul>
    </li>
    <li>
      <a href="#envrironment-and-configs-maps">Envrironment and configs maps</a>
      <ul>
        <li> <a href="#config-maps">Config maps</a></li>
      </ul>
    </li>
    <li>
      <a href="#secrets">Secrets</a>
      <ul>
        <li> <a href="#encode">Encode</a></li>
      </ul>
      <ul>
        <li> <a href="#secret">Secret</a></li>
      </ul>
    </li>
  <li>
      <a href="#service-account">Service Account</a>
      <ul>
        <li> <a href="#service-account-commands">Service Account Commands</a></li>
      </ul>
      <ul>
        <li> <a href="#sa-token">SA-token</a></li>
      </ul>
    </li>
    <li>
      <a href="#resource">Resource</a>
    </li>
</details>

  
# To Learn
  * Services, clusterip, loadbalancer, nodeportexternalname service
  * Expose a pod clusteri?? --expose
  * kubbectl replace --force -f temp file

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
Create a pod and expose it as cluster Ip in port 80: kubectl run httpd --image=httpd:alpine --port=80 --expose
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
  
  
## Namespace

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


## Args and Commands
### args
* We can define args that will be sent to a docker file. The args, override the CMD in docker file 

![image](https://user-images.githubusercontent.com/29054168/220786777-86c8df03-bfe3-4537-b370-a7058fa4ff1e.png)


### command
* We can override the entrypoint in docker by specifiying command in kubernetes

![image](https://user-images.githubusercontent.com/29054168/220786939-448e7efc-4a47-4830-b94f-1e9b98b71597.png)


The end result will be docker entrypoint is replace by "sleep" and the cmd is replace by "10". So docker will sleep 10 seconds

### Describe Pod command and args
* kubectl describe pod <pod name>

![image](https://user-images.githubusercontent.com/29054168/221383722-b7ddd329-a635-4a3b-920a-bce40accb671.png)

  
  ### Run image with arguments
  
  *  kubectl run nginx --image=nginx -- <arg1> <arg2> ... <argN>
  * nginx run testpod --image=nginx -- --color green
  ![image](https://user-images.githubusercontent.com/29054168/221383900-b94d7d3a-46fd-4c39-b8b7-90967ada2be4.png)
  
  
  
  ## Envrironment and configs maps
  
  ### Config maps

```
Create config map Imperative:  kubectl create configmap app-settings --from-literal=app=SomeValue --from-literal=mode=development
Create config map Imperative from file:  kubectl create configmap app-settings --from-file=app-config.properties
Get config maps: Kubectl get configmaps
Describe config maps: kubectl describe configmaps <name>
```

* We can create many config maps
* App-config
* Redis-config
* Mysql-config


* Load configs from file --from-file

![image](https://user-images.githubusercontent.com/29054168/221700447-ef64c3fd-cdda-4b74-9ce3-15df25d37e39.png)



## Secrets

### Encode
```
Encode: echo -n 'secretValue' | base64
Decode: echo -n 'base64value' | base64 --decode
```

### Secret 

```
Get Secrets:                 kubectl get secret
Get secret YAML:             kubectl get secret <secret name> -o yaml
Get Secret data:             kubectl get secret <secret name> -o jsonpath='{.data}'
Get secret type:             kubectl get secret <secret name> -o jsonpath='{.type}'
Create secret file dry run:  kubectl create secret generic dry-secret --dry-run=client --from-literal=key1=value1 --from-literal=key2=value2  -o yaml > secret.yaml

```



## Service Account

* Client authorize to kubernetes cluster.
* Can user use Service account? No they should use user account 
* Does a namespace always have at least one serivce account? Yes (default)
* Does pods use service account? Yes, by default if you dont specify they use "default" service account 

![image](https://user-images.githubusercontent.com/29054168/224547167-f70b77b5-f3db-4611-83d2-a3232fbf6211.png)


### Service Account Commands

```
Get Service Accounts:                          kubectl get serviceaccounts
Get service account Pod use:                   kubectl get pod <podName> -o jsonpath='{.spec.serviceAccountName}'
Get bearer token for a SA:                     kubectl create token <sa name>
Create SA:                                     kubectl create sa <name> 

```


###  SA-token

* In mount you can see the volume for accessService. There you can find the token (bearer token it use) 

![image](https://user-images.githubusercontent.com/29054168/224560309-cc0cf712-87e0-41d4-a99d-5508203d0dca.png)

* Go iteractivly instead the pod
* kubectl exec -it <podname> -- bash
* ls /var/run/secrets/kubernetes.io/serviceaccount
* cat token (to viewe the bearer token)


![image](https://user-images.githubusercontent.com/29054168/224560403-c69a5470-8b7a-4079-96a6-40919dc57cbb.png)

```
Set SA account for pod at creation:  spec.serviceAccountName: <sa name>
Dont mount service account to pod:   spec.automountServiceAccountToken: false
```
  
  
## Resource
  
* Node scheduler in control plan schedules pods in nodes if node has the capacity to run the pod
* What is the minimum CPU for a pod: 0.5 CPU
* What is the minimum memory for a pod: 256 Mi
* If you need more specifu resources in Yaml
* Request vs limit: If a node has more resources the pod can try to use more resources than it request. But not exceed its limit. 
  
* 0.1 CPU in m is= 100m 
* What is minimum CPU m? 1m
* 1 CPU in azure is 1 azure core

* Memory 1: 1G, 1M, 1K or also 1 Gi, 1Mi, 1Ki
* Can a pod use more resources in memory that its limit? Yes, but if it constantly does it it will terminate
  
![image](https://user-images.githubusercontent.com/29054168/224572521-79e032e5-fc08-4940-8066-49a164df7059.png)
  
![image](https://user-images.githubusercontent.com/29054168/224846488-a4d44aca-854c-467c-b225-3dfc400cab08.png)


  
## Taints and tolerations
  
* We can taint a node, so only pods with that taint can go to that pod. If we dont assign anything to the pod, its rejected
* Tant-effect: NoSchedule: 

```
 Tant node:         kubectl taint nodes <node-name> key=value:tant-effect(NoSchedule, PreferNoSchedule, NoExecute)
 Remove taint:      kubectl taint nodes <node-name> key1=value::tant-effect-
  
```

## Tips for exam

## Modify existing resource
```
* Get resource YAML: kubectl get pod <name> -o yaml > pod.yaml
* Delete old resource
* Make changes
* Apply new yaml
```

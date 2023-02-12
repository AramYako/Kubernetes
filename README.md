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
        <li><a href="#pods-api-imperative">Pods Api Imperative</a></li>
      </ul>
    </li>
  </ol>
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



## Pods

* Pods are the smallest unit in kubernetes
* We can have several pods in a node
* One pod can have several containers, but that is very rarlely used 

![image](https://user-images.githubusercontent.com/29054168/218312449-58a92932-c4f4-459b-8aca-5e07b2d9d461.png)

### Pods ip and ports

* Pods get unique ip addresses in a node
* Containers in a pod need to have unique ports. But containers in 2 different pods can have same port

![image](https://user-images.githubusercontent.com/29054168/218312679-cfc26b24-cc37-4775-849f-e070338103e8.png)

### Pods api Imperative
```
Create pods nginx image Imperative:        kubectl run <pod name> image=nginx:latest
Get pods:                                  kubectl get pods -o wide
Port forward, expose pod to external:      kubectl port-forward <pod-name> 8080:80
```

### Pods api Declarative
```
Run Yaml file 
kubectl --apply -f <podfile>.yml --validate=true
```



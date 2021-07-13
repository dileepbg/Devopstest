# Devopstest
Steps to run the App locally using minikube.

## Tools Used:
1. minikube - v1.22.0
2. docker - 20.10.6
3. kubernetes - v1.21.2
4. Container Registry : Docker Hub
5. IDE : Visual Studi Code and Lens (k8s cluster access)
6. Laptop : Mac 


## Steps for creating kubernetes components
- Precondition: Make sure to install all the above mnetioned tools

### Clone the repo from the below url
https://github.com/dileepbg/Devopstest.git

 This Repo contains required manifest files for both nginx and web app to create respective k8s components.

 Customised docker images are built locally and pushed to Docker Hub ( Docker files are avaialable for reference )

- start the minikube cluster by giving below command
  -  ```minikube start```

- Create certificates to configure https communication in nginx  (The CName used here is specific to the service specified in nginx_svc.yaml)
	-  ``` openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/nginx.key -out /tmp/nginx.crt -subj "/CN=nginxsvc/O=nginxsvc"  ```

- Give Below commands to create Secret and nginx service
```
kubectl create secret tls nginxsecret --key /tmp/nginx.key --cert /tmp/nginx.crt
kubectl apply -f nginx_svc.yaml
kubectl get svc

```
- Get the clusterIP of nginx svc and update this IP in webapp_deploy.yaml for NGINX env value and create webapp deployment by giving below commands ( make sure to nagivate to respective folder)

```
kubectl apply -f webapp_deploy.yaml
kubectl get po -o wide

```

- 2 pods will be created, Get the IP's of bote pods and update the IP in upstream block in default.conf under nginx folder.

```
upstream webapp {
         server 172.17.0.4:5001;
         server 172.17.0.3:5001;
}
```
- Now create config map and nginx deployment (navigate to nginx folder)

```
kubectl create configmap nginxconfigmap --from-file=default.conf
kubectl apply -f nginx_deploy.yaml

```
- Now Open the cluster in Lens IDE and check all the pods and services are healthy.

- Now give below command to access to application from localhost
```
minikube service nginxsvc

```
# Screen Shots

### minikube service nginxsvc

 https://github.com/dileepbg/Devopstest/blob/main/screenshots/minikube_service_nginxsvc.png

### weatherforcast (below screen shots are captured only for https)

 https://github.com/dileepbg/Devopstest/blob/main/screenshots/weatherforcast.png


### weatherforcast/stats

 https://github.com/dileepbg/Devopstest/blob/main/screenshots/weatherforcast_stats.png


### weatherforcast/fetch

 https://github.com/dileepbg/Devopstest/blob/main/screenshots/weatherforcast_fetch.png






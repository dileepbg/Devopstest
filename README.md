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
  - minikube start

- Create certificates to configure https communication in nginx  (The CName used here is specific to the service specified in nginx_svc.yaml)
 
	- openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/nginx.key -out /tmp/nginx.crt -subj "/CN=nginxsvc/O=nginxsvc"

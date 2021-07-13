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

Clone the repo from the below url

 This Repo contains required minifest files for both nginx and web app to create respective k8s components.

 Customised docker images are built locally and pushed to Docker Hub ( Docker files are avaialable for reference )



 	# The CName used here is specific to the service specified in nginx-app.yaml.
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/nginx.key -out /tmp/nginx.crt -subj "/CN=nginxsvc/O=nginxsvc"

	kubectl create secret tls nginxsecret --key /tmp/nginx.key --cert /tmp/nginx.crt

	kubectl apply -f nginx_svc.yaml

	kubectl get svc

	Get the clusterIP of nginx svc and update this IP in webapp_deploy.yaml for NGINX env value.

	kubectl apply -f webapp_deploy.yaml

	2 pods will be created, Get the IP's of nothe pods and update the IP in upstream block in default.conf under nginx folder

	kubectl create configmap nginxconfigmap --from-file=default.conf

	kubectl apply -f nginx_deploy.yaml

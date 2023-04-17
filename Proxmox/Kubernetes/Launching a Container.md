# Launching a Container
#Proxmox #Virtualization #Linux #Kubernetes 

## Intro
In this example we are going to be launching a NGINX container on our Kubernetes cluster.

## Procedure

1. Log in to the controller instance and create a `.yml` file.
```bash
nano web-server-pod.yml
```

The following is just an example of a Kubernetes `yml` file. In it we are defining a Pod of name 'nginx-example' in which we are going to be running a NGINX container pulled from [linuxserver.io](https://linuxserver.io) image registry.
```yml
apiVersion: v1 
kind: Pod 
metadata: 
	name: nginx-example 
	labels: 
		app: nginx 
spec: 
	containers: 
		- name: nginx 
		  image: linuxserver/nginx 
		  ports: 
			- containerPort: 80 
			  name: "nginx-http"
```

Paste and save this file.

2. Apply the `yml` file as follows:
```bash
kubectl apply -f web-server-pod.yml
```

3. Monitoring commands:
```bash
kubectl get pods
```

```bash
kubectl get pods -o wide
```

4. Now lets add a service for exposing a port to outside the pod.
```bash
nano service-nodeport.yml
```

```yml
apiVersion: v1 
kind: Service 
metadata: 
	name: nginx-example
spec: 
	type: NodePort 
	ports: 
		- name: http 
		  port: 80 
		  nodePort: 30080 
		  targetPort: nginx-http 
	selector: 
		app: nginx
```
Paste the configuration above and save the file.

5. Now apply the service.
```bash
kubectl apply -f service-nodeport.yml
```

6. Check the status of the service.
```bash
kubectl get service
```

7. You should be able now to open the NGINX web server welcome page from a browser. One of the cool things about Kubernetes is that you can reach this service with the IP address of any of the nodes in the cluster. Just make sure you add the correct port on the URL. `https://10.1.20.133:30080`
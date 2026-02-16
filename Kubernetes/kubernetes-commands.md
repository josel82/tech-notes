# Kubernetes commands

## Create a deployment
```bash
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080

```

## View deployments
```bash
kubectl get deployments
```

## Proxy access to pods.
Open another terminal and run:
```bash
kubectl proxy
```

## Getting the name of a Pod
```bash
export POD_NAME="$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\\n"}}{{end}}')"
echo Name of the Pod: $POD_NAME
```

## See the output of an Application

`curl <http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME:8080/proxy/`>

## Executing commands in a container
```bash
kubectl exec "$POD_NAME" -- env
```

## Start a terminal session inside a container
```bash
kubectl exec -ti $POD_NAME -- bash
```

## Kubectl subcommands

- `kubectl get` - list resources
- `kubectl describe` - show detailed information about a resource
- `kubectl logs` - print the logs from a container in a pod
- `kubectl exec` - execute a command on a container in a pod

## List pods by label
```bash
kubectl get pods -l key=value
```

## List services by label
```bash
kubectl get services -l key=value
```

## Delete a service by label
```bash
kubectl delete service -l key=value
```

## Apply a new label
```bash
kubectl label pods <pod-name> version=v1
```
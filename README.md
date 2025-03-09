# gripo-helm-deployment-dev
This is our repo for development

    ### Prerequisite

Ensure you have the following installed:<br />

* Docker (for container runtime)
* kubectl (Kubernetes CLI)
* Helm (v3+)
* Kind 

### Set Up a Local Kubernetes Cluster
<br />
<b>Using Kind</b>

Create a new Kind cluster:

```sh
kind create cluster --name gripo-cluster
```

Check if the cluster is running:

```sh
kubectl cluster-info --context kind-gripo-cluster
```
<br />

<b>  Load the Helm Chart</b>


If the chart is hosted in a Helm repository:

```sh
helm repo add gripo-repo https://dev.charts.gripo.io
 helm repo update
 helm install gripo gripo-io/gripo-mac
```
<br />

<b>Verify Deployment</b> 

Check if the pods are running: 

 ```sh 
kubectl get pods
```
To check Helm release:

 ```sh 
helm list
```

### Access the gripo portal

Depending on your deployment type  to use  Kind follow the below instructions: 
<br />
<b>Kind (Using Port Forwarding)</b>

Forward the port:
<br />
 ```sh 
kubectl port-forward svc/gripo-nginx 5055:5055 --namespace default
```
<br />
 Now access http://localhost:8080 in your browser.

<br />
<b> Customize Deployment(Optional)</b>

Fetch the Values YAML File If you want to save the values to a file for editing:

```sh 
helm show values gripo-repo/example-chart > custom-values.yaml
```

Modify values using custom custom values.yaml:

 ```sh 
helm install gripo -f custom-values.yaml gripo-io/gripo
```
<br />
### Stop and Cleanup
<br />
<b>Stopping the Cluster</b>

* For Kind:

 ```sh 
kind delete cluster --name gripo-cluster
```
<br />
<b>Uninstall Helm Release</b>
 
```sh 
helm uninstall gripo
```

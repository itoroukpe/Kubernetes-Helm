# Kubernetes-Helm
## Why use Helm?
Kubenetes can be difficult to manage with all the objects you need to maintain (ConfigMaps/Secrets, pods, services etc). Helm manages all of this for you. 

Helm greatly simplifies the process of creating, management and deploying application using Helm Charts. 
In addition, Helm also maintains a versioned history of every Chart (Application) installation. If something goes wrong, you can simply call "helm rollback".

Similarly, if you need to upgrade a chart, you can simply call "helm upgrade".

## What is a Helm Chart? 
In Helm, a chart is basically a collection of manifest files organized in a specific directory structure that describe a related Kubernetes resource. There are two main components to a chart: templates and values. These templates and values go through a template rendering engine, producing a manifest that is easily digestible by Kubernetes. 

Helm uses Charts to pack all the required K8s components for an application to deploy, run, and scale. 

Charts are very similar to RPM and DEB packages for Linux, making it easy for developer to distribute and consume/install applications via different repositories. 

## What is your experience using helm:
  1. In rondustech we have Used helm to deploy third party applications:
    - prometheus & Grafana for application monitoring   
    - EFK --> log management and data analytics
    - Nginx-ingress controller ---> NETWORKING and is an application LoadBalancers 

## Installing Helm
From The Helm Project
The Helm project provides two ways to fetch and install Helm. These are the official methods to get Helm releases. In addition to that, the Helm community provides methods to install Helm through different package managers. Installation through those methods can be found below the official methods.

## From Script
Helm now has an installer script that will automatically grab the latest version of Helm and install it locally.

You can fetch that script, and then execute it locally. It's well documented so that you can read through it and understand what it is doing before you run it.
```
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```
Yes, you can curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash if you want to live on the edge.

## From Apt (Debian/Ubuntu)
Members of the Helm community have contributed a Helm package for Apt. This package is generally up to date.
```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

  2. Custom developed/internal applications 
  ```
  helm create springapp  #this Create deployment manifests (helm charts) for springapp
  ```
      Use the tree to see the files in the Chart
   Important files to note: 
   - values.yaml
   - templates
   - Chart.yaml


 values.yaml: you can change
        - replicaCount
        - service account: false
        - service: CusterIP
        - autoscaling: false
        
template/Deployment.yml
     - containerPort: 8080
     template/Service
     - all are variables
     
To deploy the application
```
      helm install appName chartsName 
      $ helm install app springapp
```
To uninstall app
```
helm uninstall app # uninstall the application
```
To change the version
``
vi springapp/value.yml # to see if you have the right repository (image)
Example: Assign tag: latest
```
List deployments
```
$ helm ls    # List deployments
```

You can add a 3rd part repository
```
$ helm repo add nginx-stable https://helm.nginx.com/stable 
```
```
$ helm repo ls
```
```
$ helm search repo nginx-stable
```
See all the templates created
```
$ helm template nginx-stable/nginx-ingress #All the template created
```

Some other commands
```
helm repo rm nginx
helm search repo nginx  # searches number of deploys
helm template nginx-stable/nginx-ingress    # review charts
helm show values nginx/nginx-ingress   # show values/varaiables
```

  with helm 1500 lines of manifests file can be reduce 10 
  
helm Commands:
https://helm.sh/docs/helm/helm_dependency_list/
-------
helm:

The Helm package manager for Kubernetes.

Synopsis
The Kubernetes package manager

Common actions for Helm:

helm search: search for charts
helm pull: download a chart to your local directory to view
helm install: upload the chart to Kubernetes
helm list: list releases of charts
----------------
helm create
create a new chart with the given name

Synopsis
This command creates a chart directory along with the common files and directories used in a chart.

For example, 'helm create foo' will create a directory structure that looks something like this:

foo/
├── .helmignore   # Contains patterns to ignore when packaging Helm charts.
├── Chart.yaml    # Information about your chart
├── values.yaml   # The default values for your templates
├── charts/       # Charts that this chart depends on
└── templates/    # The template files
    └── tests/    # The test files
'helm create' takes a path for an argument. If directories in the given path do not exist, Helm will attempt to create them as it goes. If the given destination exists and there are files in that directory, conflicting files will be overwritten, but other files will be left alone.

helm create NAME [flags]
options:
-h, --help             help for create
  -p, --starter string   the name or absolute path to Helm starter scaffold


## install a chart - Another Example

Synopsis
This command installs a chart archive.

The install argument must be a chart reference, a path to a packaged chart, a path to an unpacked chart directory or a URL.

To override values in a chart, use either the '--values' flag and pass in a file or use the '--set' flag and pass configuration from the command line, to force a string value use '--set-string'. You can use '--set-file' to set individual values from a file when the value itself is too long for the command line or is dynamically generated. You can also use '--set-json' to set json values (scalars/objects/arrays) from the command line.
```
$ helm install -f myvalues.yaml myredis ./redis
```
or
```
$ helm install --set name=prod myredis ./redis
```
or

$ helm install --set-string long_int=1234567890 myredis ./redis
or
```
$ helm install --set-file my_script=dothings.sh myredis ./redis
```
or
```
$ helm install --set-json 'master.sidecars=[{"name":"sidecar","image":"myImage","imagePullPolicy":"Always","ports":[{"name":"portname","containerPort"
```
```
auto-scaling (HPA, CAS)
   prometheus and grafana 
   EFK
   statefulset, 
   requests and limits, 
   limitRange
   resource quota and 
      dev-namespace:
        apiVersion: v1 
        kind: res
   resource limits 
   ingress
```
```
Assigning Pods to Nodes  
    nodeSelector 
    Node affinity
Node isolation/restriction
Affinity and anti-affinity 
Node affinity 
preferredDuringSchedulingrequiredDuringExecution
requiredDuringSchedulingIgnoredDuringExecution
requiredDuringSchedulingrequiredDuringExecution
```

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector:
    app: dbNode
```
```
1004  kubectl get node --show-labels
 1005  kubectl  get node
 1006  kubectl label node nobe3 app=dn
 1007  kubectl label  nobe3 app=dn
 1008  kubect node label nobe3 app=dn
 1009  kubectl node label nobe3 app=dn
 1010  kubectl label nodes node3 app=dbNode
 1011  kubectl get node --show-labels
 1012  clear
 1013  kubectl get node --show-labels
 1014  kubectl label nodes node3 app=db6
```


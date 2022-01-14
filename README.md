# sample-kubernetes-ruby
New app structure using kubernetes:
![alt text](https://github.com/islamafifi17/sample-kubernetes-ruby/blob/master/app-new-structure.png?raw=true)

**Changes Made**:
  •	Add nginx ingress controller to act as our reverse proxy
  •	Create new deployment for each component 
  •	Depend on svc cluster-ip type for communication between pods

**Pods Synchroniztion**:
  •	Default behavior for docker-compose is to bring up the dependencies (defined in links section) first
  •	Simulating the same behavior by kubernetes using initContainers.. Not to add the postgres or redis in the same deployment as a an initContainer because this will cause some    troubles regarding scaling up and down situations but to implement a health check mechanism in the drkiq-app initcontainers section to make sure the postgres and redis are      up and running
  •	Use readiness probe to not receive traffic before the app-pod Is ready

**High Availability Flavor**
  •	Implement podAntiAffinity section in app deployment to make sure when having more replicas in a real environment each pod will be scheduled on different node

**Scalability Flavor**
  •	Not implemented now but in real env we can some kind of metrics server to enable kubernetes auto scaling depending on some thresholds like cpu,memory
  
**How To Use**
  1.	Make sure to have a minikube cluster up and running on your local machine
  2.	Add to your /etc/hosts file new entry **${your_minikube_cluster_ip} instabug.com**
  3.	Enable ingress on your cluster using command **minikube addons enable ingress**
  4.	Use this command to create kubernetes resources **kubectl create –f ${path_to_resources_directory}**
  5. open **instabug.com** in your browser you should see this
  ![alt text](https://github.com/islamafifi17/sample-kubernetes-ruby/blob/master/drkiq-ouput.png?raw=true)
 
 

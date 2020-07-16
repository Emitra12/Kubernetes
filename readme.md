## This is for beginners

## Commands:
  
  1) kubectl get all ---Give us all information about pods, ReplicaSets and deployment that created
  2) kubectl get ReplicaSet
  3) kubectl get pods -o wide
  4) kubectl delete pod <podame>
  5) kubectl replace -f replicaset-defination.yaml (after editing the file)
  6) kubectl scale --replicas=6 -f/replicaset replicaset-defination.yaml (without editing file)
  7) kubectl delete ReplicaSet <name>
  8) kubectl edit replicaset replicasetname
  8) kubectl get pod -n kube-system

## Deployements:
  
  1) kubectl get deployment
  2) kubectl create -f <yaml file name>
  3) kubectl apply -f <yaml file name>
  4) kubectl rollout status deployement/<app name> (deploy conatiner in the backend)
  5) kubectl rollout history deployement/<appname>
  6) kubectl delete deployement <name>
  7) kubectl describe deployement
  8) kubectl rollout undo deployment/<name> (get back to the previous revison if something happens with current one)

  rollback , upgrade, rollout , revision

## Kuberenets networking short intro:
  we use custom networking solution to assign unique ip to each pods which communicate to each other without NAT or with internal routing technique
  and for that we use different networking solution to achieve this in kubernates like vmware nsx and cisco n so on......

## Services:
  
  1) NodePort: external system/users --> nodeport ---> service port --> pods port or services
  2) ClusterIP --- Default one
  3) Loadbalancer

## Namespaces:
   1) kubectl get pods --namspace=dev/prod
   2) kubectl config set-context $(kubectl config curent-context) --namespace=dev/prod ---to set permannet namespace
   3) kubectl get pods --all-namespaces
   4) kubectl create namespace dev/prod/other
   5) service name.namespace.subdomain.localdomain (db-service.dev.scv.cluster.local) -- to communicate one namespace service to other namespace service
   6) resourcequota file in namespace
   7) kubectl get namespaces
   
## Kubernetes Microservices Architecture:
   
   Common voting application
   ---link -> to use to link beetween two application to run togather in docker
   example: Right each application running alone --
   1) docker run -d --name=redis redis
   2) docker run -d --name=db postgres:9.4
   3) docker run -d --name=vote -p 5000:80 voting-app
   4) docker run -d --name=result -p 50001:80 result-app
   5) docker run -d --name=woker worker
   
## Now each application are running togather with --link command
   
   1) docker run -d --name=redis redis
   2) docker run -d --name=db postgres:9.4
   3) docker run -d --name=vote -p 5000:80 --link redis:redis voting-app
   4) docker run -d --name=result -p 50001:80 --link db:db result-app
   5) docker run -d --name=woker --link db:db --link redis:redis worker
   
## Some good commands:
   1) /etc/hostname & /etc/hosts ---to change the hostname of console
   2) /etc/Network/interfaces -- to assign the static ip address to the node
   3) ipconfig interface-name ipaddress ---to assign the temp id address to node
   4) swapoff -a -- to off the swap  and /etc/fstab -- comments out the swap line

### Focus more on below commands for real time exam preparation:

## Create an NGINX Pod

kubectl run nginx --image=nginx
kubectl run --generator=run-pod/v1 nginx --image=nginx
kubectl run --generator=run-pod/v1 redis --image=redis --namespace=finance

## Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)

kubectl run --generator=run-pod/v1 nginx --image=nginx --dry-run -o yaml

--dry-run -- creates the resources on cluster 
--dry-run=client -- will not create resource on cluster , its just test your commands 
-o yaml -- output the resource defination in yaml format

## Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379

kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml (This will automatically use the pod's labels as selectors)

or 

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml

 (This will not use the pods labels as selectors, instead it will assume selectors as app=redis. You cannot pass in selectors as an option. So it does not work very well if your pod has a different label set. So generate the file and modify the selectors before creating the service)
 
kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml 

or 

kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml

## Create a deployment

kubectl create deployment --image=nginx nginx

## Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)

kubectl create deployment --image=nginx nginx --dry-run -o yaml

## Generate Deployment YAML file (-o yaml). Don't create it(--dry-run) with 4 Replicas (--replicas=4)

kubectl create deployment --image=nginx nginx --dry-run -o yaml > nginx-deployment.yaml

## Save it to a file, make necessary changes to the file (for example, adding more replicas) and then create the deployment.


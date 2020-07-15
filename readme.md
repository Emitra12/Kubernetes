## This is for beginners

## Commands:
  
  1) kubectl get all ---Give us all information about pods, ReplicaSets and deployment that created
  2) kubectl get ReplicaSet
  3) kubectl get pods -o wide
  4) kubectl delete pod <podame>
  5) kubectl replace -f replicaset-defination.yaml (after editing the file)
  6) kubectl scale --replicas=6 -f replicaset-defination.yaml (without editing file)
  7) kubectl delete ReplicaSet <name>

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
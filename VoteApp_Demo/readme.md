##commands:
  kubectl get all ---Give us all information about pods, ReplicaSets and deployment that created
  kubectl get ReplicaSet
  kubectl get pods -o wide
  kubectl delete pod <podame>
  kubectl replace -f replicaset-defination.yaml (after editing the file)
  kubectl scale --replicas=6 -f replicaset-defination.yaml (without editing file)
  kubectl delete ReplicaSet <name>

##Deployements:
  kubectl get deployment
  kubectl create -f <yaml file name>
  kubectl apply -f <yaml file name>
  kubectl rollout status deployement/<app name> (deploy conatiner in the backend)
  kubectl rollout history deployement/<appname>
  kubectl delete deployement <name>
  kubectl describe deployement
  kubectl rollout undo deployment/<name> (get back to the previous revison if something happens with current one)

  rollback , upgrade, rollout , revision

##Kuberenets networking short intro:
  we use custom networking solution to assign unique ip to each pods which communicate to each other without NAT or with internal routing technique
  and for that we use different networking solution to achieve this in kubernates like vmware nsx and cisco n so on......

##Services:
  1) NodePort: external system/users --> nodeport ---> service port --> pods port or services
  2) ClusterIP --- Default one
  3) Loadbalancer

## Kubernetes Microservices Architecture:
   Common voting application
   ---link -> to use to link beetween two application to run togather in docker
   example: Right each application running alone --
   docker run -d --name=redis redis
   docker run -d --name=db postgres:9.4
   docker run -d --name=vote -p 5000:80 voting-app
   docker run -d --name=result -p 50001:80 result-app
   docker run -d --name=woker worker
   
##   Now each application are running togather with --link command
   
   docker run -d --name=redis redis
   docker run -d --name=db postgres:9.4
   docker run -d --name=vote -p 5000:80 --link redis:redis voting-app
   docker run -d --name=result -p 50001:80 --link db:db result-app
   docker run -d --name=woker --link db:db --link redis:redis worker
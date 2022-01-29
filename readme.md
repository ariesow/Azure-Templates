##Install PortainerIO on AKS
az aks get-credentials --resource-group AKSFarm --name aksclust01
helm repo add portainer https://portainer.github.io/k8s/
helm repo update
kubectl create namespace portainer
helm install -n portainer portainer portainer/portainer --set service.type=LoadBalancer

#Sample output
Get the application URL by running these commands:
     NOTE: It may take a few minutes for the LoadBalancer IP to be available.
           You can watch the status of by running 'kubectl get --namespace portainer svc -w portainer'
  export SERVICE_IP=$(kubectl get svc --namespace portainer portainer --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}")
  echo http://$SERVICE_IP:9443

  #Connect to AKS Cluster - Az CLI
  az aks get-credentials --resource-group <RG Name> --name <AKS cluster name>
  
  Access to pod/container
  kubectl exec --stdin --tty mysql-0 --namespace mysql-stateful -- /bin/bash
  
  Get Status
  kubectl get all,secret,configmap
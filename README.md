# AKSCluster
AKS Cluster Setup with Azure CLI

```
az login

## Create a resource group
az group create --resource-group dohoney-aksdemo-rg  --location westus

RESOURCE_GROUP="dohoney-aksdemo-rg"
LOCATION="westus"

## Verify Microsoft.OperationsManagement and Microsoft.OperationalInsights are registered on your subscription. 
az provider show -n Microsoft.OperationsManagement -o table
az provider show -n Microsoft.OperationalInsights -o table
## If they are not registered, register Microsoft.OperationsManagement and Microsoft.OperationalInsights using:
az provider register --namespace Microsoft.OperationsManagement
az provider register --namespace Microsoft.OperationalInsights
#
#Create an AKS cluster using the az aks create command with the --enable-addons monitoring parameter to enable Azure Monitor for containers. 
#The following example creates a cluster named myAKSCluster with one node:
#
az aks create --resource-group $RESOURCE_GROUP --name myAKSCluster2 --node-count 1 --enable-addons monitoring --generate-ssh-keys --location westus

# Get API Credentials
az aks get-credentials --resource-group $RESOURCE_GROUP --name myAKSCluster2

# If you are using Windows System for Linux (WSL) -- alias kubectl
alias k="kubectl.exe"
k get nodes

# Now deploy the Application
k apply -f azure-vote.yaml
# When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.
#
k get service azure-vote-front --watch
NAME               TYPE           CLUSTER-IP    EXTERNAL-IP    PORT(S)        AGE
azure-vote-front   LoadBalancer   10.0.28.245   13.88.44.231   80:30238/TCP   29s

# Then place the EXTERNAL-IP column value in a browser and use the application


```

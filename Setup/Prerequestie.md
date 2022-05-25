


Install azure cli


$ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi; Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'; rm .\AzureCLI.msi


Install kubectl

az provider show -n Microsoft.OperationsManagement -o table
az provider show -n Microsoft.OperationalInsights -o table


 az account set --subscription "CSP-Competency Dev-IMS App Ops-Mohammed khaja Pasha"
 az account show

az group create --name POC_KA --location eastus
az aks create --resource-group POC_KA --name testargocluster --node-count 1 --enable-addons monitoring --generate-ssh-keys
az aks install-cli
az aks get-credentials --resource-group POC_KA --name testargocluster
kubectl get nodes
az aks delete --resource-group POC_KA --name testargocluster
choco install kubernetes-cli
az group delete --name POC_KA --yes --no-wait






1.Check if kubectl is working as expected
  kubectl get nodes
  
2.Create namespace
  kubectl create namespace argocd
  
3.Run the Argo CD install script provided by the project maintainers.
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  
4. Check the status of your Kubernetes pods
  kubectl get pods -n argocd

## Forwarding Ports to Access Argo CD
5.1.Retrieve the admin password which was automatically generated during your installation and decode from base64 from online.
  kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"

  M3BoRWNGVWdCOTMxUE1lMA==
  3phEcFUgB931PMe0

5.2 forward those to arbitrarily chosen other ports, like 8080, like so:
  kubectl port-forward svc/argocd-server -n argocd 8080:443
  
5.3 Access from ineternet from browser.
  http://localhost:8080 
  user id : admin
  password :base64 decoded password.
  
## Working with Argo CD from the Command Line
6. Use chocolatey utility to install in Windows ( with admin access)
   choco install argocd-cli
   
## Deploying an Example Application from argocd using argocd cli
7. Deploying an Example Application
  argocd login localhost:8080
  user id : admin
  password :base64 decoded password.
  argocd app create helm-guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path helm-guestbook --dest-server https://kubernetes.default.svc --dest-namespace default
  
7.1 Check status inside argocd
  argocd app get helm-guestbook

7.2 Actually deploy the application
  argocd app sync helm-guestbook

7.3 Port foward from onther session check the application status
  kubectl port-forward svc/helm-guestbook 9090:80
  http://localhost:9090
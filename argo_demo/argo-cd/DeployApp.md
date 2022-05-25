
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
argocd app create --name demoapp \
--repo https://github.com/abdulk3/argo.git \
--dest-server https://kubernetes.default.svc \
--dest-namespace default --path argo-cd/demoapp

or 

argocd app create demoapp https://github.com/abdulk3/argo.git --path argo-cd/demoapp --dest-server https://kubernetes.default.svc --dest-namespace default
  

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
YAML

apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: demoapp
  namespace: default
spec:
  project: default
  source:
    repoURL: https://github.com/abdulk3/argo.git
    targetRevision: HEAD
    path: argo-cd/exampleapp
  destination:
    server: https://kubernetes.default.svc
    namespace: default
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@


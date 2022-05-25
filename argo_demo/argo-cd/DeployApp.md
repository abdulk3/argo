
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
argocd app create --name demoapp \
--repo https://github.com/abdulk3/argo.git \
--dest-server https://kubernetes.default.svc \
--dest-namespace default \
--path argo_demo/demoapp

or 

argocd app create demoapp https://github.com/abdulk3/argo.git --path argo_demo/demoapp --dest-server https://kubernetes.default.svc --dest-namespace default
  

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
YAML

apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: demoapp
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/abdulk3/argo.git
    targetRevision: HEAD
    path: argo_demo/demoapp/
    directory:
      recurse: true
  destination:
    server: https://kubernetes.default.svc
    namespace: demoapp
  syncPolicy:
    automated:
      prune: false
      selfHeal: false



@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@


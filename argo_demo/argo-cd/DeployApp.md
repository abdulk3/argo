
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
argocd app create --name demoapp \
--repo https://github.com/marcel-dempers/docker-development-youtube-series \
--dest-server https://kubernetes.default.svc \
--dest-namespace default --path argo/demoapp

or 

argocd app create demoapp --repo https://github.com/argoproj/argocd-example-apps.git --path helm-guestbook --dest-server https://kubernetes.default.svc --dest-namespace default
  

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
    repoURL: https://github.com/marcel-dempers/docker-development-youtube-series.git
    targetRevision: HEAD
    path: argo_demo/example-app
  destination:
    server: https://kubernetes.default.svc
    namespace: default
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@


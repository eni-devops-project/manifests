# Manifest kubernetes

Ces manifest décrivent le fonctionnement de l'application au sein de l'orchestrateur kubernetes

# Installation

À condition d'avoir installé le cluster avec l'IaC donnée on peut simplement lancer:
- kubectl apply -f namespace.yml
- kubectl apply -f .

# Passwords
- Replace passwords in the secrets

# Installing ingress nginx

```
helm install ingress-nginx ingress-nginx/ingress-nginx \
  --create-namespace \
  --namespace $NAMESPACE \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
  --set controller.service.externalTrafficPolicy=Local
```

# Installing cert manager

```
helm upgrade \
  cert-manager oci://quay.io/jetstack/charts/cert-manager \
  --version v1.18.2 \
  --namespace cert-manager \
  --create-namespace \
  --set crds.enabled=true \
  --set config.featureGates.ACMEHTTP01IngressPathTypeExact=false
```

Last option is set due to a bug in ingress nginx prefix/exact path types.

# Installing argo cd to do gitops

- kubectl create namespace argocd
- kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
- get the password from the secret generated
- portforward on the ui and connect

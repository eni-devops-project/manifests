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

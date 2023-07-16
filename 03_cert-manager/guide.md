```
> kubectl create ns cert-manager

# Add the Helm repository
> helm repo add jetstack https://charts.jetstack.io

# Update your local Helm chart repository cache
> helm repo update

# Install `CustomResourceDefinitions`
> kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.crds.yaml

## Now you can use certificate resource
> kubectl get certificate

# Install cert-manager
> helm upgrade -i -n cert-manager cert-manager jetstack/cert-manager --version v1.11.0


# Create secret for issuer
> kubectl apply -f ./issuers/secret-cf-token.yaml

# Staging
## Create cluster issuer
> kubectl apply -f ./issuers/letsencrypt-staging.yaml

## Create certificate
> kubectl apply -f ./certificates/staging/staging.example.yaml

> kubectl logs -n cert-manager -f cert-manager-*
> kubectl get challenges

# Production
## Create cluster issuer
> kubectl apply -f ./issuers/letsencrypt-production.yaml

## Create certificate
> kubectl apply -f ./certificates/production/example.yaml

```

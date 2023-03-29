# kubernetes_ingress

## Question 1

Pour installer kind, il faut d'abord installer docker. Ensuite, il faut installer kind avec la commande suivante :

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.17.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

Pour créer un cluster, il faut utiliser la commande suivante :

```bash
kind create cluster --config kind-config.yaml
```

## Question 2

Pour installer Nginx Ingress Controller, il faut utiliser la commande suivante :

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml
```

On doit appliquer la commande suivante :

```bash
kubectl wait --namespace ingress-nginx   --for=condition=ready pod   --selector=app.kubernetes.io/component=controller   --timeout=90s
```

Pour vérifier que le controller est bien installé, il faut utiliser la commande suivante :

```bash
kubectl get pods -n ingress-nginx
```

## Question 3

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

Complétion du schéma :

![Alt text](/images/schema.png?raw=true "1")

## Question 4

Builder et publier sur le DockerHub :

Nous avons mis en place 3 DockerFiles permettant de créer les 3 images correspondant.

Pour les créer et les publier, on utilise les commandes suivantes :

```bash
docker build -t nanodeus/tacos-image -f tacos/
docker build -t nanodeus/burger-image -f burger/
docker build -t nanodeus/pizza-image -f pizza/
docker push nanodeus/tacos-image
docker push nanodeus/burger-image
docker push nanodeus/pizza-image
```

On peut retrouver nos images sur le DockerHub : <https://hub.docker.com/u/nanodeus>

![Alt text](/images/dockerhub.png?raw=true "2")

## Question 5

Pour l'exécution des déploiements et des services, on créait les fichiers yaml correspondants.

Ensuite, on utilise les commandes suivantes :

![Alt text](/images/kubectlApply.png?raw=true "3")

On peut ensuite créer l'ingress qui va nous permettre d'accéder aux services.

On applique la commande suivante :

![Alt text](/images/kubectlIngress.png?raw=true "4")

# kubernetes_ingress

## Question 1

Pour installer kind, il faut d'abord installer docker. Ensuite, il faut installer kind avec la commande suivante :

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.18.0/kind-linux-amd64
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

![Alt text](images/schema.png?raw=true "1")

## Question 4

Builder et publier sur le DockerHub :

Nous avons mis en place 3 DockerFiles permettant de créer les 3 images correspondant.

Pour les créer et les publier, on utilise les commandes suivantes :

```bash
docker build -t nanodeus/tacos-image tacos/
docker build -t nanodeus/burger-image burger/
docker build -t nanodeus/pizza-image pizza/
docker push nanodeus/tacos-image
docker push nanodeus/burger-image
docker push nanodeus/pizza-image
```

On peut retrouver nos images sur le DockerHub : <https://hub.docker.com/u/nanodeus>

![Alt text](images/dockerhub.png?raw=true "2")

## Question 5

Pour l'exécution des déploiements et des services, on créait les fichiers yaml correspondants.

Ensuite, on utilise les commandes suivantes :

![Alt text](images/kubectlApply.png?raw=true "3")

On peut ensuite créer l'ingress qui va nous permettre d'accéder aux services.

On applique la commande suivante :

![Alt text](images/kubectlIngress.png?raw=true "4")

Pour notre cas, il nous faut configurer le fichier hosts de notre machine pour pouvoir accéder aux services.

On ajoute la ligne suivante :

```bash
127.0.0.1       burgerandtacos.eatsout.com mypizza.eatsout.com
```

On peut ensuite accéder aux services en utilisant curl :

![Alt text](images/curl.png?raw=true "5")

## Question 6

Afin de pouvoir gérer une  charge plus importante, on peut utiliser la propriété replicas qui permet de créer plusieurs pods pour un même service.

```yaml
replicas: 3
```

Pour vérifier que les pods sont bien créés, on utilise la commande suivante :

```bash
kubectl get pods
```

On peut aussi utiliser un service de type LoadBalancer.

```yaml
type: LoadBalancer
```

Kubernetes créera automatiquement un équilibreur de charge pour votre Service

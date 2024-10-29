# Deploiment d'une application Flask dans kubernetes 🚀

Ce projet déploie une application Flask qui se connecte à une base de données MySQL dans un cluster Kubernetes (minikube local).

## Pré-requis 🛠️
Assurez-vous d'avoir les outils suivants installés sur votre machine :
- [Docker](https://docs.docker.com/get-docker/)
- [Git](https://git-scm.com/)
- [Minikube](https://minikube.sigs.k8s.io/docs/)

## Installation 🔧

1. **Clonez le repository localement :**

    ```bash
    git clone https://github.com/Abdoulaye123Diallo/KubernetesApp.git
    ```

2. **Accédez au répertoire du projet :**

    ```bash
    cd KubernetesApp
    ```

3. **Installer ces composants par ordre via les manifests en utilisant ces commandes :**

    ```bash
    minikube start --network-plugin=cni --cni=calico --nodes 3 --driver=docker
    kubectl apply -f database-configmap.yaml
    kubectl apply -f database-secret.yaml
    kubectl apply -f database-deployment.yaml
    kubectl apply -f database-service.yaml
    kubectl apply -f network-policy.yaml
    kubectl apply -f backend-deployment.yaml
    kubectl apply -f backend-service.yaml
    ```
    Lancer cette commande pour exposer le service :
   ```bash
    minikube service my-app-service
    ```
   Une page sera généré par le browser pour accéder au service via l'extérieur

## Tests via Postman 🔍

### Ajouter un étudiant 🧑‍🎓
Utilisez la commande `curl` ci-dessous pour ajouter un étudiant à la base de données MySQL (... est le port généré par le browser) :

```bash
curl --location 'http://localhost:.../add' \
--header 'Content-Type: application/json' \
--data '{
    "ID": 1,
    "nom": "Abdoulaye Diallo",
    "age": 23
}'
```


### Récupérer les étudiants 👥
Exécutez cette commande pour obtenir la liste des étudiants dans la base de données :

```bash
    curl --location 'http://localhost:.../etudiants'
```

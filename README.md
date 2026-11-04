# DevOps — Travaux pratiques

<p align="center">
  <img src="https://img.shields.io/badge/DevOps-Training-blue?style=for-the-badge&logo=github" alt="DevOps Training">
  <img src="https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?style=for-the-badge&logo=githubactions" alt="GitHub Actions">
  <img src="https://img.shields.io/badge/Docker-Containers-2496ED?style=for-the-badge&logo=docker" alt="Docker">
  <img src="https://img.shields.io/badge/Ansible-Automation-EE0000?style=for-the-badge&logo=ansible" alt="Ansible">
  <img src="https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?style=for-the-badge&logo=kubernetes" alt="Kubernetes">
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge" alt="Completed">
</p>

Ce dépôt regroupe mes travaux pratiques de **DevOps**, réalisés dans le cadre du cours sur le pipelining, l'intégration continue et le déploiement d'applications.

L'objectif est de comprendre comment automatiser les différentes étapes du cycle de vie d'une application : gestion du code source, vérification de sa qualité, exécution de pipelines CI/CD, conteneurisation, orchestration et configuration d'un serveur web.

Le projet s'appuie sur une application web statique affichant **Hello World !**, utilisée pour expérimenter plusieurs méthodes de déploiement : Docker, Ansible, GitHub Pages et Kubernetes.

---

## Sommaire

- [Objectifs du cours](#objectifs-du-cours)
- [Exercices — Pipelining](#exercices--pipelining)
- [Exercice avancé — Docker, GitHub Actions et GitHub Pages](#exercice-avancé--docker-github-actions-et-github-pages)
- [Déploiement avec Docker](#déploiement-avec-docker)
- [Automatisation avec Ansible](#automatisation-avec-ansible)
- [Orchestration avec Kubernetes](#orchestration-avec-kubernetes)
- [Vérification des déploiements](#vérification-des-déploiements)
- [Environnements DEV, VAL et PROD](#environnements-dev-val-et-prod)
- [Structure du projet](#structure-du-projet)
- [Technologies utilisées](#technologies-utilisées)
- [Bilan du TP](#bilan-du-tp)

---

## Objectifs du cours

- Comprendre les principes du DevOps et de la CI/CD.
- Utiliser Git et GitHub pour gérer le code source et son historique.
- Manipuler les branches et les conditions d'exécution.
- Créer des workflows automatisés avec GitHub Actions.
- Utiliser des variables et transmettre des résultats entre plusieurs jobs.
- Vérifier la qualité du HTML avec HTMLHint.
- Déployer une application web statique.
- Construire une image Docker et exécuter un conteneur.
- Publier une image sur Docker Hub.
- Automatiser l'installation et la configuration d'un serveur avec Ansible.
- Comprendre les concepts de Kubernetes et de l'orchestration de conteneurs.
- Déployer une application dans un cluster Kubernetes.
- Utiliser les namespaces, deployments, pods et services.
- Gérer l'authentification auprès d'un registre Docker privé.
- Vérifier le fonctionnement d'une application déployée.

---

## Exercices — Pipelining

### 1. Hello World

- [x] Créer un workflow qui affiche `Hello World`.

Workflow : `.github/workflows/hello-world.yml`

### 2. Informations utilisateur

- [x] Créer trois jobs pour afficher le nom, le prénom et l'adresse e-mail.
- [x] Utiliser les variables du dépôt GitHub plutôt que des valeurs codées en dur.

Workflow : `.github/workflows/informations.yml`

### 3. Exécution d'un script Python

- [x] Exécuter un script Python affichant `Commit success!`.
- [x] Déclencher automatiquement le workflow lors d'un push.

Workflow : `.github/workflows/python.yml`

### 4. Gestion des branches

- [x] Afficher le nom de la branche sur laquelle le workflow s'exécute.
- [x] Manipuler les branches `Dev`, `Val` et `Prod`.
- [x] Comprendre le rôle des branches dans le processus de développement.

Workflow : `.github/workflows/branche.yml`

### 5. Pipeline conditionnelle Dev → Val → Prod

- [x] Diviser un nombre par 2 dans l'environnement Dev.
- [x] Transmettre le résultat à Val si la condition prévue est satisfaite.
- [x] Transmettre le résultat à Prod si les conditions sont remplies.
- [x] Interrompre la progression lorsque les conditions ne sont pas remplies.

Workflow : `.github/workflows/dev-val-prod.yml`

---

## Exercice avancé — Docker, GitHub Actions et GitHub Pages

**Objectif :** automatiser la publication d'une application web statique en utilisant une image Docker publiée sur Docker Hub.

Cet exercice met en œuvre une chaîne CI/CD dans laquelle le fichier HTML n'est plus nécessaire dans le dépôt GitHub : il est récupéré directement depuis l'image Docker.

### Fonctionnement du pipeline

Le workflow `.github/workflows/docker-pages.yml` organise le processus en plusieurs jobs.

1. **Récupération de l'image Docker**
   - Authentification auprès de Docker Hub.
   - Récupération de l'image `compotescassis/docker-devops:latest`.

2. **Extraction du fichier HTML**
   - Création d'un conteneur temporaire à partir de l'image.
   - Extraction de `/usr/share/nginx/html/index.html` avec `docker cp`.
   - Suppression du conteneur temporaire.
   - Publication du fichier extrait sous forme d'artefact GitHub Actions.

3. **Déploiement sur GitHub Pages**
   - Téléchargement de l'artefact contenant le site.
   - Préparation de GitHub Pages.
   - Publication du site à partir de l'artefact.

Le job de déploiement dépend de la réussite du job d'extraction grâce à `needs`.

### Travaux réalisés

- [x] Créer une image Docker à partir du Dockerfile.
- [x] Créer un compte Docker Hub.
- [x] Créer le dépôt Docker Hub `docker-devops`.
- [x] Configurer les secrets GitHub `DOCKER_USERNAME` et `DOCKER_TOKEN`.
- [x] Publier l'image `compotescassis/docker-devops:latest` sur Docker Hub.
- [x] Supprimer `index.html` du dépôt GitHub.
- [x] Récupérer l'image Docker depuis GitHub Actions.
- [x] Créer un conteneur temporaire.
- [x] Extraire le fichier HTML du conteneur.
- [x] Transmettre le fichier HTML entre les jobs avec un artefact.
- [x] Déployer le site sur GitHub Pages.
- [x] Vérifier la réussite des jobs GitHub Actions.
- [x] Confirmer l'affichage public du site dans le navigateur.

### Ressources

**Image Docker Hub :**

https://hub.docker.com/r/compotescassis/docker-devops

**Site GitHub Pages :**

https://grignonlouis.github.io/DevOps/

**Workflow :** `.github/workflows/docker-pages.yml`

### Sécurité

Les identifiants Docker Hub sont stockés dans les secrets du dépôt GitHub :

- `DOCKER_USERNAME` : nom d'utilisateur Docker Hub.
- `DOCKER_TOKEN` : jeton d'accès Docker Hub.

Ces informations ne sont pas écrites directement dans le fichier YAML du workflow.

### Principe technique

Le fichier HTML est intégré dans l'image Docker lors de sa construction, à l'emplacement :

`/usr/share/nginx/html/index.html`

Après publication de l'image sur Docker Hub, le workflow peut récupérer ce fichier sans avoir besoin de le conserver dans le dépôt GitHub.

Cette approche permet de séparer le stockage de l'application (image Docker) du processus de déploiement (GitHub Actions).

---

## Déploiement avec Docker

**Objectif :** construire une image Docker contenant la page HTML et un serveur Nginx, puis exécuter l'application dans un conteneur.

### Principe

Le fichier `Dockerfile` définit la construction de l'image à partir de Nginx sur Alpine Linux.

Il copie le fichier `index.html` dans le répertoire web de Nginx et configure ses permissions afin que le serveur puisse lire le fichier.

Le conteneur utilise le port 80 en interne, publié sur le port 8081 de la machine Ubuntu.

### Travaux réalisés

- [x] Créer un `Dockerfile`.
- [x] Construire l'image `hello-world-tp`.
- [x] Copier `index.html` dans le répertoire web de Nginx.
- [x] Configurer les permissions du fichier HTML.
- [x] Créer et démarrer le conteneur `hello-docker`.
- [x] Diagnostiquer et corriger une erreur HTTP 403 liée aux permissions.
- [x] Consulter les conteneurs et les journaux Docker.
- [x] Ajouter un fichier `.dockerignore`.
- [x] Publier une image sur Docker Hub.

### Commandes utilisées

Construire l'image :

```bash
docker build -t hello-world-tp .
```

Démarrer le conteneur :

```bash
docker run -d --name hello-docker -p 8081:80 hello-world-tp
```

Vérifier le conteneur :

```bash
docker ps
```

Consulter les journaux :

```bash
docker logs hello-docker
```

Tester le site :

```bash
curl -I http://localhost:8081
```

Publier l'image sur Docker Hub :

```bash
docker tag hello-world-tp compotescassis/docker-devops:latest
docker push compotescassis/docker-devops:latest
```

**URL locale :** http://localhost:8081

**Dépôt Docker Hub :** https://hub.docker.com/r/compotescassis/docker-devops

**Remarque :** le fichier `index.html` a ensuite été supprimé du dépôt GitHub conformément aux consignes de l'exercice avancé. L'image déjà publiée sur Docker Hub conserve sa propre copie du fichier HTML. Une nouvelle construction de l'image nécessite donc de rendre à nouveau le fichier source disponible dans le contexte de build.

---

## Automatisation avec Ansible

**Objectif :** automatiser l'installation et la configuration de Nginx directement sur la machine Ubuntu.

Contrairement à Docker, qui exécute Nginx dans un conteneur isolé, Ansible configure un serveur Nginx installé sur le système hôte.

### Fichiers utilisés

- `ansible/inventory.ini` : définit les machines ciblées par Ansible.
- `ansible/playbook.yml` : décrit les tâches d'installation et de configuration.

L'inventaire utilise `localhost` avec `ansible_connection=local`. Les tâches sont donc exécutées sur la machine locale, sans connexion SSH.

### Travaux réalisés

- [x] Créer un inventaire Ansible ciblant `localhost`.
- [x] Tester la communication avec la machine cible.
- [x] Installer Nginx avec le module `apt`.
- [x] Copier `index.html` dans `/var/www/html/index.html`.
- [x] Définir le propriétaire et les permissions du fichier.
- [x] Configurer Nginx pour écouter sur le port 8082.
- [x] Démarrer et activer le service Nginx.
- [x] Définir un handler pour redémarrer Nginx lorsque sa configuration change.
- [x] Résoudre un problème lié au cache APT.
- [x] Exécuter le playbook sans échec.

### Commandes utilisées

Tester la connexion Ansible :

```bash
ansible -i ansible/inventory.ini web -m ping
```

Exécuter le playbook :

```bash
ansible-playbook -i ansible/inventory.ini ansible/playbook.yml --ask-become-pass
```

**URL locale :** http://localhost:8082

> Remarque : le playbook intervient sur la configuration Nginx du système hôte. Sur un serveur déjà utilisé, il faut vérifier la configuration existante avant de remplacer des fichiers ou des sites par défaut.

---

## Orchestration avec Kubernetes

**Objectif :** déployer l'application web précédemment conteneurisée dans un cluster Kubernetes local à l'aide de Minikube.

Cet exercice permet de découvrir l'orchestration de conteneurs et les principaux objets Kubernetes : Namespace, Deployment, Pods et Service.

### Environnement utilisé

- Kubernetes : plateforme d'orchestration de conteneurs.
- Minikube : cluster Kubernetes local.
- kubectl : outil en ligne de commande pour communiquer avec le cluster.
- Docker Hub : registre hébergeant l'image de l'application.

L'application déployée utilise l'image :

`compotescassis/docker-devops:latest`

### Architecture du déploiement

Le fichier `kubernetes.yml` regroupe trois ressources Kubernetes.

**1. Namespace**

Un namespace nommé `devops` est créé afin d'isoler les ressources de cet exercice.

**2. Deployment**

Un Deployment nommé `helloworld` est créé dans le namespace `devops`.

Il définit :

- Le nombre de réplicas : 3.
- L'image Docker : `compotescassis/docker-devops:latest`.
- Le port du conteneur : 80.
- Le label applicatif : `app: helloworld`.

Kubernetes est chargé de maintenir le nombre de réplicas souhaité.

**3. Service**

Un Service nommé `helloworld-service` permet d'exposer l'application.

Il utilise :

- Le type `NodePort`.
- Le port du service : 80.
- Le port cible : 80.
- Le NodePort : 30080.
- Le sélecteur `app: helloworld` pour cibler les Pods du Deployment.

Le service permet ainsi d'accéder à l'application depuis l'extérieur du cluster Minikube.

### Travaux réalisés

- [x] Installer et utiliser kubectl.
- [x] Installer et démarrer Minikube.
- [x] Créer un namespace Kubernetes nommé `devops`.
- [x] Créer un Deployment nommé `helloworld`.
- [x] Définir trois réplicas pour l'application.
- [x] Utiliser l'image Docker publiée sur Docker Hub.
- [x] Créer un Service de type `NodePort`.
- [x] Exposer l'application sur le port `30080`.
- [x] Identifier et diagnostiquer une erreur `ErrImagePull` / `ImagePullBackOff`.
- [x] Configurer un secret Kubernetes pour l'authentification Docker Hub.
- [x] Associer le secret au ServiceAccount `default` du namespace `devops`.
- [x] Relancer le Deployment pour permettre le téléchargement de l'image.

### Gestion de l'authentification Docker Hub

Lors du premier déploiement, Kubernetes n'arrivait pas à télécharger l'image Docker.

L'erreur rencontrée était :

`ImagePullBackOff`

Le problème venait de l'authentification auprès de Docker Hub : le registre refusait le téléchargement de l'image.

Pour résoudre ce problème, un jeton d'accès Docker Hub avec la permission `Read-only` a été créé.

Un secret Kubernetes nommé `dockerhub-secret` a ensuite été configuré dans le namespace `devops`.

Exemple de création du secret :

```bash
kubectl create secret docker-registry dockerhub-secret \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username="$DOCKER_USER" \
  --docker-password="$DOCKER_TOKEN" \
  -n devops
```

Le secret est associé au ServiceAccount par défaut :

```bash
kubectl patch serviceaccount default \
  -n devops \
  -p '{"imagePullSecrets":[{"name":"dockerhub-secret"}]}'
```

Le Deployment est ensuite redémarré :

```bash
kubectl rollout restart deployment helloworld -n devops
```

Cette configuration permet aux Pods de s'authentifier auprès de Docker Hub pour récupérer l'image privée.

**Sécurité :** le jeton Docker Hub ne doit jamais être publié dans le dépôt GitHub ou directement écrit dans un fichier YAML versionné.

### Commandes Kubernetes utilisées

Vérifier l'état de Minikube :

```bash
minikube status
```

Démarrer Minikube :

```bash
minikube start
```

Appliquer le manifeste Kubernetes :

```bash
kubectl apply -f kubernetes.yml
```

Afficher les namespaces :

```bash
kubectl get namespaces
```

Afficher les Pods :

```bash
kubectl get pods -n devops
```

Afficher le Deployment :

```bash
kubectl get deployments -n devops
```

Afficher les Services :

```bash
kubectl get services -n devops
```

Afficher les détails du Deployment :

```bash
kubectl describe deployment helloworld -n devops
```

Vérifier le déploiement :

```bash
kubectl rollout status deployment helloworld -n devops
```

Accéder à l'application :

```bash
minikube service helloworld-service -n devops --url
```

Cette dernière commande fournit l'URL permettant d'accéder à l'application depuis le navigateur.

**Configuration réseau :**

| Élément | Valeur |
|---|---|
| Namespace | `devops` |
| Deployment | `helloworld` |
| Nombre de réplicas | 3 |
| Image Docker | `compotescassis/docker-devops:latest` |
| Service | `helloworld-service` |
| Type de service | `NodePort` |
| Port du conteneur | 80 |
| Port du service | 80 |
| NodePort | 30080 |
| Secret Docker Hub | `dockerhub-secret` |

---

## Vérification des déploiements

Les méthodes de déploiement utilisent des instances Nginx distinctes.

| Élément | Docker | Ansible |
|---|---|---|
| Serveur web | Nginx dans un conteneur | Nginx installé sur Ubuntu |
| Port hôte | `8081` | `8082` |
| Configuration | `Dockerfile` | `ansible/playbook.yml` |
| Adresse locale | http://localhost:8081 | http://localhost:8082 |
| Vérification | `curl -I` | `curl -I` |
| Résultat obtenu | HTTP 200 OK | HTTP 200 OK |

### Tests HTTP

Vérifier la réponse du conteneur Docker :

```bash
curl -I http://localhost:8081
```

Vérifier la réponse du serveur configuré par Ansible :

```bash
curl -I http://localhost:8082
```

Les deux commandes ont renvoyé **HTTP 200 OK**, confirmant que les deux serveurs web répondent correctement aux requêtes HTTP locales.

Pour Kubernetes, les vérifications portent notamment sur :

- La présence du namespace `devops`.
- Le fonctionnement du Deployment `helloworld`.
- La disponibilité des trois Pods.
- L'exposition de l'application par le Service `helloworld-service`.
- L'accès à la page web depuis le navigateur à l'aide de l'URL fournie par Minikube.

Pour GitHub Pages, la vérification consiste à consulter l'URL publique du site et à confirmer que le contenu HTML attendu s'affiche.

---

## Environnements DEV, VAL et PROD

Le TP aborde également les principes de séparation des environnements.

| Environnement | Rôle |
|---|---|
| **DEV — Développement** | Écrire le code, ajouter des fonctionnalités et corriger les erreurs. |
| **VAL — Validation** | Vérifier le fonctionnement et la conformité de l'application avant sa mise en production. |
| **PROD — Production** | Mettre l'application à disposition des utilisateurs dans un environnement stable et contrôlé. |

La progression DEV → VAL → PROD permet de limiter les risques en validant les modifications avant leur mise à disposition des utilisateurs.

Dans ce TP, les environnements DEV, VAL et PROD ont été étudiés à travers les exercices de pipelining et les principes de CI/CD. Nous n'avons pas mis en place trois environnements de déploiement complets.

Les déploiements Docker et Ansible sont exécutés sur la même machine Ubuntu, mais utilisent des instances Nginx distinctes. Kubernetes est utilisé avec un cluster local Minikube.

---

## Structure du projet

```text
DevOps/
├── .github/
│   └── workflows/
│       ├── hello-world.yml
│       ├── informations.yml
│       ├── python.yml
│       ├── branche.yml
│       ├── dev-val-prod.yml
│       └── docker-pages.yml
├── ansible/
│   ├── inventory.ini
│   └── playbook.yml
├── Dockerfile
├── .dockerignore
├── kubernetes.yml
└── README.md
```

Cette arborescence présente les principaux fichiers du projet. Le fichier `index.html` n'est plus conservé dans le dépôt : il est récupéré depuis l'image Docker publiée sur Docker Hub au moment du déploiement.

---

## Technologies utilisées

| Technologie | Utilisation |
|---|---|
| Git | Gestion des versions et historique du code |
| GitHub | Hébergement du dépôt distant |
| GitHub Actions | Automatisation des workflows CI/CD |
| YAML | Définition des workflows, playbooks et manifestes Kubernetes |
| Python | Exécution de scripts automatisés |
| HTML / CSS | Création de la page web statique |
| HTMLHint | Vérification de la qualité du HTML |
| GitHub Pages | Publication du site statique |
| Docker | Construction d'images et exécution de conteneurs |
| Docker Hub | Hébergement et distribution de l'image Docker |
| Nginx | Serveur web HTTP |
| Ansible | Automatisation de l'installation et de la configuration |
| Kubernetes | Orchestration des conteneurs |
| Minikube | Exécution d'un cluster Kubernetes local |
| kubectl | Administration et interaction avec Kubernetes |
| Ubuntu | Système hôte des déploiements locaux |
| curl | Vérification des réponses HTTP |

---

## Bilan du TP

Ce TP m'a permis de découvrir les principales étapes d'une démarche DevOps à travers une application web simple.

J'ai appris à :

- Gérer le code source et les modifications avec Git.
- Automatiser des tâches avec GitHub Actions.
- Organiser des workflows comportant plusieurs jobs et des conditions.
- Vérifier la qualité du HTML avant un déploiement.
- Construire une image Docker et exécuter un conteneur Nginx.
- Publier une image Docker sur Docker Hub.
- Extraire un fichier depuis un conteneur avec `docker cp`.
- Transmettre des fichiers entre plusieurs jobs avec les artefacts GitHub Actions.
- Automatiser le déploiement d'un site sur GitHub Pages.
- Diagnostiquer et corriger une erreur HTTP 403 liée aux permissions.
- Automatiser l'installation et la configuration de Nginx avec Ansible.
- Vérifier le fonctionnement des serveurs avec `curl` et les codes d'état HTTP.
- Comprendre la séparation des environnements DEV, VAL et PROD.
- Déployer une application dans un cluster Kubernetes local avec Minikube.
- Créer et gérer des namespaces, Deployments, Pods et Services.
- Configurer un secret Kubernetes pour permettre le téléchargement d'une image Docker privée.
- Exposer une application Kubernetes avec un Service de type NodePort.
- Diagnostiquer et résoudre un problème de récupération d'image Docker.

**Conclusion :** le DevOps ne consiste pas uniquement à écrire du code ou à lancer une application. Il repose également sur l'automatisation, la reproductibilité, les contrôles de qualité, la gestion des conteneurs, l'orchestration et la vérification du résultat final.

Ce projet constitue une première approche des pratiques CI/CD et des méthodes de déploiement utilisées dans des environnements professionnels.

---

<p align="center">
  <i>Travaux pratiques DevOps — Apprentissage de la CI/CD, de la conteneurisation, de l'orchestration et de l'automatisation des déploiements.</i>
</p>
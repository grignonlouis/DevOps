# DevOps — Travaux pratiques

<p align="center">
  <img src="https://img.shields.io/badge/DevOps-Training-blue?style=for-the-badge&logo=github" alt="DevOps Training">
  <img src="https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?style=for-the-badge&logo=githubactions" alt="GitHub Actions">
  <img src="https://img.shields.io/badge/Docker-Containers-2496ED?style=for-the-badge&logo=docker" alt="Docker">
  <img src="https://img.shields.io/badge/Ansible-Automation-EE0000?style=for-the-badge&logo=ansible" alt="Ansible">
  <img src="https://img.shields.io/badge/Status-In%20progress-orange?style=for-the-badge" alt="In progress">
</p>

Ce dépôt regroupe mes travaux pratiques de **DevOps**, réalisés dans le cadre du cours sur le pipelining, l'intégration continue et le déploiement d'applications.

L'objectif est de comprendre comment automatiser les différentes étapes du cycle de vie d'une application : gestion du code source, vérification de sa qualité, exécution de pipelines CI/CD, conteneurisation et configuration d'un serveur web.

Le projet s'appuie sur une application web statique affichant **Hello World !**, déployée localement de deux manières différentes : avec Docker et avec Ansible.

---

## Sommaire

- [Objectifs du cours](#objectifs-du-cours)
- [Exercices — Pipelining](#exercices--pipelining)
- [Exercice avancé — GitHub Pages et CI/CD](#exercice-avancé--github-pages-et-cicd)
- [Déploiement avec Docker](#déploiement-avec-docker)
- [Automatisation avec Ansible](#automatisation-avec-ansible)
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
- Automatiser l'installation et la configuration d'un serveur avec Ansible.
- Vérifier le fonctionnement d'un serveur web avec des requêtes HTTP.

---

## Exercices — Pipelining

### 1. Hello World

- [x] Créer un workflow qui affiche `Hello World`.

Workflow : [`hello-world.yml`](.github/workflows/hello-world.yml)

### 2. Informations utilisateur

- [x] Créer trois jobs pour afficher le nom, le prénom et l'adresse e-mail.
- [x] Utiliser les variables du dépôt GitHub plutôt que des valeurs codées en dur.

Workflow : [`informations.yml`](.github/workflows/informations.yml)

### 3. Exécution d'un script Python

- [x] Exécuter un script Python affichant `Commit success!`.
- [x] Déclencher automatiquement le workflow lors d'un push.

Workflow : [`python.yml`](.github/workflows/python.yml)

### 4. Gestion des branches

- [x] Afficher le nom de la branche sur laquelle le workflow s'exécute.
- [x] Manipuler les branches `Dev`, `Val` et `Prod`.
- [x] Comprendre le rôle des branches dans le processus de développement.

Workflow : [`branche.yml`](.github/workflows/branche.yml)

### 5. Pipeline conditionnelle Dev → Val → Prod

- [x] Diviser un nombre par 2 dans l'environnement Dev.
- [x] Transmettre le résultat à Val si la condition prévue est satisfaite.
- [x] Transmettre le résultat à Prod si les conditions sont remplies.
- [x] Interrompre la progression lorsque les conditions ne sont pas remplies.

Workflow : [`dev-val-prod.yml`](.github/workflows/dev-val-prod.yml)

---

## Exercice avancé — GitHub Pages et CI/CD

**Objectif :** automatiser la vérification et le déploiement d'une application web statique affichant `Hello World !`.

### Fonctionnement du workflow

Le workflow `deploy-pages.yml` organise les étapes suivantes :

1. **Récupération du code** : checkout du dépôt GitHub.
2. **Préparation de l'environnement** : configuration de Node.js pour utiliser les outils nécessaires.
3. **Vérification du HTML** : exécution de HTMLHint sur `index.html`.
4. **Préparation du site** : création d'un artefact contenant les fichiers à publier.
5. **Déploiement** : publication sur GitHub Pages lorsque les conditions et les permissions le permettent.

Le job de déploiement dépend de la réussite du job de vérification grâce à `needs: lint`. Une pull request peut ainsi déclencher les contrôles sans lancer le déploiement.

### Travaux réalisés

- [x] Créer la page HTML `index.html`.
- [x] Configurer un workflow GitHub Actions.
- [x] Ajouter une vérification automatique du HTML avec HTMLHint.
- [x] Configurer les étapes de préparation et de publication du site.
- [x] Identifier une restriction de publication liée à la configuration du dépôt privé et au forfait GitHub utilisé.
- [ ] Confirmer que le site est effectivement accessible à l'adresse publique.

**Application :** [Consulter le site Hello World](https://grignonlouis.github.io/DevOps/)

Workflow : [`deploy-pages.yml`](.github/workflows/deploy-pages.yml)

> **Remarque :** la configuration du workflow ne garantit pas à elle seule la publication du site. L'accès à GitHub Pages, les permissions du workflow et la configuration du dépôt doivent également être vérifiés.

---

## Déploiement avec Docker

**Objectif :** construire une image Docker contenant la page HTML et un serveur Nginx, puis exécuter l'application dans un conteneur.

### Principe

Le fichier `Dockerfile` définit la construction de l'image `hello-world-tp` à partir de Nginx sur Alpine Linux.

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

**URL locale :** [http://localhost:8081](http://localhost:8081)

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

**URL locale :** [http://localhost:8082](http://localhost:8082)

> **Remarque :** le playbook intervient sur la configuration Nginx du système hôte. Sur un serveur déjà utilisé, il faut vérifier la configuration existante avant de remplacer des fichiers ou des sites par défaut.

---

## Vérification des déploiements

Les deux méthodes de déploiement utilisent le même fichier `index.html`, mais exécutent deux instances distinctes de Nginx.

| Élément | Déploiement Docker | Déploiement Ansible |
|---|---|---|
| Serveur web | Nginx dans un conteneur | Nginx installé sur Ubuntu |
| Port hôte | `8081` | `8082` |
| Configuration | `Dockerfile` | `ansible/playbook.yml` |
| Adresse locale | `http://localhost:8081` | `http://localhost:8082` |
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

Les en-têtes HTTP ont également permis de constater que les deux instances utilisent des versions de Nginx différentes.

Ces tests valident les déploiements locaux, mais ne prouvent pas que GitHub Pages est accessible publiquement.

---

## Environnements DEV, VAL et PROD

Le TP aborde également les principes de séparation des environnements.

| Environnement | Rôle |
|---|---|
| **DEV** — Développement | Écrire le code, ajouter des fonctionnalités et corriger les erreurs. |
| **VAL** — Validation | Vérifier le fonctionnement et la conformité de l'application avant sa mise en production. |
| **PROD** — Production | Mettre l'application à disposition des utilisateurs dans un environnement stable et contrôlé. |

La progression DEV → VAL → PROD permet de limiter les risques en validant les modifications avant leur mise à disposition des utilisateurs.

Dans ce TP, les environnements DEV, VAL et PROD ont été étudiés à travers les exercices de pipelining et les principes de CI/CD. Nous n'avons pas mis en place trois environnements de déploiement complets.

Les déploiements Docker et Ansible sont exécutés sur la même machine Ubuntu, mais utilisent des instances Nginx distinctes.

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
│       └── deploy-pages.yml
├── ansible/
│   ├── inventory.ini
│   └── playbook.yml
├── index.html
├── Dockerfile
├── .dockerignore
└── README.md
```

Cette arborescence présente les principaux fichiers du projet. Elle peut évoluer en fonction des exercices ajoutés au dépôt.

---

## Technologies utilisées

| Technologie | Utilisation |
|---|---|
| Git | Gestion des versions et historique du code |
| GitHub | Hébergement du dépôt distant et collaboration |
| GitHub Actions | Automatisation des workflows |
| YAML | Définition des workflows et playbooks |
| Python | Exécution de scripts automatisés |
| HTML / CSS | Création de la page web statique |
| HTMLHint | Vérification de la qualité du HTML |
| GitHub Pages | Publication d'un site statique |
| Docker | Construction d'images et exécution de conteneurs |
| Nginx | Serveur web HTTP |
| Ansible | Automatisation de l'installation et de la configuration |
| Ubuntu | Système hôte des déploiements locaux |
| curl | Vérification des réponses HTTP |

---

## Bilan du TP

Ce TP m'a permis de découvrir les principales étapes d'une démarche DevOps à travers une application web simple.

J'ai appris à :

- gérer le code source et les modifications avec Git ;
- automatiser des tâches avec GitHub Actions ;
- organiser des workflows comportant plusieurs jobs et des conditions ;
- vérifier la qualité du HTML avant un déploiement ;
- construire une image Docker et exécuter un conteneur Nginx ;
- diagnostiquer et corriger une erreur HTTP 403 liée aux permissions ;
- automatiser l'installation et la configuration de Nginx avec Ansible ;
- vérifier le fonctionnement des serveurs avec `curl` et les codes d'état HTTP ;
- comprendre la séparation des environnements DEV, VAL et PROD.

**Conclusion :** le DevOps ne consiste pas uniquement à écrire du code ou à lancer une application. Il repose également sur l'automatisation, la reproductibilité, les contrôles de qualité et la vérification du résultat final.

Ce projet constitue une première approche des pratiques CI/CD et des méthodes de déploiement utilisées dans des environnements professionnels.

---

<p align="center">
  <i>Travaux pratiques DevOps — Apprentissage de la CI/CD, de la conteneurisation et de l'automatisation des déploiements.</i>
</p>
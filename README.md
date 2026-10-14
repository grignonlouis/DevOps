# DevOps — Travaux pratiques

<p align="center">
  <img src="https://img.shields.io/badge/DevOps-Training-blue?style=for-the-badge&logo=github" alt="DevOps Training">
  <img src="https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?style=for-the-badge&logo=githubactions" alt="GitHub Actions">
  <img src="https://img.shields.io/badge/Status-In%20progress-orange?style=for-the-badge" alt="In progress">
</p>

Ce dépôt regroupe mes travaux pratiques de **DevOps**, réalisés dans le cadre du cours sur le *pipelining*. L'objectif est de découvrir l'automatisation des tâches, les pipelines CI/CD et le déploiement continu avec GitHub Actions.

---

## Sommaire

- [Objectifs du cours](#-objectifs-du-cours)
- [Exercices — Pipelining](#-exercices--pipelining)
- [Exercice avancé — GitHub Pages](#-exercice-avancé--github-pages)
- [Technologies utilisées](#-technologies-utilisées)

---

## Objectifs du cours

- Comprendre le fonctionnement des pipelines d'intégration continue.
- Automatiser des tâches avec GitHub Actions.
- Manipuler les branches Git et les conditions d'exécution.
- Utiliser des variables et transmettre des résultats entre plusieurs jobs.
- Déployer une application web statique sur GitHub Pages.

## Exercices — Pipelining

### 1. Hello World

- [x] Créer une pipeline qui affiche `Hello World`.

Workflow : [`hello-world.yml`](.github/workflows/hello-world.yml)

### 2. Informations utilisateur

- [x] Créer trois jobs pour afficher le nom, le prénom et l'adresse e-mail.
- [x] Utiliser les variables du dépôt GitHub plutôt que des valeurs codées en dur.

Workflow : [`informations.yml`](.github/workflows/informations.yml)

### 3. Exécution d'un script Python

- [x] Exécuter un script Python affichant `Commit success!`.
- [x] Déclencher automatiquement la pipeline lors d'un push.

Workflow : [`python.yml`](.github/workflows/python.yml)

### 4. Gestion des branches

- [x] Afficher le nom de la branche dans laquelle la pipeline s'exécute.
- [x] Manipuler les branches `Dev`, `Val` et `Prod`.

Workflow : [`branche.yml`](.github/workflows/branche.yml)

### 5. Pipeline conditionnelle Dev → Val → Prod

- [x] Diviser un nombre par 2 dans l'environnement Dev.
- [x] Transmettre le résultat à l'environnement Val si celui-ci est pair.
- [x] Transmettre le résultat à Prod si la condition est satisfaite.
- [x] Arrêter la progression si les conditions ne sont pas remplies.

Workflow : [`dev-val-prod.yml`](.github/workflows/dev-val-prod.yml)

---

## Exercice avancé — GitHub Pages

**Objectif :** déployer automatiquement une application web statique affichant *Hello World*.

- [x] Créer une page HTML `index.html`.
- [x] Configurer un workflow GitHub Actions pour préparer les fichiers du site.
- [x] Déployer l'application avec GitHub Pages.
- [ ] Vérifier que le déploiement est accessible publiquement.

**Application :** [Consulter le site Hello World](https://grignonlouis.github.io/DevOps/)

Workflow : [`deploy-pages.yml`](.github/workflows/deploy-pages.yml)

---

## Technologies utilisées

| Technologie | Utilisation |
|---|---|
| Git & GitHub | Gestion du code source |
| GitHub Actions | Automatisation des pipelines |
| YAML | Définition des workflows |
| Python | Exécution de scripts automatisés |
| HTML / CSS | Création de la page web |
| GitHub Pages | Hébergement du site statique |

---

<p align="center">
  <i>Travaux pratiques DevOps — Apprentissage de la CI/CD et de l'automatisation.</i>
</p>
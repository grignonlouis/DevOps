# Documentation — Gestion du parc automobile (Mairie de Narbonne)

Documentation fonctionnelle et technique de l'application de gestion du parc automobile,
rédigée pour être lue par des agents de la DSI, sans prérequis en développement.

> Les diagrammes sont au format **Mermaid** : ils s'affichent directement dans la plupart
> des visionneuses Markdown (GitHub, GitLab, VS Code avec extension Mermaid, IntelliJ…).

## Sommaire

| # | Document | Contenu |
|---|---|---|
| 1 | [Présentation générale](01-presentation.md) | À quoi sert l'application, qui l'utilise, les grandes fonctionnalités. |
| 2 | [Architecture](02-architecture.md) | Construction en couches, principe « isoler ce qui change », diagrammes d'architecture et de modules. |
| 3 | [Modèle de données](03-modele-donnees.md) | Les entités, leurs liens (diagramme entité-association), cycles de vie. |
| 4 | [Sécurité et RGPD](04-securite-rgpd.md) | Authentification, double authentification, force brute, en-têtes HTTP, cookies, rôles, minimisation des données, protection des fichiers, dev/prod. |
| 5 | [Intégrations externes](05-integrations.md) | Active Directory, SMTP, Easy Connect ; état réel/simulé ; ports remplaçables. |
| 6 | [Exploitation](06-exploitation.md) | Lancement, profils, variables d'environnement, migrations SQL, stockage, sauvegardes. |

### Annexes sécurité

| Document | Contenu |
|---|---|
| [Sécurité — déploiement](securite-deploiement.md) | Mesures de sécurité à mettre en œuvre avec la DSI au déploiement (profil prod, HTTPS, LDAP, PostgreSQL, sauvegardes, scan CVE). |
| [Rapport d'audit de sécurité](rapport-securite.md) | Audit statique complet du dépôt (constats, risques, plan d'action). |

## Lecture conseillée

- **Vue rapide non technique** : documents 1 puis 4.
- **Compréhension d'ensemble** : 1 → 2 → 3.
- **Mise en service / exploitation** : 5 puis 6.

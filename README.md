# microservices-orchestration
Ce dépôt contiendra le fichier docker-compose.yml qui coordonne les deux services et une base de données MySQL.

## Docker Compose

Ce dépôt contient la configuration de l'orchestration des services via Docker Compose. Contrairement aux autres services (api-app et auth-app), ce dépôt n'utilise pas de workflow GitHub Actions.

## Services orchestrés
Le fichier docker-compose.yml orchestre les services suivants:
- auth-app: Service d'authentification
- api-app: API principale
- db: Base de données MySQL

## Note sur les workflows CI/CD
Pour consulter les workflows CI/CD qui construisent les images Docker utilisées par ce docker-compose:
- Voir le workflow de api-app: [api-app/.github/workflows/docker-build.yml](../api-app/.github/workflows/docker-build.yml)
- Voir le workflow de auth-app: [auth-app/.github/workflows/docker-build.yml](../auth-app/.github/workflows/docker-build.yml)

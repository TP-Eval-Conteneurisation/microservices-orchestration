
# Microservices Orchestration

Ce dépôt contient la configuration d'orchestration des microservices pour un projet basé sur une architecture microservices. L'application est divisée en deux services principaux : **auth-app** pour l'authentification, et **api-app** pour les fonctionnalités métier, avec une base de données **MySQL**.

## Architecture

L'architecture du projet est basée sur **Docker Compose** pour orchestrer les différents services :

- **auth-app** : Service d'authentification qui génère des tokens JWT.
- **api-app** : Service métier qui valide les tokens JWT et interagit avec la base de données.
- **db** : Base de données MySQL utilisée par **api-app** pour stocker les données.

## Prérequis

- Docker
- Docker Compose

## Configuration

### Variables d'Environnement

Les fichiers `.env` sont utilisés pour stocker les variables d'environnement nécessaires à la configuration des services.

#### Exemples de variables dans **auth-app** :
```env
JWT_SECRET=supersecretkey
```

#### Exemples de variables dans **api-app** :
```env
DB_HOST=db
DB_PORT=3306
DB_USER=user
DB_PASSWORD=password
DB_NAME=mydatabase
```

### Docker Compose

Ce projet utilise **Docker Compose** pour gérer l'orchestration des microservices. Il permet de construire, configurer et lancer tous les services en une seule commande.

#### Services :
- **auth-app** : Service d'authentification qui génère des tokens JWT.
- **api-app** : Service qui consomme les tokens JWT et interagit avec la base de données MySQL.
- **db** : Base de données MySQL.

## Installation

### 1. Clonez le dépôt
Clonez ce dépôt sur votre machine locale :

```bash
git clone https://github.com/username/microservices-orchestration.git
cd microservices-orchestration
```

### 2. Construisez et lancez les services avec Docker Compose

Construisez et démarrez tous les services avec Docker Compose :

```bash
docker-compose up --build
```

Cela va :

- Télécharger les images nécessaires
- Construire l'image pour chaque service s'il y a des modifications
- Lancer les services définis dans le fichier `docker-compose.yml`

### 3. Accédez aux services

- **auth-app** sera disponible sur `http://localhost:3001`.
- **api-app** sera disponible sur `http://localhost:3000`.
- **MySQL** sera accessible via `localhost:3306` pour toute interaction avec la base de données.

## Structure du Projet

```
/microservices-orchestration
│
├── docker-compose.yml          # Fichier d'orchestration Docker Compose
├── /auth-app                   # Code source du service d'authentification
├── /api-app                    # Code source du service métier
└── /db                         # Dockerfile et scripts SQL de la base de données (optionnel)
```

## Docker Compose

Le fichier `docker-compose.yml` contient la configuration suivante :

- **auth-app** : Service Node.js qui génère des tokens JWT.
- **api-app** : Service Node.js qui valide les tokens JWT.
- **db** : Service MySQL.

Exemple de service dans `docker-compose.yml` :

```yaml
version: '3.8'

services:
  auth-app:
    build: ./auth-app
    ports:
      - "3001:3001"
    env_file:
      - ./auth-app/.env
    depends_on:
      - db

  api-app:
    build: ./api-app
    ports:
      - "3000:3000"
    env_file:
      - ./api-app/.env
    depends_on:
      - db

  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mydatabase
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    ports:
      - "3306:3306"
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

## Contribution

Les contributions sont les bienvenues ! Si vous souhaitez contribuer à ce projet :

1. Forkez le dépôt
2. Créez une nouvelle branche (`git checkout -b feature/nouvelle-fonctionnalité`)
3. Faites vos changements et committez-les (`git commit -am 'Ajout de fonctionnalité'`)
4. Poussez la branche (`git push origin feature/nouvelle-fonctionnalité`)
5. Créez une pull request

## Licence

Ce projet est sous la licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

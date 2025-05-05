markdown
# TP Microservices avec REST, GraphQL, gRPC et Kafka

## 📝 Description
Ce projet implémente une architecture de microservices pour gérer des films et des séries TV. Il utilise :
- **gRPC** pour la communication synchrone entre microservices.
- **REST** et **GraphQL** via un API Gateway comme points d'entrée.
- **Kafka** pour la communication asynchrone entre les services.

## 🎯 Objectifs
- Créer deux microservices (`movie` et `tvShow`) avec gRPC.
- Mettre en place un API Gateway avec REST et GraphQL.
- Intégrer Kafka pour la gestion d'événements asynchrones.

## 🛠 Technologies utilisées
- Node.js
- Express.js
- Apollo Server (GraphQL)
- gRPC
- Kafka (avec KafkaJS)
- Protobuf

---

## ⚙️ Prérequis
- Node.js v18+
- Kafka et Zookeeper ([Télécharger Kafka](https://kafka.apache.org/downloads))
- npm ou yarn

---

## 🚀 Installation

### 1. Cloner le projet
```bash
git clone [URL_DU_DÉPÔT]
cd tp-microservices
2. Installer les dépendances
bash
npm install
3. Configurer Kafka
Démarrer Zookeeper et Kafka (suivre la documentation officielle).

Créer les topics Kafka :

bash
kafka-topics --create --topic movies_topic --bootstrap-server localhost:9092
kafka-topics --create --topic tvshows_topic --bootstrap-server localhost:9092
🏃 Exécution
1. Démarrer les microservices
Microservice Films :

bash
node movieMicroservice.js
Microservice Séries TV :

bash
node tvShowMicroservice.js
2. Démarrer l'API Gateway
bash
node apiGateway.js
📡 Endpoints
REST (API Gateway)
Films :

GET /movies : Lister tous les films.

GET /movies/:id : Obtenir un film par ID.

POST /movies : Créer un film (publie un événement Kafka).

Séries TV :

GET /tvshows : Lister toutes les séries TV.

GET /tvshows/:id : Obtenir une série par ID.

POST /tvshows : Créer une série (publie un événement Kafka).

GraphQL
Accéder à l'interface GraphQL via http://localhost:3000/graphql.

Exemple de requête :

graphql
query {
  movie(id: "1") {
    title
    description
  }
}
🧩 Structure des fichiers
movie.proto / tvShow.proto : Schémas Protobuf pour gRPC.

movieMicroservice.js / tvShowMicroservice.js : Implémentation des microservices.

apiGateway.js : Point d'entrée REST/GraphQL.

schema.js / resolvers.js : Configuration GraphQL.

Kafka :

Producteurs : Intégrés dans les endpoints POST.

Consommateurs : À implémenter dans les microservices (exemple fourni).

🔍 Tests
Requête REST (curl)
bash
curl http://localhost:3000/movies/1
Requête GraphQL
graphql
query {
  movies {
    id
    title
  }
}
🔄 Extension
Base de données : Remplacer les données mockées par une connexion à une base (MongoDB, PostgreSQL).

Kafka :

Ajouter des consommateurs pour synchroniser les données entre services.

Implémenter des retries et gestion d'erreurs.

🐛 Dépannage
Erreurs de port : Vérifier que les ports 50051, 50052 (gRPC) et 3000 (API Gateway) sont libres.

Kafka non démarré : Redémarrer Zookeeper et Kafka.

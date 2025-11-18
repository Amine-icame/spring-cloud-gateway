# Spring Cloud API Gateway

Ce projet est la passerelle API de notre architecture de microservices. Il agit comme un point d'entrée unique pour les clients externes, acheminant les requêtes vers les microservices appropriés. Il utilise Eureka pour découvrir les services et assure le load balancing.

## 🚀 Technologies Utilisées

-   **Spring Boot 3+**
-   **Spring Cloud Gateway**
-   **Spring Cloud Eureka Client** (pour la découverte de services)
-   **Spring Cloud Config Client** (pour la configuration centralisée)
-   **Spring Boot Actuator** (pour le monitoring)
-   **Maven**
-   **Java 17+**

## ⚙️ Comment le Lancer ?

1.  **Prérequis :**
    -   `spring-cloud-config-server` doit être lancé (sur `http://localhost:8888`).
    -   `spring-cloud-eureka-server` doit être lancé (sur `http://localhost:8761`).
    -   `microservice-commandes` et `microservice-produits` doivent être lancés et enregistrés auprès d'Eureka.

2.  **Lancement :**
    ```bash
    mvn spring-boot:run
    ```
    La Gateway sera accessible sur `http://localhost:8080` (port configuré via le Config Server).

## 💡 Configuration

Ce microservice récupère sa configuration (y compris la définition des routes) depuis le `spring-cloud-config-server` via le fichier `spring-cloud-gateway.properties` situé dans le dépôt `microservices-config-repo`.

### Routes Définies

-   **`/commandes/**` :** Toutes les requêtes correspondant à ce chemin sont routées vers le `microservice-commandes`.
    *Exemple :* `http://localhost:8080/commandes` est routé vers `http://MICROSERVICE-COMMANDES/commandes`
-   **`/produits/**` :** Toutes les requêtes correspondant à ce chemin sont routées vers le `microservice-produits`.
    *Exemple :* `http://localhost:8080/produits` est routé vers `http://MICROSERVICE-PRODUITS/produits`

## 🧪 Vérification

-   Accédez au tableau de bord Eureka (`http://localhost:8761`) pour confirmer que la Gateway est enregistrée.
-   Testez l'accès aux microservices via la Gateway :
    -   `http://localhost:8080/commandes`
    -   `http://localhost:8080/produits`
-   Vérifiez le load balancing en lançant plusieurs instances de `microservice-produits` et en observant les logs lors des appels via la Gateway à `http://localhost:8080/produits`.

## 📊 Monitoring

-   **Actuator Endpoints :** `http://localhost:8080/actuator` (inclut `health`, `info`)

---

*Développé par Amine Içame / Salma BenOmar pour le module JEE.*

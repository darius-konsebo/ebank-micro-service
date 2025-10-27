# Activité Pratique N°2 - Développement d'un Micro-service

## Introduction

Dans le cadre de cette activité pratique, nous avons pour objectif de développer un micro-service Spring Boot permettant de gérer des comptes bancaires. Ce travail s’inscrit dans l’apprentissage des architectures microservices, largement utilisées dans le développement d’applications modernes et distribuées.

L’application repose sur les technologies Spring Boot, Spring Data JPA, H2 Database, et Lombok, afin d’assurer une gestion efficace des données et une structure de code simplifiée. Elle met en œuvre une approche complète du développement d’un microservice, depuis la création de l’entité JPA et du dépôt de données jusqu’à l’exposition d’API RESTful documentées avec Swagger et d’un service GraphQL.

Cette activité permet ainsi de comprendre les étapes clés de la mise en place d’un microservice : la conception du modèle de données, l’implémentation de la couche d’accès aux données, la création des services métier et la publication d’interfaces de communication modernes (REST et GraphQL). Le tout sera testé à l’aide d’outils tels que Postman pour la vérification des endpoints et Swagger UI pour la documentation dynamique des API.

---

## I. Créer un projet Spring Boot avec les dépendances Web, Spring Data JPA, H2, Lombok

La première étape consiste à créer un **projet Spring Boot** en utilisant **Spring Initializr**. Lors de la configuration du projet, nous avons ajouté les dépendances suivantes :

- **Spring Web** pour le développement d’API REST,
- **Spring Data JPA** pour l’accès et la manipulation des données,
- **H2 Database** pour disposer d’une base de données embarquée en mémoire et faciliter les tests,
- **Lombok** pour simplifier le code en générant automatiquement les getters, setters et constructeurs.

Cette configuration initiale permet de disposer d’une base solide pour le développement du microservice et d’assurer une intégration fluide entre les différentes couches de l’application.

## II. Créer l'entité JPA Compte

Dans cette étape, nous avons créé la classe **`BankAccount`**, qui représente l’entité principale du microservice. Elle correspond à un **compte bancaire** et sera directement mappée à une table de la base de données grâce à **JPA (Java Persistence API)**.

Le fichier source de cette classe se trouve dans le répertoire `src/main/java/com/example/bankaccountservice/entities/BankAccount.java`.

Cette classe est annotée avec `@Entity` pour indiquer qu’il s’agit d’une entité JPA, et utilise **Lombok** pour réduire le code boilerplate grâce aux annotations `@Data`, `@NoArgsConstructor`, `@AllArgsConstructor` et `@Builder`.



Cette entité contient les principaux attributs d’un compte bancaire : **identifiant**, **date de création**, **solde**, **devise** et **type de compte** (courant ou épargne). Grâce à cette structure, elle servira de base à toutes les opérations de gestion des comptes dans le microservice.


## III. Créer l'interface CompteRepository basée sur Spring Data

Après avoir défini l’entité `BankAccount`, nous avons créé l’interface **`BankAccountRepository`**, qui représente la **couche d’accès aux données (DAO)** du microservice. Cette interface hérite de **`JpaRepository`**, ce qui permet de bénéficier automatiquement de toutes les méthodes CRUD (Create, Read, Update, Delete) sans avoir à les implémenter manuellement.

Le fichier est situé dans le répertoire `src/main/java/com/example/bankaccountservice/repositories/BankAccountRepository.java`

En étendant `JpaRepository<BankAccount, String>`, cette interface indique que le type d’entité géré est **`BankAccount`** et que son identifiant est de type **`String`**. Grâce à Spring Data JPA, cette couche DAO offre un accès simplifié et rapide à la base de données, tout en garantissant une abstraction du code SQL.

## IV. Tester la couche DAO

Afin de vérifier le bon fonctionnement de la couche d’accès aux données (**DAO**), nous avons implémenté un test simple dans la classe principale de l’application : **`BankAccountServiceApplication`**.
Ce test utilise un **`CommandLineRunner`**, qui s’exécute automatiquement au démarrage de l’application pour insérer plusieurs enregistrements dans la base de données **H2** en mémoire.

Concrètement, la méthode `start()` injecte le **`BankAccountRepository`**, puis crée plusieurs objets `BankAccount` avec des valeurs générées aléatoirement (identifiant unique, solde, type de compte, etc.) avant de les enregistrer dans la base via la méthode `save()`.

La configuration de la base de données est définie dans le fichier `application.properties` :

```
spring.datasource.url=jdbc:h2:mem:account-db
spring.h2.console.enabled=true
server.port=8081
```

L’utilisation de **H2** (base de données en mémoire) simplifie le test, car elle ne nécessite aucune installation ni configuration externe. De plus, la console H2, accessible via `http://localhost:8081/h2-console`, permet de visualiser les enregistrements créés.

Pour se connecter à la base entrer l'url `https//localhost:8081/h2-console` dans un navigateur. Dans le formulaire login entrer l'url donné à base de données dans `application.properties` :

![Image1](screenshots/login_H2.png)

Après la connexion cliquer sur la table `BANK_ACCOUNT` puis `run` pour voir les dinnées générées :

![Image2](screenshots/test_DAO.png)

Ainsi, cette étape confirme que la couche DAO fonctionne correctement et que la persistance des données via **Spring Data JPA** est pleinement opérationnelle.

## V. Créer le Web service Restfull qui permet de gérer des comptes

## VI. Tester le web micro-service en utilisant un client REST comme Postman

## VII. Générer et tester le documentation Swagger de des API Rest du Web service

## VIII. Exposer une API Restful en utilisant Spring Data Rest en exploitant des projections 

## IX. Créer les DTOs et Mappers

## X. Créer la couche Service (métier) et du micro service

## XI. Créer un Web service GraphQL pour ce Micro-service

---

## Conclusion

---

## Réalisé par :
- **Nom :** Wendbénédo Albéric Darius KONSEBO
- **Module :** Systèmes Distribués et Parallèles
- **Encadré par :** Pr. Mohamed YOUSSFI
- **Année académique :** 2025 - 2026
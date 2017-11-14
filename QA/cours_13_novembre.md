# Cours du 13 novembre

## Retour ARCH-2

Modèle hexagonal: Domaine au centre, avec une couche de protection autour(*anticorruption*). Autour du domaine, nous avons des **plugins**:

- Infrastructure
- Application
- UI

### Repository

Entrepôt. Sauvegarde et permet de récupérer des objets du domaine directement. N'est pas un DAO, car le DAO est un pattern de DAL pendant que Repository est un pattern de domaine. Le domaine impose le contrat!

Un repository n'est pas une factory. Une factory créé un nouvel objet pour la première fois, pendant que le repository ne fait qu'hydrater et déshydrater des objets du domaine.

### Assembler

DTO: Data Transfer Object. Permet de faire passer des données entre les couches.

L'*assembleur* permet de construire et de déconstruire des objets du domaine vers des DTO et inversement.

### CRUD vs Rich Domain

Mettre du DDD, des repositories, etc dans un domaine problème simple qui se prête au CRUD va causer une explosion de la complexité. DDD et repositories sont des patterns adaptés au Rich Domain mais pas aux applications CRUD.

À l'inverse, une application avec un domaine riche va gagner fortement à utiliser de tels patterns afin d'augmenter la maintenabilité du système malgré le haut niveau de complexité du problème.

**Attention**: Souvent, des applications CRUD subissent des change request qui augmente le nombre de règles d'affaires... Deviennent des applications de domaine riche, et les patterns doivent changer en conséquence (*Last responsible moment*)

Il y a un dégradé entre CRUD et Rich Domaine.

> La complexité commande des moyens tributaires du contexte.

Il faut toujours douter et prendre en compte le contexte avant de faire des décisions architecturales.

### Couche de services applicatifs

Cette couche existe en DDD. Son rôle? Sert à **ORCHESTRER**. Souvent, représente un use case, représentant les *contextes d'utilisation*.

Il n'y a pas de logique d'affaires, mais il y a de la logique applicative.
Exemples:

- Transactions BD
- Appels aux repositories
- Délégation de la déconstruction de DTOs (Assemblers)
- Délégation de la construction de DTOs (Assemblers)
- Etc.

Pour un remplir un use case, le service applicatif ne sait pas comment le remplir mais quoi faire et quand le faire => orchestration.

## Contenu de la remise 3 (individuelle)

On rajoute une story. Elle est **obligatoire**. Corriger les problèmes relevés lors de la deuxième remise. Ajouter une série de tests non unitaires, mais on nous donne quoi faire (quelles stories, quelles tests). On ne nous donne pas la portée du test cependant.

## Tests

Pyramide de la portée de Google: Large, Medium, Small.
**Small**: Une couple de classes.
**Medium**: Pas plus qu'une composante intégrée qui est testée.
**Large**: Deux composantes réelles de production se parlent ensemble, ou plus.

Cette pyramide n'est pas discrète, mais continue. Il s'agit d'un degradé.
La vaste majorité des tests automatisés devrait être des *small*. (70%)
Les autres devraient avoir, si on connait pas ça, 20% pour *medium* et 10% pour *large*.

Anti-pattern: Ice cream cone of tests.
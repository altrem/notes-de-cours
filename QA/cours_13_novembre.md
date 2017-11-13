# Cours du 13 novembre

## Retour ARCH-2

Modèle hexagonal: Domaine au centre, avec une couche de protection autour(*anticorruption*). Autour du domaine, nous avons des **plugins**:

- Infrastructure
- Application
- UI

### Repository

Entrepôt. Sauvegarde et permet de récupérer des objets du domaine directement. N'est pas un DAO, car le DAO est un pattern de DAL pendant que Repository est un pattern de domaine. Le domaine impose le contrat!

### Assembler

DTO: Data Transfer Object. Permet de faire passer des données entre les couches.

L'*assembleur* permet de construire et de déconstruire des objets du domaine vers des DTO et inversement.

### CRUD vs Rich Domain

Mettre du DDD, des repositories, etc dans un domaine problème simple qui se prête au CRUD va causer une explosion de la complexité. DDD et repositories sont des patterns adaptés au Rich Domain mais pas aux applications CRUD.

À l'inverse, une application avec un domaine riche va gagner fortement à utiliser de tels patterns afin d'augmenter la maintenabilité du système malgré le haut niveau de complexité du problème.

**Attention**: Souvent, des applications CRUD subissent des change request qui augmente le nombre de règles d'affaires... Deviennent des applications de domaine riche, et les patterns doivent changer en conséquence (*Last responsible moment*)
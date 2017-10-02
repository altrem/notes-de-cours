# Cours du 10 octobre

## Retour sur le dernier cours

### Mocks

Si on a trop de mocks:

- Tests fragiles
- Difficile à maintenir
- Le test est très conscient de la manière dont la méthode a été implémentée. Vu que je me suis trop inséré dans les dépendances (classes mockées), cela impactera le test.

**TL;DR**: Il faut mettre des mocks avec parcimonie:

- On ne mocke pas une structure de données
- Ne pas mocker des classes qui changent "au même rythme" que le test
- Ne pas mocker des classes concrètes, seulement des abstractions

## Tests unitaires

Un *test unitaire* devrait être:

- Isolé
- Ne pas communiquer avec
  - Système de fichiers
  - Bases de données
  - Interface utilisateur
- Ne pas traverser de couches
- Ne pas avoir de threading (pêché capital)

### Problèmes de tests dans la couche DAL

Il peut y avoir des problèmes impossibles à tester dans cette couche. Vu qu'on est pas sensé tester la connexion avec la BD, il est difficile de **tester le SQL exécuté**.

Stratégies pour tester cette partie:

- Fausse base de données (in-memory si possible, mais même implémentation SQL que la vraie)
- Utiliser un ORM au lieu d'écrire des requêtes SQL dans le code ( ? )

### Problèmes avec la couche UI

Pour la tester, on a plusieurs possibilités. En gros, il s'agit de le déconnecter du reste de l'application.

Dans un système Web moderne, il est possible que ce qui tourne dans le navigateur ne soit pas bindé solidement au reste de l'application: on utilise souvent un payload JSON avec un protocole REST, par exemple. On pourrait **simuler l'API REST** dans ce cas-ci.

### Autres

Plusieurs trucs doivent être abordés dans l'assurance qualité

- Bogues d'environnement
- Performance
- Etc.

## Tests d'acceptation

**Objectif**: Savoir que le système fait ce qu'il est supposé de faire en vertu des requis du client.


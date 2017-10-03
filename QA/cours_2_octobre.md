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

### Tests unitaires

Un *test unitaire* devrait être:

- Isolé
- Ne pas communiquer avec
  - Système de fichiers
  - Bases de données
  - Interface utilisateur
- Ne pas traverser de couches
- Ne pas avoir de threading (pêché capital)

#### Problèmes de tests dans la couche DAL

Il peut y avoir des problèmes impossibles à tester dans cette couche. Vu qu'on est pas sensé tester la connexion avec la BD, il est difficile de **tester le SQL exécuté**.

Stratégies pour tester cette partie:

- Fausse base de données (in-memory si possible, mais même implémentation SQL que la vraie)
- Utiliser un ORM au lieu d'écrire des requêtes SQL dans le code ( ? )

#### Problèmes avec la couche UI

Pour la tester, on a plusieurs possibilités. En gros, il s'agit de le déconnecter du reste de l'application.

Dans un système Web moderne, il est possible que ce qui tourne dans le navigateur ne soit pas bindé solidement au reste de l'application: on utilise souvent un payload JSON avec un protocole REST, par exemple. On pourrait **simuler l'API REST** dans ce cas-ci.

### Autres

Plusieurs trucs doivent être abordés dans l'assurance qualité

- Bogues d'environnement
- Performance
- Etc.

### Tests d'acceptation

**Objectif**: Savoir que le système fait ce qu'il est supposé de faire en vertu des requis du client.

## Clean coders: nous en tant que professionnels

Il y a des problèmes avec le paradigme actuel du développement logiciel.

- Peu d'imputabilité des développeurs pour les bogues
- Systèmes critiques ne sont pas aussi testés qu'il le faudrait...
- Sécurité informatique déficiente (IoT, etc.)

**TL;DR**: We don't know what we are doing.

L'économie est en transformation. L'intelligence artificielle est de plus en plus présente.

Certains économistes parle de l'*amazonification de l'économie*. Les cycles normaux d'emploi versus l'inflation, les profits et autres.

- Perte de pouvoir des travailleurs
- Les entreprises qui grandissent ne créent plus autant d'emplois.

Moins d'emploi? Moins de taxes! Concentration de l'économie.
C'est nous qui va contrôler le futur économique. Il nous faire preuve de plus de **responsabilité**.

### Logiciel

Tout va reposer sur du logiciel. Un logiciel repose sur des lignes de code. Il y a plus de LoC dans une voiture moyenne que sur Facebook (fun fact!)

Quelle est notre mission en tant que professionnels? On doit **assumer nos responsabilités**. Nos lignes de code peuvent tuer des gens et occasionner des pertes matérielles énormes. Dans les prochaines années, il faut aussi **faire vivre une expérience à vos utilisateurs**.

Selon Google, "Smart Creatives combine technical knowledge, business expertise and creativity.""

Il nous faut être:

- Innovant
- Ouvert d'esprit et au changement
- Curieux
- Créatifs
- Avoir un *savoir-être*

Dans une vie, on fait plus que 70 000 heures de travail. Autant avoir du fun...

Il nous faut nous *tenir à jour*. On devient plus niaiseux à chaque jour...

### Professionnalisme

Modèle de Brifus, un modèle d'apprentissage à 5 niveaux.

1. Débutant
1. Débutant avancé
1. Intermédiaire
1. Avancé
1. Expert

Au premier niveau, on cherche une **recette** vu qu'on ne comprend pas ce qu'on fait. Au second niveau, on a plein de recettes mais on n'a pas de compréhension intrinsèque de ce qu'on fait, on fait juste appliquer un algorithme. La majorité de la population mondiale ne franchira jamais ce niveau dans n'importe quelle capacité. Au niveau 3, on commence à avoir un modèle mental, une abstraction qui permet d'assimiler d'autres cas sans recettes. Au niveau 4, on est enfin capable de faire une boucle inspection-adaptation.

## Dette technique

Coût technique qui doit être payé à chaque fois qu'on veut maintenir ou étendre les fonctionnalités de l'application. Analogie des intérêts sur une carte de crédit.

**Refactoring**: Améliorer le code en gardant la même fonctionnalité.

Deux types de qualité:

- Qualité externe: Perçue par le client
- Qualité interne: Qualité du code

Pour atteindre l'excellence, il faut avoir les deux!


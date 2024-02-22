# Cassandra

- Base de données NoSQL open source pour un stockage rapide des données
- MongoDB se concentre sur la cohérence, tandis que Cassandra se concentre sur la haute disponibilité et l'évolutivité.
- Comment Cassandra assure-t-il un débit d'écriture élevé ? En ne prévoyant pas de lecture avant écriture par défaut


# Guide des Concepts Clés Cassandra

Apache Cassandra est une base de données NoSQL distribuée conçue pour gérer de grandes quantités de données avec une haute disponibilité sans point de défaillance unique. Voici les concepts essentiels à comprendre pour travailler efficacement avec Cassandra.

## 1. Clé-Partition

- **Description**: Identifiant unique pour une partition dans Cassandra, permettant une distribution efficace des données à travers les nœuds.
- **Exemple**: Une clé de partition basée sur `userId` pour une table d'utilisateurs.
- **Cas d'usage**: Requêtes efficaces par `userId`, distribution équilibrée des données.

## 2. Table (ou ColumnFamily)

- **Description**: Collection de données structurées où les lignes représentent des enregistrements et les colonnes des attributs de ces enregistrements.
- **Exemple**: Table `Utilisateurs` contenant `userId`, `nom`, `email`.
- **Cas d'usage**: Stockage structuré de données similaires.

## 3. Clé-Primaire

- **Description**: Unique identifiant pour chaque ligne dans une table, composée d'une clé de partition et éventuellement d'une ou plusieurs clés de clustering.
- **Exemple**: Clé primaire composée de `userId` (clé de partition) et `emailId` (clé de clustering).
- **Cas d'usage**: Unicité des enregistrements et requêtes efficaces.

## 4. Clé de Clustering

- **Description**: Utilisée avec la clé de partition pour définir l'ordre de tri des données au sein d'une partition.
- **Exemple**: `emailId` comme clé de clustering dans une table de messages.
- **Cas d'usage**: Tri des messages par `emailId` au sein d'une partition `userId`.

## 5. Modèle de Données Dénormaisé

- **Description**: Cassandra favorise un modèle de données où les données sont souvent dénormaisées pour optimiser les performances de lecture.
- **Exemple**: Stocker les adresses d'un utilisateur directement dans la table `Utilisateurs` plutôt que dans une table séparée.
- **Cas d'usage**: Réduire le nombre de requêtes pour lire des données relationnelles.

## 6. Réplication

- **Description**: Cassandra réplique automatiquement les données à travers plusieurs nœuds pour assurer la redondance et la fiabilité.
- **Exemple**: Stratégie de réplication avec un facteur de réplication de 3.
- **Cas d'usage**: Haute disponibilité et tolérance aux pannes.

## 7. Consistance

- **Description**: Niveau de garantie que lors d'une lecture, les données retournées reflètent le plus récent état écrit.
- **Exemple**: Consistance QUORUM pour les lectures et écritures.
- **Cas d'usage**: Équilibre entre performance et fiabilité des données.

## 8. Nœud

- **Description**: Instance individuelle de Cassandra exécutée sur une machine virtuelle ou physique.
- **Exemple**: Un cluster Cassandra composé de plusieurs nœuds répartis.
- **Cas d'usage**: Scalabilité et redondance des données.

## 9. Cluster

- **Description**: Ensemble de nœuds Cassandra travaillant ensemble pour servir les données et fournir des performances élevées.
- **Exemple**: Un cluster global réparti géographiquement.
- **Cas d'usage**: Haute disponibilité, reprise après sinistre.

## 10. Espace de Noms (Keyspace)

- **Description**: Plus haut niveau de conteneur de données dans Cassandra, similaire à une base de données dans les systèmes relationnels.
- **Exemple**: Keyspace `ApplicationWeb` contenant différentes tables.
- **Cas d'usage**: Isolation et gestion des données par application.

## 11. SSTable

- **Description**: Fichier sur disque qui stocke les données pour une table Cassandra de manière durable.
- **Exemple**: Plusieurs SSTables stockant les données de la table `Utilisateurs`.
- **Cas d'usage**: Persistance des données, compactions.

## 12. Mémoire Vive (Memtable)

- **Description**: Structure de données résidant en mémoire, où Cassandra écrit les enregistrements avant de les écrire sur disque dans des SSTables.
- **Exemple**: Memtable recevant les écritures en temps réel.
- **Cas d'usage**: Amortissement des écritures disque, réduction de la latence.

## 13. Compaction

- **Description**: Processus de fusion de plusieurs SSTables en un seul, optimisant l'espace disque et les performances de lecture.
- **Exemple**: Compaction déclenchée après un seuil d'SSTables atteint.
- **Cas d'usage**: Maintenance et optimisation du stockage.

## 14. Snitch

- **Description**: Composant configurant la topologie du cluster Cassandra et aidant à la stratégie de réplication des données.
- **Exemple**: Snitch définissant la topologie comme étant dans plusieurs datacenters.
- **Cas d'usage**: Configuration optimale de la réplication pour la tolérance aux pannes et la latence.

## 15. Stratégie de Réplication

- **Description**: Définit comment les copies des données sont réparties à travers le cluster.
- **Exemple**: Stratégie de réplication `NetworkTopologyStrategy` pour des déploiements multi-datacenters.
- **Cas d'usage**: Personnalisation de la réplication pour répondre aux besoins spécifiques de redondance et performance.

## 16. CQL (Cassandra Query Language)

- **Description**: Langage de requête pour interagir avec les données dans Cassandra, similaire en syntaxe au SQL.
- **Exemple**: `SELECT * FROM Utilisateurs WHERE userId = '123';`
- **Cas d'usage**: Requêtes de données, gestion de schéma.

## 17. Hinted Handoff

- **Description**: Mécanisme permettant à Cassandra de gérer temporairement les écritures destinées à un nœud en panne.
- **Exemple**: Stockage temporaire des écritures en attendant la remise en ligne du nœud destinataire.
- **Cas d'usage**: Amélioration de la fiabilité et de la disponibilité des écritures.

## 18. Gossip

- **Description**: Protocole de communication utilisé par Cassandra pour échanger des informations d'état entre les nœuds du cluster.
- **Exemple**: Échange d'informations sur la santé des nœuds et les métadonnées du schéma.
- **Cas d'usage**: Découverte et gestion de l'état du cluster.

## 19. Réparation (Repair)

- **Description**: Processus de synchronisation des données entre les nœuds pour assurer la consistance des répliques.
- **Exemple**: Exécution périodique de réparations pour corriger les divergences de données.
- **Cas d'usage**: Maintien de la consistance des données dans un environnement distribué.

## 20. Tunning de Performance

- **Description**: Ensemble de pratiques et configurations visant à optimiser les performances de Cassandra pour des charges de travail spécifiques.
- **Exemple**: Ajustement des paramètres de JVM, compaction, et configurations de cache.
- **Cas d'usage**: Amélioration des performances de lecture/écriture, réduction de la latence.

Ce guide offre une vue d'ensemble des fonctionnalités et concepts clés de Cassandra avec des exemples pratiques et des cas d'usage pour chacun. Il sert de référence rapide pour comprendre comment ces concepts s'appliquent dans des situations réelles.

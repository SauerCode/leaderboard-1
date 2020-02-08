# Leader Board

## Sommaire

| Sommaire | Valeur |
| --- | --- |
| Cours | CSI 2532 |
| Date | Winter 2020 |
| Professor | [Andrew Forward](aforward@uottawa.ca) |
| TA 1 | [Kyle Quintal](kquin039@uottawa.ca) |
| TA 2 | [Lintian Wang](lwang263@uottawa.ca) |
| Equipe | Andrew Forward 1484511<br>Ayana 9021000 |

## Livrables

* [Livrable 1 (5%) Hello-World](deliverable1.fr.md)

### Livrable 2 (5%) Application + DB

| Mark | Description | Commentaire |
| --- | --- | --- |
| 3.0 | Modèle ER | Voir ci-dessous |
| 3.0 | Modèle relationnel / schéma SQL | Les images ci-dessous, et [schema.sql](db/schema.sql) et [migrations](db/migrations) |
| 1.0 | Application (READ-ONLY) | Les instructions ci-dessous |
| 1.0 | SQL "seed" / exemples pour INSERT, UPDATE, SELECT, DELETE des données | Le [seed.sql](seed.sql) et les exemples ci-dessous |
| 1.0 | README.md contient toutes les informations requises | Voir _cette_ page |
| 1.0 | Utilisation de git (messages de commit, tous les étudiants impliqués) | Voir [les commits dans GitHub](https://github.com/aforward/leaderboard/commits/master) |
| / 10 | |


## Description de l'application

La base de données du leaderboard modéliser les athlètes (`athletes`), y compris
des détails tels que leur nom (`name`), leur date de naissance
(`date of birth`) et leur sexe (`gender`).

Le leaderboard inclus les `competitions`. Un compétition a un nom (`name`),
lieu (`venue`), les date (`start_date` et `end_date`).

Un `athlete` peut s'inscrire (`register`) à n'importe quelle compétition.

## Modèle ER

Le diagramme ER a été créé avec [Lucidchart](/lucidchart.md).

![Modèle ER](assets/ErModel.png)

## Modèle relationnel

Le modèle relationnel (diagramme) a également été créé avec [Lucidchart](/lucidchart.md).

![Modèle relationnel](assets/RelationalModel.png)

## Schéma SQL

Le [schèma SQL](db/schema.sql).

Il était testé avec [PostgreSQL](https://www.postgresql.org/).

Pour créer le base de donnée `leaderboard`, exécutez

```bash
psql -c "create database leaderboard"
```

Pour remplir le [schèma](db/schema.sql) pour le base de donnée, exécutez

```bash
psql -d leaderboard -f ./db/schema.sql
```

Si vous avez déjà une base de donnée, les migrations sont disponsible dans

```bash
db/migrations
```

Exécutez toutes les migrations (manquantes) en order de la date dans le
nom de fichier (e.x `YYYYMMDDhhmmss` of `20200205100000-create-athletes.sql`).

```sql
psql -d leaderboard -f ./db/migrations/20200205100000-create-athletes.sql
```

## Exemples de requêtes SQL

Pour remplir le base de donnée avec le (seed.sql)

```bash
psql -d leaderboard -f ./db/seed.sql
```

Maintenant on peut tester, on va utiliser le console PostgreSQL.

```bash
psql -d leaderboard
```

Trouvez tous les athlètes «F»

```sql
SELECT *
FROM athletes
WHERE identified_gender = 'F';
```

Mettez à jour tous les «m» à «M».

```sql
UPDATE athletes
SET identified_gender = 'M'
WHERE identified_gender = 'm';
```

Et maintenant, tous les athlètes «M»

```sql
SELECT *
FROM athletes
WHERE identified_gender = 'M';
```

Supprimons tous les athlètes.

```sql
DELETE FROM athletes;
```

Et maintenant c'est vide.

```sql
SELECT count(*)
FROM athletes;
```
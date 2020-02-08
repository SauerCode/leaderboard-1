# Leader Board

## Outline

| Outline | Value |
| --- | --- |
| Course | CSI 2532 |
| Date | Winter 2020 |
| Professor | [Andrew Forward](aforward@uottawa.ca) |
| TA 1 | [Kyle Quintal](kquin039@uottawa.ca) |
| TA 2 | [Lintian Wang](lwang263@uottawa.ca) |
| Team | Andrew Forward 1484511<br>Ayana 9021000 |

## Deliverables

* [Deliverable 1 (5%) Hello World](deliverable1.md)

### Deliverable 2 (5%) DB Backed Application

| Mark | Description | Comment |
| --- | --- | --- |
| 3.0 | ER model  | See below |
| 3.0 | Relational model / SQL schema | Les images ci-dessous Image below, et [schema.sql](db/schema.sql) |
| 1.0 | Application (read-only) | Instructions below |
| 1.0 | SQL seed / examples to INSERT, UPDATE, SELECT and DELETE data | See below and seed.sql (link to come) |
| 1.0 | README.md contains all required information | See _this_ page |
| 1.0 | Git usage (commit messages, all students involved) | See [commit details in GitHub](https://github.com/aforward/leaderboard/commits/master)
| / 10 | |


## Application Description

The leaderboard database models an `athletes`, including
details such as their `name`, `date of birth`, and identified `gender`.

The leaderboard tracks `competitions`.  A competition has a `name`,
`venue`, a `start_date` and a `end_date`.

An `athlete` can `register` for any competition.


## ER Model

The ER diagram was created with [Lucidchart](/lucidchart.md).

![ER Model](assets/ErModel.png)

## Relational Model

The Relational Model (diagram) was also created with [Lucidchart](/lucidchart.md).

![ER Model](assets/RelationalModel.png)

## SQL Schema

The [SQL Schema is available here](db/schema.sql).

It was tested using [PostgreSQL](https://www.postgresql.org/).

To create the `leaderboard` database run

```bash
psql -c "create database leaderboard"
```

To create the schema run

```bash
psql -d leaderboard -f ./db/schema.sql
```

If you already have a database, the migrations are available in

```bash
db/migrations
```

Run any (missing) migrations based on the timestamp date in the
filename (i.e. `YYYYMMDDhhmmss` of `20200205100000-create-athletes.sql`).

```sql
psql -d leaderboard -f ./db/migrations/20200205100000-create-athletes.sql
```

## Example SQL Queries

To populate to database [run this SEED file](db/seed.sql).

```bash
psql -d leaderboard -f ./db/seed.sql
```

Now we can test out our databse in the postgres console.

```bash
psql -d leaderboard
```

Let's find all 'F' athletes.

```sql
SELECT *
FROM athletes
WHERE gender = 'F';
```

Let's update all 'm's to 'M's.

```sql
UPDATE athletes
SET gender = 'M'
WHERE gender = 'm';
```

And now all 'M' athletes.

```sql
SELECT *
FROM athletes
WHERE gender = 'M';
```

Let's delete all athletes.

```sql
DELETE FROM athletes;
```

And now the table is empty.

```sql
SELECT count(*)
FROM athletes;
```
$ = bash
> = psql

$ createdb mydb
$ psql mydb
$ dropdb mydb

-- Testa att det funkar
> SELECT version();
> SELECT current_date;
> SELECT 2 + 2;

-- Lista användare
> \du

-- Lista databaser
> \l

Lista relationer (tabeller?) i nuvarande databas:
> \d

-- Läs kommandon från en .sql-fil
> \i [FILNAMN]

-- Byt databas
> \c [NAMN]

-- Skapa tabell
CREATE TABLE friends (
  name varchar(80),
  age int
);

CREATE TABLE gamedevs (
  devname varchar(80),
  country varchar(80)
);

-- Ta bort tabell
DROP TABLE [NAMN];

-- Fyll tabell med värden
INSERT INTO friends VALUES ('Johannes', 27);
INSERT INTO friends (age, name) VALUES (29, 'Jonas');

COPY friends FROM '/file.txt';

-- Fråga efter saker
SELECT * FROM friends;
SELECT name FROM friends;
SELECT age, name FROM friends;
SELECT name, age * 10 AS big_age FROM friends;
SELECT name FROM friends WHERE age < 28;
SELECT name, age FROM friends ORDER BY age;
SELECT DISTINCT age FROM friends ORDER BY age;

-- Joins (lägg ihop eller jämför tabeller)
SELECT * FROM friends, gamedevs WHERE name = devname;
SELECT name, age, country FROM friends, gamedevs WHERE name = devname;

-- Kvalificerade namn (rekommenderat, kan ha samma namn i flera tabeller då)
SELECT friends.name, friends.age, gamedevs.country
FROM friends, gamedevs
WHERE friends.name = gamedevs.devname;

-- Inner join (ger samma resultat som ovan)
SELECT * FROM friends INNER JOIN gamedevs ON (friends.name = gamedevs.devname);

-- Left outer join (tar med alla rader i den vänstra/första tabellen)
SELECT * FROM friends LEFT OUTER JOIN gamedevs ON (friends.name = gamedevs.devname);

-- Self join (jämför fält mot sig själv, här hittar jag personer med samma namn som sitt land)
SELECT * FROM gamedevs g1, gamedevs g2 WHERE g1.devname = g2.country;

-- Aggregatfunktioner
SELECT max(age) FROM friends;

-- Ta bort rad
DELETE FROM friends WHERE name = 'Erik';

-- Ändra på värde
UPDATE friends SET name = 'Eirich' WHERE age = 30;

-- Textsökning, hitta alla med namn som innehåller 'sson'
SELECT * FROM friends WHERE strpos(name, 'sson') > 0;

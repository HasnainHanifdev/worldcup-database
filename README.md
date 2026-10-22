# World Cup Database

A PostgreSQL database of every knockout-stage game (Eighth-Final through Final) from the 2014 and 2018 FIFA World Cups. Built as part of the freeCodeCamp Relational Database certification.

## What it does

- Stores 24 unique teams and 32 games in two linked tables.
- Loads all data from `games.csv` with a Bash script (no hard-coded IDs).
- Answers 12 questions about the data with SQL queries.

## Database structure

    teams                          games
    -----                          -----
    team_id  SERIAL PRIMARY KEY    game_id         SERIAL PRIMARY KEY
    name     VARCHAR UNIQUE        year            INT
                                   round           VARCHAR
                                   winner_id       INT -> teams(team_id)
                                   opponent_id     INT -> teams(team_id)
                                   winner_goals    INT
                                   opponent_goals  INT

All columns are `NOT NULL`.

## Files

| File | Purpose |
|---|---|
| `games.csv` | Source data: year, round, winner, opponent, goals |
| `insert_data.sh` | Reads `games.csv` and fills the `teams` and `games` tables |
| `queries.sh` | Runs 12 queries (totals, averages, joins, UNION, DISTINCT, LIKE) |
| `worldcup.sql` | Full database dump, to rebuild everything |

## How to run

Rebuild from the dump:

    psql -U postgres < worldcup.sql

Or load the data again and run the queries:

    chmod +x insert_data.sh queries.sh
    ./insert_data.sh
    ./queries.sh

## Concepts used

- Primary keys, foreign keys, UNIQUE and NOT NULL constraints
- Bash while-read loops with IFS
- INSERT ... ON CONFLICT DO NOTHING and subqueries to look up IDs
- Aggregates: SUM, AVG, ROUND, MAX, COUNT
- INNER JOIN, UNION, DISTINCT, LIKE, ORDER BY

## Tools

PostgreSQL, Bash, Git

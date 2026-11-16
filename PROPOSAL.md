# Project proposal

* Name: Armand VIEAU
* Project title: Board Game Shelf
* Pitch: A public catalogue of my board game collection where friends can browse games, read a short rules summary, and record play sessions with scores and winners.
* Target users: Board game players and friend groups who want to track what they own, what they played and who won.

## Pages

| URL | Content | Dynamic segment? | Rendering strategy and why |
|---|---|---|---|
| / | Home page: presentation of the collection, latest games added and latest play sessions | No | ISR (`revalidate`): public page, SEO matters, content changes only when a game or session is added |
| /games | Full catalogue of games (title, number of players, duration, cover) | No | ISR (`revalidate`): public catalogue, good for SEO, updated a few times a week at most |
| /games/[slug] | Detail of one game: description, rules summary, players, duration, plus its list of play sessions and stats (times played, last winner) | Yes, `[slug]` | SSG with `generateStaticParams` plus `revalidate`: public SEO page with a fixed URL per game, regenerated when sessions are added |
| /games/new | Form to add a new game to the collection | No | Dynamic: page with a form that writes data (the form itself is a Client Component) |
| /games/[slug]/sessions/new | Form to record a play session for a game (date, players, winner, notes) | Yes, `[slug]` | Dynamic (`force-dynamic`): depends on the game and writes data, no SEO value |
| /about | What the app is and how to use it | No | Static (SSG): content never changes |

## Data

Entities (2 to 4), their main fields, and how they are related:

* **Game**: id, slug, title, description, rulesSummary, minPlayers, maxPlayers, minutes, year, createdAt
* **PlaySession**: id, gameId, playedAt, players (text, comma separated), winner, notes, createdAt
* Relation: one Game has many PlaySessions; one PlaySession belongs to one Game (one-to-many, foreign key `gameId`).

## Write actions

What users can create, update or delete:

* Create a game (`POST /api/games`)
* Record a play session for a game (`POST /api/games/[slug]/sessions`)
* Edit a game's information
* Delete a play session (in case of a mistake)

## Repository

GitHub URL: https://github.com/AlTAR333/<your-repository>

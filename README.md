# borgo-wine-feed

Aktuální vinný lístek restaurace [Borgo Agnese](https://www.borgoagnese.cz) (Brno) ve strojové podobě
pro tablety s aplikací **Borgo Agnese – vinný lístek**.

Jediný soubor, který tu něco znamená, je `wines.json`. **Needitovat ručně** – přepíše ho
automat (GitHub Actions v repozitáři s kódem aplikace), který 3× denně:

1. stáhne aktuální PDF karty z webu restaurace,
2. rozparsuje ji a zkontroluje kvalitu (počet vín, ceny, výrobci, shoda s minulou kartou),
3. když karta projde, commitne sem nový `wines.json`; když ne, nechá poslední dobrou verzi.

Tablety čtou
`https://raw.githubusercontent.com/NexusSync-Systems/borgo-wine-feed/main/wines.json`
a novou kartu si vezmou do několika hodin.

## Formát

```json
{
  "schema": 1,
  "feed_id": "<sha PDF>-<otisk parseru>",
  "generated_at": "2026-09-25T17:07:25+00:00",
  "categories": [ { "name": "…", "countries": [ { "name": "…", "regions": [ { "name": "…", "wines": [ … ] } ] } ] } ]
}
```

Tablet načte novou kartu jen při změně `feed_id`.

## Ruční oprava

Potřebujete-li kartu opravit hned, nahrajte opravený `wines.json` (s jiným `feed_id`) jako
sdílený soubor na Google Disk – ten má před tímto repem přednost. Postup je v `docs/feed-setup.md`
v repozitáři aplikace.

Provozuje NexusSync Systems s.r.o. · kontakt@nexusstack.eu

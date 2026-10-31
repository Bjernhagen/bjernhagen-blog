# bjernhagen.se

Personlig blogg byggd med [Hugo](https://gohugo.io/), med kategorierna **Resor**, **Tankar** och **Projekt**. Lila gradient-design, vita inläggskort, RSS-feed och redo för deployment på Netlify.

## Innehåll

- [Kom igång lokalt](#kom-igång-lokalt)
- [Lägga till ett nytt inlägg](#lägga-till-ett-nytt-inlägg)
- [Skriva från projektet Funderingar](#skriva-från-projektet-funderingar)
- [Frontmatter-fält](#frontmatter-fält)
- [Hero-bilder](#hero-bilder)
- [Videor](#videor)
- [Kategorisidor och arkiv](#kategorisidor-och-arkiv)
- [RSS-feed](#rss-feed)
- [Mappstruktur](#mappstruktur)
- [Deploy till Netlify](#deploy-till-netlify)

## Kom igång lokalt

1. Installera Hugo (extended-versionen), t.ex. via winget:

   ```bash
   winget install --id Hugo.Hugo.Extended -e
   ```

2. Starta utvecklingsservern från projektmappen:

   ```bash
   hugo server -D
   ```

3. Öppna [http://localhost:1313](http://localhost:1313) i webbläsaren. Sidan uppdateras automatiskt när du sparar ändringar.

## Lägga till ett nytt inlägg

Varje inlägg är en Markdown-fil i en av de tre kategorimapparna:

```
content/resor/     → Resor
content/tankar/     → Tankar
content/projekt/    → Projekt
```

Enklast är att använda Hugos `new`-kommando, som skapar filen med rätt frontmatter-mall automatiskt:

```bash
hugo new resor/min-nya-resa.md
hugo new tankar/en-ny-tanke.md
hugo new projekt/mitt-nya-projekt.md
```

Öppna sedan den skapade filen, fyll i innehåll och sätt `draft: false` när inlägget är klart att publiceras.

## Skriva från projektet Funderingar

Inläggen kan skrivas i Claude-projektet **Funderingar** och publiceras härifrån:

1. Skriv klart inlägget i projektet och be om en Markdown-fil med frontmatter (instruktionen nedan ligger i projektets instruktioner).
2. Spara filen, t.ex. i Hämtade filer.
3. Be Claude Code i den här mappen: *"Lägg in `filnamn.md` under Tankar"* (eller Resor/Projekt). Filen läggs in i rätt kategorimapp, sidan byggs för kontroll och publiceras (push till GitHub) först när du säger till.
4. Har du en bild, ange filen så komprimeras den och läggs i `static/images/`. Saknas bild kan en stiliserad SVG skapas.

Den kategori du anger när du ber om publicering styr vilken mapp filen hamnar i. Datumet i frontmatter styr sorteringen, så sätt ett äldre datum för ett äldre minne.

Instruktion att klistra in i projektet Funderingar:

```
När jag ber dig skriva klart ett blogginlägg: leverera en Markdown-fil på svenska med exakt denna frontmatter:

---
title: "Rubrik"
date: ÅÅÅÅ-MM-DD
category: "Tankar"   # Resor, Tankar eller Projekt
hero: ""             # lämna tomt om bild saknas
description: "En mening som sammanfattar inlägget"
draft: false
---

Brödtexten i Markdown. Upprepa inte rubriken i texten (titeln visas automatiskt).
Använd ## för mellanrubriker. Filnamnet ska vara en kort slug utan å, ä, ö,
till exempel skumgummimadrasserna.md.
```

## Frontmatter-fält

Varje inlägg börjar med ett metadata-block (frontmatter) mellan `---`:

```yaml
---
title: "Min nya resa"
date: 2026-07-22
category: "Resor"
hero: "/images/min-bild.jpg"
description: "Kort sammanfattning som visas i inläggskort och i sökmotorer."
draft: false
---
```

| Fält          | Beskrivning                                                                 |
|---------------|------------------------------------------------------------------------------|
| `title`       | Rubriken på inlägget                                                        |
| `date`        | Publiceringsdatum (styr sorteringen på start-, kategori- och arkivsidan)    |
| `category`    | Visningsnamn för kategorin (bör matcha mappen: Resor, Tankar eller Projekt) |
| `hero`        | Sökväg till hero-bilden, t.ex. `/images/min-bild.jpg`                       |
| `description` | Kort textrad som visas i kort och i `<meta description>`                   |
| `draft`       | `true` döljer inlägget från publicerad sajt, `false` publicerar det         |

## Hero-bilder

Lägg bildfiler i `static/images/` och referera till dem i frontmatter som `/images/filnamn.jpg`. Bilderna visas som stort hero-foto överst på inlägget och som utsnitt i inläggskorten. Exempel-inläggen använder genererade SVG-bilder — byt gärna ut dem mot egna foton.

## Videor

Ladda upp videon till YouTube eller Vimeo (kan vara **"Olistad"** på YouTube om du inte vill att den ska synas i sökningar — bara den med länken hittar den) och bädda in den var som helst i inläggstexten:

```
{{< youtube VIDEO-ID >}}
```

`VIDEO-ID` är delen efter `v=` i YouTube-länken, t.ex. `dQw4w9WgXcQ` från `youtube.com/watch?v=dQw4w9WgXcQ`.

För Vimeo används samma sätt: `{{< vimeo VIDEO-ID >}}`.

Ladda inte upp videofiler direkt i projektet — de blir för stora för Git och Netlifys gratisgränser. YouTube/Vimeo sköter streaming och komprimering gratis.

## Kategorisidor och arkiv

- Varje kategori har en egen sida: `/resor/`, `/tankar/` och `/projekt/` — dessa listar automatiskt alla inlägg i respektive mapp, nyast först.
- `/arkiv/` visar samtliga inlägg från alla kategorier, grupperade per år.
- Startsidan visar de senaste inläggen från alla kategorier i ett gemensamt flöde.

## RSS-feed

Hugo genererar RSS-feeds automatiskt:

- Hela sajten: `/index.xml`
- Per kategori: `/resor/index.xml`, `/tankar/index.xml`, `/projekt/index.xml`

Länk till RSS-feeden finns i sajtens header och footer.

## Mappstruktur

```
.
├── archetypes/          Mall som används av "hugo new"
├── content/
│   ├── resor/            Inlägg i kategorin Resor
│   ├── tankar/            Inlägg i kategorin Tankar
│   ├── projekt/           Inlägg i kategorin Projekt
│   └── arkiv/_index.md   Arkivsidan
├── layouts/               HTML-mallar (header, footer, listor, enskilda inlägg m.m.)
├── static/
│   ├── css/style.css     Design (lila gradient, vita kort)
│   └── images/            Hero-bilder
├── hugo.toml              Sajtens konfiguration
└── netlify.toml            Deploy-inställningar för Netlify
```

## Deploy till Netlify

1. Pusha projektet till ett Git-repo (GitHub, GitLab eller Bitbucket).
2. Skapa en ny site i Netlify och koppla den till repot. `netlify.toml` innehåller redan byggkommandot (`hugo --gc --minify`) och publiceringsmappen (`public`), så inga extra inställningar behövs.
3. Under **Site settings → Domain management** i Netlify, lägg till den egna domänen `bjernhagen.se` och följ instruktionerna för att peka domänens DNS mot Netlify (antingen genom att flytta DNS till Netlify eller genom att lägga till en `CNAME`/`A`-post hos din nuvarande DNS-leverantör).
4. Netlify utfärdar automatiskt ett gratis SSL-certifikat för domänen när DNS är verifierad.

Varje gång du pushar ändringar till huvudgrenen bygger Netlify om och publicerar sajten automatiskt.

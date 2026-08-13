---
title: "Så byggde jag den här bloggen med Hugo"
date: 2026-07-20
category: "Projekt"
hero: "/images/projekt-hugoblogg.svg"
description: "En snabb genomgång av hur bjernhagen.se är uppbyggd — från Hugo-mallar till deployment på Netlify."
draft: false
---

Efter att ha testat några olika bloggplattformar landade jag till slut i Hugo. Snabbt, enkelt och inga databaser att hålla reda på.

## Varför Hugo?

Jag ville ha något som:

- Bygger sidor blixtsnabbt
- Låter mig skriva inlägg i Markdown
- Är enkelt att versionshantera med Git
- Kan deployas gratis på Netlify

## Struktur

Bloggen har tre kategorier — **Resor**, **Tankar** och **Projekt** — som var sin egen sektion i innehållsmappen. Varje inlägg är en Markdown-fil med metadata i toppen (titel, datum, kategori och en hero-bild).

## Design

Jag ville att bloggen skulle kännas varm och personlig, så jag valde en lila gradient som bakgrund och vita, lite svävande kort för varje inlägg. Enkelt, men med lite färg.

## Deployment

Sista steget var att koppla ihop projektet med Netlify och peka den egna domänen `bjernhagen.se` dit. Varje gång jag pushar ett nytt inlägg till Git byggs sidan om automatiskt.

Nästa steg blir att lägga till fler inlägg — och kanske en sökfunktion, om jag orkar.

# LærbarXR — Builder

Værktøj i browseren til at bygge 360°-simulationer til undervisning. Åbn `index.html` i en moderne browser; der er intet at installere og intet build-trin.

LærbarXR består af tre repos:

- **LaerbarXR-Builder** (dette repo): byg en simulation og eksportér den som `.zip`
- [LaerbarXR-Player](https://github.com/MoHaulik/LaerbarXR-Player): afspil den på Quest 3 eller i en browser
- [LaerbarXR-Dashboard](https://github.com/MoHaulik/LaerbarXR-Dashboard): start og følg klassen live, saml resultater

Udgivet på https://mohaulik.github.io/LaerbarXR-Builder/ (GitHub Pages fra `main`).

## Kom i gang

1. Åbn `index.html`.
2. **+ Add Video Node**, upload 360°-video eller billeder under **Assets**, og tilføj tekst, billeder og spørgsmål.
3. Tryk **Preview** for at afprøve forløbet. Preview er Players egen side indlejret i en iframe, så den viser det samme som headsettet. Player skal derfor ligge i mappen ved siden af (eller på samme GitHub Pages-domæne).
4. Eksportér med **Export WebXR Player Package (.zip)** og indlæs filen i Player og i Dashboardet (**Vælg simulation**).

Et projekt kan gemmes og åbnes igen som `.lxr`. Der ligger et eksempel i `demo-scenarios/` og eksempelmedier i `realmedia/`.

## Funktioner

- Scener med 360°/180°-video eller billede, forbundet i et forløb med forgreninger.
- Tekst, billeder og spørgsmål placeret på hele kuglen (X/Y i procent), med tidsstyring (start og varighed) og formatering (størrelse, farver, justering).
- Op til 20 svarmuligheder pr. spørgsmål. Player lægger dem i et gitter.
- **Startretning** pr. scene (hvilken vej eleven ser, når scenen starter).
- **Kigge-tid** pr. scene (standard 2,0 s).
- **Svartype "Flere rigtige"**: eleven krydser alle rigtige svar af og trykker Bekræft. Eleven får ikke at vide, hvor mange der er rigtige, medmindre *Fortæl eleven hvor mange der er rigtige* er slået til.
- **↻ Se igen** pr. scene: knap i VR der starter scenens video forfra.
- **Markering i Dashboard**: grøn (rigtigt udfald) eller rød (forkert) på scenen, også på lærerens livekort.
- **Simulation-indstillinger**: vis/skjul Afslut-knappen, og udeluk headsets der har ligget stille i N sekunder (0 = fra, nye simulationer starter på 60).
- Autogem i browseren og fortryd.

## Filformat

Den eksporterede `.zip` indeholder `project.json` samt mapperne `videos/` og `images/`. Den samme pakke læses af både Player og Dashboard.

Vigtige felter i `project.json`:

- Projekt: `title`, `startNode`, `coordSpace` (`sphere360`; projekter uden feltet er lavet i det gamle flade system og konverteres, når de åbnes her), `hideExit`, `idleTimeoutSec`.
- Scene: `videoYaw`, `question`, `choices`, `questionMode` (`multi` for flervalg), `multiShowCount`, `replayEnabled`, `replayTime`, `sceneColor`, `defaultNext`.

Alle nyere felter er valgfrie. Ældre projekter uden dem virker som før.

## Sikkerhed

Værdier fra uploadede filer (farver, positioner, skala, URL'er) valideres, før de bruges i siden, og `.zip`-filer tjekkes for antal filer og stier uden for `videos/` og `images/`.

## Afhængigheder

Ligger i `vendor/`; siden henter intet fra et CDN.

| Fil | Version | Licens |
| --- | --- | --- |
| `vendor/jszip.min.js` | JSZip 3.10.1 | MIT / GPLv3 |

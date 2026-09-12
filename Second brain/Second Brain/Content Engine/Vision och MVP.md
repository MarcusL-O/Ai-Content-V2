# Vision och MVP

[Projektstart](Start.md) · Status: B för produktinriktning, R/A för föreslagna mätgränser.

## Produkt och användning

Marcus ska slippa återskapa instruktioner, flytta filer mellan verktyg och manuellt avgöra vilket produktionssteg som kommer härnäst. Motorn håller samman karaktär, källor, manus, scener, referenser, genereringsförsök, utvärderingar och faktiska kostnader. Ett misslyckat försök får kosta inom sin tillåtna ram men får inte försvinna ur kalkylen.

Marcus godkänner en identitet och röst, väljer en testad produktionsprofil, sätter kostnadstak och aktiverar ett schema. Vid aktivering validerar kod hela paketet. Servern skapar sedan jobb även när datorn är avstängd. Jobbet låser sina konfigurationer, tar fram research och en idé, skriver manus och scenplan, genererar bilder och röst, skapar rörelseklipp, granskar dem, monterar och levererar. Misslyckande ger scen, orsak, använda pengar och nästa möjliga åtgärd i jobbvyn.

Marcus öppnar den autentiserade jobbvyn, ser förhandsvisning och total kostnad, laddar ned och gör slutlig publiceringsgranskning. Han markerar separat vad som faktiskt publicerats. `ready` betyder tekniskt färdig och godkänd av motorns kontroller; det betyder varken att Marcus godkänt kvaliteten eller att innehållet publicerats.

## Första release

B: Abby först, återanvändbar motor, självständig kedja inklusive research och videoproduktion, manuell publicering, utbytbara leverantörer, versionsstyrda profiler. R: `influencer_voiceover_v1`, 15–30 sekunder, 9:16, 1080×1920 export, 24 eller 30 fps låst per testad profil, 3–5 korta scener, amerikansk engelska. Föreslagen standard är 30 fps; konvertering från modellens bildfrekvens mäts i utvärderingen. 4K är senare exportvariant och uppskalning ska redovisas.

Första kvalitetssäkrade formatet visar Abby i lugna vuxna semester-/lifestyle-situationer med voiceover. Några miljöbilder kan komplettera, men en ren bildpresentation bevisar inte ett fungerande videoflöde: testsviten måste innehålla synlig naturlig rörelse. Manus ska ge en enkel stylingidé, ett igenkännbart skämt eller en liten berättelse, inte bara snygga miljöer.

Leveransen innehåller `final.mp4`, ren `master.mp4`, `captions.srt`, `cover.jpg`, `post-copy.md` och `manifest.json`. Manifestet anger källor, asset-hashar, paket-/profilversioner, försök, kvalitetsstatus, kostnadsstatus och om bilden är uppskalad. Musik är valfri och utelämnas tills en godkänd källa finns. Jobbvyn behöver start, paus/nödstopp, status, fel, kostnad, förhandsvisning, nedladdning och manuell publiceringsmarkering. Ingen avancerad dashboard behövs.

## MVP-acceptans – förslag att godkänna före provdrift

| Bevis | Föreslagen godkänd nivå |
|---|---|
| Sammanhängande kedja | Schemalagt jobb går research → färdigt paket utan manuell filflytt eller promptskrivning |
| Leveranskvalitet | Minst 8 av 10 förregistrerade jobb får slutvideo godkänd av Marcus inom beslutad budget och försöksgräns; alla 10 räknas |
| Automatik | Minst sju sammanhängande dygn utan manuell jobbstart; förläng till tio jobb om schemat är ett per dag |
| Driftavbrott | Testad omstart efter bild, under pågående beställning och under montering återanvänder färdiga assets |
| Ekonomi | Parallella jobb kan inte överreservera budget; okända utfall spärrar ny beställning; verklig överskjutande debitering bokförs och stoppar fortsättning |
| Dubbletter | Inga dubbla schemajobb i test av två schedulerprocesser och sommartidsövergång; inga blinda ombeställningar vid timeout |
| Leveransformat | Filer öppnas, röst hörs, textning matchar tal, 15–30 s och 9:16 enligt låst profil |
| Arbetsinsats | R: högst fem minuter aktiv granskning/hantering per godkänd leverans i median; allt korrigeringsarbete loggas |
| Återställning | Dokumenterad restaurering till isolerad miljö och kontrollerade asset-referenser |

Detaljerade kvalitetsgränser ägs av [Utvärdering](Utvärdering.md), budgetregler av [Drift och kostnader](Drift%20och%20kostnader.md). Tekniska tester får använda simulerade leverantörer; verklig produktionskvalitet kan aldrig godkännas med mockdata.

## Avgränsning och expansion

B: ingen automatisk publicering, kontohantering, likes, kommentarer eller DM i MVP. Ingen Jarvis, flerkundsprodukt, sponsorförhandling, affiliateavtal eller försäljning. Läppsynk, dans, smink, flera personer, exakt produktkontakt, långvideo och animation kräver egna utvärderingar och workflows. Full realism och intäkter är mål/hypoteser, inte acceptanslöften.

En reklamprofil återanvänder kö, kostnadsbok, lagring och export men kräver produktreferenser, verifierad produkttext, kommersiell metadata och produktlikhet som hårt kvalitetskrav. Mason återanvänder samma motor med undervisningsprofil och faktiska demonstrationsassets. Långvideo behöver kapitelplanering och längre kontinuitetshistorik. Detta motiverar separata profiler, inte en ny motor per användning.

## Affärsexperiment

Initial intäkt budgeteras till noll. Hypotes 1: Abby får återkommande tittande genom personlighet plus stylingvärde; testa tre format med jämförbar längd efter MVP. Hypotes 2: publiken vill klicka på relevanta produkter; pröva först när rätt produkter och relationer är verifierade. Hypotes 3: samma produktionskedja kan säljas som tjänst; prova ett avgränsat kundbrief senare och mät manuellt arbete. Hypotes 4: automatisering ger lägre total kostnad än ett manuellt flöde; logga utvecklingstid och drift separat så att låg API-kostnad inte döljer hög arbetsinsats.

R: cirka 30 manuellt publicerade videor, tre format, omkring en per dag efter tekniskt godkännande. Avläs efter 48 timmar och sju dagar; jämför tittartid, slutförandegrad, sparningar/delningar, följare per visning och senare verifierade klick/köp inom samma plattform. Saknade mått är null, inte noll. Små urval ger vägledning, inte bevis på stabil tillväxt.

# Roadmap och konkret backlog

[Projektstart](Start.md) · P0 = blockerar nästa etapp eller säker körning, P1 = krävs för etappens slut, P2 = senare utvidgning. Status “planerad” betyder inte implementerad. E0 är färdigskrivet granskningsunderlag, ännu inte godkänt av Marcus.

## Etapper och beslutspunkter

| Etapp | Resultat och grind |
|---|---|
| E0 Dokumentation | Sammanhängande plan och inaktiva paket, källkonflikter synliga, original bevarade; Marcus granskar |
| E1 Begränsat produktionstest | Godkända referenser/budget, jämförda vägar och kompletta pilotvideor; välj första verifierade format eller avbryt/omforma |
| E2 Motorns grund | Offline-kontrakt och simulerade leverantörer, kö, budget och bevisad resume; inga produktionsinköp behövs för grundtesten |
| E3 Hela kedjan | Verkliga testvinnare bakom adaptrar, research till färdigt paket och enkel jobbvy |
| E4 Schemalagd drift | CPU-server, schema, privata media, backup och återställningsprov |
| E5 MVP-godkännande | Sju dygns automatisk drift och totalt tio förregistrerade jobb; kvalitet, kostnad och manuellt arbete godkänns |
| E6 Publiktest | Marcus publicerar, faktisk statistik analyseras; ingen självpåverkande profiländring |
| E7 Vidareutveckling | Mason, reklam, läppsynk och andra format provas separat; Jarvis använder motorns befintliga API |

E1 är rekommenderad nästa etapp. Börja med uppgift CE-01 nedan som kostnadsfri förberedelse; pengar används först när konkreta referenser, kandidatkostnader och testtak är beslutade. Dokumentationsuppdraget i sig ger inte tillstånd att genomföra E1–E7.

## Nästa implementationsuppgift – CE-01 i detalj

Syfte: kunna genomföra ett begränsat jämförande test utan att först bygga motorn. Läs [Utvärdering](Utvärdering.md), [Abby](Karaktärspaket/Abby/Paket.md), [Workflows](Workflows.md) och F1–F4 i [Beslut och frågor](Beslut%20och%20frågor.md).

Leverera en förregistrerad experimentbeskrivning i valvet med T1–T3, exakt taltext, kandidat A/B, officiella capability-/pris-/villkorskällor och datum, kostnadsövre gräns per beställning samt total worst-case för föreslaget antal försök. Lägg fram ett granskningsbart referensurval om Marcus redan har godkända assets; om referenser saknas ska skapandet beskrivas som separat budgeterad del av experimentet. Påhittade referenser får inte göra readiness grön.

Om Marcus samtidigt ber om kodförberedelse för testet, skapa utanför valvet en minimal offline testharness med manifestvalidering och simulerad adapter; den är inte början på en full backend. Planerad kommandoyta är “validera experiment”, “visa kostnadsplan”, “kör ett uttryckligt test-ID” och “sammanställ alla försök”. Ingen nätverks-/betalåtkomst i standardläget. Exakta CLI-namn bestäms i implementationen, dessa är funktionskrav.

Acceptans: varje planerat betalt anrop har en dokumenterad kapabilitet, prisbas, maxförsök och kostnadsram; alla luckor syns som spärrar; två spår använder samma brief/referenser och rubric; summan inklusive omtag/reserv ryms inom det tak Marcus senare godkänner. Om det inte ryms, föreslå ett mindre experiment innan något köps. Denna uppgift ska inte sluta i installation av ComfyUI eller VPS av slentrian.

## Ordning och arbetskort

Varje rad anger konkret uppgift, syfte, beroenden, leverans och klart-definition. Teknikdetaljer ägs av länkade huvuddokument, så backloggen ändrar inte kontrakten på egen hand.

### CE-00 · E0 · Konsolidera projektplanen

- **Prioritet/status:** P0 · Skrivet, inväntar granskning.
- **Syfte:** Ge ett enda läsbart underlag.
- **Beroenden:** Beställning och original.
- **Konkret leverans:** Start, huvuddokument, inaktiva paket, ersättningskarta och granskningsprotokoll.
- **Acceptanskriterium:** Länkar fungerar, original/hashar oförändrade, ingen kod/inköp, nästa uppgift begriplig.

### CE-01 · E1 · Förregistrera experiment och verifiera kandidater

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Testa rätt sak inom ram.
- **Beroenden:** CE-00.
- **Konkret leverans:** Testbriefs T1–T3, officiellt capability/pris/rättighetsblad, kostnadsplan och vid separat koduppdrag offline harness.
- **Acceptanskriterium:** Detaljkraven ovan uppfyllda; saknade behörigheter och referenser blockerar riktig körning.

### CE-02 · E1 · Godkänn referensidentitet, röst, rubric och testtak

- **Prioritet/status:** P0 · Väntar Marcus beslut.
- **Syfte:** Förhindra test mot oklar målbild.
- **Beroenden:** CE-01; F1–F4.
- **Konkret leverans:** Beslutslogg, tillåtna bild-/röstassets och rättighetsproveniens.
- **Acceptanskriterium:** Verkliga asset-ID/hashar finns; testtak gäller definierat kassautflöde; inga påhittade voice-ID.

### CE-03 · E1 · Kör begränsad modelljämförelse

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Mät kvalitet och alla försök.
- **Beroenden:** CE-02.
- **Konkret leverans:** A/B-scenresultat, två kompletta pilotvideor om ramen räcker, kostnads-/minutrapport.
- **Acceptanskriterium:** Samma brief/rubric, alla misslyckanden räknade, ingen överskriden godkänd beställningsram; ofullständig jämförelse märks.

### CE-04 · E1 · Välj verifierat första format och model policy

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Undvik stort bygge runt dåligt material.
- **Beroenden:** CE-03.
- **Konkret leverans:** Marcus kvalitetsbeslut och låsta kandidatversioner eller omformad testplan.
- **Acceptanskriterium:** Minst komplett pilot bedömd, kostnadssäkerhet och begränsningar redovisade; ingen vinnare på leverantörsreklam.

### CE-05 · E2 · Implementera domänkontrakt och konfigurationsexport

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Skapa ett original och isolerade karaktärer.
- **Beroenden:** CE-04; Arkitektur och Karaktärspaket.
- **Konkret leverans:** Schemas, draft/active-validering, oföränderlig releaseexport/import.
- **Acceptanskriterium:** Null godtas i draft men blockerar active; samma version/annan hash avvisas; otillåtna paths/andra karaktärers assets blockeras.

### CE-06 · E2 · Inför databas och beständig jobbclaim

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Gör jobb återstartbara.
- **Beroenden:** CE-05.
- **Konkret leverans:** Migrationer, StepRun/ProviderRequest/Asset och lease/fencing.
- **Acceptanskriterium:** Två workers claimar inte samma aktiva steg; gammal worker kan inte skriva över efter leaseövertagande.

### CE-07 · E2 · Implementera kostnadsbok och reservation

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Håll samtidiga jobb inom gemensam ram.
- **Beroenden:** CE-06; Drift och kostnader.
- **Konkret leverans:** Decimalbokföring, budgetkonton, jobbram och anropsdelar.
- **Acceptanskriterium:** Parallella reservationer över tak avvisas; ingen dubbelräkning; midnatt frigör inte utestående åtaganden; överskjutande faktura syns och stoppar.

### CE-08 · E2 · Bygg simulerade adaptrar och anropsjournal

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Bevisa säkra felvägar utan pengar.
- **Beroenden:** CE-06, CE-07.
- **Konkret leverans:** Fake text/bild/röst/video/status med styrda timeout-/felutfall.
- **Acceptanskriterium:** Krasch före/efter submit, med/utan provider-ID, idempotensfönster och policyavslag ger rätt status och ingen blind ombeställning.

### CE-09 · E2 · Koppla agentkontrakt och workflow med mockdata

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Validera hela datakedjan.
- **Beroenden:** CE-05, CE-08; Agenter och Workflows.
- **Konkret leverans:** Steg 0–12 med låsta profiler, validerad payload och dependency-hashar.
- **Acceptanskriterium:** Fel JSON, okänd scen/referens, underkänd bild och förbrukade attempts stoppar rätt steg; success återanvänds efter omstart.

### CE-10 · E2 · Avgör workflow-/köbibliotek genom liten prototyp

- **Prioritet/status:** P1 · Planerad.
- **Syfte:** Begränsa egen komplexitet.
- **Beroenden:** CE-09.
- **Konkret leverans:** Beslut explicit workflow/LangGraph och eventuell underhållen kö.
- **Acceptanskriterium:** Samma avbrottsprov, ett auktoritativt stegtillstånd, konkret underhållsmotiv; inga överlappande ramverk utan behov.

### CE-11 · E3 · Implementera de testade leverantörsadaptrarna

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Koppla verklig produktion till säkra kontrakt.
- **Beroenden:** CE-04, CE-08, CE-10.
- **Konkret leverans:** Adapters med capabilities, price snapshot, submit/status/cancel där stödd.
- **Acceptanskriterium:** Ogiltig längd/ratio avvisas före nätverk; betalda integrationstester separat budgeterade; unknown hanteras enligt journalen.

### CE-12 · E3 · Integrera research, manus och scenplan

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Ge relevant innehåll och genomförbar regi.
- **Beroenden:** CE-09, CE-11.
- **Konkret leverans:** Källcache, ResearchBundle till GenerationPlan med riktiga profilanrop.
- **Acceptanskriterium:** Källa saknas → evergreen eller spärr enligt policy; karaktärsisolering, faktakrav och en manusrevision verifierade.

### CE-13 · E3 · Integrera bilder, röst, timing och video

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Skapa stabila godkända scener.
- **Beroenden:** CE-11, CE-12.
- **Konkret leverans:** Bildgrind, TTS/alignment, Timeline, scenvis video/retry.
- **Acceptanskriterium:** Video beställs aldrig före bildpass; röstlängd styr timing; ändrad bild ogiltigförklarar beroende klipp utan att nollställa attempts.

### CE-14 · E3 · Montera och paketera med slutkontroll

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Leverera användbara filer.
- **Beroenden:** CE-13.
- **Konkret leverans:** Master/final MP4, SRT, omslag, post-copy och manifest.
- **Acceptanskriterium:** Filer öppnas, format/längd/ljud verifieras, SRT bygger på tidsatt tal; exportfel kräver inte ny AI-generering.

### CE-15 · E3 · Bygg liten autentiserad jobbvy och CLI

- **Prioritet/status:** P1 · Planerad.
- **Syfte:** Gör motorn hanterbar för Marcus.
- **Beroenden:** CE-14.
- **Konkret leverans:** Status, kostnad, stopp, preview, download, markera publicerat.
- **Acceptanskriterium:** Obehörig åtkomst nekas, privata nedladdningar löper ut, ready skiljs från publicerat, tekniska fel är begripliga.

### CE-16 · E4 · Förbered och driftsätt CPU-tjänster och privat lagring

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Kör utan lokal dator.
- **Beroenden:** CE-15; separat godkänt driftuppdrag/F6.
- **Konkret leverans:** Låst image/Compose, hemlighetshantering, privat bucket och driftinstruktion.
- **Acceptanskriterium:** Server kör oberoende av Mac, ingen offentlig databas/media, kostnader och återstart kontrollerade.

### CE-17 · E4 · Implementera schema och nödstopp

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Automatisera inom tydliga gränser.
- **Beroenden:** CE-07, CE-16; F6.
- **Konkret leverans:** Tidszonsschema, unik lucka, skip catchup och global stoppspärr.
- **Acceptanskriterium:** Två schedulerprocesser, sommartid, midnatt och restart ger inga dubbletter; nödstopp stoppar nya beställningar.

### CE-18 · E4 · Säkerhetskopiera, återställ och övervaka

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Bevisa återhämtning före MVP.
- **Beroenden:** CE-16, CE-17; F7.
- **Konkret leverans:** Backupjobb, isolerad restorelogg, larm/jobbfel och retentionpolicy.
- **Acceptanskriterium:** Restore utan betalanrop, provideravstämning efter backup, checksummor kontrollerade och faktisk RPO/RTO redovisad.

### CE-19 · E5 · Kör förregistrerad schemalagd MVP-provdrift

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Mät att hela produkten fungerar.
- **Beroenden:** CE-18, F3 och godkänd driftbudget.
- **Konkret leverans:** Minst sju dygn och tio startade jobb, full kostnads-/kvalitetsrapport.
- **Acceptanskriterium:** 8/10 enligt beslutad rubric, alla tio räknas, median manuell tid redovisad, budget-/avbrottstester gröna.

### CE-20 · E5 · Godkänn eller åtgärda MVP

- **Prioritet/status:** P0 · Väntar föregående etapper.
- **Syfte:** Skilj fungerande demo från accepterad release.
- **Beroenden:** CE-19.
- **Konkret leverans:** Marcus acceptans eller prioriterad bristlista och omprov.
- **Acceptanskriterium:** Inga öppna hårda fel; kostnadsram och driftrutin accepterade, inget MVP-påstående enbart för att exporter finns.

### CE-21 · E6 · Genomför manuellt publiktest

- **Prioritet/status:** P1 · Planerad.
- **Syfte:** Testa affärshypoteser.
- **Beroenden:** CE-20; F8 och aktuella publiceringskrav.
- **Konkret leverans:** Cirka 30 videor enligt valt schema, verifierade länkar och 48h/7d-mätningar.
- **Acceptanskriterium:** Producerat/publicerat hålls isär, statistik definierad och samma plattform/tidsfönster jämförs.

### CE-22 · E6 · Jämför nya agent-/modellversioner

- **Prioritet/status:** P1 · Planerad.
- **Syfte:** Förbättra utan självpåverkande produktion.
- **Beroenden:** CE-21 eller identifierad kvalitetsbrist.
- **Konkret leverans:** Kandidatrelease, kontrollurval, kostnads- och regressionsrapport.
- **Acceptanskriterium:** Promotion kräver evidens och Marcus kvalitetsbeslut; rollback fungerar; latest används inte.

### CE-23 · E7 · Aktivera Mason genom separat education-prov

- **Prioritet/status:** P2 · Planerad.
- **Syfte:** Bevisa återanvändning för ny persona.
- **Beroenden:** CE-20; F5.
- **Konkret leverans:** Lösta källkonflikter, education-instruktioner/workflow och riktiga demos.
- **Acceptanskriterium:** Ingen ny kärnmotor krävs; inga Abby-assets/röster eller fabricerade skärmdemos; egen rubric godkänd.

### CE-24 · E7 · Prova avancerade format ett i taget

- **Prioritet/status:** P2 · Planerad.
- **Syfte:** Utöka endast med verifierad kvalitet.
- **Beroenden:** CE-20 och separat budget.
- **Konkret leverans:** Läppsynk-/smink-/dans-/flerperson-/reklamprofiler med egna tester.
- **Acceptanskriterium:** Varje profil har tydlig kapabilitetsgrind, alla försök/kostnader och produkt-/rörelse-/talbedömning.

### CE-25 · E7 · Lägg Jarvis ovanpå befintligt API

- **Prioritet/status:** P2 · Planerad.
- **Syfte:** Ge naturligt gränssnitt till samma motor.
- **Beroenden:** CE-20 och stabil administration.
- **Konkret leverans:** Verktyg för jobbstatus/kostnad, tillåtna jobb och schemaförslag.
- **Acceptanskriterium:** Jarvis kan inte kringgå budget, rättigheter, profilpromotion eller stopp; inga parallella jobbtillstånd.

### CE-26 · E7 · Utred publiceringsintegration och långvideo separat

- **Prioritet/status:** P2 · Planerad.
- **Syfte:** Utvidga utan att försvaga MVP.
- **Beroenden:** CE-20; nytt scope.
- **Konkret leverans:** Officiell API-/rättighetsutredning respektive kapitel-/kontinuitetsprov.
- **Acceptanskriterium:** Ingen social handling aktiveras utan uttryckligt uppdrag; långvideo har egen kostnads- och kvalitetsgrind.

## Arbetsordning vid avvikelser

Misslyckad E1 innebär nytt avgränsat format-/referensbeslut, inte att hela motorbygget fortsätter ändå. E2 kan bara tidigareläggas som uttryckligt avgränsat offlinearbete; testade modellparametrar får då inte låtsas finnas. Betalda integrationstester, drift och publiktest har egna beslut och budgetar; E1-taket ger inte automatiskt mandat till senare utgifter.

När en uppgift implementeras uppdateras status med datum och evidenslänk. Godkänd dokumentation är inte samma status som fungerande kod. Jarvis blir en klient till API:ets redan validerade funktioner: läs jobb/kostnad, föreslå schema och starta tillåtna jobb. Samma kostnadsbok, konfiguration och worker används även om användarens kommando kommer från tal.

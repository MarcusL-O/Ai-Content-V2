# Roadmap och konkret backlog

[Projektstart](Start.md) · P0 = blockerar nästa etapp eller säker körning, P1 = krävs för etappens slut, P2 = senare utvidgning. Status “planerad” betyder inte implementerad. Planens riktning godkändes av Marcus 2026-09-13; de fyra avgränsade dokumentförbättringarna är genomförda. Det innebär inte godkänd testbudget eller start av implementation.

## Etapper och beslutspunkter

| Etapp | Resultat och grind |
|---|---|
| E0 Dokumentation | Sammanhängande plan och inaktiva paket, källkonflikter synliga, original bevarade; riktning godkänd, detaljbeslut inför test kvarstår |
| E1 Begränsat produktionstest | ComfyUI på tillfällig hyrd GPU: godkända referenser/budget → interaktivt bild-/rörelseprov → låst container och rent omstartsprov vid godkänd kvalitet. API-jämförelse och full voiceoverpilot vid separat budget/underlag |
| E2 Motorns grund | Offline-kontrakt och simulerade leverantörer, kö, budget och bevisad resume; inga produktionsinköp behövs för grundtesten |
| E3 Hela kedjan | Verkliga testvinnare bakom adaptrar, research till färdigt paket och enkel jobbvy |
| E4 Schemalagd drift | CPU-server, schema, privata media, backup och återställningsprov |
| E5 MVP-godkännande | Sju dygns automatisk drift och totalt tio förregistrerade jobb; kvalitet, kostnad och manuellt arbete godkänns |
| E6 Publiktest | Marcus publicerar, faktisk statistik analyseras; ingen självpåverkande profiländring |
| E7 Vidareutveckling | Mason, reklam, läppsynk och andra format provas separat; Jarvis använder motorns befintliga API |

Kostnadsfri CE-01-förberedelse är utförd på Marcus uppdrag. Nästa grind är CE-02 samt återstående startkontroller i CE-01; inga hyrda resurser, installationer eller betalda försök är beställda. B6 prioriterar öppna vikter i egen ComfyUI-container. Detaljerna i Utvärdering är experimentets enda testplan.

## CE-01 – konkret förberedelse och återstående startkontroll

[Utvärdering](Utvärdering.md) innehåller nu modellkombination, officiell licens-/kapabilitetsverifiering, filnamn, konton, GPU-inställningar, T1–T3, max sex bildförsök och sex videoförsök samt föreslaget tak 300 kr. Inga referensassets, miljöversioner eller priser får antas godkända enbart för att planen finns.

Före en senare auktoriserad session ska Codex registrera verkliga referenshashar, exakt basimage-digest/ComfyUI-version och modellrevisioner, kontrollera image-/beroendelicenser och faktisk Pod-prisbild. Marcus ordnar referenser, röstunderlag och budget enligt CE-02. Kompatibilitet/VRAM mäts i CE-03; en källa får inte märkas tested utan körningsrapport. Kvalitetsprov föregår full serverless-drift. Ingen offline harness eller motorimplementation ingår i nuvarande uppdrag.

E2:s arbetsordning är CE-05 → CE-10 → CE-06 → CE-07 → CE-08 → CE-09. CE-10 fattar teknikbeslutet; senare uppgifter implementerar och verifierar det fullt ut.

## Ordning och arbetskort

Varje rad anger konkret uppgift, syfte, beroenden, leverans och klart-definition. Teknikdetaljer ägs av länkade huvuddokument, så backloggen ändrar inte kontrakten på egen hand.

### CE-00 · E0 · Konsolidera projektplanen

- **Prioritet/status:** P0 · Klar som dokumentationsunderlag; riktning godkänd 2026-09-13.
- **Syfte:** Ge ett enda läsbart underlag.
- **Beroenden:** Beställning och original.
- **Konkret leverans:** Start, huvuddokument, inaktiva paket, ersättningskarta och granskningsprotokoll.
- **Acceptanskriterium:** Länkar fungerar, original/hashar oförändrade, ingen kod/inköp, nästa uppgift begriplig.

### CE-01 · E1 · Förregistrera experiment och verifiera kandidater

- **Prioritet/status:** P0 · Kostnadsfri förberedelse klar; startkontroller av exakta filer/image och kontospecifikt pris återstår.
- **Syfte:** Testa rätt sak inom ram.
- **Beroenden:** CE-00.
- **Konkret leverans:** Befintlig Utvärdering: T1–T3, Qwen/Wan-licenser och referensstöd, GPU-/kostnadsblad, fil-/kontolista och interaktiv körplan; inga installationer.
- **Acceptanskriterium:** Dokumenterat stöd skiljs från eget test; återstående startkontroller är synliga och verifieras före GPU-start. Billigare produktion påstås inte utan mätning.

### CE-02 · E1 · Godkänn referensidentitet, röst, rubric och testtak

- **Prioritet/status:** P0 · Väntar Marcus beslut.
- **Syfte:** Förhindra test mot oklar målbild.
- **Beroenden:** CE-01; F1–F4.
- **Konkret leverans:** Beslutslogg, tillåtna bild-/röstassets och rättighetsproveniens.
- **Acceptanskriterium:** Godkända bildkopior med rättigheter/hashar och pilotens kassautflödestak finns. Marcus hanterar rösten; ljudlös del kan provas separat men full voiceovergrind kvarstår.

### CE-03 · E1 · Kör interaktiv ComfyUI-pilot och paketera godkänd miljö

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Mät kvalitet och alla försök.
- **Beroenden:** CE-02.
- **Konkret leverans:** T1–T3-bild/klipp, sessionskostnad inklusive start/laddning/fel och Marcus bedömning. Vid godkänd kvalitet: låst image/modellmanifest, UI-/API-workflow och rent omstartsprov inom tillåten ram. Helhetsexport med befintliga klipp när tre scener passerat; API-jämförelse separat budgeterad.
- **Acceptanskriterium:** Högst sex bild- och sex klippförsök inklusive omstartsprov, fyra GPU-timmar och godkänt kostnadstak; minst två av tre scener godkända för pilotmålet. Tre krävs för helhetsprov. Filer exporteras före terminering. Ingen serverless-plattform krävs; avsaknad av ljud/API-jämförelse markeras.

### CE-04 · E1 · Välj verifierat första format och model policy

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Undvik stort bygge runt dåligt material.
- **Beroenden:** CE-03.
- **Konkret leverans:** Marcus kvalitetsbeslut och låsta kandidatversioner eller omformad testplan.
- **Acceptanskriterium:** Ljud-/voiceoverpilot måste vara bedömd före motorbygge; ett ljudlöst rörelseprov räcker inte. Miljön återstartad rent, kostnad och begränsningar redovisade; inget påstående om API-besparing utan jämförelse.

### CE-05 · E2 · Implementera domänkontrakt och konfigurationsexport

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Skapa ett original och isolerade karaktärer.
- **Beroenden:** CE-04; Arkitektur och Karaktärspaket.
- **Konkret leverans:** Schemas, draft/active-validering, oföränderlig releaseexport/import.
- **Acceptanskriterium:** Null godtas i draft men blockerar active; samma version/annan hash avvisas; otillåtna paths/andra karaktärers assets blockeras.

### CE-10 · E2 · Avgör workflow-/köval genom liten prototyp

- **Prioritet/status:** P0 · Planerad; genomförs före CE-06 och CE-09. ID behålls för spårbarhet.
- **Syfte:** Motivera workflow-/kövalet innan beroende implementation byggs.
- **Beroenden:** CE-04, CE-05; dokumenterade kontrakt i Arkitektur och Workflows.
- **Omfattning/genomförande:** Ett isolerat trestegsflöde: förbered simulerad beställning → invänta simulerat svar → spara resultat. Prova explicit workflow och högst ett motiverat alternativ (LangGraph). Prova minimal jobbclaim enligt köförslaget; bedöm högst en underhållen kökandidat om egen lease-/retrykod blir oproportionerlig. Återanvänd små fixtures och tillfälligt prototyptillstånd; CE-06 bygger sedan produktionsmigrationer och beständig kö.
- **Konkret leverans:** Kort beslutsnotering med vald väg, avvisat alternativ, observerad komplexitet, avbrottsutfall och konsekvenser för CE-06/CE-09. Ingen full backend, agentintegration, GPU eller betalda anrop.
- **Acceptanskriterium/verifiering:** Kontrollera omstart efter färdigt steg, två konkurrerande claims och okänt simulerat beställningsutfall. Vald väg ska ha ett auktoritativt stegtillstånd och inget blint återutskick. Motivera med prototypens observationer; fulla produktionsgarantier verifieras senare i CE-06–CE-09.
- **Stoppvillkor:** R: högst en arbetsdag. Stoppa när beslutskriterierna är besvarade; vid olöst kritisk risk dokumenteras den och beroende implementation pausas. Utvidga inte till en generell ramverksutredning.

### CE-06 · E2 · Inför databas och beständig jobbclaim

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Gör jobb återstartbara.
- **Beroenden:** CE-05, CE-10.
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
- **Beroenden:** CE-05, CE-08, CE-10; Agenter och Workflows.
- **Konkret leverans:** Steg 0–12 med låsta profiler, validerad payload och dependency-hashar.
- **Acceptanskriterium:** Fel JSON, okänd scen/referens, underkänd bild och förbrukade attempts stoppar rätt steg; success återanvänds efter omstart.

### CE-11 · E3 · Implementera de testade leverantörsadaptrarna

- **Prioritet/status:** P0 · Planerad.
- **Syfte:** Koppla verklig produktion till säkra kontrakt.
- **Beroenden:** CE-04, CE-08, CE-10.
- **Konkret leverans:** ComfyUI-adapter för låst container/API-workflow, prompt-ID/status, resurskostnad och assets; färdiga API-adaptrar kan anslutas som alternativ. Capabilities, price snapshot och cancel där stödd.
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

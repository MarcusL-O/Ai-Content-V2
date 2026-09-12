# Drift och kostnader

[Projektstart](Start.md) · R: driftutformning. A: alla historiska belopp och målkostnader. Inga inköp godkända i denna etapp.

## När datorn är avstängd

En CPU-VPS kör administration, scheduler, worker, databas och lätt övervakning. Samma containerimage kan användas med olika processkommandon. Scheduler läser serverns aktiva release och skriver unika schemaluckor till databasen. Worker kan vänta på externa API:er utan lokal GPU. Marcus dator behövs för att redigera och exportera en ny konfiguration, inte för att genomföra redan aktiverade schemajobb.

GPU-arbete körs via färdigt API eller en separat GPU-worker som startas vid behov. R: börja med max ett samtidigt betalt medieanrop, tillåt senare ökning efter budget- och avbrottstester. Om GPU-spåret används provas flexibla workers med minsta antal noll och definierad idle-timeout. Extern kötid, uppstart, bearbetning och idle loggas separat. Modeller och custom nodes får en låst testad kombination, inte okontrollerade nedladdningar vid varje start.

Docker paketerar processer och beroenden och Compose beskriver flera tjänster. Beständiga data måste placeras i volymer eller extern lagring. Docker garanterar inte kvalitet, backup, kostnadsfri inaktivitet eller GPU-nedskalning; det senare måste ordnas hos driftleverantören. [Docker overview](https://docs.docker.com/get-started/docker-overview/), läst 2026-09-12. Vår föreslagna driftsammansättning är inte testad på Marcus dator; macOS-/Python-/Docker-stöd verifieras före eventuell installation. Ingen lokal CUDA krävs i planen.

RunPods dokumentation skiljer mellan workerutföranden och debiterade faser; lagring kan debiteras separat. Kontrollera vald endpoint, start och idle före ett test. Detta styr vår rekommendation att mäta hela körningen, inte bara modellens inferenstid. [RunPod serverless pricing](https://docs.runpod.io/serverless/pricing), läst 2026-09-12. R2 debiterar lagring och vissa operationer; gratis direkt egress betyder inte att hela lösningen är gratis. [R2 pricing](https://developers.cloudflare.com/r2/pricing/), läst 2026-09-12. Inga aktuella styckepriser har låsts eller använts som offert här.

Även med GPU av kostar CPU-server, databasdisk, backup, medielagring, modellvolymer, register, eventuella abonnemang och vissa operationer. Dessa poster måste rymmas i månadskalkylen.

## Schema och driftkontroll

R: Europe/Stockholm för schema och dygnsbudget; alla händelser lagras UTC med ursprunglig tidszon. Vid vårens saknade klockslag hoppas luckan över; vid höstens dubbla klockslag körs första förekomsten endast en gång. En unik lokal lucknyckel i databasen stoppar dubbletten. UTC-offset sparas. Missade luckor vid driftavbrott hoppas över; ingen automatisk kostnadsdrivande ikappkörning. Dessa regler gäller även om två schedulerprocesser startar samtidigt.

Heartbeat, ålder på köjobb, unknown-anrop, felkvot, återstående budget och lagringsutrymme syns i jobbvyn. Föreslagen varning: utebliven scheduler-heartbeat i fem minuter, lease saknad i två minuter, unknown-beställning omedelbart. Rapport i jobbvyn ingår; extern e-post/notifiering kräver senare konfiguration och aktivering. Loggar bär jobb-/steg-/request-ID men redigerar nycklar och privata signeringslänkar.

## Budgetreservation utan dubbelräkning

R: reservera hela godkända maxramen per jobb innan planering. Det är konservativt men lätt att förstå vid en video per dag. När detaljerad plan finns fördelas delar av denna ram till anrop, utan att hela jobbet och varje anrop räknas dubbelt mot samma konto.

`period_exponering = bokförd förbrukning + kvarvarande jobbramar + andra ej täckta åtaganden`. Jobbramen täcker sina egna outstanding requests. Att omvandla ett anrop från reservation till debitering ökar förbrukning och minskar motsvarande kvarvarande ram i samma transaktion. Kod kontrollerar jobb-, dygns-, månads-, experiment- och global operatörsbudget med samma låsordning innan reservation godkänns. Flera karaktärer får inte kringgå det gemensamma taket.

Varje betald operation kräver pris-/kapabilitetssnapshot och en konservativ övre anropsgräns som ryms i kvarvarande ram. Fastpris per genererad sekund räknar hela beställda klipplängden, inte bara de använda sekunderna. För rörlig GPU-debitering krävs dokumenterad tidsgräns och marginal; om bindande maxkostnad inte kan uppskattas stoppas automatisk beställning. Estimat är inte garanti mot sen leverantörsdebitering. Faktisk kostnad över reservation bokförs alltid som överskridande och stoppar nya anrop; den får inte klippas till budgettaket i rapporten.

Illustrativt, ej beviljad budget: jobbram 100 kr, första anropets reserv 25 kr. Efter faktisk debitering 20 kr blir förbrukning 20 och kvarvarande jobbram 80; den oanvända anropsdelen 5 är åter disponibel inom ramen. Nästa anrop på 85 kr blockeras. Vid avslut utan okända beställningar frigörs de 80 kronorna. Om ett annat anrop på 30 kr har okänt utfall kan den delen inte frigöras.

Ett jobb tillhör det lokala dygn/månad där det antogs; reserverade åtaganden bärs över periodgränsen tills utfall känts. Bokför separat faktisk debiteringstid för kassauppföljning. Reserverade pengar får inte bli fritt utrymme vid midnatt. Globalt utestående tak kontrolleras över alla perioder.

CostEntry skiljer `estimate`, `reserve`, `settle`, `release`, `adjustment`. Decimalbelopp i leverantörsvaluta sparas med SEK-kurs, kursdatum, prisdatum och certainty `estimated|provider_reported|invoice_confirmed`. Utebliven faktura är pending_reconciliation, inte kostnad noll. Kredit bokförs först när den är verifierad; policyavslag eller nätfel betyder inte automatiskt återbetalning.

## Undvik dubbla beställningar

1. Kod reserverar anropsdelen och skriver en `prepared` ProviderRequest med unik intern nyckel och request-hash i en transaktion före nätverket.
2. Om dokumenterad provider-idempotens finns skickas samma nyckel för samma logiska beställning; spara dokumenterat giltighetsfönster. Svar med provider-ID sparas omedelbart.
3. Pollning eller webhook följer samma ID. Webhook verifieras enligt adapterkontrakt och måste tåla dubbletter. Download och checksumma får upprepas utan ny generering.
4. Timeout efter möjlig accept, eller krasch mellan skickat anrop och sparat ID, markeras `unknown`. Kontrollera status via känt ID eller dokumenterad sökning på kundnyckel. Utan sådan funktion får anropet inte skickas igen blint. Behåll reservation och sätt needs_review med instruktion till operatören att avstämma leverantörsloggen.
5. Nytt försök tillåts bara när det gamla säkert inte accepterats, eller när leverantörens idempotens fortfarande täcker samma beställning. Ett definitivt misslyckat men debiterat försök behåller kostnaden; ett nytt genereringsförsök får nytt attempt-ID och kräver ny anropsreservation.

Interna job-hashar förhindrar inte dubbletter hos en extern leverantör utan idempotens. Vi lovar inte exakt-en-gång över denna gräns. Vid leaseövertagande måste gammal worker förlora skrivrätten med fencing-token; redan skickade externa anrop måste fortfarande avstämmas.

R: statuspollning med backoff 5/10/20/40/60 s inom adapterdeadline; tekniskt retrytak tre för säkra status-/läsoperationer. Detta är skilt från de kreativa försöksgränserna i [Workflows](Workflows.md). Använd dokumenterad Retry-After där sådan ges. Okänt POST-utfall är inte ett vanligt retryfall.

Nödstopp sätter en global spärr som varje worker kontrollerar precis före nästa beställning. Pågående anrop avbryts när adaptern stöder det, men kostnad kan kvarstå. Avstämningsworker får fortsätta läsa status och bokföra. Avbryt inte kostnadsloggen när jobbet avbryts.

Felrapport: job_id, failed_step, scene_id, error_code, short_reason, attempts_used, charged_amount, reserved_unknown_amount, cost_certainty, last_provider_id nullable, next_action. Exempel nästa åtgärd: “Avstäm request med okänt utfall hos leverantören; ny beställning spärrad”.

## Backup, retention och återställning

R: daglig krypterad databasbackup till separat lagringsplats, 7 dagliga och 4 veckovisa kopior; versionslåsta konfigurationsreleaser och assetmanifest inkluderas. Föreslagna mål RPO 24 h och RTO 4 h är oprövade och ska mätas. Referensmedia och färdiga masterfiler säkerhetskopieras, inte bara deras metadata. Spara rättighetsunderlag så länge dess assets används.

R: underkända råförsök 30 dagar, godkända leveranser/master 90 dagar eller längre enligt Marcus beslut. Referenser och kostnads-/proveniensmetadata får inte raderas med en generell råmediaregel. Inför retention först efter beslut och återställningstest; radera inget i denna etapp.

Återställ först till isolerad miljö med scheduler av och alla betalda adaptrar spärrade. Återläs databas, releasehashar och nödvändiga assets. Kontrollera checksummor och referenser. Avstäm alla externa anrop efter backupens tidpunkt innan kö återaktiveras: en gammal databas kan annars sakna en redan debiterad beställning. Importera providerlogg där möjligt; olösta intervall lämnas blockerade. Mät faktisk tid och redovisa dataförlust mot RPO. Testa återställning före MVP och efter större lagrings-/databasändring.

## Kostnadsscenarier från underlaget

Källa: [ursprunglig brief](../../Content-Engine-Codex-Brief.md), avsnitt 12, daterad 2026-09-12. Alla belopp nedan är bevarade planeringsantaganden, inga offerter eller benchmarks. Kalkylkurs 10 SEK/USD; före moms, valutapåslag, egen arbetstid och abonnemangsminimum. Faktiskt kassautflöde kan därför bli högre.

| Scenario | Antagande och tolkning |
|---|---|
| CPU + backup + mindre kringkostnader | 150–400 kr/månad; inte kontrollerad leverantörsoffert |
| Första experiment | Föreslaget totalt tak 1 500 kr; Marcus måste besluta omfattning och om taket avser faktiskt kassautflöde |
| Utvecklingsexperiment till första release | Grovt 1 500–6 000 kr; inte automatiskt godkännande av mer än första testet |
| Utvecklingstid | Grovt 95–210 h från briefen; stor osäkerhet, inget leveranslöfte |
| Användbar 20 s video | Testmål omkring 100 kr; inte uppmätt |
| 30 videor med 100 kr/st + 250 kr fast drift | 3 250 kr/månad under just dessa antaganden |
| 90 videor med 100 kr/st + 250 kr fast drift | 9 250 kr/månad; volymen är ingen planerad startnivå |
| Historiskt klippkostnadsexempel | 32 genererade sekunder × 0,40 USD/s × 10 = 128 kr; 0,60 USD/s ger 192 kr. Två fulla försök ger 256 respektive 384 kr före övriga steg |

Äldre exempel 17/43 kr per video gäller enklare antagna klipp och omtagningar; de verifierar inte senaste modell, 4K, läppsynk eller fotorealism. Ingen räknerad är ett uppmätt resultat för detta projekt.

`rörlig kostnad per godkänd video = alla försök för hela kohorten (research, LLM, bild, röst, video, montering och rörlig lagring) / antal godkända videor`. Visa även `total kontant kostnad per godkänd = (rörligt + periodens fördelade fasta kostnader) / godkända`, och manuella minuter separat. Vid noll godkända rapporteras “ingen användbar styckkostnad, total förbrukning X”; dividera inte med antalet försök som om de vore leveranser.

Känslighetsexempel: om ett produktionsförsök antas kosta 50 kr och inga andra kostnader finns blir kostnaden per godkänd cirka 62,50 kr vid 80 % godkännande och 100 kr vid 50 %. I verkligheten skiljer sig försökskostnader och fler poster tillkommer; summera därför faktiska CostEntries i utvärderingen.

Intäkt initialt 0. Med 3 250 kr drift och antagen faktisk provision 50 kr krävs 65 godkända köp för att täcka kontanta driften före arbete/skatt. Detta är en hypotetisk division, inte en prognos eller uppgift om verkligt affiliateavtal. Modell-/röstpriser, rättigheter och kommersiella villkor ska verifieras på officiella källor i E1 innan pengar används.

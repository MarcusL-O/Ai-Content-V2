# Beslut, risker och öppna frågor

[Projektstart](Start.md) · Beslutsregister 2026-09-12. B/R/A/F definieras på startsidan. Inget rekommenderat teknikval är ett godkänt inköp.

## Beslut och rekommendationer

| ID | Typ | Beslut eller förslag | Grund och konsekvens |
|---|---|---|---|
| B1 | Beslutat med Marcus | Återanvändbar modulär motor från research till leverans | Beställningen/briefens beslutsdel; MVP är hela kedjan |
| B2 | Beslutat med Marcus | Abby först, manuell publicering; Jarvis och kontointeraktion senare | Begränsar första releasen och undviker onödig integration |
| B3 | Beslutat med Marcus | Versionsstyrda agent-/karaktärs-/workflowprofiler, utbytbara leverantörer | Jobb låser profiler och modeller |
| B4 | Beslutat med Marcus | Planering och nya paket i innersta Second Brain, skyddade original och äldre utkast bevaras | Senaste beställningen ersätter briefens äldre placeringsförslag |
| B5 | Beslutat med Marcus | Ingen kod, installation, betalning, deployment eller push under etapp 0 | Bara granskningsunderlag och konfigurationsutkast |
| R1 | Rekommendation | 15–30 s voiceover, 9:16, 1080p och låg rörelsekomplexitet | Kortare kvalitetsprov innan läppsynk/komplexa scener; se MVP |
| R2 | Rekommendation | Python/FastAPI/Pydantic, PostgreSQL, CPU-VPS/Compose, FFmpeg, privat objektlagring | Projektskäl och byteskriterier i Arkitektur; gamla docs angav felaktigt vissa val som accepterade |
| R3 | Rekommendation | Explicit workflow först, LangGraph som begränsad prototypkandidat | Ett auktoritativt stegtillstånd förenklar återhämtning; avsteg från briefens preliminära LangGraph-val |
| R4 | Rekommendation | Testa färdigt medie-API mot GPU/ComfyUI eller andra API om GPU-spåret inte ryms | Inget ComfyUI-/RunPod-tvång innan uppmätt nytta |
| R5 | Rekommendation | Valv → validerad oföränderlig export → server | Ett redigerbart konfigurationsoriginal; inga samtidiga manuella serverkopior |
| R6 | Rekommendation | Konservativ jobbram, max ett betalt anrop samtidigt initialt, stoppa okänt utfall | Begripligt kostnadsskydd med låg produktionsvolym |
| R7 | Rekommendation | en-US för båda paket; Mason som arbetsnamn; oklar exakt Abby-ålder lämnas null | Följer huvudprofiler utan att dölja källkonflikter |
| A1 | Antagande att testa | Kvalitet kan bli tillräcklig utan LoRA och dedikerad GPU | Referens- och rörelseprov avgör |
| A2 | Antagande att testa | Cirka 100 kr per godkänd 20 s video | Inga egna mätningar; alla försök räknas |
| A3 | Antagande att testa | 8/10 godkända jobb och median högst 5 manuella minuter räcker för första MVP | Marcus kalibrerar acceptans före provdrift |
| A4 | Antagande att testa | Publiktest på cirka 30 videor ger användbar riktning | Ingen garanti om räckvidd, affiliate eller intäkt |

B-besluten här återger användarens uttryckliga underlag, inte en ny muntlig överenskommelse. Förändringar får datum, motivering och ersatt besluts-ID; tidigare beslut skrivs inte om utan spår.

## Frågor som kräver Marcus beslut

Frågorna blockerar inte denna dokumentationsetapp. De lämnas samlade för granskning, med föreslagen väg framåt.

| ID | Fråga och rekommenderat svar | När det behövs | Konsekvens om obesvarat |
|---|---|---|---|
| F1 | Godkänn eller ändra experimenttaket 1 500 kr. R: taket bör avse verkligt kassautflöde inklusive moms/avgifter och reserverade okända anrop | Före första betalda referens-/modelltest | Endast kostnadsfri testförberedelse |
| F2 | Vilket ansikte och vilken röst godkänns för Abby, med vilket rättighetsunderlag? R: en originalidentitet, härledda vinklar och separat ljudprov | Före berörd medieproduktion | Paketet förblir inaktivt; inga fejkade asset-/voice-ID |
| F3 | Godkänn 15–30 s voiceover som första format och rubric/8-av-10-mål. R: börja där och utvärdera synligt tal separat | Före testdesignen fryses och senare MVP-prov | R/A-gränser kvarstår som förslag |
| F4 | Ska Abby ha fryst 25-årsålder eller följa födelsedatum 2000-05-05? R: fryst fiktiv vuxen ålder, utan offentlig födelsedag | Före paketaktivering/offentlig åldersuppgift | Ingen exakt åldersuppgift används |
| F5 | Är Mason slutligt namn och är MA2:s Abby-röst felplacerad? R: Mason enligt titel; ta fram separat manligt röstprov utan att flytta original | Före Mason-aktivering | Education-paketet förblir spärrat |
| F6 | Vilka löpande jobb-/dygns-/månadstak och schematid gäller efter pilot? R: en daglig lucka först vid provdrift och separat globalt tak | Före schemaläggning | Budget och schema står null/av |
| F7 | Godkänn föreslagen backup/retention eller välj längre bevarande | Före drift och automatisk radering | Ingen råmediaretention aktiveras |
| F8 | Vilket publiktest önskas: AB1:s två veckor/lägre takt eller briefens cirka 30 videor? R: 30 videor efter teknisk MVP | Efter MVP | Ingen automatisk publicering; testplanen är ett förslag |

Val av exakt text-, bild-, video- och röstmodell är en teknisk utvärderingsuppgift, inte en blockerande allmän produktfråga till Marcus. Föreslå kandidater med verifierade officiella data i E1 och visa konkret kostnad/kvalitet före produktionsval.

## Riskregister och praktisk hantering

| Risk | Tidigt tecken | Motåtgärd och ansvar | Kontrollpunkt |
|---|---|---|---|
| Identitet/rörelse håller inte | T1–T3 underkänns upprepat | Förenkla rörelse, förbättra referenser, jämför modell; utvecklare föreslår, Marcus bedömer | E1 före motorbygge |
| Kostnaden per leverans blir hög | Låg godkännandegrad eller stor genererad/utnyttjad tidskvot | Mät alla försök, kortare scener, stoppa dyr gren; budgetkod stoppar nya anrop | Varje anrop och experimentrapport |
| Dubbelt betalt anrop | Krasch/timeout före provider-ID | Durable request, dokumenterad idempotens eller spärrad avstämning | E2 avbrottstest |
| Fel källa blandar karaktärer | Abby-röst hos Mason, Ethan i bio | Proveniens och aktiveringsspärr, character-scope i alla läsningar | Paketvalidering och F4/F5 |
| Automatgranskare godkänner fel | Marcus underkänner ett maskin-pass | Kalibrera och sätt berörd kategori needs_review | E1 och varje profilpromotion |
| Två konkurrerande konfigurationer | Servertext skiljer sig från valvets hash | Oföränderliga releaser, ändring bara i valvet | Export och import |
| Falska resultat/produktdetaljer | Manus saknar claim-källa eller riktig demo | Writer blockerar, Reviewer jämför; Marcus godkänner kommersiellt underlag | Manus och slutkontroll |
| Återställning dubblar beställningar | Backup saknar senaste provider-request | Betalspärr efter restore, avstäm leverantörslogg | E4 restoreövning |
| Leverantör ändrar pris eller stöd | Capability/pricing-snapshot löper ut eller anrop avvisas | Stoppa ny produktion och utvärdera adapter/release; ingen tyst fallback | Före inköp och profilpromotion |
| För stort bygge före bevis | Tid går till dashboard/ramverk medan inget klipp är godkänt | E1-gate, minimal monolit, avgränsad backlog | Etappbyte |

## Aktuella källor och verifieringsgräns

Arkitektur och drift anger officiella dokumentationslänkar och läsdatum 2026-09-12 för PostgreSQL, LangGraph, FastAPI, Pydantic, ffprobe, Docker, RunPod och R2. Dessa belägger verktygens dokumenterade egenskaper; våra teknikval och gränsvärden är egna rekommendationer. Vi har inte installerat eller kört dessa komponenter som del av motorn.

Exakta modellkapabiliteter, leverantörspriser, kommersiella licenser, plattformsregler och lokalt utvecklingsstöd är ännu inte verifierade för en vald produktionskombination. De ska inte läsas som löften i denna plan. E1 gör officiell verifiering före test; E6 kontrollerar aktuella publiceringskrav före uppladdning. Äldre länkar och forskningspåståenden i karaktärsoriginal har lästs som källinnehåll men har inte antagits vara validerade affärsresultat.

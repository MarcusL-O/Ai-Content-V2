# Utvärdering, kvalitet och modellval

[Projektstart](Start.md) · R: försöksdesign och gränsvärden. Inga egna produktionstester eller benchmarkresultat finns ännu.

## Första begränsade experimentet

Syfte: bevisa ett användbart Abby-format innan större motorbygge. Marcus godkänner först referensidentitet, röstanvändning, experimenttak och preliminär rubric. Föreslaget 1 500 kr är ett tak att ta ställning till, ingen beställning. Om två spår inte ryms minskas urvalet eller spår B avslutas med skäl; dra då ingen slutsats om en jämförelse som inte genomförts.

E1 börjar kostnadsfritt med capability/pris/rättighetsblad och testbriefs. Kandidat A är ett färdigt bild-/video-API; kandidat B ComfyUI på extern GPU om licenser, uppstart och total kostnad ryms. Om GPU-förberedelsen är oproportionerlig väljs ett andra färdigt API och detta beslut dokumenteras. ElevenLabs kan ingå som en TTS-kandidat, tillsammans med en andra relevant röstväg när kostnad/rättigheter tillåter. Inga exakta aktuella modell-ID:n eller tillgänglighetslöften är verifierade här; de väljs och dokumenteras före test.

R: använd samma godkända referenser, brief, taltext, målformat och rubric. Börja med tre scener per väg och ett försök per scen; högst ett jämförande omtag om experimentramen tillåter. Gör sedan två kompletta 15–30 s videor med den mest lovande vägen för att mäta montering och helhet. Detta lilla piloturval väljer riktning, inte statistiskt bevisad produktionsstandard. Separat MVP-prov använder tio förregistrerade jobb enligt [Vision och MVP](Vision%20och%20MVP.md).

Föreslagen experimentfördelning inom godkänt tak: högst 15 % till referens-/röstprov, 50 % till första jämförelsescener, 25 % till kompletta videor och 10 % reserv. Aktuella prisestimat ska visa att minst ett avslutande helhetsprov ryms innan första betalda test startas. Om två kandidater faller på samma hårda fel två gånger, pausa och förenkla format eller referenser; fortsätt inte köpa omtag bara för att budget finns.

## Fast scenbank

| ID | Test | Vad det isolerar | Etapp |
|---|---|---|---|
| T1 | Ansiktsnära i morgonljus, liten huvudrörelse | Identitet, hud, ögon, mun | Första tre scener |
| T2 | Helkropp, kort lugn promenad | Proportioner, ben/rörelse, kläder | Första tre scener |
| T3 | Sittande vid kaffekopp utan att lyfta den | Händer i vila, rekvisita, kontinuitet | Första tre scener |
| T4 | Två klipp i samma outfit och miljö | Scenövergång och konsekvens | Komplett pilotvideo |
| T5 | Klädbyte mellan två tydliga scener | Samma person trots ny styling | Senare formatutvidgning |
| T6 | 8–10 s talande ansikte med godkänd röst | Läppsynk, uttal, identitet under tal | Separat experiment, ej voiceover-godkännande |
| T7 | Miljöklipp med långsam kamera | Geometri, bakgrundsrörelse | Komplett pilotvideo |
| T8 | Ta kopp, sminka, dansa, två personer | Kontakt och komplexa rörelser | Fyra separata senare prov |
| T9 | Godkänd produkt i nära bild och hand | Form, färg, märkning och kontakt | Reklamprofil |
| T10 | Verklig skärmdemo med Mason-berättarröst | Korrekt teknik, läsbarhet, lärande | Education-profil |

Samma scener betyder samma avsedda innehåll, inte nödvändigtvis identiska prompts: adapteranpassning är tillåten men loggas och tidsbegränsas lika för båda spår. Registrera genererad längd/upplösning och export separat. Slumpfrön sparas där de stöds men bevisar inte reproducerbarhet.

## Bedömningsskala och hårda stopp

Skala 1–5: 1 oanvändbart, 2 tydliga återkommande fel, 3 märkbara men begränsade brister, 4 naturligt nog för avsett format vid normal uppspelning, 5 mycket övertygande även vid närgranskning. Bedöm mot godkänd referens, inte en abstrakt idealbild. Föreslagna gränser kräver Marcus kalibrering före betalt experiment.

| Dimension | Mätmetod | Föreslagen grind |
|---|---|---|
| Karaktärslikhet | Jämför ansikte/proportioner med referens i början, mitten, slutet och rörelse | ≥4 och ingen tydlig identitetsförändring |
| Röst | Lyssna blint på samma text, kontrollera uttal, rytm och referenslikhet | ≥4; inga felaktiga ord eller avklippt tal |
| Läppsynk | Full uppspelning plus tidsatt läpp-/ljudkontroll | Ej tillämpligt=null i voiceover; synligt osynkat tal underkänns. Separat talprov kräver ≥4 och föreslaget max 100 ms tydlig offset |
| Rörelse och händer | Normal uppspelning samt långsam kontroll av rörelsens toppar | ≥4; extra fingrar, smältande kroppsdel eller orimlig kontakt är hårt fel |
| Kontinuitet | Jämför outfit, smycken, miljö, tid och färger mellan scener | ≥4; oförklarat identitets-/outfitbyte är hårt fel |
| Manus och tittarvärde | Marcus återger hook, handling och vad tittaren får | ≥4 för tydlighet/värde; inga ogrundade fakta |
| Produktlikhet | Jämför godkänt produktmaterial med visad form/färg/logo/funktion | Null utan produkt; annars ≥4 och ingen vilseledande produktavvikelse |
| Leveransteknik | ffprobe, ljudlyssning och jämförelse SRT/tal | Rätt format/längd, inga korrupta assets, ingen klippning av tal, läsbar text |

Ingen medelpoäng får väga upp ett hårt fel, saknade rättigheter eller fabricerat resultat. Fail går till begränsad korrigering; uncertain kräver mänsklig granskning. Automatiska bildmått kan hjälpa men ersätter inte att samma karaktär känns igen i rörelse. En granskarmodell som bara sett några stillbilder får inte påstå att hela videons rörelser har verifierats.

## Mät varje försök och varje leverans

Försöksrad: experiment_id, brief_id, character_release, profile_version, model/provider-version, capability/pricing-datum, reference_hashes, prompt_hash, seed nullable, attempt_id, requested/generated/used_seconds, native/export_resolution, upscale, queue/start/run_seconds, paid_amount_original, SEK-rate/date, cost_certainty, failure_code, scores, human_minutes och selected_for_delivery.

Jobbrad: alla attempt-ID, total förbrukning även för bortvalda assets, kvarvarande okända reservationer, slutstatus, Marcus beslut och manuella minuter för promptändring/granskning/redigering/nedladdning. Skilj aktiv mänsklig tid från väntetid. Märk pilotvideo och testmaterial som opublicerat.

Rapportera `godkända jobb / samtliga startade testjobb`, `godkända scenförsök / samtliga scenförsök`, kostnad per godkänd video inklusive förlorade försök, median och spann i manuella minuter, end-to-end ledtid och felorsaker. Ange numerator/denominator; 8/10 är ett litet urval, inte bevis på framtida 80 %. Okända kostnader redovisas som intervall/reservation tills faktura/status avstämts.

## Kalibrera Reviewer och släpp profiler

Marcus bedömer kandidatklipp i slumpad ordning utan leverantörsetikett där praktiskt möjligt. Spara hans poäng före modellgranskarens slutsats. Bygg en liten märkt samling av bra, dåliga och osäkra klipp med varierad rörelse. Jämför false accept (maskin pass, Marcus fail) och false reject separat. R: ingen false accept för kända hårda fel i kalibreringssamlingen; om granskaren missar sådana måste berörd scenkategori gå till needs_review tills förbättring testats.

En kandidatprofil får status draft → evaluation → approved → retired. Promotion kräver testmanifest, kostnadsrapport, samma eller bättre hårda felutfall, rimlig manuell tid och Marcus kvalitetsbeslut. Senaste modell provas på separat kandidat-ID; inget produktionsjobb använder “latest”. Modellbyte omfattar prompt, adapterkapabilitet, referenser, pris och granskarbeteende. Spara en del briefs som osett kontrollurval och välj inte bara klipp som användes vid promptjusteringen.

Rollback aktiverar föregående godkända release för nya jobb. Pågående jobb behåller sina låsningar eller stoppas uttryckligen; de byter inte modell halvvägs. Ingen agent självpåverkar produktionsinstruktionen utifrån enstaka publikutfall.

## Kapabilitetsblad före inköp

Varje kandidat ska ha officiell URL och avläsningsdatum för modell-ID/version, region/åtkomst, text-to-image/image-to-video, antal referenser, ratio/upplösning/fps, klipplängder, ljudläge, asynkron status, idempotensfönster, avbrytning, prisbas, kommersiella villkor och retention. Använd `unsupported`, `documented` eller `unverified`; ett senare eget test ger separat `tested` med rapport-ID. Leverantörens dokumenterade stöd är ingen garanti om vår bildkvalitet. Null på kostnadskritisk kapabilitet blockerar automatisk produktion.

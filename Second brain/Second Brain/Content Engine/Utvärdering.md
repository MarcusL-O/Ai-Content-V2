# Utvärdering, kvalitet och modellval

[Projektstart](Start.md) · R: försöksdesign och gränsvärden. Inga egna produktionstester eller benchmarkresultat finns ännu.

## CE-01 – första experimentet, kostnadsfri förberedelse 2026-09-13

B: förstahandsspåret är egna modeller med öppna vikter via ComfyUI i container på hyrd GPU. Vi testar kvalitet, total kostnad och kontroll samt lärande om modeller, containers och drift. Billigare produktion är A, inte ett uppmätt resultat. Färdiga API:er kvarstår som jämförelse/alternativ via adaptrar. Text och röst väljs separat. Denna plan är förberedd utan installation, GPU-start eller generering; experimentet nedan kräver nytt körningsuppdrag och budgetbeslut.

### Rekommenderad modellkombination och verifiering

R: **Qwen-Image-Edit-2511 → Wan2.2-TI2V-5B**. Först skapas scenbilder från godkända identitetsreferenser; Marcus godkänner bilden innan den blir startbild till Wan. Detta prioriterar referensstyrning och ett hanterbart första rörelseprov. 5B är en baslinje, inte ett påstående om högsta tillgängliga kvalitet. Om den missar identitet/rörelse trots bra startbild föreslås ett separat prov av Wan2.2-I2V-A14B eller färdigt API, med ny kapabilitets-/licens-/budgetkontroll före anrop.

Alla källor i följande tabell lästes **2026-09-13**. `documented` betyder officiellt beskrivet, inte lokalt testat. Modellrevisioner och filhashar låses före hämtning/körning; inga fabricerade revisions-ID används här.

| Del | Officiellt underlag och slutsats | Kvar att mäta/kontrollera |
|---|---|---|
| Bildmodell | [Qwen-Image-Edit-2511 modellkort](https://huggingface.co/Qwen/Qwen-Image-Edit-2511): 20B/BF16, bildredigering och förbättrad identitetskonsekvens enligt utgivaren, Apache-2.0. [ComfyUI native-flöde](https://docs.comfy.org/tutorials/image/qwen/qwen-image-edit-2511) dokumenterar referensbilder och modellfiler | Egen identitetsbedömning. Börja med en primär bild per scen; extra referens endast via mallens dokumenterade ingång, inte som påhittat generellt referensantal |
| Video | [Wan2.2-TI2V-5B modellkort](https://huggingface.co/Wan-AI/Wan2.2-TI2V-5B): image-to-video med en startbild, 720p-klass, vertikalt exempel 704×1280; referensimplementationen anger minst 24 GB med offload/CPU-T5 | Ingen garanti om ansiktslås över klippet. Faktisk VRAM, RAM, renderingtider och porträttformat kontrolleras på vald ComfyUI-version |
| ComfyUI/Wan | [Native Wan2.2-flöde](https://docs.comfy.org/tutorials/video/wan/wan2_2) dokumenterar 5B, valfri Load Image och längd/upplösning. ComfyUI nämner 8 GB med sin offloading | 8 GB gäller annan körväg än utgivarens 24 GB; används inte som GPU-dimensionering eller prestandalöfte i piloten |
| GPU för första sessionen | R: en A100 PCIe 80 GB, minst 100 GB värd-RAM. Qwens lästa officiella guide anger inget fast VRAM-minimum för hela flödet; 20B BF16 motsvarar cirka 40 GB enbart för modellvikterna, före encoder/aktiveringar | 80 GB är vår försiktiga pilotdimensionering, inte verifierat minimikrav. Kör modeller sekventiellt och frigör den föregående. Mät peak VRAM/RAM. Senare 48/24 GB eller kvantisering provas som separat kostnadsoptimering |
| Pris | [RunPod Pods-prislista](https://www.runpod.io/pricing): A100 PCIe 80 GB visades som 1,59 USD/h; 117 GB RAM i den listade konfigurationen | Listpris, inte bokad kapacitet eller offert. Kontrollera vald region/Pod-pris i kassan före start; föreslaget pristak 2 USD/h |

### Modellfiler och licensgrind

Använd officiella ComfyUI-mallar och deras länkade modellfiler, utan extra community-LoRA, GGUF-wrapper eller Lightning-acceleration i baslinjen. Filnamnen nedan är dokumenterade nedladdningsmål, inte filer som redan finns lokalt:

| Under ComfyUI/models | Qwen-bildsteg | Wan-videosteg |
|---|---|---|
| diffusion_models | `qwen_image_edit_2511_bf16.safetensors` | `wan2.2_ti2v_5B_fp16.safetensors` |
| text_encoders | `qwen_2.5_vl_7b_fp8_scaled.safetensors` | `umt5_xxl_fp8_e4m3fn_scaled.safetensors` |
| vae | `qwen_image_vae.safetensors` | `wan2.2_vae.safetensors` |

Filfördelningen kommer från ComfyUI-guiderna ovan. För Qwen-encodern väljs uttryckligen [Qwen-Image_ComfyUI/text_encoders](https://huggingface.co/Comfy-Org/Qwen-Image_ComfyUI/tree/main/split_files/text_encoders), som listar samma FP8-fil under Apache-2.0. 2511-guidens direkta encoderlänk går till ett Hunyuan-repo med annan övergripande licensmetadata; vi använder därför Qwen-källan och verifierar filens hash där. Qwen-VAE hämtas också från Qwen-Image_ComfyUI. Spara exakt repo, revisionshash, nedladdnings-URL, SHA-256 och licenskälla per fil vid förberedelse av körningen. Välj de specificerade basfilerna; en gemensam repokatalog kan innehålla andra modellvarianter med andra villkor.

**Licensslutsats för avsedd användning:** de valda basmodellernas officiella modellkort anger Apache-2.0. Utgivarnas fulla [Qwen-licens](https://raw.githubusercontent.com/QwenLM/Qwen-Image/main/LICENSE) och [Wan-licens](https://raw.githubusercontent.com/Wan-Video/Wan2.2/main/LICENSE.txt) medger användning, bearbetning och distribution utan ett icke-kommersiellt förbud. Att köra dem själv för kommersiellt Abby-innehåll är därför förenligt med dessa modelllicenser, under deras villkor. Vid distribution av modell-/containerkopior bevaras licenstext, tillämpliga notices och ändringsmarkeringar. Detta ger inte rätt till någon annans referensbilder, röst eller varumärke.

Även [Comfy-Org Qwen-repack](https://huggingface.co/Comfy-Org/Qwen-Image-Edit_ComfyUI), [Wan-repack](https://huggingface.co/Comfy-Org/Wan_2.2_ComfyUI_Repackaged), [Qwen2.5-VL-7B](https://huggingface.co/Qwen/Qwen2.5-VL-7B-Instruct) och [UMT5-XXL](https://huggingface.co/google/umt5-xxl) anger Apache-2.0. Repack-metadata ersätter inte filvis ursprungskontroll. Hugging Faces direkta LICENSE-länkar för de två basmodellerna gick inte att läsa med webbverktyget; fulltexten ovan verifierades i utgivarnas officiella GitHub-repon och kopplades till modellkortens licensangivelse.

[ComfyUI-koden](https://github.com/Comfy-Org/ComfyUI/blob/master/LICENSE) har GPL-3.0, en separat licens från vikterna. Kommersiell körning är tillåten; eventuell distribution av en image med programmet kräver att relevanta GPL-villkor följs. Basimage, CUDA/PyTorch och övriga beroenden ska dokumenteras vid låsning av den faktiska imagen. **Ingen komplett container har ännu licens- eller kompatibilitetsverifierats.** Detta är en kvarvarande startkontroll, inte ett skäl att anta ett generellt kommersiellt förbud.

### Exakt underlag Marcus ska ordna

Följande är föreslagna arbetskopienamn, inte upptäckta filer eller nya krav på att döpa om original. Lämna godkända kopior i en separat lokal katalog utanför Git, exempelvis `~/ContentEngineMedia/abby/ce01/`, och ange dess faktiska sökväg. Originalmapparna ska inte ändras. Vid inventeringen hittades inga bild-/ljudmedia i karaktärsoriginalmapparna; eventuella filer på andra platser behöver pekas ut.

| Arbetskopia | Krav och användning |
|---|---|
| `abby-face-front.png` | Skarpt godkänt vuxet ansikte framifrån, utan filter/text; primär T1-referens |
| `abby-face-threequarter.png` | Samma godkända person i trekvart, för identitetskontroll under vridning; även T3-bildreferens om lämplig |
| `abby-body-front.png` | Samma person i neutral helkropp, synliga proportioner/händer; primär T2-referens |
| `references.md` | Verkligt ursprung, datum, rättighetsunderlag, vilken bild Marcus godkänt och eventuell tillåten användningsbegränsning per fil; kopior får SHA-256 före uppladdning |
| `abby-voiceover.wav` + `voiceover.txt` | Marcus färdiga godkända röst och exakt transkript, cirka 15–20 s, för senare monteringsprov. Inte krav för det första ljudlösa bild-/rörelseprovet |

R: minst cirka 1024 px på långsidan för bilder, ingen kollagebild med flera identiteter. Godkänn en enkel gemensam outfit och fiktiv terrassmiljö från paketets stil. Om identitetsreferenserna saknas måste de skapas/godkännas i separat definierat arbete; en redigeringsmodell eller textbeskrivning räknas inte som en redan godkänd identitet.

**Konton:** Marcus behöver ett eget [RunPod-konto](https://console.runpod.io/) med betalning först efter godkänt testtak, och tillgång till sin lokala SSH-nyckel (bara publik nyckel registreras i kontot). [Officiell SSH-guide](https://docs.runpod.io/pods/configuration/use-ssh). Hugging Face-konto/read-token ordnas endast om en vald fil kräver autentisering; publika vikter innebär inte krav på betald HF-inferens. Inget Comfy Cloud-abonnemang, socialt konto, separat medie-API-konto eller containerregister behövs för första interaktiva sessionen. Privat register kan behövas vid senare paketering. Klistra inte in hemligheter i chatt eller dokument.

**Inställningar vid ett senare godkänt starttillfälle:** Pods, on-demand (inte spot/serverless), en GPU enligt tabellen, inga extra repliker, minst 100 GB RAM, föreslaget 30 GB containerdisk + 150 GB volym på `/workspace`. Välj datacenter efter faktisk tillgång inom pristaket. Använd granskad container med stödd NVIDIA/PyTorch-miljö; lås dess digest och ComfyUI-commit före generering. Ange ingen image som “testad” innan den startats. ComfyUI nås via SSH-tunnel till port 8188; exponera inte en oskyddad publik ComfyUI-port. Ingen automatisk påfyllning av kontot. Följ pris, starttid och nedstängning i konsolen; en webbläsarflik som stängs stoppar inte GPU:n.

### Testkort, försök och kvalitetsgrind

R: experiment `ce01-openweights-01`, **högst 300 SEK i total faktisk utgift**, varav planerad resursförbrukning högst 200 SEK och 100 SEK reserv för avgifter/fördröjning. Detta är ett nytt mindre förslag, inte tidigare 1 500-kronorsramen och inte en godkänd betalning. Kontopåfyllning och eventuell oanvänd kredit redovisas separat från resurskostnad men måste också rymmas inom godkänt kassautflöde. Ingen API-jämförelse ingår i dessa 300 kr; sådan beställs separat om vi behöver en extern kvalitets-/kostnadsreferens.

1. **Bildprov:** T1–T3 nedan, en bild per scen och högst ett korrigerat omtag per scen: maximalt sex bildförsök. Använd paketets godkända identitet och samma stil. Spara seed 101/102/103 för basförsöken, ändra endast ett dokumenterat fel i omtaget. Marcus måste ge bilden identitet ≥4/5 och inga hårda fel innan video får skapas.
2. **Videoprov:** tre godkända scenbilder, ett klipp per bild och högst ett omtag per scen: maximalt sex klippförsök. R: 121 frames vid 24 fps, ungefär 5 s, vertikalt 704×1280 som första native-prov. Dessa frame-/samplerinställningar är testparametrar, inte verifierad optimal preset. Behåll officiella mallens sampler/scheduler/steps/CFG vid första körning och registrera faktiska värden innan Run; inga Lightning-LoRA. Om vald nod avvisar formatet stoppas körningen för rättning, inte tyst byte av modell.
3. **Helhet om tre scener godkänns:** montera cirka 15 s av de tre klippen, ren master och separat export. 704×1280 är inte exakt 9:16: prova uttrycklig beskärning till 704×1252 före export till 1080×1920 och logga beskärning/uppskalning. Granska att ansikte/händer inte beskärs. Röst läggs endast till om Marcus levererat godkänt ljud. Utan ljud är detta ett rörelseprov, inte ett godkänt voiceoverformat eller full MVP.

| Scen | Bildbrief – illustrativ Abby-tillämpning | Rörelseprompt för Wan |
|---|---|---|
| T1 | Ansiktsnära på fiktiv kustterrass, samma godkända ansikte, mjukt morgonljus, paketets creme/korallstil | “Small natural head turn and relaxed expression. Locked camera. Preserve face, hair and clothing. Mouth at rest, no speaking.” |
| T2 | Helkropp på samma terrass i samma outfit, realistiska proportioner, inga andra personer | “Two slow natural steps, then settle. Static camera, consistent face and body proportions. No speaking, no wardrobe changes.” |
| T3 | Halvnära sittande vid kopp, händer lugnt synliga, samma ljus/outfit | “Gentle breathing and a subtle glance. Hands remain still beside the cup. No lifting, no extra people, no visible speech.” |

Bildpromptens grund: “Use the approved reference as the same fictional adult character. Preserve identity and proportions. Create [bildbrief]. Follow the supplied character style. Natural skin and lighting, no text or logos.” Referensen ges via bildingång, inte enbart genom namn i prompten. Bildomtag får inte ändra identiteten för att få en lättare video.

Grind: varje använt klipp ska nå ≥4/5 för identitet, rörelse/händer och kontinuitet, utan hårda fel enligt rubric nedan. Marcus ser hela klippet i normal fart och granskar avvikande frames. Pilotens mål är minst två av tre scener godkända inom sina två försök; tre krävs för monteringsprovet. Sex lyckade enskilda försök räknas inte som sex unika scener. Testa ljud/manus separat vid helhetsprovet. Två identiska hårda fel i en scen avslutar scenen. En OOM avslutar försöket; en dokumenterad minnesjustering kan göras inom samma försöks-/tidsram, aldrig obegränsade omstarter.

### Interaktiv session först, automatisk container därefter

**Före debiterad start:** frys referenser, samtliga fil-/licenslänkar, containerkandidat, ComfyUI-version och testkort; verifiera faktisk prisbild och budget. Inga sådana tjänster startas nu. [RunPods mallguide](https://docs.runpod.io/pods/templates/create-custom-template) beskriver hur containerimage och startinställningar kopplas till Pod; faktisk image-digest och kompatibilitet återstår att kontrollera i körningsförberedelsen.

**Session med Marcus när den uttryckligen beställts:** öppna ComfyUI interaktivt, ladda den officiella Qwen-mallen och dess filer, ta bort/bypassa eventuell valfri Lightning-gren och använd basmodellens inställningar. Anpassa enbart referens, prompt och testformat. Mät kallstart, nedladdning och modellinläsning. Kör högst sex bildförsök; avlasta Qwen innan Wan laddas. Ladda native Wan 5B I2V, använd endast godkända bilder och följ testkorten. Pausa för granskning först efter att GPU-kostnaden noterats; GPU som är idle är fortfarande hyrd.

**Tidsstopp:** högst fyra debiterade GPU-timmar totalt inklusive start, hämtning, laddning, felsökning och framtida verifierande omstart. Fördela högst tre timmar till första sessionen och reservera en till verifiering från ren miljö om kvaliteten räcker. Stoppa tidigare vid planerad resursförbrukning 200 kr eller risk att nästa försök inte ryms. Börja stänga ned i god tid före gränsen; detta är en övervakad manuell pilot, inte ett implementerat automatiskt kostnadstak. Om installation/laddning inte ger körklar miljö inom 45 minuter avslutas sessionen med felrapport. Kvarvarande lagring måste räknas även efter stopp.

**Efter godkänd bild/rörelse, inom separat tillåtet paketeringsarbete:** spara UI-workflow JSON och API-format, ComfyUI-commit, alla nodversioner, Python/PyTorch/CUDA-versioner, basimage-digest, exakta modellrevisioner/hashar och en dependency-/licenslista. Bygg en reproducerbar image med granskade beroenden och startupkommando. Vikterna ligger i versionsstyrd modellmanifestlista och cachevolym; de måste inte bakas in i imagen. Återstarta rent och kör en redan räknad scen som reproduktionskontroll inom kvarvarande försöks-/tidsram. Spårbar jämförbar kvalitet krävs, inte bitidentiska pixlar.

Nästa automationssteg är samma container + API-workflow med in-/utdatafiler och status. [ComfyUI routes](https://docs.comfy.org/development/comfyui-server/comms_routes) dokumenterar `/prompt`, `/history` och `/ws`; ComfyUI:s prompt-ID är inte i sig en garanti om beständig exakt-en-gång-körning. Motorns framtida adapter kopplar detta till ProviderRequest, assetlagring och kostnadsjournal. Serverless-handler, autoskalning, kö och CPU-scheduler byggs först senare när kvalitet och körbar miljö är bevisade.

### Kostnadsblad för pilotens alla försök

RunPods [lagringstabell](https://docs.runpod.io/pods/storage/types) anger containerdisk 0,10 USD/GB/månad, volym 0,10 under körning och 0,20 när stoppad; nätverksvolym 0,07. Piloten väljer lokal volym, ingen nätverksvolym som default. Volymdata försvinner när Pod termineras. [Hantera Pods](https://docs.runpod.io/pods/manage-pods) beskriver stopp/terminering. Exportera resultat, manifest och workflows, kontrollera kopiorna och terminera därefter den tillfälliga Poden. En stoppad Pod med kvarvarande volym är inte kostnadsfri.

Illustrativ beräkning, inte offert: fyra timmar × visat 1,59 USD/h = 6,36 USD. Med 30+150 GB aktiva diskar i fyra timmar blir lagring cirka 0,10 USD vid förenklad 30-dagarsmånad. En dag med 150 GB stoppad volym tillför cirka 1 USD. Med gammal **antagen** kurs 10 SEK/USD blir detta cirka 74,60 kr före moms/avgifter. Faktisk kurs, pris, skatter och diskdebitering kontrolleras vid start; 300 kr är en stoppbudget, inte ett utlovat styckpris. Vid pristak 2 USD/h blir motsvarande kalkyl cirka 91 kr före påslag. Tidsramen garanterar inte att alla försök hinner slutföras.

Registrera session_id, start/stop/terminate-tid, GPU-typ/timpris, container/image/model/workflow-hashar, start/laddning/aktiv/idle/felsökningstid, peak VRAM/RAM, lagringsdygn och varje bild-/klippförsök inklusive misslyckanden och eventuell clean-start-repetition. Stängda/avbrutna försök försvinner inte ur kostnaden. Redovisa nedladdningstid även om viktfilen var gratis.

`total pilotkostnad per godkänt unikt klipp = (all GPU-hyra + lagring + överföring/övriga avgifter + eventuella externa testkostnader) / antal godkända unika scenklipp`. Bildgenerering och misslyckade video-/bildförsök ingår. Vid noll godkända anges total utgift och “ingen användbar styckkostnad”. Visa också kostnad per användbar sekund och, om helhetsvideo finns, kostnad per godkänd leverans. Summera sessionkostnaden en gång; fördela gemensam start/idle på scener med en redovisad metod, inte både som full sessionskostnad och en gång till per försök. Arbetstid för lärande/setup och aktiv redigering/granskning loggas separat; påstå inte att lägre GPU-utgift betyder lägre total ekonomisk kostnad.

### Modellbyte och eventuell API-jämförelse

Efter piloten kan samma godkända startbilder användas för ett färdigt API-prov med separat pris-/licensblad och budget. Jämför samma scenmål, använda sekunder, rubric och alla försök; API-spåret ska också bära sina bild-/röstkostnader eller tydligt dela en redovisad gemensam kostnad. Utan sådan jämförelse kan vi rapportera egen kostnad men inte påstå att egen drift är billigare.

Ny modell innebär nytt versionslåst ComfyUI-workflow och vid behov adapterversion: noder, VAE/encoder, promptstruktur, referensingångar, VRAM, längd/fps och outputformat kan ändras. Kör T1–T3 och ett rent omstartsprov igen, kontrollera ny licens/filproveniens och promotion/rollback enligt avsnitten nedan. Domänkontrakten består där det är möjligt; kompatibilitetsbrott kräver schemaändring. Ett modellbyte är planerat arbete, inte en garanterat friktionsfri filersättning.

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

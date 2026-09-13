# Status – Content Engine

Uppdaterad 2026-09-13 · [Projektstart](Start.md) · [Arbetssätt](../../../Marcus-och-Codex-Arbetssatt.md)

## Nuläge och beslut

Planriktningen är godkänd. Nytt **B6** prioriterar öppna bild-/videovikter i egen ComfyUI-container på hyrd GPU. Kontroll, kvalitet och lärande är mål; billigare produktion ska mätas. API-adaptrar behålls och text/röst väljs separat. Tidigare API-först-rekommendation är ersatt med bevarad historik i [Beslut och frågor](Beslut%20och%20frågor.md).

**CE-01:s kostnadsfria förberedelse är utförd** i befintlig [Utvärdering](Utvärdering.md): Qwen-Image-Edit-2511 → Wan2.2-TI2V-5B, officiella licens-/ComfyUI-/referenskällor, GPU-dimensionering, listpriser, konkreta filer/konton och T1–T3-testkort. Basmodellerna anger Apache-2.0 och medger avsedd kommersiell användning enligt villkoren. Hela runtime-miljön är ännu inte verifierad.

R: A100 PCIe 80 GB för första sessionen, max fyra GPU-timmar, sex bild- och sex klippförsök inklusive omtag/återstartsprov, föreslaget totalt kassautflödestak 300 SEK. Ingen GPU, installation, containerbuild eller generering har startats. Inga nya testkostnader har uppstått. Karaktärspaket är fortsatt inaktiva och original/röstunderlag orörda.

## Aktuellt fokus och referensgranskning

Marcus har avgränsat nästa arbete till Abby. Fyra befintliga bilder i hennes Base Pictures har granskats visuellt, alla 1024×1536: frontporträtt, snett porträtt, profil och sidovänd helkropp. Bedömning och exakta filnamn finns i [Utvärdering](Utvärdering.md). Frontporträttet är föreslaget ansiktsfacit; en neutral helkropp framifrån med båda händerna synliga rekommenderas före T2. Fler porträtt är inte blockerande för T1. Godkännande/ursprung och rättigheter är inte fastställda enbart av bildgranskningen.

300 kr har förklarats som föreslaget totalt utgiftstak för ett övervakat försök, inte ett köpt paket eller en garanti om tre färdiga filmer. Inget budgetgodkännande eller hyrtillstånd har lämnats i detta steg.

## Blockerare före betalt prov

Marcus behöver godkänna pilotbudgeten och bildreferenser med rättighetsunderlag enligt CE-02. Referenslistan i Utvärdering anger framifrån, trekvart, helkropp och arbetskopienamn. Marcus hanterar röstunderlaget själv; det behövs först för voiceover-/helhetsprovet, inte första ljudlösa rörelsetestet. RunPod-konto/betalning och publik SSH-nyckel ordnas av Marcus inför ett uttryckligen godkänt startuppdrag.

Codex återstående startkontroller: exakt container-digest, ComfyUI-/modellrevisioner och filhashar, basimage-/beroendelicenser, faktisk GPU-tillgång och pris i vald konfiguration. Qwens exakta VRAM-krav för flödet saknar fast officiellt minimum; 80 GB är en rekommendation, peak-minne/tid mäts i piloten. Dokumenterat native-stöd är inte en genomförd kompatibilitetstest. Inga påhittade image-ID eller referenshashar fyller luckorna.

## Nästa uppgift

Granska pilotplanen i Utvärdering och hantera **CE-02** samt återstående CE-01-startkontroller. Därefter krävs ett uttryckligt uppdrag för **CE-03**: hyr tillfälligt, testa interaktivt och avbryt enligt taket. Vid godkänd kvalitet paketeras den fungerande miljön och provas från ren start inom kvarvarande eller nytt godkänt utrymme. Full serverless-/motordrift kommer senare. CE-10 ligger fortsatt före CE-06/CE-09 och avser workflow-/köprototyp, inte bildmodelltestet.

## Verifiering och Git

Officiella webbkällor avlästa 2026-09-13; källor och verifieringsgränser står vid respektive påstående i Utvärdering. Kontrollerat: 71 lokala länkar, 27 backlog-ID utan cykler och 7 oförändrade filer i de skyddade originalkatalogerna. Whitespace-kontrollen är utan anmärkning. Ingen uppmätt klippkvalitet, faktisk GPU-kostnad eller runtime-prestanda finns ännu.

Historiskt: teknikplanens startcommit var `96ce10c` (`update info`). Vid denna bildgranskning var arbetskatalogen ren; uppdateringarna av Utvärdering och STATUS är inte committade. Kontrollera Git-status inför återupptagning.

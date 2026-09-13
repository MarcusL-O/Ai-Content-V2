# Inventering och överlämning

[Projektstart](Start.md) · Inventerat och konsoliderat 2026-09-12.

## Vad som fanns

Det faktiska Obsidian-valvet är `Second brain/Second Brain`, med `.obsidian`, `Agents` och `Karaktärer`. Den nya sammanhängande planen ligger i valvets `Content Engine`. Ingen ytterligare Second Brain-mapp har skapats. Briefen låg vid inventeringen en nivå ovanför valvet och finns nu i reporoten: [Content-Engine-Codex-Brief](../../../Content-Engine-Codex-Brief.md).

Läst underlag: användarens fullständiga bilaga, hela briefen, samtliga 13 Markdownfiler i docs, fyra filer i äldre character-packs, fyra karaktärsoriginal och nio befintliga rollanteckningar under Agents. Den enda befintliga AGENTS.md som hittades i projektet var docs/AGENTS.md; den var en kort rollskiss och ingen fullständig rotinstruktion. Inga AGENTS.md hittades i kontrollerade överordnade kataloger. En ny rot-AGENTS.md dokumenterar arbetsomfattning och exakta skyddade originalvägar enligt briefen.

Vid start hade Git sex redan raderade spårade anteckningar. Dessa har inte återställts eller ersatts på samma sökväg:

- `Second brain/Second Brain/00 Start/Översikt.md`
- `Second brain/Second Brain/01 Verksamhet/Om mig.md`
- `Second brain/Second Brain/01 Verksamhet/Vision och plan.md`
- `Second brain/Second Brain/03 Innehåll/Idéer och produktion.md`
- `Second brain/Second Brain/Arbetsätt till färdig video.md`
- `Second brain/Second Brain/To-Do.md`

Briefen, docs och character-packs var ospårade vid start. Under dokumentationsetappen gjordes ingen Git-stage, commit, push eller ändring av deras innehåll. Efterföljande rensning beskrivs nedan. Raderade anteckningar har inte behandlats som aktuellt källunderlag eller hämtats tillbaka från Git.

## Vad som ersätter tidigare utkast

Filerna i docs och character-packs bevarades byte för byte under dokumentationsetappen. På Marcus efterföljande uppdrag att ta bort felaktiga äldre filer raderades dessa 17 ersatta utkast och deras tomma kataloger. Före raderingen verifierades att filerna inte hade ändrats sedan inventeringen. Tabellen är fortsatt den historiska ersättningskartan.

| Tidigare fil relativt reporoten | Nytt huvuddokument i valvet |
|---|---|
| `docs/VISION.md`, `docs/MVP.md` | [Vision och MVP](Vision%20och%20MVP.md) |
| `docs/ARCHITECTURE.md` | [Arkitektur](Arkitektur.md) |
| `docs/AGENTS.md` | [Agenter](Agenter.md), produktionsroller; rotens AGENTS.md styr Codex |
| `docs/WORKFLOWS.md` | [Workflows](Workflows.md) |
| `docs/CHARACTERS.md` | [Karaktärspaket](Karaktärspaket.md) |
| `docs/EVALUATION.md` | [Utvärdering](Utvärdering.md) |
| `docs/COSTS.md` | [Drift och kostnader](Drift%20och%20kostnader.md) |
| `docs/DECISIONS.md`, `docs/OPEN-QUESTIONS.md` | [Beslut och frågor](Beslut%20och%20frågor.md) |
| `docs/ROADMAP.md`, `docs/TODO.md` | [Roadmap och backlog](Roadmap%20och%20backlog.md) |
| `docs/HANDOFF.md` | Detta dokument samt [Start](Start.md) |
| `character-packs/abby/manifest.yaml`, `character-packs/abby/persona.md` | [Abby Paket](Karaktärspaket/Abby/Paket.md) och [manifest](Karaktärspaket/Abby/manifest.json) |
| `character-packs/mason/manifest.yaml`, `character-packs/mason/persona.md` | [Mason Paket](Karaktärspaket/Mason/Paket.md) och [manifest](Karaktärspaket/Mason/manifest.json) |

De nio ursprungliga Agents-anteckningarna bevaras som källbeskrivningar. Den operativa rollspecifikationen för denna motor ägs nu av Agenter. Skyddade karaktärsprofiler ersätts inte som kreativa original; nya paket är källspårade motoranpassningar. Briefen är kravunderlag, medan planeringsbeslut och detaljer framöver uppdateras i valvets huvuddokument.

## Identifierade brister som har hanterats

Äldre manifest hade sv-SE; nya följer en-US från båda huvudprofilerna. Gamla DECISIONS angav Python/FastAPI och GPU/ComfyUI som accepterade trots att briefen gav teknikförslag; nya registret skiljer uttryckliga beslut från rekommendationer. Gamla WORKFLOWS saknade tydligt videosteg och hade “budget rollback vid fel” samt idempotens genom hash: nya planen behåller förbrukad/okänd kostnad och beskriver journal, avstämning och idempotensens begränsning.

Gamla HANDOFF gick direkt mot backend/ComfyUI; nya planen börjar med ett begränsat produktionstest för att inte bygga runt obevisad kvalitet. Abby har ålderskonflikt och tom röstfil. Mason har Ethan-formuleringar och Abby-röst i Voice.md. Dessa är dokumenterade i paketen och F4/F5, utan omskrivna original eller påhittade lösningar.

## Efterföljande rensning

Rensningen omfattade endast de 13 gamla Markdownfilerna i docs och de fyra gamla paketfilerna i character-packs som listas i ersättningskartan. Briefen, nya projektplanen, rotens AGENTS.md, befintliga agentanteckningar och skyddade karaktärsoriginal behölls. Rotens arbetsregler uppdaterades för att återspegla rensningen. De sex redan raderade spårade anteckningarna lämnades orörda.

## Egen granskning och bevis från dokumentationsetappen

Före ändringar togs SHA-256 på 33 befintliga filer: docs, äldre paket, båda originalkatalogerna och nio rollanteckningar. Efter skrivningen kontrollerades att samtliga fanns kvar med samma hash. Baseline låg tillfälligt utanför projektet; detta är en kontroll av denna arbetsetapp, inte ett runtime-skydd eller påstående om Git-commit.

Genomförda kontroller:

- 13 nya Markdowndokument och två JSON-manifest i valvet; dessutom rotens AGENTS.md. Samtliga dokument innehåller projektspecifik substans och inga tomma ämnesmallar.
- 65 lokala Markdownlänkar och alla manifestens käll-/personareferenser löstes till befintliga filer.
- Sju fristående JSON-exempel parsades; båda JSON-manifesten parsades, har avstängt paket/schema och null i samtliga kostnadstak.
- Samtliga sju Abby-profilreferenser återfinns i agentdokumentet. Mason-profilerna är uttryckligen framtida olösta beroenden som blockerar aktivering.
- Kontraktskedjan granskades manuellt: ResearchBundle → ContentBrief → Script → ScenePlan → GenerationPlan → assets/Timeline → Review → PackageCopy. Kod ansvarar för verkliga asset-ID, tidsstämplar, filskrivning och status. Omslagskandidater extraheras vid montering och granskas före paketering.
- MVP, workflow och backlog innehåller både bild-till-video-steget och hela vägen till leverans; senare format och Jarvis ligger efter MVP.
- Kostnadsexemplens kurs, exkluderade poster och osäkerhet är synliga. Reservation är skild från debitering, och okänt utfall frigör inte pengar automatiskt.
- 33 befintliga filer hade oförändrad SHA-256. Git-status behåller samma sex ursprungliga raderingar och visar endast nya projektfiler utöver ursprungliga ospårade filer.

Kontrollerna avser dokumentstruktur, JSON-syntax och planens interna sammanhang. Inga runtime-scheman eller automatiska budget-/avbrottstester har genomförts. Mermaid-diagrammen är textgranskade men inte renderade i Obsidian under etappen. Modellkvalitet, drift och leverantörskostnader är inte uppmätta.

## Överlämning

Skrivet: produkt/MVP, teknikansvar/dataflöden, sju utförliga MVP-roller och fyra framtida stödroller med riktiga instruktioner och exempel, stegvis workflow med Abby-exempel, två källspårade inaktiva paket, utvärderingsplan, drift/kostnadsbok, besluts-/riskregister och 27 konkreta backloguppgifter. Rekommendationen är ett kort voiceoverformat, liten modulär motor, strikt avstämning av okända betalda anrop och versionslåsta konfigurationsexporter.

Marcus nästa beslut: experimenttak, godkänd Abby-identitet/röst och kvalitetsnivå; lös dessutom ålders-/namn-/röstkonflikter före berörd aktivering. Nästa genomförande är CE-01 i E1: kostnadsfri förregistrering och aktuell officiell kandidatverifiering, därefter godkänt begränsat produktionstest. Ingen tjänst behöver installeras eller köpas för att granska dokumentationen.

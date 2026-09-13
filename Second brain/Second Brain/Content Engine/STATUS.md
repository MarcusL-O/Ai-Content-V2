# Status – Content Engine

Uppdaterad 2026-09-13 · [Projektstart](Start.md) · [Arbetssätt](../../../Marcus-och-Codex-Arbetssatt.md)

## Nuläge

E0 är färdig som dokumentationsunderlag och planens riktning är godkänd. De fyra beställda förbättringarna är genomförda: karaktärsoberoende influencer-instruktioner, tidigare CE-10, arbetssättslänk/status och B4 med bevarad historik. Ingen motor, teknikprototyp eller verklig modellutvärdering har implementerats eller körts. Paketen är inaktiva.

Influencer-profilerna är 0.1.1; Abby-paketets version/hänvisningar har följt med. Persona och röstunderlag har inte ändrats. CE-10 är en begränsad planerad prototyp efter CE-05 och före CE-06/CE-09; den ska motivera ett val med simulerat trestegsflöde och högst en arbetsdag.

## Beslut och blockerare

[Beslut och frågor](Beslut%20och%20frågor.md) äger beslutsdetaljerna. B4 återger nu både ursprungligt bevarande och senare auktoriserad rensning. Godkänd planriktning innebär inte godkända inköp eller start av implementation.

Marcus hanterar röstunderlagen själv. Inför betald produktion behövs fortfarande dokumenterad budget, godkända referenser/röst och rättighetsunderlag samt fastställda testkriterier enligt CE-02/F1–F5. Dessa hindrar inte kostnadsfri testförberedelse. Ingen originaländring eller betalning ingår i nuvarande uppdrag.

## Verifiering och Git

Lokal länkkontroll, profilreferenser, JSON-syntax och backloggens beroendegraf har kontrollerats efter ändringarna. Alla beroende-ID finns, inga cykler finns och CE-10 föregår beroende implementation. Karaktärsoriginalens filhashar är oförändrade. Ingen runtime- eller modellkvalitet har testats.

Dokumentändringarna och denna statusfil är ännu inte committade. Vid uppdragets start fanns redan en raderad `Second brain/Content-Engine-Codex-Brief.md` och en ospårad `Content-Engine-Codex-Brief.md` i reporoten; flytten är bevarad och projektets länkar har anpassats. Senaste befintliga commit vid kontroll: `1144521` (`info`); den innehåller inte denna revision. Kontrollera alltid aktuell Git-status vid återupptagning.

## Nästa uppgift

**CE-01 – förregistrera experiment och verifiera kandidater**, efter ett nytt uppdrag att börja nästa etapp. Läs [Utvärdering](Utvärdering.md), [Workflows](Workflows.md) och CE-01 i [Roadmap och backlog](Roadmap%20och%20backlog.md). Leverera T1–T3-testbriefs, aktuella officiella kapabilitets-/pris-/villkorskällor och en kostnadsplan med maxförsök och synliga spärrar. Kontrollera att hela planerade experimentet ryms i det tak Marcus beslutar innan någon beställning görs. Röstunderlag tas emot från Marcus; de skapas eller ändras inte av Codex i denna uppgift.

# Marcus och Codex – arbetssätt för Content Engine

Version 1.0 • 2026-09-12

Detta dokument kompletterar Content-Engine-Codex-Brief.md och projektplanen i Second Brain. Det beskriver hur vi samarbetar, inte en ny produktarkitektur. Befintliga skyddsregler för Abby och Mason gäller fortsatt.

## 1. Nästa uppgift till Codex

När den pågående dokumentationsetappen är färdig ska du genomföra följande arbete. Avbryt inte pågående arbete för att skapa en konkurrerande plan.

1. Läs detta dokument, projektunderlaget och dokumentationen du har skapat. Kontrollera befintliga AGENTS.md och Git-status.
2. Placera detta arbetssätt i rätt projektmapp i det faktiska Obsidian-valvet Second Brain och länka från projektets startsida. Om motsvarande dokument redan finns: komplettera det varsamt i stället för att skapa en dubblett.
3. Granska planen mot Marcus uttalade mål. Identifiera luckor, motsägelser, outredda antaganden och onödig komplexitet. Fyll själv i konkreta tekniska förslag där underlaget räcker.
4. Skilj frågor som kräver Marcus beslut från frågor du kan utreda. För varje fråga till Marcus: ange varför svaret behövs, ditt rekommenderade alternativ och vad valet påverkar. Besvara inte hans personliga preferenser eller budgetbeslut åt honom.
5. Skriv en prioriterad backlog enligt avsnitt 4. Detaljera närmast kommande etapp så att den går att genomföra. Beskriv senare etapper utan att låsa alla implementationsdetaljer i förtid.
6. Gör det tidiga produktionstestet till en tydlig uppgift: visa om vi kan skapa användbart Abby-innehåll med rimlig kostnad innan hela motorn byggs.
7. Skapa en aktuell status-/överlämningsanteckning enligt avsnitt 8.
8. Avsluta med vad du ändrat, de beslut Marcus behöver ta och en konkret rekommendation om nästa etapp.

**Denna uppgift godkänner dokumentationsarbete. Den godkänner inte produktionsimplementation, installationer, betalda anrop, nya konton, driftsättning eller publicering.** Gör dokumentationen färdig och granskningsbar innan du lämnar över. Fråga inte om lov för varje vanlig dokumentändring inom uppgiften.

## 2. Roller

### Marcus – produktägare och kvalitetsansvarig

Marcus bestämmer vision, prioriteringar, kreativa preferenser, kostnadsram och när en etapp ska börja. Han bedömer om karaktärer och videor håller avsedd kvalitet och fattar beslut om publicering och externa åtaganden.

Marcus skapar vid behov konton, godkänner tjänstevillkor och betalning samt lägger in API-nycklar genom tjänsternas och projektets avsedda funktioner. Codex ska ge tydliga instruktioner när en sådan insats behövs.

Marcus behöver inte detaljstyra varje kodrad. Uppdraget ska ange önskat resultat och begränsningar; Codex ansvarar för att föreslå och utföra lämplig implementation inom uppdraget.

### Codex – utvecklare och teknisk samarbetspartner

Codex läser projektets dokumentation, föreslår teknik, skriver och ändrar kod, genomför relevanta tester, felsöker och uppdaterar dokumentationen. Codex får ifrågasätta beslut med konkreta skäl och alternativ.

Codex ska inte låtsas att ett test är genomfört, ett API fungerar eller en kostnad är verifierad om det saknas evidens. Skilj mellan rekommendation, implementation, simulering och verklig verifiering.

Codex slutför auktoriserade uppgifter självständigt. Om en extern åtgärd saknas ska Codex färdigställa det som kan göras säkert utan den och lämna en specifik instruktion till Marcus. Installera inte extra verktyg eller byt ramverk utan koppling till uppgiftens behov.

### Chatten på webben – andra granskning

Marcus kan dela aktuella dokument, ändringar och resultat här för att granska riktning och tekniska antaganden. Webbchatten har inte automatiskt åtkomst till den senaste lokala kodbasen eller Codex-sessionen.

Beslut från webbchatten förs tillbaka till projektets dokumentation. Dokumentationen i repot är den gemensamma aktuella planen. En rekommendation i en separat chatt är inte automatiskt ett godkänt projektbeslut.

## 3. Från plan till utveckling

### A. Granska planen

Kontrollera att vision, MVP, workflows, karaktärspaket, teknik, budget och roadmap beskriver samma produkt. Varje viktig osäkerhet ska ha ett test, ett beslut eller en tydlig framtida avgränsning.

Samla frågor i tre grupper: krävs före nästa etapp, kan avgöras under implementation och kan vänta. Undvik att blockera dokumentation på sådant som först behövs inför drift.

### B. Testa produktionskvaliteten tidigt

Genomför efter godkänd budget ett litet jämförande test av bilder, röster och videor med godkända referenser. Mät alla försök, inte bara lyckade generationer. Marcus bedömer identitet, rörelser, röst och om slutresultatet är användbart.

Om produktionen inte håller: justera format, referenser eller modeller. Fortsätt inte bygga hela automatiseringen utifrån ett obevisat kvalitetsantagande.

### C. Implementera avgränsade etapper

Varje etapp ska ange omfattning, leverans, tester, beroenden och stoppvillkor. Codex arbetar igenom etappen och rättar relevanta fel, utan att be Marcus besluta om rutinmässiga kodval.

Utveckla med simulerade leverantörer där det är lämpligt. Det får inte beskrivas som verifierad riktig API-integration. Om ett externt system saknas, ange vad som återstår innan integrationen är klar.

### D. Granska och dokumentera resultatet

Efter varje etapp gör Codex en egen granskning av ändringarna och redovisar resultat. Marcus granskar beteende och relevanta förändringar. Därefter sparas en fungerande Git-version enligt aktuell tillåtelse för commits. Push och driftsättning hanteras separat och sker bara inom uttryckligt godkänt uppdrag.

## 4. Backlog: user stories och tekniska uppgifter

Använd user stories för funktioner med tydligt användarvärde. Använd tekniska uppgifter för infrastruktur, integration och tester där en user story blir konstlad. Båda måste vara konkreta.

Varje uppgift innehåller:

| Fält | Innehåll |
| --- | --- |
| ID och titel | Stabilt ID, exempelvis CE-010 |
| Syfte | Problemet och nyttan |
| Omfattning | Vad som ska ingå och relevanta avgränsningar |
| Beroenden | Uppgifter, beslut eller externa resurser som behövs |
| Genomförande | Föreslagna tekniska steg och berörda komponenter |
| Acceptanskriterier | Observerbara villkor för godkänt resultat |
| Verifiering | Vilka tester eller manuella kontroller som behövs |
| Extern insats | Vad Marcus behöver ordna, om något |
| Kostnad | Krävs betalda tester? Budget måste i så fall godkännas |
| Status | Ej startad, pågår, blockerad, redo för granskning, klar |

### Exempel: CE-010 – validera ett inaktivt karaktärspaket

Som skapare vill jag kunna kontrollera ett nytt karaktärspaket innan det aktiveras, så att felaktiga inställningar inte startar produktion.

Genomförande:

1. Utgå från dokumenterat paketschema och skilj utkast från aktiverbar konfiguration.
2. Validera ID, version, profilreferenser och mediereferenser.
3. Lägg till aktiveringskontroll för obligatoriska budget- och leverantörsfält.
4. Ge tydliga felmeddelanden med fält och åtgärd.
5. Exponera kontrollen via projektets valda CLI eller API.

Acceptanskriterier:

- Ett korrekt utkast kan läsas och kontrolleras utan att starta jobb.
- Saknade uppgifter rapporteras tydligt.
- Aktivering blockeras när obligatoriska krav saknas.
- Inga karaktärsoriginal skrivs till och inga betalda anrop sker.

Verifiering: testfall för giltigt utkast, ogiltig profilreferens, saknad budget vid aktivering och bevarande av originalfiler. Detta är ett exempel; anpassa det till den fastställda arkitekturen.

## 5. Tester under hela arbetet

Tester kommer löpande, inte enbart efter att hela systemet skrivits.

- Funktionstester för viktig logik: validering, budget och tillståndsövergångar.
- Integrationstester för databas, kö, leverantörsanslutningar och export.
- Återhämtningstester för avbrott, okända API-utfall och återupptagning.
- Begränsade riktiga API-tester när de har en godkänd kostnadsram.
- Mänsklig kvalitetsbedömning av genererat innehåll.

Prioritera risker som dubbla betalda beställningar, överskriden budget, ändrade original och felaktig återstart. Vanliga lokala tester ska använda simulerade svar och inte förbruka krediter av misstag.

Ett grönt kodtest bevisar inte att Abby ser naturlig ut. En snygg video bevisar inte att schemat eller budgetkontrollen fungerar. Båda behöver verifieras.

Skriv inte tester som bara upprepar implementationen eller för varje låg-risk-dokumentändring. Beskriv vad testet faktiskt visar och vilka begränsningar som återstår.

## 6. När Marcus behöver göra något

Ge en konkret instruktion med:

1. Vad som behövs och varför.
2. Vilken tjänst och officiell sida som avses.
3. Vilken inställning eller behörighet som behövs, så begränsad som möjligt.
4. Vilken kostnad eller gräns som gäller, om verifierad; annars markera osäkerheten.
5. Var uppgiften ska konfigureras lokalt, exempelvis namnet på en miljövariabel.
6. Hur vi verifierar att det fungerar utan att visa hemligheter.
7. Vilken uppgift som kan fortsätta efteråt.

Begär inte att Marcus klistrar in nycklar i chatten. Lägg bara ofarliga exempel i .env.example. Hemligheter ska hållas utanför Git, dokumentation, skärmbilder och loggar. Ett utvecklingsabonnemang ska inte antas betala för motorns externa API-anrop.

## 7. Klart-definition och rapport efter varje etapp

En uppgift är klar när acceptanskriterierna uppfyllts och den relevanta verifieringen genomförts. Om en riktig integration ännu inte testats, beskriv exakt vad som är implementerat och vad som återstår.

Rapportera kort:

- Vad som fungerar nu och varför ändringen gjordes.
- Vilka centrala filer/komponenter som ändrats.
- Vad som testats och resultatet.
- Vad som är simulerat, overifierat eller blockerat.
- Eventuell faktisk testkostnad eller tydligt markerat estimat.
- Vad Marcus behöver göra.
- Nästa rekommenderade uppgift.

Koppla resultatet till backlog-ID. Uppdatera berörd dokumentation så att den beskriver verkligheten, inte bara den gamla planen.

## 8. Fortsätta nästa dag eller i en ny Codex-chatt

Skapa och håll aktuell en kort STATUS.md på projektets dokumentationsplats. Den ska innehålla:

- Aktuell etapp och senast avslutade uppgifter.
- Pågående arbete och relevanta osparade Git-ändringar.
- Senaste verifiering och kvarvarande fel.
- Nya beslut och länkar till deras motiveringar.
- Externa beroenden och blockerare utan hemligheter.
- Exakt nästa uppgift och hur den startas/verifieras.
- Senaste relevanta commit om sådan finns; hitta inte på ett ID.

Spara kod och dokument löpande. Förlita dig inte på att en viss chatt eller modell minns allt. Inför återupptagning läser Codex AGENTS.md, STATUS.md, TODO och relevanta beslut, kontrollerar arbetskatalogen och fortsätter därifrån. Redan godkända beslut ska inte tas om utan nya skäl.

## 9. Principer som gäller genom hela projektet

- Planen är gemensam, men Marcus fattar produkt- och investeringsbeslut.
- Codex ska vara aktiv, kritisk och konkret; inte bara instämma eller skriva platshållare.
- Ändra inte Abby-/Mason-originalen. Separata motorpaket får utvecklas inom godkänt uppdrag.
- Håll produktionskod, planer och verkligt testresultat tydligt åtskilda.
- Välj nästa arbete efter beroenden och största osäkerheten, inte efter vad som är enklast att generera kod för.
- En token-/användningsgräns ändrar inte uppgiftens status. Dokumentera det verkliga läget så nästa session kan fortsätta.
- Utöka inte scope tyst. Föreslå större ändringar med konsekvenser.
- En bra etapp lämnar både fungerande resultat och tillräckligt med dokumentation för nästa steg.

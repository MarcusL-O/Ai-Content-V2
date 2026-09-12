
**1. Bestäm namn och reservera sociala konton**

Skapa TikTok, Instagram och YouTube för Abby och Ethan.

- Kontrollera användarnamnen och välj helst samma på alla plattformar.
- Ordna inloggningsmejl och tvåfaktorsautentisering.
- Lägg in bio från karaktärsfilerna.
- Beskriv dem tydligt som virtuella AI-kreatörer.
- Spara profiladresserna i Obsidian.

Profilbilderna lägger du in efter nästa steg. Du behöver inte börja publicera direkt.

**Klart när:** båda karaktärerna har sina konton och du kan logga in.

**2. Skapa och lås deras utseenden**

Börja med **Abby**, gör klart hennes referenser och upprepa sedan för Ethan.

Skapa:

- Ett huvudporträtt.
- En bild i trekvartsvinkel.
- En helkroppsbild.
- Några uttryck, exempelvis neutralt och leende.

Utgå från den godkända huvudbilden när du skapar resten. Spara bilderna och instruktionerna som gav bra resultat i Obsidian.

**Klart när:** du tycker att bilderna föreställer samma person och vill behålla det utseendet.

**3. Testa video och röst innan du producerar mycket**

Karaktärerna behöver lite olika produktion:

|Karaktär|Första test|
|---|---|
|**Abby**|En kort scen där hon rör sig naturligt i en outfit eller semestermiljö|
|**Ethan**|En talande introduktion, följd av en riktig skärminspelning av din Second Brain|

Jag skulle testa **Runway för Abbys bild-till-video** och **HeyGen för Ethans talande avatar**. Båda har API:er, vilket gör dem möjliga att koppla till produktionen senare. [Runway](https://docs.dev.runwayml.com/guides/using-the-api/?utm_source=chatgpt.com), [HeyGen](https://www.heygen.com/api-pricing?utm_source=chatgpt.com)

Välj och spara ett röstprov samt tjänstens röst-ID när du hittar rätt. Abby kan börja med talfria klipp.

**Klart när:** du har en användbar testvideo per karaktär och vet ungefär hur många försök den krävde.

**4. Gör tre riktiga inlägg per karaktär**

Använd mig som Ronny manuellt: lämna karaktärsfilen och be om idéer, manus och scener. Sedan producerar du med bild- och videoverktygen.

Förslag:

|Abby|Ethan|
|---|---|
|Presentation av hennes virtuella värld|Presentation av vad kanalen lär ut|
|Rolig outfit- eller packningsvideo|Så organiserade du din Second Brain|
|Två looks som publiken får välja mellan|Så skapade du Abbys första bild/video|

Spara för varje inlägg: **idé, instruktioner, referenser, verktyg, slutfil, kostnad och vad du rättade**. Det blir underlaget till agenterna.

**5. Publicera manuellt och samla återkoppling**

Publicera i en takt du kan hålla. Anpassa text och märkning för varje plattform.

Registrera:

- Vad folk tittar på och reagerar på.
- Vilka frågor de ställer.
- Vad de sparar eller delar, när statistiken finns.
- Vilka delar av produktionen som tar mest tid.

Du behöver inte vänta på många följare för att börja automatisera. **Det viktiga är att du kan upprepa produktionen med acceptabel kvalitet och kostnad.**

**6. Bygg Ronny i n8n Cloud**

**n8n blir programmet där vi bygger dina arbetsflöden.** Mitt förslag är Cloud-versionen i webbläsaren, så att vi slipper börja med serverinstallation på din äldre Mac.

Ronny får först ett enkelt flöde:

1. Du väljer **Abby eller Ethan** och antal idéer.
2. Flödet hämtar rätt karaktärsprofil.
3. En AI-modell får profilen, Ronnys instruktioner och tidigare idéer.
4. Den lämnar idéer och kompletta produktionsförslag.
5. Förslagen sparas för din granskning.

Här börjar du använda **AI via API**, med separat användningskostnad. Du behöver inte ett eget abonnemang för varje agent.

**En viktig detalj:** n8n Cloud kan inte automatiskt läsa Obsidian-mappen på din Mac. Första testet kan använda profiltext som du klistrar in. Därefter lägger vi godkända profilkopior och referenser i en ansluten molnmapp, exempelvis Google Drive. Beständiga resultat sparas också där. [n8n om filåtkomst och lagring](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.readwritefile/?utm_source=chatgpt.com)

Obsidian är tills vidare originalet du redigerar. Vi dokumenterar när kopian som agenten använder uppdaterades.

**7. Bygg Vinny i n8n**

Vinny tar emot **ett godkänt produktionsförslag** från Ronny.

Flödet:

1. Hämta rätt profil och bildreferenser.
2. Skicka instruktionerna till bild-/video-API.
3. Kontrollera om jobbet är klart eller misslyckat.
4. Hämta och spara resultatet.
5. Visa dig filerna och kostnaden.

Börja med **en enda typ av produktion**, exempelvis en Abby-bild. Lägg sedan till video och därefter Ethans talande format. Samma Vinny kan välja olika produktionsvägar beroende på beställningen.

**8. Koppla ihop dem och lägg till schema**

När båda fungerar får du:

**Ronny föreslår → du godkänner → Vinny producerar → du granskar och publicerar.**

Nästa utveckling är att Ronny och Vinny producerar utkast på schema. Lägg då in kostnadstak, begränsade omförsök och stopp när kön är full. Automatisk publicering kan komma senare.

**Verktygen kommer alltså in stegvis:**

|När|Verktyg|
|---|---|
|**Nu**|Obsidian, ChatGPT och sociala konton|
|**Första produktionen**|Bildverktyg samt test av Runway/HeyGen|
|**Första agenten**|n8n Cloud och ett AI-API|
|**Automatisk medieproduktion**|Bild-/video-API och ansluten fillagring|
|**Senare**|Analys, schemaläggning och eventuell dashboard|
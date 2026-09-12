# Karaktärspaket

[Projektstart](Start.md) · Huvudregel B: originalen är skyddade; motorpaketen är separata och inaktiva.

## Exakta skyddade original

Sökvägarna nedan är relativa reporoten `/Users/marcuslis-olivebring/Desktop/Ai-ContentV2`. Skyddet gäller hela båda katalogerna, inklusive framtida media. Inga ändringar, flyttar, namnbyten eller raderingar gjordes i dem under denna etapp.

| Käll-ID | Exakt sökväg | Inventerad status |
|---|---|---|
| AB1 | `Second brain/Second Brain/Karaktärer/Abby Marlow/Basic Info.md` | Utförlig karaktärsprofil, en-US, vuxen fiktiv kvinna |
| AB2 | `Second brain/Second Brain/Karaktärer/Abby Marlow/Voice.md` | Tom fil; ger ingen röstinställning |
| MA1 | `Second brain/Second Brain/Karaktärer/Mason Hartley/Mason Hartley.md` | Utförlig utbildningsprofil, men Ethan förekommer i bio/prompt och flera stycken |
| MA2 | `Second brain/Second Brain/Karaktärer/Mason Hartley/Voice.md` | Beskriver Abby och kvinnlig röst; används inte som Mason-konfiguration |

Klickbara original: [Abby profil](../Karaktärer/Abby%20Marlow/Basic%20Info.md), [Abby röst](../Karaktärer/Abby%20Marlow/Voice.md), [Mason profil](../Karaktärer/Mason%20Hartley/Mason%20Hartley.md), [Mason röst](../Karaktärer/Mason%20Hartley/Voice.md).

AB1 anger både 25 år och födelsedatum 2000-05-05, vilket skulle innebära 26 år på planeringsdatumet. R: för generering används en tydligt vuxen person i mitten av 20-årsåldern; exakt ålder/födelsedag anges inte offentligt innan F4 avgjorts. MA1:s titel/frontmatter pekar på Mason; R: behåll Mason som paketnamn och behandla Ethan-formuleringarna som olösta källkonflikter, inte som ny karaktär eller alias. MA2 kopieras inte heller till Abby bara för att den nämner henne. Källfel dokumenteras utan att originalet rättas.

## Separata paket och fält

[Abby motorpaket](Karaktärspaket/Abby/Paket.md) och [Mason motorpaket](Karaktärspaket/Mason/Paket.md) innehåller verkligt källstödd persona, kreativa standarder, källproveniens och begränsningar. Varje katalog har ett [Abby manifest](Karaktärspaket/Abby/manifest.json) respektive [Mason manifest](Karaktärspaket/Mason/manifest.json). JSON är valt som enkelt strikt konfigurationsutkast; ingen runtime-loader finns ännu. Paket.md är den mänskligt redigerbara personainstruktionen som exporten senare låser med hash.

| Fält | Innebörd och aktiveringskrav |
|---|---|
| schema_version/id/version | Schema 1, stabilt internt character-ID, semantisk paketversion; samma version får inte få ny hash |
| enabled/status | false/draft i båda utkasten; active kräver validerad release och operatörsbeslut |
| source_documents | Faktiska relativa källsökvägar; inga genererade filer presenteras som original |
| identity/persona_file | Namn, språk, fictional_adult, osäker exakt ålder; persona från Paket.md |
| references.images | Godkända assets med ID, fil/objektreferens, sha256, datum, ursprung, rättighetsunderlag och approved_by/at |
| voice | Beskrivning + senare verklig provider/voice_id, godkänt sample och rättighetsunderlag; inga påhittade ID |
| agent_profiles | Roll → tillämpning/version; alla ska kunna lösas i aktuell release |
| production_profile/workflow | Versionslåst format respektive ordningsdefinition; Mason har framtida, ännu ej definierat workflow |
| schedule | Avstängt, Europe/Stockholm, klockslag null; takten är förslag, ingen aktivering |
| budget | SEK, max per jobb/dag/månad/experiment null; positiva gränser och godkännande måste fyllas i |
| continuity | Historikscope för just karaktären; kanonisk persona skild från producerade/fiktiva händelser och faktisk publicering |
| activation | Lista över olösta spärrar; bara kod kontrollerar att de verkligen har lösts |

Draft-validering ska tillåta null och kända framtida profilreferenser men rapportera varje aktiveringsspärr. Aktiv validering måste avvisa sådana luckor. `enabled:false` får aldrig automatiskt konverteras till true genom export eller migration. Referenser på disk valideras mot tillåtna rötter; symboliska länkar får inte kringgå läs-/skrivgränser. Inga kontolösenord, e-postinloggningar eller nycklar hör hemma i paketet.

## Godkänn referenser och behåll kontinuitet

R: godkänn först ett originalansikte, därefter framifrån, trekvart, profil, neutral helkropp, leende och neutral min som samma identitet. Första begränsade testet kan starta med mindre referensmängd om vald modell stöder det och Marcus godkänner identitetsgrunden; det ersätter inte full kontinuitetsutvärdering. Inga sådana assets upptäcktes i de skyddade originalkatalogerna.

Rösten provas på kort neutral text, humor och längre mening. Godkänt ljudprov, användningsrätt och faktisk voice-ID sparas innan TTS aktiveras. Numeriska leverantörsparametrar hålls null tills adapter och prov valts. Varje ny röstversion jämförs mot den godkända referensen.

Historiken lagrar berättelsekapitel, plats, klädsel och händelser separat från namn/personlighet. `produced`, `approved` och `published` är olika fakta. Ett övergivet manus får inte senare behandlas som Abbys publicerade resa. Idéagenten får senaste 30 relevanta poster och aktuellt kapitel, alltid för samma character_id. Ändrad kanonisk identitet kräver ny paketversion och operatörsbeslut.

## Lägg till en tredje karaktär

1. Skapa en ny katalog under Content Engine/Karaktärspaket med unikt stabilt ID, Paket.md och manifest.json kopierat som inaktiv struktur. Återanvänd inte någon annans källor eller asset-ID.
2. Fyll i originalkälla, fiktiv/vuxen identitet, namn, språk, personlighet, målgruppshypotes, ämnen, visuella fasta drag, gränser och källkonflikter. Ange vad som är eget förslag.
3. Ange godkända bildreferenser och röstprov med verkligt ursprung/rättigheter. Lämna saknade ID null och behåll aktiveringsspärr.
4. Välj befintliga roll-/produktionsprofiler och workflow om formatet passar. En ny persona kräver inte ny kärnkod. Ny medietyp eller nya kontraktsfält kräver däremot separat utvärderat profil-/schemaarbete.
5. Välj schema, tidszon, budget per jobb/dag/månad och försöksgränser. Fyll operatörsgodkännande. Kör draft- och aktiv validering, karaktärsisolering och fast kvalitetsprov innan export.
6. Exportera ny release utan att uppdatera gamla jobb. Bekräfta att historiken börjar tom för denna karaktär och att nya jobbet inte får Abby-/Mason-assets.

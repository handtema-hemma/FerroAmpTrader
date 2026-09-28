# Lönsamhet för 14 kWh Ferroamp-batteri + solceller (SE3, Tibber-kund)

Underlag för att bedöma hur du bäst ökar avkastningen på ditt befintliga
Ferroamp EnergyHub-system (14 kWh batteri, solceller, elområde SE3, Tibber
som elleverantör idag). Sammanställt 2026-09-28.

Alla belopp är hämtade från respektive leverantörs egna sidor eller
pressmaterial och märkta med källa. Där ett belopp är ett exempel/estimat
snarare än ett garanterat pris är det uttryckligen markerat.

## Bakgrund / vad triggade det här

Tibber ger idag bara smart elbilsladdning för den här installationen — inte
batteristyrning eller stödtjänster för Ferroamp. Det finns ingen "enkel
knapp" hos Tibber för att tjäna extra pengar på batteriet ännu.

## Sammanfattningstabell

| Alternativ | Funkar med Ferroamp idag? | Tillgängligt i SE3 nu? | Ersättning (bekräftat/exempel) | Krav / vad du ger upp |
|---|---|---|---|---|
| **Ferroamp/Ntricity via Varberg Energi ("Flex Plus"/"Flex Batteri")** | Ja | Ja, men just nu tar de bara emot intresseanmälningar för nya kunder (inte garanterad direktstart) | **10 kr/kW tillgänglig effekt/månad** (aktuellt pris, sep 2026). Tidiga ~700 pilotkunder 2024 uppgavs få "flera tusen kr/månad" — sannolikt från betydligt högre FCR-D-priser då | Måste teckna **elhandelsavtal med Varberg Energi** (byta bort Tibber som elleverantör). Du behåller ~70% av batterikapaciteten för eget bruk, 100% av effekten intecknas |
| **CheckWatt / Currently** | **Nej – ej kompatibelt med Ferroamp-växelriktare** | – | Exempel för kompatibla märken: snitt **1 607 kr/månad (~19 300 kr/år)** för 10 kW/10 kWh-batteri 2024. H1 2025-exempel: 1 290–4 230 kr beroende på tjänstekombination. 2025 uppges ligga lägre, ~8 000–15 000 kr/10 kWh/år | Kräver bytt växelriktarmärke (se "Byta system" nedan) |
| **Tibber Grid Rewards** | Nej, inte idag | Nej | Endast Homevolt/SAJ HS3/Huawei/Sigenergy m.fl. idag. "Alla integrerade batterier" utlovas sommaren 2026, men Ferroamp nämns inte i något källmaterial | Oklart om/när Ferroamp läggs till – bevaka, räkna inte med det |
| **Flower (Ellevio-ägt)** | Ingen bekräftad koppling | – | Stödjer bl.a. Sungrow, Solis | – |
| **FerroAI (Ferroamps egen spotprisstyrning)** | Ja, inbyggd | Ja | Gratis under introduktionsfas, blir abonnemang senare (pris ej offentliggjort) | Ferroamp avråder från extern styrning parallellt – oklart om FerroAI går att kombinera med Flex Batteri-avtalet (att verifiera med Ferroamp/Varberg Energi) |
| **DIY-spotprisarbitrage via Home Assistant** | Ja, via lokala MQTT ExtAPI (kräver att Ferroamp aktiverar ExtAPI/EMS) | Ja | Inga kända siffror/backtester – grovt estimat i storleksordningen några tusen kr/år för ett 14 kWh-batteri vid perfekt daglig styrning, kräver egen modellering för att verifieras | Eget tekniskt arbete, ersätter/konkurrerar med FerroAI, inget skyddsnät om logiken har buggar |
| **Byta system helt** (t.ex. SAJ HS3, Sigenergy) | Löser CheckWatt/Tibber-kompatibilitet | Ja | Se kalkyl nedan | Stor investering, tappar värdet i befintligt Ferroamp-system |

## 1. Ferroamp/Ntricity via Varberg Energi — mest konkreta steget idag

- Ferroamp + mjukvarubolaget Ntricity är godkända av Svenska kraftnät för
  FCR-D i SE3. Varberg Energi är den operatör som idag levererar tjänsten
  ("Flex Batteri"/"Flex Plus").
- **Aktuell ersättning (september 2026): 10,00 kr per kW tillgänglig
  batterieffekt och månad**, förutsatt 100 % uppkoppling.
  ([varbergenergi.se – Flex Plus](https://www.varbergenergi.se/privat/el/smarta-tjanster/flextjanster/flex-plus-maximerar-ditt-hembatteri))
- Du får betalt för **100 % av batteriets effekt** men behåller **~70 % av
  kapaciteten** för eget bruk.
  ([Effektpoolen](https://www.effektpoolen.se/post/checkwatt-batterier-vilka-modeller-ar-kompatibla))
- **Viktig brasklapp:** de första ~700 kunderna som anslöt 2024 uppgavs tjäna
  "flera tusen kronor i månaden"
  ([ENERGInyheter.se](https://www.energinyheter.se/20240112/30649/ferroamp-och-ntricity-godkanda-av-svenska-kraftnat-innovativa-stodtjanster)).
  Det var innan FCR-D-priserna föll kraftigt under 2024–2025 pga fler
  aktörer på marknaden
  ([Svenska kraftnät](https://www.svk.se/press-och-nyheter/nyheter/balansansvar/2025/laga-priser-pa-fcr-nar-2024-summeras/)).
  Dagens 10 kr/kW/månad är alltså sannolikt betydligt lägre än vad de tidiga
  kunderna fick — **räkna med nutidsnivån, inte pilotsiffrorna.**
- **Grov kalkyl för dig:** om ditt Ferroamp-batteri har t.ex. 10–15 kW
  effekt (verifiera din faktiska effekt i Ferroamp-portalen) ger 10 kr/kW/mån
  ungefär **1 200–2 250 kr/år**. Blygsamt, men det är i princip "gratis
  pengar" för att bara ställa kapacitet till förfogande — ingen extra
  styrning eller risk för dig.
- **Enda "kostnaden":** du måste teckna elhandelsavtal med Varberg Energi,
  dvs lämna Tibber som elleverantör. Det påverkar din nuvarande Tibber-baserade
  elbilsladdning och ev. andra Tibber-förmåner — väg det mot de ~1 200–2 250
  kr/år.
- Anmälan sker via
  [varbergenergi.se](https://www.varbergenergi.se/privat/tjanster/energilosningar/flex-batteri/battre-ekonomi-med-ett-hembatteri-fran-ferroamp/teckna-elhandelsavtal/):
  teckna elhandelsavtal → få Flex Batteri-avtal skickat. Enligt sökresultat
  tar de för närvarande främst emot **intresseanmälningar** snarare än
  garanterar direktstart — verifiera aktuell kö/status direkt med dem.

## 2. CheckWatt — inte tillgängligt för dig idag

CheckWatt är den mest kända aggregatorn och har historiskt gett klart högre
ersättning i sina exempel (se tabellen) än Varberg Energis nuvarande nivå,
men **stödjer inte Ferroamp-växelriktare** idag
([hemsol.se](https://hemsol.se/batterilagring-lagra-el-batteri-hemma/checkwatt/)).
Relevant bara om du överväger att byta system (se avsnitt 6).

## 3. Tibber Grid Rewards — bevaka, räkna inte med det än

Tibbers egen stödtjänst finns idag bara för ett fåtal märken (Homevolt, SAJ
HS3, Huawei, nyligen Sigenergy). Utrullning till "alla integrerade
batterier" är utlovad sommaren 2026, men **Ferroamp nämns inte** i något
officiellt material vi hittat
([tibber.com/se/grid-rewards](https://tibber.com/se/grid-rewards)). Värt att
höra av sig till Tibbers support och fråga rakt ut om Ferroamp finns på
roadmapen.

## 4. FerroAI vs. extern styrning/stödtjänst — öppen fråga

- FerroAI är Ferroamps inbyggda AI som redan optimerar mot spotpris, väder
  och din förbrukning. Just nu gratis (introduktionsfas), blir abonnemang
  senare till okänt pris
  ([FerroAI-produktblad](https://ferroamp.com/wp-content/uploads/2025/04/FerroAI-produktblad.pdf)).
- Ferroamp avråder uttryckligen från extern styrning parallellt med FerroAI
  ("för att FerroAI ska fungera optimalt rekommenderas att inga externa
  system används för styrning").
- Flex Batteri-tjänsten är designad för att köras *parallellt* med egen
  användning ("Use the battery yourself. Simultaneously"), men det är
  **oklart om FerroAI och Flex Batteri-avtalet är förenliga eller om Flex
  Batteri kräver att FerroAI stängs av** — det bör du verifiera direkt med
  Ferroamp/Varberg Energi innan du tecknar avtal.
- Eftersom du inte ännu bestämt dig kring FerroAI: en rimlig ordning är att
  (a) höra med Ferroamp/Varberg Energi om kombinationen fungerar, (b) om ja,
  testa Flex Batteri parallellt med FerroAI eftersom det är i praktiken
  riskfritt, (c) om nej, väga 1 200–2 250 kr/år i stödtjänstintäkt mot vad
  FerroAI's egen spotprisoptimering ger dig (svårt att kvantifiera utan
  Ferroamps egna sparande-siffror för din anläggning).

## 5. DIY-spotprisarbitrage via Home Assistant

Community-projekt finns men inget är Ferroamp-specifikt eller
färdigpaketerat:

- **`ha-ferroamp-control`** — styr batteriet via lokala MQTT ExtAPI
  (charge/discharge/auto). Kräver att Ferroamp aktiverar ExtAPI/EMS på din
  hub. Ingen inbyggd prislogik.
- **`ha-smart-battery-pilot`** — vendor-neutral arbitrageplanerare (stödjer
  Tibber/Nordpool/ENTSO-E direkt), men saknar Ferroamp-stöd — skulle behöva
  kopplas ihop manuellt med `ha-ferroamp-control` via HA-scripts.
- Inga dokumenterade backtester eller verifierade avkastningssiffror hos
  något av projekten. Ett grovt "handviftat" estimat: med 14 kWh kapacitet,
  ~90 % rondtrip-verkningsgrad och Tibbers historiska dagliga prisspridning
  skulle en perfekt daglig arbitrage kunna ge i storleksordningen några
  tusen kr/år extra — men detta bör verifieras med en riktig simulering mot
  dina egna Tibber-priser innan du lägger ner arbete på det.
- Eftersom detta konkurrerar med FerroAI om styrningen gäller samma
  avvägning som i avsnitt 4.

## 6. Byta system helt — sannolikt inte lönsamt

Eftersom CheckWatt inte stödjer Ferroamp var frågan om ett hårdvarubyte
(till ett CheckWatt- eller Tibber Grid Rewards-kompatibelt märke) skulle
löna sig.

**Nya system, ungefärligt pris installerat (efter grönt teknik-avdrag):**

| Märke | Ungefärlig storlek | Pris (efter avdrag) | Ekosystem |
|---|---|---|---|
| SAJ HS3 | 10–15 kWh | ~53 000–65 000 kr | CheckWatt-kompatibel, Tibber Grid Rewards-kompatibel direkt |
| Sigenergy SigenStor | 16–18 kWh | ~45 000–68 000 kr | Tibber Grid Rewards-kompatibel (ny integration); CheckWatt-kompatibilitet ej bekräftad |

Källor: [hemsol.se](https://hemsol.se/solceller/solcellsbatteri/saj/),
[amss.se](https://www.amss.se/sv/energilagring/sigenergy-sigenstor-15kw-16kwh-allt-i-ett-vaxelriktare-15kw-och.html)

**Vad det skulle kosta dig:**

- Ditt befintliga Ferroamp-system fungerar och är sannolikt en av de dyrare
  investeringarna på marknaden (Ferroamp är känt som ett premiumval, ofta
  dyrare än 15–25 000 kr *bara* för en jämförbar 5–8 kW-växelriktare, plus
  Pylontech-batterierna). Andrahandsvärdet vid demontering är sannolikt lågt
  — nischprodukt, och ROT/grönt-avdrag går inte att använda igen på samma
  effekt/kapacitet.
- Ny investering: **~45 000–65 000 kr** för ett jämförbart system, plus
  arbete för demontering av det gamla.

**Vad det skulle ge:**

- CheckWatts *exempel*-siffror (1 607 kr/månad ≈ 19 300 kr/år för 10 kW,
  2024; lägre ~8 000–15 000 kr/10 kWh/år uppgivet för 2025) är klart högre
  än Varberg Energis nuvarande 10 kr/kW/månad (~1 200–2 250 kr/år för ditt
  batteri).
- **Men:** samma nedåtgående pristrend som drabbat Ferroamp/Varberg Energis
  ersättning (fler aktörer, fallande FCR-D-priser) drabbar rimligen även
  CheckWatt framöver — deras egna siffror visar redan en nedgång från 2024
  till 2025. Det är inte säkert att gapet består.

**Enkel payback-kalkyl:**

Om vi (optimistiskt) antar att CheckWatt skulle ge dig ~15 000–20 000 kr/år
mer än vad du får kvar hos Ferroamp/Varberg Energi (~1 200–2 250 kr/år),
dvs en skillnad på ~13 000–19 000 kr/år, och investeringen är ~45 000–65 000
kr netto (utan restvärde på gamla systemet) → **payback-tid ~3–5 år**, under
antagandet att dagens CheckWatt-nivåer håller i sig, vilket historiken talar
emot.

**Slutsats:** Att byta ett fungerande, redan betalt 14 kWh-system enbart för
stödtjänst-ersättning är sannolikt **inte** ekonomiskt försvarbart givet
fallande marknadspriser och en payback-tid på flera år som bygger på
optimistiska antaganden. Bytet blir mer motiverat om/när du ändå av andra
skäl (garantitid ute, kapacitetsbehov, fel på systemet) planerar en
uppgradering — då är det värt att välja ett CheckWatt- *och*
Tibber-Grid-Rewards-kompatibelt märke som SAJ HS3 för att hålla dörren öppen
åt båda hållen.

## Rekommendation

1. **Kortsiktigt, lågt hängande frukt:** anmäl intresse hos Varberg Energi
   för Flex Batteri. Det är i praktiken riskfritt (du behåller 70 % av
   kapaciteten) men kräver att du väger bort Tibber som elleverantör mot
   ~1 200–2 250 kr/år i extra intäkt — jämför det mot vad du faktiskt
   värdesätter i Tibbers elbilsladdning/appen.
2. **Innan du tecknar:** fråga Ferroamp/Varberg Energi uttryckligen om
   FerroAI kan vara påslaget samtidigt som Flex Batteri-avtalet.
3. **Behåll Ferroamp-hårdvaran.** Ett systembyte för att komma åt CheckWatt
   ger en payback på flera år baserat på optimistiska och historiskt
   fallande ersättningsnivåer — vänta tills en uppgradering ändå är aktuell.
4. **Bevaka Tibber Grid Rewards** — hör av dig till Tibber-support och fråga
   om Ferroamp finns på deras roadmap för sommaren 2026.
5. **DIY-arbitrage** är intressant att utforska tekniskt men bör inte
   prioriteras före punkt 1 — den lågt hängande frukten (Flex Batteri) kräver
   inget eget utvecklingsarbete alls.

## Källor

- [Ferroamp och Ntricity godkända av Svenska kraftnät](https://www.energinyheter.se/20240112/30649/ferroamp-och-ntricity-godkanda-av-svenska-kraftnat-innovativa-stodtjanster)
- [Ferroamp: Ny lösning för stödtjänster ger batteriägare dubbel nytta](https://ferroamp.com/om-ferroamp/nyheter/ny-losning-for-stodtjanster-ger-batteriagare-dubbel-nytta/)
- [Varberg Energi – Flex Plus maximerar ditt hembatteri](https://www.varbergenergi.se/privat/el/smarta-tjanster/flextjanster/flex-plus-maximerar-ditt-hembatteri)
- [Varberg Energi – Teckna elhandelsavtal / Flex Batteri (Ferroamp)](https://www.varbergenergi.se/privat/tjanster/energilosningar/flex-batteri/battre-ekonomi-med-ett-hembatteri-fran-ferroamp/teckna-elhandelsavtal/)
- [Effektpoolen – CheckWatt växelriktare, vilka modeller är kompatibla?](https://www.effektpoolen.se/post/checkwatt-batterier-vilka-modeller-ar-kompatibla)
- [hemsol.se – CheckWatt: Omdöme, Funktion, Pris och Ersättning (2026)](https://hemsol.se/batterilagring-lagra-el-batteri-hemma/checkwatt/)
- [CheckWatt – Så hade CheckWatts virtuella kraftverk ökat intjäningen H1 2025](https://checkwatt.com/sv/news/sa-hade-checkwatts-virtuella-kraftverk-okat-intjaningen-for-ett-villabatteri-under-forsta-halvaret-2025/)
- [Svenska kraftnät – Låga priser på FCR när 2024 summeras](https://www.svk.se/press-och-nyheter/nyheter/balansansvar/2025/laga-priser-pa-fcr-nar-2024-summeras/)
- [Tibber – Grid Rewards](https://tibber.com/se/grid-rewards)
- [Tibber – integration för Sigenergy (Takkraft)](https://www.takkraft.se/blogg/tibber-lanserar-integration-foer-sigenergy)
- [FerroAI-produktblad (PDF)](https://ferroamp.com/wp-content/uploads/2025/04/FerroAI-produktblad.pdf)
- [GitHub – beolink/ha-ferroamp-control](https://github.com/beolink/ha-ferroamp-control)
- [GitHub – cygnusb/ha-smart-battery-pilot](https://github.com/cygnusb/ha-smart-battery-pilot)
- [GitHub – henricm/ha-ferroamp](https://github.com/henricm/ha-ferroamp)
- [hemsol.se – SAJ Batteri pris](https://hemsol.se/solceller/solcellsbatteri/saj/)
- [amss.se – Sigenergy SigenStor pris](https://www.amss.se/sv/energilagring/sigenergy-sigenstor-15kw-16kwh-allt-i-ett-vaxelriktare-15kw-och.html)

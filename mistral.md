# Mistral AI – Európsky šampión umelej inteligencie

*Stav ku koncu novembra 2026.*

Zatiaľ čo OpenAI je dnes najznámejšou AI spoločnosťou na svete, v Európe
vyrástol jej priamy konkurent – **Mistral AI**. Francúzsky startup založený
v roku 2023 sa za rekordne krátky čas vypracoval na pozíciu európskej
„vlajkovej lode“ umelej inteligencie. Vo februári 2026 jeho ročné
opakované príjmy (ARR) presiahli **400 miliónov dolárov**, pričom o rok
predtým dosahovali len okolo 20 miliónov. Koncom októbra 2026 zverejnil
váhy svojho doteraz najväčšieho modelu **Mistral Large 4** s približne
biliónom parametrov. Ako je možné, že spoločnosť, ktorej modely
v niektorých benchmarkoch zaostávajú za americkou aj čínskou konkurenciou,
zaznamenáva taký raketový rast? Odpoveďou je **suverenita**.

## 1. Vznik spoločnosti a zakladatelia

Mistral AI bola založená v apríli **2023** v Paríži tromi bývalými
výskumníkmi z amerických technologických gigantov:

- **Arthur Mensch (CEO)** – predtým výskumník v Google DeepMind, dnes tvár
  a hlavný hovorca spoločnosti.
- **Timothée Lacroix (CTO)** – technický riaditeľ zodpovedný za
  infraštruktúru a vývoj, predtým pôsobil v Meta AI.
- **Guillaume Lample (hlavný vedec)** – kľúčová výskumná kapacita,
  predtým pôsobil v Meta AI (spoluautor modelu LLaMA).

Všetci traja sú absolventmi popredných francúzskych škôl (École
Polytechnique, École normale supérieure) a priniesli si do startupu
skúsenosti z najlepších AI laboratórií na svete. Ich spoločným cieľom bolo
vytvoriť **nezávislú európsku alternatívu** k uzavretým modelom
amerických gigantov.

Prvým modelom bol **Mistral 7B** (september 2023), malý, no na svoju
veľkosť mimoriadne výkonný model s otvorenými váhami. V decembri 2023
nasledoval **Mixtral 8x7B**, ktorý popularizoval architektúru
Mixture-of-Experts (MoE) v open-source komunite.

Dnes má Mistral **viac ako 1 000 zamestnancov** a kancelárie okrem Paríža
aj v Londýne, Amsterdame, Mníchove, Linzi, San Franciscu a Singapure.
V novembri 2026 otvoril v Singapure ázijsko-pacifické ústredie.

---

## 2. Financovanie a rastúce ocenenie

Mistral AI sa môže pochváliť jedným z najstrmších rastov ocenenia v histórii
európskeho technologického sektora:

| Dátum | Kolo | Vyzbieraná suma | Ocenenie po kole | Hlavný investor |
| :--- | :--- | :--- | :--- | :--- |
| Jún 2023 | Seed | €105M (~$113M) | ~€240M (~$260M) | Lightspeed Venture Partners |
| December 2023 | Séria A | €385M (~$415M) | ~$2,0B | Andreessen Horowitz |
| Jún 2024 | Séria B | €600M (~$640M) | ~€5,8B (~$6,0B) | General Catalyst |
| September 2025 | Séria C | €1,7B (~$2,0B) | €11,7B (~$13,8B) | **ASML** (€1,3B) |
| Marec 2026 | Dlhové financovanie | $830M | – | konzorcium 7 bánk |
| September 2026 | Séria D | €3B (~$3,6B) | > €21B (~$24B) | Samsung, Scaleup Europe Fund, PSG Equity |

V súčasnosti je Mistral AI najhodnotnejším európskym AI startupom.
Od svojho založenia vyzbierala celkovo približne **7,6 miliardy dolárov**
v kombinácii vlastného a dlhového kapitálu. Dlhové financovanie z marca
2026 (BNP Paribas, Crédit Agricole CIB, HSBC, MUFG, Bpifrance a ďalšie)
je určené na nákup GPU pre vlastné dátové centrum pri Paríži.

### Séria D – najväčšie kolo v histórii európskeho tech sektora

Sériu D vo výške 3 miliárd eur Mistral uzavrel **8. septembra 2026**.
Viedol ju Samsung Electronics, spoluinvestormi na čele boli Scaleup Europe
Fund (fond podporovaný EÚ a spravovaný firmou EQT) a PSG Equity. Podľa
Mistralu ide o najväčšie kolo vlastného kapitálu, aké kedy získala súkromná
európska technologická firma. Peniaze majú ísť na vlastné dátové centrá
a väčšie modely. Microsoft sa kola nezúčastnil.

V novembri 2026 oznámil **Deutsche Telekom**, že jeho fond T.Capital
Tech Fund investoval do Série D **100 miliónov eur** ako prvý krok
k partnerstvu pre nemecké firmy a verejné inštitúcie. Ocenenie nad 21
miliárd eur sa tým nemení.

### Prečo ASML?

Účasť holandského výrobcu čipových litografických strojov **ASML** ako
najväčšieho externého akcionára je strategická. ASML nie je len investor –
je aj **zákazníkom**, ktorý využíva modely Mistral na urýchlenie vlastných
inžinierskych riešení. Rovnaký vzorec platí aj pre Samsung, ktorý po Sérii D
oznámil nasadenie modelov Mistral vo vlastnom prostredí (on-premise) pri
návrhu a výrobe polovodičov. Toto prepojenie medzi investorom a zákazníkom
je pre Mistral typické.

---

## 3. Modelová rodina – technický prehľad

Mistral sa preslávil najmä vďaka **open-weight** modelom, ktoré si môže
ktokoľvek stiahnuť, upravovať a spúšťať na vlastnej infraštruktúre.
Na rozdiel od prevažne uzavretých API OpenAI či Anthropic tento prístup
dáva zákazníkom **plnú kontrolu**. (OpenAI síce v roku 2025 vydala
open-weight modely gpt-oss, jej hlavné modely však zostávajú uzavreté.)

| Model | Dátum vydania | Celkové parametre | Aktívne parametre | Kontext | Cena (vstup/výstup za 1M tokenov) | Licencia |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Mistral Large 4** | Október 2026 (váhy 29. 10.) | ~1T | ~49B | 1M | $0,70 / $2,10 | Mistral Ecosystem Open-Weight License (upravená MIT) |
| **Mistral Small 4** | Marec 2026 | 119B | ~6B | 256K | $0,15 / $0,60 | Apache 2.0 |
| **Mistral Medium 3.5** | Apríl 2026 | ~128B (hustý) | 128B | 256K | v útlme (koniec 30. 4. 2027) | upravená MIT |
| **Mistral Large 3** | December 2025 | ~675B | ~41B | 256K | v útlme (koniec 30. 4. 2027) | Apache 2.0 |

*Poznámka: Large 4, Large 3 a Small 4 využívajú riedku (sparse)
architektúru Mixture-of-Experts (MoE) – pre každý token aktivujú len časť
parametrov, čo výrazne znižuje prevádzkové náklady. Medium 3.5 je naopak
hustý (dense) model, ktorý pri každom tokene využíva všetky parametre.
Modely Large 3 a Medium 3.5 Mistral 31. októbra 2026 označil za zastarané
(deprecated) a ako náhradu odporúča Large 4; v API budú dostupné do
30. apríla 2027.*

### 3.1 Mistral Large 4 („Le Chonk“) – nová vlajková loď

Mistral Large 4 bol predstavený **6. októbra 2026** ako verejný preview.
Po ďalších troch týždňoch trénovania (posilňovacím učením) Mistral
**29. októbra 2026 zverejnil váhy** vylepšenej verzie na Hugging Face
(`mistralai/Mistral-Large-4-1T-A52B`, plus samostatný kontrolný bod
v NVFP4 pre GPU Blackwell). Plná dostupnosť v API (GA) nasledovala
5. novembra 2026.

- **Architektúra:** MoE s približne **1 biliónom parametrov**, 128
  expertmi (4 aktívne na token) a jedným zdieľaným expertom. Na token je
  aktívnych 49 miliárd parametrov (52 miliárd vrátane vstupných
  a výstupných vrstiev).
- **Vstupy a kontext:** text aj obrázky, kontext až **1 milión tokenov**.
- **Režimy uvažovania:** Low, Medium a High (predvolený).
- **Cena v API:** $0,70 za vstup a $2,10 za výstup (za 1M tokenov) – teda
  približne polovica ceny počas preview ($1,36 / $4,18).
- **Licencia:** Mistral Ecosystem Open-Weight License, upravená MIT
  licencia. Interné použitie vo firme je voľné, no kto by chcel model
  ponúkať tretím stranám ako službu (Model-as-a-Service), potrebuje
  osobitnú komerčnú licenciu od Mistralu.
- **Nasadenie:** príklady v dokumentácii počítajú s jedným uzlom
  s **8 GPU**. Model je teda otvorený, ale na jeho prevádzku treba
  serverový hardvér, nie pracovnú stanicu.
- **Pôvod:** podľa Mistralu bol model natrénovaný od nuly na európskej
  infraštruktúre.
- **Zameranie:** agentické programovanie a obranná kybernetická
  bezpečnosť. Variant pre penetračné testovanie je dostupný len
  overeným partnerom.

### 3.2 Mistral Small 4 – pracant s nízkymi nákladmi

Architektonicky najzaujímavejší menší model. Zo **119 miliárd**
celkových parametrov (128 expertov, z nich 4 aktívne) aktivuje len
približne **6 miliárd** na token, čo umožňuje veľmi rýchle a lacné
generovanie. Prináša aj **nastaviteľnú úroveň uvažovania** (reasoning
effort) – vývojári môžu podľa potreby voliť medzi rýchlymi štandardnými
odpoveďami a hĺbkovou analýzou. Od septembra 2026 poháňa aj funkciu
Smart Window v prehliadači **Firefox** (v USA, Kanade a Francúzsku).

### 3.3 Mistral Medium 3.5 a Large 3 – modely na odchode

- **Medium 3.5** (apríl 2026) – hustý model so 128 miliardami parametrov,
  ktorý v jedných váhach spájal plnenie inštrukcií, uvažovanie
  a programovanie. Je k dispozícii aj v Microsoft Foundry a Copilot Studio.
- **Large 3** (december 2025) – MoE model so 675 miliardami parametrov
  (41 miliárd aktívnych), ktorý sa dal v nízkej presnosti prevádzkovať
  na jedinom uzle s 8 GPU (napr. 8× H200).

Oba modely nahrádza Large 4. Ich váhy však zostávajú voľne dostupné, takže
firmy, ktoré ich prevádzkujú vo vlastnom prostredí, môžu pokračovať.

### 3.4 Ďalšie produkty

- **Vibe** (do mája 2026 **Le Chat**) – asistent a agent pre bežných
  používateľov aj firmy (obdoba ChatGPT). Zvláda aj dlhšie úlohy, napr.
  programovanie a rešerše. Od 17. novembra 2026 existuje aj ako desktopová
  aplikácia pre macOS a Windows. Predplatné Pro stojí $14,99 mesačne.
- **Mistral Studio** – firemná platforma na tvorbu AI agentov, workflowov
  a aplikácií. Od 5. novembra 2026 ponúka spravovaných agentov
  (managed agents) a dá sa nasadiť v cloude, vo vlastnom VPC alebo
  on-premise.
- **Codestral** – model na dopĺňanie kódu.
- **Ministral 3** (3B, 8B, 14B) – malé modely pre zariadenia na okraji
  siete (edge), licencia Apache 2.0.
- **Mistral OCR 4.1** – rozpoznávanie a spracovanie dokumentov.
- **Voxtral 3** (október 2026) – modely na prepis a syntézu reči a SDK
  pre hlasových agentov.
- **Timestral** (október 2026) – modely na predpovedanie časových radov.

*Samostatné modely na uvažovanie (Magistral) už v cenníku nie sú –
uvažovanie je dnes priamo súčasťou hlavných modelov.*

### 3.5 Kde sú modely Mistral v porovnaní s konkurenciou?

Mistral Large 4 je podľa nezávislej firmy **Artificial Analysis**
najsilnejším open-weight modelom mimo Číny: v jej indexe
Intelligence Index v5 získal 26 bodov, najviac spomedzi západných
open-weight modelov. V indexe programovacích agentov (Coding Agent Index)
dosiahol 48,3 bodu, takmer rovnako ako najlepší open-weight model GLM-5.3
od čínskej Z.ai (48,9).

Celkovo však najlepšie čínske open-weight modely (napr. Kimi K3.1 Pro)
dosahujú vyššie skóre a uzavreté modely OpenAI, Anthropic a Google sú
ešte o úroveň vyššie. Mistral teda vedie medzi západnými otvorenými
modelmi, nie v absolútnom poradí.

---

## 4. Porovnanie so súčasnými špičkovými modelmi

Pre lepšiu predstavu, kde sa Mistral nachádza, uvádzame prehľad
vlajkových modelov hlavných hráčov ku koncu novembra 2026. Tabuľka je
**ilustračná** – ceny sa často menia a uvádzame ich v dolároch
za 1 milión tokenov (vstup / výstup).

| Model | Firma (krajina) | Otvorené váhy | Cena (vstup/výstup) | Typické silné stránky |
| :--- | :--- | :--- | :--- | :--- |
| **GPT-6.2 Astra** | OpenAI (USA) | nie | $8 / $40 | vlajkový model OpenAI (od 17. 11. 2026), náročné uvažovanie |
| **Claude Fable 5.2** | Anthropic (USA) | nie | $8 / $40 | najvýkonnejší model Anthropic (od 9. 11. 2026), dlhé agentické úlohy |
| **Claude Opus 5.5** | Anthropic (USA) | nie | $4 / $20 | programovanie, AI agenti |
| **Gemini 4 Carbon** | Google (USA) | nie | $2 / $10 (úvodná cena do 30. 11.), potom $4 / $20 | najvýkonnejší model Google, dlhý kontext |
| **Kimi K3.1 Pro** | Moonshot AI (Čína) | áno (od 4. 11. 2026) | $2 / $10 | jeden z najsilnejších open-weight modelov |
| **DeepSeek V4.1 Flash** | DeepSeek (Čína) | áno | $0,30 / $1,20 (mimo špičky polovica) | výborný pomer výkonu a ceny |
| **Mistral Large 4** | Mistral AI (Francúzsko) | áno (od 29. 10. 2026) | $0,70 / $2,10 | európska jurisdikcia, nasadenie on-premise |
| **Mistral Small 4** | Mistral AI (Francúzsko) | áno | $0,15 / $0,60 | rýchlosť, veľmi nízka cena |

*Poznámka: DeepSeek v septembri 2026 stiahol model V4 Pro – požiadavky
naň presmeroval na lacnejší V4.1 Flash, ktorý ho podľa DeepSeeku
prekonáva. Nástupca V4.1 Pro zatiaľ nevyšiel. Google ponúka aj model
Gemini 4 Argon za rovnakú cenu a na bežné programovanie a kancelársku
prácu ho odporúča prednostne.*

### Čo z porovnania vyplýva

- **Výkon:** Na absolútnom vrchole benchmarkov sú uzavreté americké modely
  (OpenAI, Anthropic, Google). Medzi open-weight modelmi vedú čínske
  modely (Kimi, GLM, DeepSeek). Mistral Large 4 je najsilnejší otvorený
  model mimo Číny, no na čele open-weight rebríčkov nie je.
- **Cena:** Výstup z Mistral Large 4 je približne **10× lacnejší** než
  z Claude Opus 5.5 a približne **19× lacnejší** než z GPT-6.2 Astra
  či Claude Fable 5.2. Mistral Small 4 je ešte rádovo lacnejší.
  Najlacnejšie čínske modely sú však za porovnateľný výkon ešte lacnejšie.
- **Otvorenosť:** Žiadne z veľkých amerických laboratórií (OpenAI,
  Anthropic, Google) nezverejňuje váhy svojho vlajkového modelu, Mistral
  áno. Čínske open-weight modely sú síce silné, no pre európske banky,
  úrady či armádu je ich pôvod často neprijateľný.
- **Jurisdikcia:** Mistral je jediný hráč v tabuľke so sídlom v EÚ –
  a práve v tom spočíva jeho hlavná konkurenčná výhoda.

*Upozornenie: Výsledky benchmarkov sa rýchlo menia, závisia od
nastavení (napr. úrovne uvažovania) a časť z nich si merajú samotní
výrobcovia. Pred praktickým rozhodnutím odporúčame overiť aktuálne
nezávislé rebríčky, napr. LMArena, Artificial Analysis či Vals AI.
Úvodné ceny Google (Gemini 4) sa od 1. decembra 2026 zdvojnásobujú.*

---

## 5. Komerčný rast – príjmy raketovo rastú

Napriek technickému zaostávaniu v niektorých oblastiach **komerčný rast
Mistralu nemá v Európe obdobu**:

| Obdobie | ARR / príjmy | Strategické faktory |
| :--- | :--- | :--- |
| Začiatok 2025 | ~$20M | Prvé veľké podnikové kontrakty |
| September 2025 | ~$300M (odhad) | Séria C, masívne podnikové kontrakty |
| **Február 2026** | **> $400M** | **približne 20-násobný rast za rok** |
| September 2026 | – | CFO Johan Bergqvist: firma smeruje k $1B ARR do konca roka |
| **Koniec 2026 (cieľ)** | **~$1B** | Verejný cieľ vedenia, zatiaľ nepotvrdený |

*Poznámka: Mistral nezverejňuje auditované finančné výkazy, časť čísel
pochádza z odhadov analytikov a médií. Novšie číslo ARR ako z februára
2026 firma k novembru 2026 nezverejnila. Približne 60 % príjmov pochádza
z Európy.*

Za týmto rastom stojí viac než **100 veľkých podnikových zákazníkov**
vrátane ASML, Samsungu, TotalEnergies, HSBC, Stellantis, Airbusu
a viacerých európskych vlád. Obranné zákazky tvoria podľa Mistralu
10 – 15 % príjmov.

### Kľúčoví zákazníci v praxi

- **Francúzske ministerstvo ozbrojených síl** – rámcová zmluva
  (december 2025) o využívaní AI v obrane, jedna z prvých veľkých
  suverénnych AI zákaziek v Európe.
- **Airbus** – päťročné partnerstvo (máj 2026) pre civilné, obranné
  aj vesmírne aktivity.
- **BMW Group** – partnerstvo pre urýchlenie automobilového dizajnu
  a simulácií nárazov.
- **TotalEnergies** – trojročný program za viac ako 100 miliónov eur
  na AI modely pre geovedy (september 2026).
- **BNP Paribas, Orange, SNCF, Veolia, Thales** – všetci využívajú
  Mistral na interné AI iniciatívy.
- **HSBC** – nasadenie v privátnom prostredí s dôrazom na bezpečnosť dát.

---

## 6. Vertikálna integrácia – od modelov k infraštruktúre

Mistral sa neuspokojil s úlohou poskytovateľa modelov. V roku 2025
predstavil (v spolupráci s Nvidiou) vlastnú cloudovú platformu
**Mistral Compute** a postupne sa mení na **full-stack AI spoločnosť**,
ktorá ovláda modely, infraštruktúru aj aplikácie.

### 6.1 Akvizícia Koyeb – posilnenie vlastného cloudu

Vo februári 2026 Mistral oznámil svoju **prvú akvizíciu** – kúpil
parížsky serverless cloudový startup **Koyeb**. Traja zakladatelia
(bývalí inžinieri Scaleway) a 13 zamestnancov sa pripojili k tímu
Mistralu a platforma Koyeb sa začlenila do Mistral Compute.

Koyeb prináša:

- **Orchestráciu na bare-metal serveroch** – nasadenie priamo na
  fyzický hardvér bez virtualizácie.
- **Automatické škálovanie** – rýchle prispôsobenie výkonu aktuálnemu
  dopytu.
- **Izolované „sandboxy“** – bezpečné prostredie pre AI agentov.

Vďaka Koyebu môže Mistral ponúknuť zákazníkom **„deploy anywhere“** –
spúšťať modely na CPU, GPU alebo špecializovaných akcelerátoroch
s minimálnou konfiguráciou.

### 6.2 Ďalšie akvizície v roku 2026

Koyeb nebol posledný – do novembra 2026 Mistral uskutočnil **päť
akvizícií**:

1. **Koyeb** (február) – serverless cloud.
2. **Emmi AI** (máj) – rakúsky startup z Linzu, ktorý vyvíja AI modely
   na fyzikálne simulácie v priemyselnom inžinierstve; viac ako 30
   výskumníkov a inžinierov.
3. **Pimento** (september) – parížsky startup na tvorbu reklamného
   obsahu pomocou AI; tím posilnil vývoj asistenta Vibe.
4. **New Material** (október) – tvorca nástrojov pre používateľské
   rozhranie AI aplikácií.
5. **SkipLabs** (november) – francúzsky startup zameraný na spoľahlivejšie
   a bezpečnejšie generovanie kódu; jeho tím vytvoril v Mistrale nový
   tím Language (jazyky, kompilátory, statická analýza).

### 6.3 Vlastné dátové centrá – suverenita na úrovni hardvéru

Mistral buduje vlastné dátové kapacity, aby zaručil, že dáta európskych
zákazníkov **neopustia európsku jurisdikciu**:

- **Bruyères-le-Châtel (Francúzsko, pri Paríži)** – centrum s **13 800**
  GPU Nvidia GB300 (Blackwell), prevádzkované firmou Eclairion
  a financované dlhovým úverom $830M. Celková kapacita Mistralu tým
  dosiahne približne **44 MW**.
- **Les Ulis (Francúzsko)** – menšie inferenčné centrum s výkonom
  **10 MW**, ohlásené na tretí štvrťrok 2026 (spustenie zatiaľ
  nepotvrdené).
- **Švédsko (Borlänge)** – investícia **€1,2 miliardy** v partnerstve
  s EcoDataCenter, otvorenie plánované na rok 2027.
- **Cieľ do konca 2027** – približne **200 MW** výpočtovej kapacity.

---

## 7. Regulačné výhody – prečo si Európa vyberá Mistral

Najväčšou konkurenčnou výhodou Mistralu nie je technická prevaha, ale
**regulačný súlad**. S postupným nábehom povinností podľa **EU AI Act**
(pre modely všeobecného určenia platia od augusta 2025) a popri GDPR,
DORA a NIS2 je pre európske podniky kľúčové, aby dáta zostali pod
európskou jurisdikciou.

### Problém amerických poskytovateľov

Americké spoločnosti podliehajú zákonu **US CLOUD Act**, ktorý umožňuje
americkým úradom vyžiadať si dáta, ktoré má americká firma pod kontrolou,
bez ohľadu na to, kde sú fyzicky uložené. Pre európske banky, nemocnice
či obranné zložky je to vážne riziko.

### Riešenie Mistralu

Mistral je **francúzska spoločnosť** (Mistral AI SAS), ktorá prevádzkuje
služby na **európskej infraštruktúre**. Riziko prístupu amerických úradov
k zákazníckym dátam je preto výrazne nižšie než pri amerických
poskytovateľoch – najmä ak zákazník prevádzkuje model vo vlastnom
prostredí. Ako uviedol CEO Arthur Mensch: *„Záleží na tom, aby si
zákazníci vzali AI systémy a urobili ich vlastnými.“*

### Open-weight ako cesta k súladu

Viaceré modely Mistral (napr. Small 4, Ministral 3 či staršie Large 3) sú
dostupné pod licenciou **Apache 2.0**, vlajkový Large 4 pod vlastnou
licenciou odvodenou od MIT, ktorá firmám dovoľuje voľné interné použitie.
Firmy si ich môžu nasadiť **vo vlastnom prostredí** – na vlastnom
hardvéri, dokonca aj bez pripojenia na internet. Majú tak plnú kontrolu
nad dátami aj nad tým, ako model funguje, čo im uľahčuje plnenie
požiadaviek EU AI Act (správa dát, záznamy, posudzovanie zhody) bez
závislosti od netransparentných API amerických poskytovateľov. Od novembra
2026 sa dá vo vlastnom prostredí prevádzkovať aj platforma Mistral Studio
na tvorbu agentov.

Otvorené váhy majú aj druhú stránku: raz stiahnutý model už nemôže
dostať bezpečnostné aktualizácie od výrobcu a jeho prevádzka si vyžaduje
drahý hardvér.

## 8. Mistral a Slovensko

Slovensko patrí medzi krajiny, ktoré nadviazali strategické partnerstvo
s Mistral AI.

### Memorandum s MIRRI

V marci 2026 podpísalo **Ministerstvo investícií, regionálneho rozvoja
a informatizácie SR (MIRRI)** s Mistral AI dohodu o partnerstve
(memorandum). Jej cieľom je vytvoriť rámec pre výskum, vývoj
a zodpovedné nasadzovanie generatívnej AI vo verejnom sektore. Dohoda
stanovuje päť oblastí spolupráce:

1. **Výskum a inovácie** – výmena informácií o vývoji a vyhodnocovaní
   AI modelov.
2. **Využívanie AI vo verejnom sektore** – pilotné projekty v štátnej
   správe.
3. **Dôveryhodná AI** – riadenie rizík, kybernetická bezpečnosť a súlad
   s EU AI Act.
4. **Budovanie kapacít** – školenia, workshopy a výmena expertov.
5. **Politický dialóg** – strategické konzultácie o správe AI.

### Workshop so štátnou správou

Na memorandum nadviazali stretnutia splnomocnenca vlády SR pre umelú
inteligenciu so zástupcami Mistral AI. Cieľom bolo preskúmať praktické
využitie AI v štátnej správe – vrátane nasadenia AI agentov
do úradných procesov, zefektívnenia procesov, znižovania administratívnej
záťaže a zlepšenia kvality služieb pre občanov.

### Spolupráca s IT Asociáciou Slovenska

Mistral rokoval aj s **IT Asociáciou Slovenska (ITAS)** o hľadaní
obchodných príležitostí a partnerov pre nasadenie AI riešení na slovenskom
trhu. Osobitná pozornosť sa venovala **zlepšovaniu spracovania slovenčiny**
veľkými jazykovými modelmi, čo je predpokladom pre lepšie využitie AI
v slovenských firmách.

### Slovenský model Mistral

Na platforme Hugging Face je dostupný model **`slovak-nlp/mistral-sk-7b`**
– verzia Mistral 7B dotrénovaná na slovenských textoch (korpus Araneum
Slovacum VII Maximum s približne 5,3 miliardy tokenov). Vznikol
v spolupráci Technickej univerzity v Košiciach a Jazykovedného ústavu
Ľ. Štúra SAV a je dostupný pod licenciou Apache 2.0. Ide o základný
model; na ňom je postavená napríklad inštrukčná verzia
`mrshu/mistral-sk-7b-alpaca-slovak-it`, určená na odpovedanie na otázky,
prepisovanie a sumarizáciu v slovenčine. Je to praktický dôkaz, že
otvorené modely Mistralu sa dajú prispôsobiť aj pre **menšie jazyky**,
čo je pre Slovensko kľúčové.


## 9. Partnerstvá a ekosystém

### Microsoft – od malej investície k strategickému spojenectvu

Microsoft investoval do Mistralu už vo februári 2024 (15 miliónov eur)
a sprístupnil jeho modely v cloude Azure. V júli 2026 obe spoločnosti
oznámili **rozšírenie partnerstva v hodnote niekoľkých miliárd dolárov**.
Microsoft bude využívať časť európskej výpočtovej kapacity Mistralu
(postavenej na systémoch Nvidia Vera Rubin) a modely Mistral Medium 3.5
a OCR 4 sú dostupné v Microsoft Foundry a Copilot Studio – vo verejnom
cloude aj v úplne odpojených prostrediach (Azure Local). Tento krok
podčiarkuje stratégiu Microsoftu nespoliehať sa výlučne na OpenAI. Pre
Mistral to znamená **priamy prístup ku globálnej predajnej sieti
Microsoftu**.

### Accenture

Vo februári 2026 Mistral vstúpil do strategického partnerstva
s **Accenture**. Dohoda integruje modely Mistral do nástrojov Accenture
pre dátovú konverziu a cloudové ERP, čo umožňuje bezpečné nasadenie AI
pre nadnárodné firmy vyžadujúce regionálny regulačný súlad.

### SAP

V spolupráci s nemeckým softvérovým gigantom **SAP**, podporovanou
francúzskou a nemeckou vládou, vznikajú **suverénne AI riešenia** pre
verejnú správu a regulované odvetvia. Modely Mistral bežia v izolovaných
cloudových prostrediach SAP, čo umožňuje automatizáciu služieb občanom
bez porušenia pravidiel o lokalizácii dát.

### Samsung a Deutsche Telekom

Obaja noví investori sú zároveň obchodnými partnermi. **Samsung**
(hlavný investor Série D) nasadzuje modely Mistral vo vlastnom prostredí
pri návrhu čipov, výrobe a inžinierstve. **Deutsche Telekom** chce
po investícii z novembra 2026 prinášať modely Mistral nemeckým firmám
a verejným inštitúciám.

### Ďalšie partnerstvá

- **Mozilla** – model Mistral Small 4 poháňa funkciu Smart Window
  v prehliadači Firefox.
- **Európska vesmírna agentúra (ESA)** – v septembri 2026 podpísala
  s Mistralom memorandum o spolupráci na AI pre vesmírne aplikácie.

---

## 10. Zhrnutie

Mistral AI je **ukážkovou prípadovou štúdiou** ekonomiky podnikovej
umelej inteligencie v roku 2026:

- **Zakladatelia** – traja bývalí výskumníci z Google DeepMind a Meta,
  ktorí dali Európe vlastného AI šampióna.
- **Modely** – open-weight, vysoko efektívne MoE architektúry (najnovšie
  Large 4 s približne biliónom parametrov a otvorenými váhami od konca
  októbra 2026). V benchmarkoch zaostávajú za americkou špičkou aj za
  najlepšími čínskymi otvorenými modelmi, no ponúkajú **plnú kontrolu
  a transparentnosť**.
- **Financovanie** – ocenenie vzrástlo z ~€240M (2023) na viac ako
  **€21 miliárd** (2026); medzi investormi sú ASML, Samsung aj
  Deutsche Telekom.
- **Príjmy** – z ~$20M na **$400M ARR** za jediný rok, s cieľom
  **$1 miliarda** do konca 2026 (zatiaľ nepotvrdeným).
- **Infraštruktúra a akvizície** – vlastné dátové centrá vo Francúzsku
  a Švédsku, päť akvizícií v roku 2026 (Koyeb, Emmi AI, Pimento,
  New Material, SkipLabs).
- **Regulačná výhoda** – najväčší európsky poskytovateľ, ktorý vďaka
  európskej jurisdikcii a otvoreným váham uľahčuje súlad s EU AI Act,
  GDPR a znižuje riziká spojené s US CLOUD Act.
- **Slovensko** – memorandum s MIRRI, stretnutia so štátnou správou,
  rokovania s ITAS a existujúci slovenský model.

Mistral AI dokázal, že európske firmy a vlády sú ochotné platiť za
**suverénnu, bezpečnú a regulačne vyhovujúcu** AI infraštruktúru – aj
keď jej modely nie sú na vrchole globálnych benchmarkov. Arthur Mensch
opakovane zdôrazňuje, že otvorené modely z dlhodobého hľadiska zvíťazia,
pretože ako jediné dávajú zákazníkom ekonomický zmysel aj kontrolu.

## 11. Otázky do diskusie

1. **Benchmark vs. biznis:** Ako je možné, že spoločnosť s modelmi,
   ktoré v niektorých testoch zaostávajú, zvýšila svoje príjmy za rok
   dvadsaťnásobne?
2. **Suverenita vs. globalizácia:** Je európska snaha o technologickú
   nezávislosť od USA udržateľná z dlhodobého hľadiska? Ako do tohto
   obrazu zapadá partnerstvo s Microsoftom či investícia kórejského
   Samsungu?
3. **Open-source vs. uzavreté modely:** Aké sú výhody a nevýhody
   open-weight stratégie Mistralu oproti uzavretým API OpenAI či
   Anthropic?
4. **Slovensko a AI:** V ktorých oblastiach štátnej správy by podľa
   vás mohla AI (napr. od Mistralu) priniesť najväčší úžitok?
5. **Regulácia ako konkurenčná výhoda:** Chránia európske regulácie
   (EU AI Act) domácich poskytovateľov pred americkou konkurenciou,
   alebo brzdia inovácie?
6. **Výkon vs. cena:** Kedy sa firme oplatí zaplatiť 10- až 20-krát viac
   za špičkový americký model a kedy stačí lacnejší európsky?
7. **Čo je „otvorený“ model?** Licencia Mistral Large 4 dovoľuje voľné
   interné použitie, no poskytovatelia modelu ako služby potrebujú
   osobitnú licenciu. Je to ešte otvorený model?
8. **Čínske vs. európske open-weight modely:** Prečo by si európska
   firma vybrala Mistral, keď čínske otvorené modely dosahujú lepšie
   výsledky a sú často lacnejšie?

# Tokeny – mena jazykových modelov  

V predchádzajúcich kapitolách sme pri každom modeli uvádzali cenu  
„za milión tokenov". Token je základná jednotka, s ktorou jazykový model  
pracuje, a zároveň jednotka, v ktorej sa za model platí. Kto rozumie  
tokenom, vie odhadnúť, koľko bude aplikácia stáť, prečo je odpoveď  
drahšia ako otázka a ako možno účet znížiť o desiatky percent bez straty  
kvality.  

*Stav k októbru 2026. Ceny a cenové politiky sa rýchlo menia.*  

## Čo je token  

Model nečíta text po písmenách ani po celých slovách. Text sa najprv  
rozdelí na **tokeny** – kúsky, ktoré model pozná zo svojho slovníka.  
Tento krok sa volá **tokenizácia** a robí ju **tokenizér**.  

Token môže byť:  

*   celé bežné slovo, napr. `the` alebo ` house` (aj s medzerou pred ním);  
*   časť slova – koreň, predpona alebo koncovka;  
*   jedno písmeno, číslica alebo interpunkčné znamienko;  
*   pri zriedkavých znakoch (emoji, exotické písma) aj len kúsok znaku.  

Ilustračný príklad (presné delenie závisí od tokenizéra):  

```
Text:    Programovanie je zábava.
Tokeny:  Program | ovanie | je | zá | bava | .
```

Každý token má v slovníku svoje **číslo** (ID). Model v skutočnosti  
nevidí text, ale postupnosť čísel, napr. `[48213, 7841, 1253, ...]`.  

### Ako vzniká slovník tokenov  

Väčšina modelov používa metódu **BPE** (*Byte Pair Encoding*) alebo  
príbuzné postupy. Princíp je jednoduchý:  

1.  Začne sa s jednotlivými bajtmi (znakmi).  
2.  V obrovskom množstve textu sa nájde dvojica, ktorá sa vyskytuje  
    najčastejšie, a zlúči sa do nového tokenu.  
3.  Krok sa opakuje, kým slovník nedosiahne želanú veľkosť – typicky  
    100 000 až 250 000 tokenov.  

Výsledok: časté slová sa stanú jedným tokenom, zriedkavé slová sa  
poskladajú z viacerých kúskov. Model tak dokáže zapísať akýkoľvek text,  
no bežný text zapíše úspornejšie.  

### Pravidlá palca  

Pre anglický text platí približne:  

| Jednotka | Približne |
| :--- | :--- |
| 1 token | ~4 znaky, ~¾ slova |
| 100 tokenov | ~75 slov |
| 1 strana A4 | ~500 – 700 tokenov |
| 1 000 000 tokenov | ~750 000 slov, niekoľko hrubých kníh |

### Slovenčina je drahšia  

Tokenizéry sa trénujú prevažne na angličtine. Slovenčina má navyše  
bohaté skloňovanie a diakritiku, takže to isté slovo existuje v desiatkach  
tvarov (*mesto, mesta, mestu, mestom, mestách...*). Slovenský text sa preto  
rozpadne na **viac tokenov** – často 1,5- až 2-násobok anglického textu  
s rovnakým obsahom.  

Praktické dôsledky:  

*   ten istý dokument v slovenčine **stojí viac** ako v angličtine;  
*   do kontextového okna sa ho **zmestí menej**;  
*   odpoveď v slovenčine sa **generuje dlhšie**.  

### Každý model má iný tokenizér  

Tokenizér je súčasťou modelu. Ten istý text má u OpenAI, Anthropic,  
Google či DeepSeeku **rôzny počet tokenov**. Dokonca aj nová generácia  
modelu tej istej firmy môže priniesť nový tokenizér – napríklad Claude  
Opus 4.7 zaviedol tokenizér, ktorý pre rovnaký text vytvorí 1- až  
1,35-násobok tokenov oproti starším modelom Claude.  

Preto pri porovnávaní cien nestačí pozrieť sa na cenu za milión tokenov.  
Model s nižšou cenou za token môže pri vašich dátach vyjsť drahšie, ak ich  
rozdelí na viac tokenov. Najspoľahlivejšie je **zmerať** spotrebu na  
vlastných typických požiadavkách.  

## Tokeny a kontextové okno  

**Kontextové okno** je maximálny počet tokenov, ktorý model spracuje  
v jednej požiadavke – vrátane systémových inštrukcií, histórie  
konverzácie, priložených dokumentov, definícií nástrojov aj samotnej  
odpovede. Aktuálne špičkové modely (Claude, GPT-6, Gemini, DeepSeek-V4)  
majú okno približne **1 milión tokenov**.  

Okrem toho má model limit na **dĺžku odpovede** (napr. 128 000 tokenov  
pri modeloch Claude). V API ho vývojár nastavuje parametrom  
`max_tokens` – ak odpoveď limit dosiahne, je useknutá.  

Dôležitý detail: **model si nič nepamätá medzi požiadavkami**. Pri každej  
ďalšej otázke v konverzácii sa posiela celá doterajšia história znova.  
Dlhá konverzácia teda s každou výmenou zdražuje – desiata otázka stojí  
oveľa viac ako prvá.  

## Druhy tokenov  

Vo vyúčtovaní sa rozlišuje niekoľko druhov tokenov, každý s inou cenou:  

| Druh | Čo zahŕňa | Cena |
| :--- | :--- | :--- |
| **Vstupné** (*input*) | prompt, história, dokumenty, nástroje | základná |
| **Výstupné** (*output*) | text odpovede, volania nástrojov | 4- až 8-krát vyššia |
| **Uvažovacie** (*thinking, reasoning*) | „premýšľanie" pred odpoveďou | ako výstupné |
| **Zápis do cache** | vstup uložený na opakované použitie | o niečo vyššia ako vstup |
| **Čítanie z cache** | vstup načítaný z cache | zlomok ceny vstupu |

Do tokenov sa prepočítavajú aj **obrázky**, **PDF** či **zvuk**. Obrázok  
stojí podľa rozlíšenia stovky až niekoľko tisíc tokenov.  

### Uvažovacie tokeny – skrytý náklad  

Moderné modely pred odpoveďou „premýšľajú" (pozri kapitolu o LLM).  
Toto uvažovanie sa **platí ako výstup**, aj keď ho používateľ často vôbec  
nevidí – modely Claude aj GPT ho predvolene skrývajú alebo zobrazujú len  
zhrnutie. Krátka odpoveď „Áno." tak môže stáť tisíce tokenov, ak model  
predtým dlho uvažoval.  

Hĺbku uvažovania riadi parameter **effort** (úsilie) od `low` po `max`.  
Pre jednoduché úlohy (klasifikácia, krátke odpovede, chat) stačí nízke  
úsilie a ušetrí sa veľa výstupných tokenov.  

## Ako sa tokeny oceňujú  

Ceny sa uvádzajú v dolároch **za 1 milión tokenov** (v angl. často  
skratka *MTok* alebo *per 1M*). Prehľad aktuálnych cien z predchádzajúcich  
kapitol:  

| Model | Vstup | Výstup | Pomer |
| :--- | ---: | ---: | ---: |
| Claude Fable 5.1 | 10 $ | 50 $ | 1 : 5 |
| GPT-6 Astra | 10 $ | 50 $ | 1 : 5 |
| Claude Opus 5.5 | 4 $ | 20 $ | 1 : 5 |
| Claude Sonnet 5.5 | 2 $ | 10 $ | 1 : 5 |
| GPT-6 Sol | 2 $ | 10 $ | 1 : 5 |
| DeepSeek-V4-Pro | 1,32 $ | 3,96 $ | 1 : 3 |
| Mistral Large 3 | 0,50 $ | 1,50 $ | 1 : 3 |
| Claude Haiku 5.5 | 0,10 $ | 0,50 $ | 1 : 5 |
| GPT-6 Luna | 0,10 $ | 0,50 $ | 1 : 5 |

Rozdiel medzi najdrahším a najlacnejším modelom je **stonásobný**.  

### Výpočet ceny požiadavky  

Cena jednej požiadavky sa vypočíta takto:  

```
cena = vstupné_tokeny × cena_vstupu / 1 000 000
     + výstupné_tokeny × cena_výstupu / 1 000 000
```

**Príklad:** Požiadavka na Claude Opus 5.5 so 3 000 vstupnými  
a 1 000 výstupnými tokenmi (vrátane uvažovania):  

```
vstup:   3 000 × 4 $  / 1 000 000 = 0,012 $
výstup:  1 000 × 20 $ / 1 000 000 = 0,020 $
spolu:                              0,032 $
```

Jedna požiadavka stojí zlomok centu, no aplikácia s 10 000 takými  
požiadavkami denne zaplatí 320 $ za deň, teda takmer 10 000 $ mesačne.  
Pri modeli Haiku 5.5 by to isté stálo 40-krát menej.  

### Prečo je výstup drahší ako vstup  

Vstupné tokeny model spracuje **naraz a paralelne** – grafická karta  
prečíta celý prompt v jednom kroku. Výstup však vzniká **token po tokene**:  
každý nový token vyžaduje samostatný prechod celým modelom. Generovanie  
je preto pomalé a viaže výpočtový výkon oveľa dlhšie. Odtiaľ pochádza  
bežný pomer cien 1 : 3 až 1 : 8.  

## Cenové politiky  

Cena za token nie je pevná. Ten istý model môže stáť rôzne podľa toho,  
**ako rýchlo** a **kedy** potrebujete odpoveď, aký dlhý je prompt alebo  
cez koho model voláte.  

### Hromadné spracovanie (Batch API)  

Ak na odpoveď nikto nečaká, možno požiadavky odoslať v dávke. Poskytovateľ  
ich spracuje, keď má voľnú kapacitu – zvyčajne do niekoľkých hodín,  
najneskôr do 24 hodín. Odmenou je **zľava 50 %**.  

Batch ponúkajú Anthropic, OpenAI, Google aj Mistral. Hodí sa na:  

*   spracovanie tisícov dokumentov (sumarizácia, preklad, extrakcia údajov);  
*   hodnotenie modelov (*evals*) a testovanie promptov;  
*   nočné úlohy a dávkové reporty.  

U Anthropic sa zľava sčítava s cachingom – 50 % sa odráta aj z ceny  
čítania a zápisu do cache.  

### Flex – lacnejšie, ale bez záruky  

OpenAI ponúka úroveň **Flex**: požiadavka sa spracuje hneď, ale  
s nižšou prioritou – môže byť pomalšia alebo občas odmietnutá pre  
nedostatok kapacity. Cena je rovnako ako pri batchi **polovičná**.  
Vhodné na úlohy, kde nevadí počkať, no nechceme riešiť dávky.  

### Priorita a rýchly režim  

Opačným smerom ide príplatok za **rýchlosť a spoľahlivosť**:  

*   **Fast mode** – ten istý model generuje výrazne rýchlejšie (pri Claude  
    Opus až 2,5-krát) za **dvojnásobnú cenu**. Claude Opus 5.5 vo fast  
    mode stojí 8 $ / 40 $ namiesto 4 $ / 20 $. OpenAI premenovala svoje  
    *Priority processing* na Fast mode v júli 2026 s rovnakým  
    dvojnásobným príplatkom.  
*   **Priority Tier** – firmy si predplatia garantovanú kapacitu, aby  
    ich požiadavky neboli odmietnuté ani v špičke.  

### Mimošpičkové ceny  

**DeepSeek** ako jeden z mála poskytovateľov mení cenu podľa času:  
v pracovné dni ráno a dopoludnia (podľa nášho času) platí plná cena,  
popoludní, večer a cez víkend **polovičná**. Poskytovateľ tak vyrovnáva  
vyťaženie svojich serverov.  

### Príplatok za dlhý kontext  

Spracovanie veľmi dlhého promptu je pre poskytovateľa neúmerne drahšie,  
preto niektoré modely majú cenové pásma:  

*   **GPT-6 Astra** – nad 272 000 vstupných tokenov sa celá požiadavka  
    účtuje za dvojnásobnú cenu vstupu a 1,5-násobnú cenu výstupu.  
*   **Claude Haiku 5.5** – uvedená cena 0,10 $ / 0,50 $ platí do 100 000  
    tokenov, nad touto hranicou 0,50 $ / 2,50 $.  

Pri práci s veľkými dokumentmi sa teda oplatí skontrolovať, či sa  
požiadavka nedostala do drahšieho pásma.  

### Bezplatné úrovne  

*   **Google Gemini API** má bezplatnú úroveň s denným limitom  
    požiadaviek – vstupné dáta však môže Google použiť na zlepšovanie  
    služieb.  
*   **OpenRouter** ponúka vybrané modely zadarmo na experimentovanie.  
*   **Lokálne modely** (Ollama, LM Studio) sú bez poplatkov za tokeny –  
    platí sa len za vlastný hardvér a elektrinu.  

### Predplatné vs. platba za tokeny  

Bežný používateľ ChatGPT či Claude za tokeny priamo neplatí. Platí  
**mesačné predplatné** (napr. 20 $ za Pro), v rámci ktorého má **limity  
používania** – tie sú však v pozadí tiež merané v tokenoch. Preto dlhá  
konverzácia s veľkými prílohami vyčerpá limit rýchlejšie ako krátke  
otázky.  

| | Predplatné (ChatGPT, Claude) | API (platba za tokeny) |
| :--- | :--- | :--- |
| **Pre koho** | jednotlivci, bežná práca | vývojári, aplikácie, automatizácia |
| **Cena** | pevná mesačne | podľa spotreby |
| **Riziko** | dosiahnutie limitu | nečakane vysoký účet |
| **Kontrola** | malá | úplná (model, parametre, cache) |

### Cloudoví partneri a sprostredkovatelia  

Modely sú dostupné aj cez **Amazon Bedrock**, **Google Vertex AI**  
či **Microsoft Foundry**, prípadne cez **OpenRouter**. Ceny bývajú  
podobné ako priamo u tvorcu, ale nemusia byť rovnaké a niektoré funkcie  
(fast mode, priority) môžu chýbať. Modely s otvorenými váhami, ako  
DeepSeek či Qwen, ponúkajú desiatky poskytovateľov s rôznymi cenami.  

## Caching – opakované použitie promptu  

**Prompt caching** je najdôležitejší nástroj na zníženie nákladov.  
Využíva jednoduchý fakt: väčšina požiadaviek v aplikácii začína rovnako.  

Typická požiadavka chatbota zákazníckej podpory:  

```
[ systémové inštrukcie – 5 000 tokenov       ]  ← rovnaké pri každej otázke
[ definície nástrojov – 3 000 tokenov        ]  ← rovnaké
[ firemná príručka – 40 000 tokenov          ]  ← rovnaké
[ otázka zákazníka – 100 tokenov             ]  ← vždy iná
```

Bez cachingu model pri každej otázke znova spracuje 48 000 rovnakých  
tokenov. S cachingom poskytovateľ uloží výsledok spracovania tohto  
začiatku (tzv. **prefixu**) a pri ďalšej požiadavke ho len načíta.  
Načítanie z cache je **rádovo lacnejšie** a odpoveď prichádza **rýchlejšie**.  

### Ako cache funguje  

Cache funguje na princípe **zhody prefixu**: znovu sa použije iba tá časť  
promptu, ktorá je **od začiatku úplne zhodná** s predchádzajúcou  
požiadavkou. Akákoľvek zmena – aj jeden znak – zneplatní cache od miesta  
zmeny až po koniec.  

Z toho vyplýva zlaté pravidlo:  

> **Nemenné veci na začiatok, premenlivé na koniec.**  

Typické chyby, ktoré cache potichu znefunkčnia:  

*   aktuálny dátum a čas v systémovom prompte;  
*   ID požiadavky alebo meno používateľa na začiatku promptu;  
*   nástroje v náhodnom poradí;  
*   JSON s rozdielne zoradenými kľúčmi;  
*   zmena modelu – cache patrí vždy jednému modelu.  

Cache má obmedzenú **životnosť** (*TTL – time to live*). Ak ju nikto  
nepoužije, po čase sa vymaže. Každé čítanie ju obnoví.  

### Anthropic – explicitný caching  

V Claude API vývojár sám označí, kam až sa má prompt uložiť, pomocou  
značky `cache_control` (môže ich byť najviac štyri). Prípadne zapne  
automatický caching jedným parametrom na úrovni požiadavky.  

| Operácia | Cena oproti bežnému vstupu |
| :--- | :--- |
| Zápis do cache, životnosť 5 minút | 1,25× |
| Zápis do cache, životnosť 1 hodina | 2× |
| Čítanie z cache | 0,1× (Opus 5.5: 0,05×, Fable 5.1: 0,025×) |

Pre Claude Sonnet 5.5 (vstup 2 $) to znamená: zápis 2,50 $, čítanie  
**0,20 $** za milión tokenov. Pri modeli Fable 5.1 stojí čítanie z cache  
len 0,25 $ namiesto 10 $ – teda 40-krát menej.  

Zápis je síce drahší, no pri 5-minútovej cache sa oplatí už pri **druhej**  
požiadavke (1,25 + 0,1 = 1,35 oproti 2 bez cache). Hodinová cache sa  
oplatí od tretej požiadavky. Najmenší prefix, ktorý sa uloží, má pri  
aktuálnych modeloch 512 tokenov – kratšie prompty sa do cache nedostanú.  

```python
import anthropic

client = anthropic.Anthropic()

prirucka = open("prirucka.md", encoding="utf-8").read()

response = client.messages.create(
    model="claude-sonnet-5-5",
    max_tokens=2000,
    system=[
        {"type": "text", "text": "Si asistent zákazníckej podpory."},
        {
            "type": "text",
            "text": prirucka,
            # všetko až po túto značku sa uloží do cache
            "cache_control": {"type": "ephemeral"},
        },
    ],
    messages=[{"role": "user", "content": "Ako zmením heslo?"}],
)

u = response.usage
print("zapísané do cache:", u.cache_creation_input_tokens)
print("načítané z cache: ", u.cache_read_input_tokens)
print("bežný vstup:      ", u.input_tokens)
print("výstup:           ", u.output_tokens)
```

Pri prvom spustení bude `cache_creation_input_tokens` veľké číslo. Ak  
program spustíme znova do 5 minút, rovnaké číslo sa objaví  
v `cache_read_input_tokens` – prefix sa načítal z cache. Ak zostáva  
`cache_read_input_tokens` stále nulové, niečo v prefixe sa mení.  

### OpenAI – automatický caching  

OpenAI cachuje **automaticky**, bez akýchkoľvek značiek. Ak sa začiatok  
promptu zhoduje s nedávnou požiadavkou, zhodná časť sa účtuje ako  
*cached input*. Pri GPT-6 Astra stojí cachovaný vstup **1 $** namiesto  
10 $, teda 90 % zľava. Výhodou je jednoduchosť, nevýhodou menšia  
kontrola nad tým, čo sa a ako dlho uchová.  

### Google Gemini – poplatok za uloženie  

Gemini ponúka implicitný (automatický) aj explicitný caching. Pri  
explicitnom si vývojár vytvorí cache s presnou dobou platnosti a okrem  
lacnejšieho čítania platí aj **poplatok za uloženie** – za každý milión  
uložených tokenov a každú hodinu (napr. okolo 1 $ za milión tokenov  
za hodinu). Vhodné je to pri veľkom dokumente, nad ktorým sa kladie veľa  
otázok v krátkom čase.  

### DeepSeek – cache hit  

DeepSeek cachuje automaticky na disku. Pri zhode prefixu (*cache hit*)  
je cena vstupu **rádovo nižšia** ako pri prvom spracovaní (*cache miss*).  
Spolu s mimošpičkovou zľavou patrí DeepSeek k najlacnejším možnostiam  
na trhu.  

### Príklad: koľko ušetrí caching  

Chatbot na modeli Claude Sonnet 5.5 (2 $ / 10 $) vybaví 1 000 otázok  
denne. Každá požiadavka má 20 000 tokenov spoločného prefixu  
(inštrukcie a príručka), 200 tokenov otázky a 500 tokenov odpovede.  
Otázky prichádzajú priebežne, takže cache zostáva „teplá".  

| Položka | Bez cache | S cache |
| :--- | ---: | ---: |
| Spoločný prefix (20 mil. tokenov) | 40,00 $ | 4,00 $ |
| Otázky (0,2 mil. tokenov) | 0,40 $ | 0,40 $ |
| Odpovede (0,5 mil. tokenov) | 5,00 $ | 5,00 $ |
| Zápis do cache | – | ~0,05 $ |
| **Spolu za deň** | **45,40 $** | **~9,45 $** |

Caching znížil denné náklady zhruba o **80 %** – bez akejkoľvek zmeny  
kvality odpovedí. Ušetril však len na vstupe; výstupné tokeny stoja  
rovnako. Preto sa caching najviac oplatí pri dlhých promptoch  
a krátkych odpovediach, typicky pri agentoch a chatbotoch nad  
dokumentmi.  

## Ako zistiť počet tokenov  

*   **Pole `usage` v odpovedi API** – každá odpoveď obsahuje presný počet  
    vstupných, výstupných a cachovaných tokenov. Je to jediný  
    spoľahlivý údaj pre vyúčtovanie a oplatí sa ho logovať.  
*   **Endpoint na počítanie tokenov** – Claude API ponúka bezplatné  
    `count_tokens`, ktoré spočíta tokeny ešte pred odoslaním požiadavky.  
*   **Knižnica `tiktoken`** – tokenizér modelov OpenAI. Pre iné modely  
    dáva iba hrubý odhad; tokeny Claude podhodnocuje približne o 15 – 20 %  
    a pri kóde či neanglickom texte ešte viac.  
*   **Webové nástroje** – napr. OpenAI Tokenizer, kde sa dá vizuálne  
    pozrieť, ako sa text delí na tokeny.  
*   **Konzoly poskytovateľov** – prehľady spotreby a nákladov podľa dní,  
    modelov a API kľúčov.  

```python
import anthropic

client = anthropic.Anthropic()

text = open("kapitola.md", encoding="utf-8").read()

result = client.messages.count_tokens(
    model="claude-sonnet-5-5",
    messages=[{"role": "user", "content": text}],
)
print("Počet tokenov:", result.input_tokens)
```

## Ako šetriť tokeny  

Poradie od najjednoduchších krokov, ktoré neznižujú kvalitu, po tie,  
ktoré si vyžadujú kompromis:  

1.  **Zapnite caching** a usporiadajte prompt tak, aby nemenné časti  
    boli na začiatku.  
2.  **Neposielajte zbytočnosti** – nepotrebnú históriu, celé dokumenty  
    namiesto relevantných častí, nepoužívané nástroje.  
3.  **Obmedzte výstup** – požiadajte o stručnú odpoveď, nastavte  
    rozumný `max_tokens`, používajte štruktúrovaný výstup (JSON).  
4.  **Použite Batch API** pre všetko, na čo nikto nečaká.  
5.  **Znížte úsilie** (*effort*) pri jednoduchých úlohách.  
6.  **Zvoľte menší model** – pri klasifikácii, extrakcii či preklade  
    často stačí Haiku alebo Luna za zlomok ceny.  
7.  **Kombinujte modely** – lacný model vybaví bežné požiadavky, drahý  
    len tie náročné.  

Dôležité je merať **cenu za vyriešenú úlohu**, nie za požiadavku. Lacný  
model, ktorý úlohu vyrieši až na tretí pokus, nemusí byť v konečnom  
dôsledku lacnejší.  

## Zhrnutie kapitoly  

*   **Token** je kúsok textu – slovo, časť slova alebo znak. Model text  
    vidí ako postupnosť čísel tokenov.  
*   Anglický token má približne 4 znaky. **Slovenčina** potrebuje  
    na ten istý obsah viac tokenov, a preto je drahšia.  
*   Každý model má **vlastný tokenizér** – počty tokenov sa medzi modelmi  
    líšia.  
*   Platí sa za **vstupné** a **výstupné** tokeny. Výstup je 3- až  
    8-krát drahší, pretože sa generuje token po tokene. Uvažovanie  
    modelu sa platí ako výstup.  
*   Cenu ovplyvňujú **cenové politiky**: batch a flex (−50 %), fast mode  
    (2×), mimošpičkové ceny, príplatky za dlhý kontext.  
*   **Caching** ukladá spoločný začiatok promptu; čítanie z cache stojí  
    zlomok bežnej ceny. Funguje iba pri presnej zhode prefixu.  
*   Presný počet tokenov udáva pole **`usage`** v odpovedi API.  

## Otázky a diskusia  

1.  Prečo jazykové modely nepracujú priamo s písmenami alebo celými  
    slovami? Aké výhody a nevýhody by mal každý z prístupov?  
2.  Je spravodlivé, že používatelia menej rozšírených jazykov, ako je  
    slovenčina, platia za rovnakú službu viac? Ako by sa to dalo zmeniť?  
3.  Prečo je výstupný token drahší ako vstupný? Bude tento rozdiel  
    podľa vás pretrvávať?  
4.  Navrhnite poradie častí promptu (inštrukcie, dátum, profil  
    používateľa, dokumenty, otázka) tak, aby caching fungoval čo najlepšie.  
5.  Vypočítajte, koľko by stál chatbot z príkladu v tejto kapitole  
    na modeli Claude Haiku 5.5 s cachingom a bez neho.  
6.  Kedy sa oplatí predplatné a kedy platba za tokeny cez API?  
7.  Skryté uvažovacie tokeny tvoria často väčšinu ceny odpovede. Mali by  
    poskytovatelia uvažovanie vždy zobrazovať, keď zaň používateľ platí?  

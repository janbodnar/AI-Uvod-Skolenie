# OpenRouter – jedno API pre stovky modelov  

V predchádzajúcich kapitolách sme spoznali troch tvorcov jazykových  
modelov: OpenAI, Anthropic a DeepSeek. Každý z nich má vlastnú webovú  
stránku, vlastné API kľúče, vlastné ceny a vlastné spôsoby platby.  
Vývojár, ktorý chce vyskúšať alebo kombinovať modely od viacerých firiem,  
musí spravovať niekoľko účtov naraz. Práve tento problém rieši  
**OpenRouter** – služba, ktorá sprístupňuje stovky modelov od desiatok  
poskytovateľov cez **jedno API a jeden účet**.  

*Stav k októbru 2026. Údaje o modeloch, cenách a financiách sa rýchlo menia.*  

## Čo je OpenRouter  

OpenRouter je tzv. **AI brána** (*AI gateway*) alebo **router modelov**.  
Sám žiadne modely nevyvíja ani netrénuje. Funguje ako sprostredkovateľ  
medzi aplikáciou a poskytovateľmi modelov:  

```
Aplikácia  →  OpenRouter  →  OpenAI / Anthropic / Google / DeepSeek / ...
```

Aplikácia pošle požiadavku na OpenRouter s názvom modelu, napríklad  
`anthropic/claude-sonnet-5.5`. OpenRouter ju prepošle vhodnému  
poskytovateľovi, vráti odpoveď a vyúčtuje spotrebu z jedného kreditu.  

V októbri 2026 ponúkal OpenRouter **462 modelov** od 55 tvorcov,  
dostupných prostredníctvom **112 poskytovateľov**. Rozlišovať tieto dva  
pojmy je dôležité:  

*   **Tvorca modelu** (*author*) – firma, ktorá model vyvinula, napr.  
    DeepSeek alebo Meta.  
*   **Poskytovateľ** (*provider*) – firma, ktorá model prevádzkuje  
    na svojich serveroch. Model s otvorenými váhami, ako DeepSeek-V4,  
    môže ponúkať aj desať rôznych poskytovateľov s rôznou cenou,  
    rýchlosťou a pravidlami ochrany údajov.  

## Vznik a vývoj spoločnosti  

OpenRouter založili v roku **2023** **Alex Atallah**, spoluzakladateľ  
a bývalý technický riaditeľ NFT trhoviska OpenSea, a **Louis Vichy**.  
Služba vznikla krátko po spustení ChatGPT, keď začali pribúdať  
konkurenčné a open-source modely a vývojári potrebovali jednoduchý  
spôsob, ako ich porovnávať.  

Rast OpenRoutera kopíruje rast celého odvetvia:  

| Dátum | Udalosť |
| :--- | :--- |
| 2023 | Založenie spoločnosti |
| jún 2025 | Investičné kolo Series A (40 mil. $), vedené a16z a Menlo Ventures |
| máj 2026 | Series B (113 mil. $) vedené fondom CapitalG (Alphabet), ocenenie ~1,3 mld $ |
| máj 2026 | ~25 biliónov tokenov týždenne, 8 miliónov používateľov |
| aug. 2026 | Stripe oznámil dohodu o kúpe OpenRoutera, podľa médií za viac ako 7 mld $ |

Za pol roka (od konca roka 2025 do mája 2026) vzrástol objem  
spracovaných tokenov päťnásobne – z 5 na 25 biliónov týždenne.  

### Prečo OpenRouter kupuje Stripe?  

**Stripe** je jedna z najväčších platobných spoločností na svete. Ak sa  
AI stáva bežnou súčasťou softvéru, každá aplikácia neustále „nakupuje"  
tokeny od rôznych poskytovateľov. Stripe chce byť pri tom, keď sa  
tieto platby rozhodujú – a OpenRouter mu dáva kontrolu nad vrstvou, cez  
ktorú tečú miliardy dolárov za AI. Analytici hovoria o boji o  
**„spotrebnú vrstvu AI"**.  

## Prečo používať OpenRouter  

*   **Jeden kľúč a jedna faktúra:** Netreba zakladať účty u každého  
    poskytovateľa ani riešiť rôzne platobné metódy.  
*   **Jednotné API:** Všetky modely sa volajú rovnako, vo formáte  
    kompatibilnom s OpenAI. Zmena modelu znamená zmenu jedného reťazca.  
*   **Záložné riešenie (fallback):** Ak poskytovateľ zlyhá alebo je  
    preťažený, OpenRouter automaticky skúsi ďalšieho.  
*   **Porovnávanie modelov:** Ten istý prompt možno jednoducho poslať  
    viacerým modelom a porovnať kvalitu, rýchlosť a cenu.  
*   **Prístup k novinkám:** Nové modely sa na OpenRouteri často objavia  
    v deň vydania.  
*   **Bezplatné modely:** Na experimentovanie a výučbu.  

Nevýhody:  

*   **Ďalší sprostredkovateľ:** Dáta prechádzajú cez ďalšiu firmu, čo  
    pridáva bezpečnostné aj právne otázky.  
*   **Poplatok za kredit:** Približne 5,5 % pri nákupe kreditu kartou.  
*   **Nie všetky funkcie:** Niektoré špecifické funkcie jednotlivých API  
    (napr. najnovšie beta funkcie) nemusia byť cez OpenRouter dostupné  
    hneď alebo vôbec.  
*   **Mierne vyššia latencia:** Každá požiadavka prechádza cez ďalší  
    server.  

## Ako funguje cenotvorba  

OpenRouter si na samotných modeloch **neprirába** – cena za token je  
rovnaká ako priamo u poskytovateľa. Zarába na **poplatku pri nákupe  
kreditu**: 5,5 % pri platbe kartou (minimálne 0,80 $), 5 % pri platbe  
kryptomenou.  

Príklady cien za 1 milión tokenov (október 2026):  

| Model | Identifikátor | Vstup | Výstup |
| :--- | :--- | ---: | ---: |
| Claude Fable 5.1 | `anthropic/claude-fable-5.1` | 10 $ | 50 $ |
| GPT-6 Astra | `openai/gpt-6-astra` | 10 $ | 50 $ |
| Claude Opus 5.5 | `anthropic/claude-opus-5.5` | 4 $ | 20 $ |
| Claude Sonnet 5.5 | `anthropic/claude-sonnet-5.5` | 2 $ | 10 $ |
| GPT-6 Sol | `openai/gpt-6-sol` | 2 $ | 10 $ |
| DeepSeek-V4-Pro | `deepseek/deepseek-v4-pro-0813` | 0,66 $ | 1,98 $ |
| Claude Haiku 5.5 | `anthropic/claude-haiku-5.5` | 0,10 $ | 0,50 $ |
| GPT-6 Luna | `openai/gpt-6-luna` | 0,10 $ | 0,50 $ |

Takáto tabuľka na jednom mieste je sama osebe užitočná: rozdiel medzi  
najdrahším a najlacnejším modelom je **stonásobný**. Výber modelu je  
preto vždy kompromisom medzi kvalitou a cenou.  

Identifikátor modelu má vždy tvar `tvorca/model`. Niektoré modely majú aj  
**varianty** označené príponou:  

*   `:free` – bezplatná verzia s obmedzeniami.  
*   `:batch` – hromadné spracovanie za polovičnú cenu (výsledok  
    nepríde okamžite).  
*   `:nitro` – uprednostní najrýchlejšieho poskytovateľa.  
*   `:floor` – uprednostní najlacnejšieho poskytovateľa.  

### Bezplatné modely  

OpenRouter ponúka aj modely zadarmo – v októbri 2026 ich bolo 14,  
napríklad Gemma 4 od Googlu či Nemotron od Nvidie. Sú vhodné na výučbu  
a experimenty, no majú prísne limity:  

*   bez zakúpeného kreditu **50 požiadaviek denne**,  
*   po zakúpení aspoň 10 $ kreditu **1 000 požiadaviek denne**.  

Pozor: bezplatní poskytovatelia môžu niekedy používať vstupy  
na trénovanie svojich modelov. Do bezplatných modelov preto nepatria  
citlivé ani osobné údaje.  

## Použitie v Pythone  

Keďže API OpenRoutera je kompatibilné s formátom OpenAI, použijeme  
knižnicu `openai`, ktorú už poznáme. API kľúč vytvoríme na  
openrouter.ai a uložíme do premennej prostredia:  

```bash
export OPENROUTER_API_KEY="sk-or-..."
```

### Základné volanie  

```python
import os
from openai import OpenAI

client = OpenAI(
    base_url="https://openrouter.ai/api/v1",
    api_key=os.environ["OPENROUTER_API_KEY"],
)

response = client.chat.completions.create(
    model="anthropic/claude-sonnet-5.5",
    messages=[{"role": "user", "content": "Vysvetli mi, čo je AI brána."}],
)

print(response.choices[0].message.content)
```

Ak chceme použiť iný model, stačí zmeniť jediný riadok – napríklad  
`model="deepseek/deepseek-v4.1-flash"` alebo `model="openai/gpt-6-luna"`.  

### Porovnanie viacerých modelov  

Jednotné API umožňuje jednoducho porovnať odpovede rôznych modelov  
na rovnakú otázku:  

```python
models = [
    "anthropic/claude-haiku-5.5",
    "openai/gpt-6-luna",
    "deepseek/deepseek-v4.1-flash",
]

question = "Vysvetli jednou vetou, čo je neurónová sieť."

for model in models:
    response = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": question}],
    )
    print(f"--- {model} ---")
    print(response.choices[0].message.content)
```

### Záložné modely a výber poskytovateľa  

Parametre špecifické pre OpenRouter odovzdáme cez `extra_body`.  
Parameter `models` určuje záložné modely pre prípad, že prvý zlyhá.  
Parameter `provider` ovplyvňuje výber poskytovateľa – napríklad  
uprednostní najnižšiu cenu a vylúči poskytovateľov, ktorí dáta  
ukladajú alebo na nich trénujú:  

```python
response = client.chat.completions.create(
    model="deepseek/deepseek-v4-pro-0813",
    messages=[{"role": "user", "content": "Navrhni názov pre kaviareň."}],
    extra_body={
        "models": ["anthropic/claude-sonnet-5.5", "openai/gpt-6-sol"],
        "provider": {
            "sort": "price",
            "data_collection": "deny",
        },
    },
)

print(response.model)  # ktorý model nakoniec odpovedal
print(response.choices[0].message.content)
```

### Automatický výber modelu  

OpenRouter ponúka aj špeciálne „modely", ktoré v skutočnosti vyberajú  
model za nás:  

*   `openrouter/auto` – **Auto Router** vyberie vhodný model podľa  
    obsahu promptu.  
*   `openrouter/free` – náhodne vyberie jeden z bezplatných modelov.  
*   `openrouter/fusion` – pošle otázku skupine modelov, ktoré ju  
    analyzujú paralelne, a ich odpovede spojí do jednej.  

## Ochrana údajov  

Pri používaní OpenRoutera prechádzajú dáta cez **dve firmy**: OpenRouter  
a konkrétneho poskytovateľa. Treba preto poznať pravidlá oboch:  

*   OpenRouter štandardne **neukladá obsah** promptov a odpovedí, iba  
    metadáta (čas, model, počet tokenov). Kto ukladanie povolí, získa  
    zľavu 1 %.  
*   Každý poskytovateľ má vlastné pravidlá – niektorí dáta neukladajú  
    vôbec (*zero data retention*), iní ich uchovávajú alebo používajú  
    na trénovanie.  
*   V nastaveniach účtu aj v každej požiadavke (parameter `provider`)  
    možno vylúčiť poskytovateľov, ktorí dáta ukladajú alebo na nich  
    trénujú.  

Pre firmy s citlivými údajmi je dôležité aj to, **v ktorej krajine**  
poskytovateľ model prevádzkuje. Model DeepSeek spustený cez amerického  
alebo európskeho poskytovateľa neposiela dáta do Číny – na rozdiel  
od oficiálneho API DeepSeeku.  

## OpenRouter ako zdroj dát o trhu AI  

OpenRouter zverejňuje **rebríčky** (*rankings*) modelov podľa toho,  
koľko tokenov cez ne používatelia reálne spracujú. Keďže ide o skutočné  
používanie, nie o umelé testy, sledujú ich novinári, analytici  
aj investori. Dáta však treba čítať opatrne – používatelia OpenRoutera  
sú najmä vývojári a startupy, nie celý trh.  

Niekoľko zaujímavých trendov z roku 2026:  

*   V apríli 2026 tvorili **čínske modely viac ako 45 %** všetkej  
    prevádzky na OpenRouteri. Používatelia si vyberajú najmä podľa  
    pomeru ceny a výkonu.  
*   V auguste 2026 smerovalo **84 % tokenov** k modelom, ktoré nepatria  
    medzi najvýkonnejšie. Na väčšinu bežných úloh stačia lacnejšie modely.  
*   V septembri 2026 používatelia po prvý raz za viac ako dva a pol  
    roka minuli viac peňazí za modely **OpenAI** než za modely  
    **Anthropic**.  

Rebríčky ukazujú aj to, **na čo** ľudia AI používajú – dlhodobo  
dominuje **programovanie**, nasleduje hranie rolí (*roleplay*),  
marketing či preklady.  

### Tajné modely  

OpenRouter sa stal aj miestom, kde firmy pred oficiálnym vydaním  
testujú nové modely pod krycími menami (tzv. *stealth models*).  
Napríklad model **Quasar Alpha** (apríl 2025) sa neskôr ukázal ako  
predbežná verzia GPT-4.1 od OpenAI. Komunita na sociálnych sieťach  
potom súťaží v hádaní, kto za tajným modelom stojí.  

## Alternatívy k OpenRouteru  

OpenRouter nie je jedinou AI bránou. Medzi alternatívy patria:  

*   **LiteLLM** – open-source knižnica a proxy server, ktorý si firma  
    prevádzkuje sama. Dáta tak neprechádzajú cez ďalšiu firmu.  
*   **Vercel AI Gateway** a **Cloudflare AI Gateway** – brány  
    od poskytovateľov webovej infraštruktúry.  
*   **Cloudové platformy** – **Amazon Bedrock**, **Google Vertex AI**  
    a **Microsoft Foundry** ponúkajú modely viacerých firiem v rámci  
    jedného cloudu. Firmy ich volia najmä vtedy, keď už v danom cloude  
    majú dáta a zmluvy.  
*   **Priame API** – pri jednom modeli a veľkom objeme je priame  
    pripojenie k poskytovateľovi často najjednoduchšie a umožňuje  
    využiť všetky jeho funkcie.  

## Zhrnutie kapitoly  

*   **OpenRouter** je AI brána, ktorá sprístupňuje stovky modelov  
    od desiatok poskytovateľov cez **jedno API vo formáte OpenAI**.  
*   Založili ho v roku 2023 Alex Atallah a Louis Vichy. V roku 2026 bol  
    ocenený na 1,3 mld $ a v auguste **Stripe oznámil jeho kúpu** za  
    viac ako 7 mld $.  
*   Ceny modelov sú rovnaké ako u poskytovateľov, OpenRouter zarába  
    na **poplatku pri nákupe kreditu** (približne 5,5 %).  
*   Hlavné výhody: jeden účet, jednoduchá zmena modelu, **záložné  
    modely**, porovnávanie modelov a **bezplatné modely** na experimenty.  
*   Treba rozlišovať **tvorcu** a **poskytovateľa** modelu – od  
    poskytovateľa závisí cena, rýchlosť aj ochrana údajov.  
*   **Rebríčky** OpenRoutera sú cenným zdrojom dát o tom, ako sa AI  
    v praxi používa.  

## Otázky a diskusia  

1.  Aký je rozdiel medzi tvorcom a poskytovateľom modelu? Prečo môže  
    ten istý model stáť u rôznych poskytovateľov rôzne?  
2.  Kedy by ste použili OpenRouter a kedy priame API konkrétnej firmy?  
3.  Aké riziká prináša, keď všetky požiadavky aplikácie prechádzajú cez  
    jedného sprostredkovateľa?  
4.  Prečo by platobná firma ako Stripe zaplatila za OpenRouter viac ako  
    7 miliárd dolárov?  
5.  Čo nám hovoria rebríčky OpenRoutera o trhu AI? Prečo ich nemožno  
    považovať za obraz celého trhu?  
6.  Prečo podľa vás používatelia OpenRoutera posielajú väčšinu tokenov  
    lacnejším modelom, a nie tým najvýkonnejším?  
7.  **Praktická úloha:** Pomocou kódu z kapitoly pošlite rovnakú otázku  
    trom bezplatným modelom. Porovnajte kvalitu, dĺžku a rýchlosť  
    odpovedí. Ktorý model by ste zvolili pre školský chatbot a prečo?  
8.  **Praktická úloha:** Vypočítajte, koľko by stálo spracovanie  
    1 000 dokumentov po 5 000 slovách (asi 7 000 tokenov vstupu  
    a 500 tokenov výstupu na dokument) s modelmi Claude Opus 5.5,  
    Claude Haiku 5.5 a DeepSeek-V4-Pro.  

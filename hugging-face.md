# Hugging Face: centrum otvorenej umelej inteligencie  

## 1. Čo je Hugging Face  

Hugging Face je platforma, kde ľudia a firmy zdieľajú modely umelej  
inteligencie, dáta na ich trénovanie a malé aplikácie, ktoré si môžete hneď  
vyskúšať. Často sa o nej hovorí ako o „GitHube pre AI“. Tak ako GitHub slúži na  
zdieľanie programového kódu, Hugging Face slúži na zdieľanie modelov a dát.  

Adresa: huggingface.co. Základné prezeranie a sťahovanie verejného obsahu je  
zadarmo.  

## 2. Krátka história  

Spoločnosť vznikla v roku 2016 a pôvodne vyvíjala chatbota pre tínedžerov. Zlom  
nastal, keď tím zverejnil knižnicu Transformers, ktorá výrazne zjednodušila  
prácu s jazykovými modelmi. Platforma sa postupne stala hlavným miestom, kde  
vývojári a výskumníci zverejňujú otvorené modely.  

## 3. Z čoho sa platforma skladá  

Jadrom je takzvaný Hub, teda verejný register troch druhov obsahu:  

- Modely (Models): hotové modely na stiahnutie alebo vyskúšanie. Nájdete tu  
  jazykové modely, modely na obrázky, zvuk, preklad aj rozpoznávanie reči.  
- Datasety (Datasets): zbierky dát na trénovanie a testovanie modelov, napríklad  
  texty, obrázky, nahrávky alebo záznamy robotov.  
- Spaces: malé webové aplikácie a ukážky, ktoré bežia priamo v prehliadači.  
  Hodia sa na rýchle vyskúšanie modelu bez inštalácie.  

Rozsah je obrovský. Podľa údajov z augusta 2026 Hub obsahuje približne 3 milióny  
verejných modelov a vyše milióna Spaces. Väčšina modelov je však využívaná  
minimálne. Drvivú väčšinu sťahovaní majú len malé percento najpopulárnejších.  

## 4. Knižnice, ktoré za platformou stoja  

Hugging Face vyvíja aj open-source nástroje pre programátorov. Pre netechnické  
publikum stačí poznať ich názvy a účel:  

- Transformers: štandardná knižnica na používanie moderných modelov.  
- Datasets: načítanie a spracovanie dát.  
- Diffusers: modely na generovanie obrázkov a videa.  
- PEFT a TRL: úsporné dolaďovanie a trénovanie modelov.  
- Gradio: rýchle vytvorenie webového rozhrania k modelu. Je základom väčšiny  
  Spaces.  
- Safetensors: bezpečný formát na ukladanie váh modelov.  

## 5. Ako sa modely spúšťajú  

Model si môžete vyskúšať aj bez vlastného výkonného počítača:  

- Spaces: ukážkové aplikácie v prehliadači. Najjednoduchší začiatok.  
- Inference Providers: jedno API na volanie modelov, ktoré bežia u rôznych  
  poskytovateľov.  
- Inference Endpoints: vlastný, platený a spravovaný server pre konkrétny model,  
  určený na produkčné nasadenie.  
- Lokálne spustenie: stiahnutie modelu do vlastného počítača, typicky v  
  kvantizovanej podobe (napr. formát GGUF).  
- HuggingChat: chatovacie rozhranie, v ktorom možno skúšať otvorené modely.  

## 6. Prečo je dôležitá pre tému otvorených modelov  

Väčšina otvorených modelov (open weights), o ktorých sme hovorili, sa zverejňuje  
práve tu. Patria sem napríklad modely rodín Qwen, Mistral, DeepSeek, GLM, Kimi  
či Muse Glimmer od Meta. Uzavreté modely ako GPT alebo Claude tu k stiahnutiu  
nie sú, dostupné sú len cez API ich poskytovateľov.  

Otvorené váhy umožňujú spustiť model vo vlastnej infraštruktúre, čo je dôležité  
pre firmy, ktoré nechcú posielať dáta tretím stranám. Pripomíname, že open  
weights neznamená vždy aj open source. Licencia sa líši model od modelu.  

## 7. Ako začať: prvé kroky  

1. Otvorte huggingface.co a vytvorte si bezplatný účet.  
2. V sekcii Models vyhľadajte model podľa úlohy (napr. text generation) alebo  
   mena.  
3. Otvorte kartu modelu (model card). Nájdete v nej popis, licenciu, obmedzenia  
   a spôsob použitia.  
4. Ak má model ukážku alebo Space, vyskúšajte ho priamo v prehliadači.  
5. Pozrite si záložku Community, kde používatelia hlásia problémy a zdieľajú  
   skúsenosti.  

## 8. Na čo si dať pozor  

- Licencia: pred komerčným použitím vždy čítajte licenciu konkrétneho modelu.  
  Niektoré majú obmedzenia pre veľké firmy alebo oblasti.  
- Kvalita: platí, že dostupné neznamená dobré. Pozrite si sťahovania, popis a  
  recenzie, a model vždy otestujte na vlastných úlohách.  
- Dôveryhodný zdroj: preferujte modely od overených organizácií. Neznáme súbory  
  môžu obsahovať škodlivý kód, najmä staršie formáty. Bezpečnejší je formát  
  safetensors.  
- Citlivé dáta: do verejných Spaces nevkladajte osobné ani firemné údaje.  
  Nevieme, kam sa ukladajú.  
- Obmedzený prístup: niektoré modely vyžadujú schválenie žiadosti a súhlas s  
  podmienkami autora (tzv. gated modely).  
- Halucinácie a skreslenia platia aj pre otvorené modely. Výstupy treba  
  overovať.  

## 9. Cenník v skratke  

Verejné prezeranie, stiahnutie modelov a zdieľanie verejných repozitárov je  
zadarmo. Platené plány (PRO, Team, Enterprise) ponúkajú napríklad súkromné  
repozitáre, viac výpočtového výkonu a podporu. Za výkonnejšie hardvérové  
prostredie pre Spaces či Inference Endpoints sa platí podľa spotreby. Aktuálne  
ceny si overte na stránke huggingface.co/pricing.  

## 10. Praktické cvičenie  

1. Nájdite model na rozpoznávanie reči a vyskúšajte ho v Space.  
2. Nájdite dva modely na tú istú úlohu a porovnajte ich model cards: licenciu,  
   veľkosť a popis obmedzení.  
3. Nájdite dataset súvisiaci s vašou oblasťou a pozrite si jeho náhľad priamo v  
   prehliadači.  
4. Otvorte jednu ukážku v Spaces a odpovedzte: môžem tomu dôverovať s firemnými  
   dátami?  

## 11. Užitočné odkazy  

- https://huggingface.co/spaces/LiquidAI/system-one-arcade
- https://huggingface.co/spaces/ACE-Step/ACE-Step

- huggingface.co: hlavná stránka a Hub  
- huggingface.co/models: katalóg modelov  
- huggingface.co/datasets: katalóg datasetov  
- huggingface.co/spaces: ukážkové aplikácie  
- huggingface.co/docs: dokumentácia  
- huggingface.co/learn: bezplatné kurzy  
- huggingface.co/pricing: aktuálny cenník  

## 12. Zhrnutie  

- Hugging Face je hlavné miesto na zdieľanie otvorených modelov, datasetov a  
  ukážkových aplikácií.  
- Pre začiatočníkov je najjednoduchšie začať cez Spaces a model cards.  
- Open weights prinášajú kontrolu a flexibilitu, no vyžadujú pozornosť pri  
  licencii, bezpečnosti a kvalite.  
- Platforma je kľúčová pre každého, kto chce AI nielen používať, ale aj pochopiť  
  a prispôsobiť.

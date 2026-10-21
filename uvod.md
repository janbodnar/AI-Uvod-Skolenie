# Úvod do umelej inteligencie

## 1. Vitajte na školení

Umelá inteligencia sa za pár rokov dostala z výskumných laboratórií do bežných  
kancelárií, škôl aj domácností. Píše emaily, sumarizuje dokumenty, prekladá,  
programuje, vytvára obrázky a čoraz častejšie samostatne vykonáva celé úlohy.  
Kto s ňou vie pracovať, ušetrí čas a získa nové možnosti. Kto ju ignoruje,  
riskuje, že zaostane.  

Cieľom tohto školenia je, aby ste AI rozumeli a vedeli ju prakticky a bezpečne  
používať. Nepotrebujete vedieť programovať ani mať technické vzdelanie. Stačí  
zvedavosť a ochota skúšať.  

Po absolvovaní školenia budete:  

- rozumieť, čo AI je, ako vzniká a prečo niekedy zlyháva  
- vedieť písať kvalitné zadania (prompty) a kriticky hodnotiť výstupy  
- poznať hlavné nástroje, modely a platformy a vedieť si medzi nimi vybrať  
- vedieť spustiť AI model na vlastnom počítači  
- vedieť vytvoriť jednoduchú automatizáciu, aplikáciu či agenta  
- poznať riziká, pravidlá a zásady zodpovedného používania  

## 2. Čo je umelá inteligencia

Umelá inteligencia (AI, z anglického Artificial Intelligence) je oblasť  
informatiky, ktorá sa zaoberá tvorbou systémov schopných vykonávať úlohy, na  
ktoré by inak bolo potrebné ľudské myslenie: rozpoznávať reč a obrázky,  
rozumieť textu, rozhodovať sa, plánovať či tvoriť.  

Pojmy, ktoré budete často počuť, do seba zapadajú ako matriošky:  

- Umelá inteligencia: najširší pojem, zahŕňa všetky prístupy k  
„inteligentnému" správaniu strojov, aj tie staršie založené na ručne  
napísaných pravidlách.  
- Strojové učenie (machine learning): systém sa pravidlá neučí od  
programátora, ale sám ich odvodí z príkladov v dátach.  
- Hlboké učenie (deep learning): strojové učenie pomocou veľkých neurónových  
sietí s mnohými vrstvami.  
- Generatívna AI: modely, ktoré nový obsah nielen analyzujú, ale aj vytvárajú,  
napríklad text, obrázky, hudbu, video alebo kód.  
- Veľké jazykové modely (LLM): generatívne modely trénované na obrovskom  
množstve textu. Patria sem modely za službami ChatGPT, Claude, Gemini či  
Copilot.  

Dôležité rozlíšenie: dnešná AI je takzvaná úzka (narrow) AI. Je vynikajúca v  
konkrétnych typoch úloh, no nemá vlastné ciele, vedomie ani skutočné  
porozumenie svetu v ľudskom zmysle. Všeobecná umelá inteligencia (AGI), ktorá  
by zvládla akúkoľvek intelektuálnu úlohu ako človek, je zatiaľ predmetom  
výskumu a živých debát.  

## 3. Prečo práve teraz

Myšlienka umelej inteligencie je stará vyše 70 rokov. Prečo zažívame boom  
práve teraz? Zišli sa tri faktory naraz:  

- Dáta: internet vytvoril obrovské množstvo textov, obrázkov a videí, na  
ktorých sa modely môžu učiť.  
- Výpočtový výkon: grafické karty (GPU) umožnili trénovať modely s miliardami  
parametrov.  
- Algoritmy: architektúra Transformer z roku 2017 výrazne zlepšila prácu s  
jazykom a stala sa základom dnešných jazykových modelov.  

Zlomovým momentom pre verejnosť bol november 2022, keď OpenAI sprístupnila  
ChatGPT. Za približne dva mesiace mal podľa odhadov okolo 100 miliónov  
používateľov, čím sa stal jednou z najrýchlejšie rastúcich aplikácií v  
histórii. Odvtedy sa vývoj nezastavil: modely sú presnejšie, lacnejšie,  
pracujú s obrázkami, zvukom aj videom a čoraz viac samostatne konajú.  

## 4. Čo AI dnes zvláda a čo nie

AI je dnes veľmi dobrá v týchto úlohách:  

- písanie, prepisovanie, skracovanie a preklad textov  
- sumarizácia dlhých dokumentov a vyhľadávanie v nich  
- vysvetľovanie zložitých tém jednoduchým jazykom  
- generovanie a opravovanie kódu  
- tvorba obrázkov, prezentácií a návrhov  
- brainstorming a hľadanie nápadov  
- analýza tabuliek a dát  

Slabiny, na ktoré treba myslieť:  

- Halucinácie: model dokáže sebaisto tvrdiť nepravdu, vymyslieť citát, zdroj  
či číslo.  
- Aktuálnosť: znalosti modelu končia dátumom tréningu, ak nemá prístup k  
vyhľadávaniu.  
- Presnosť vo faktoch a výpočtoch: výsledky treba overovať, najmä čísla, mená  
a odkazy.  
- Kontext: model nevie nič o vašej firme ani situácii, kým mu to nepoviete.  
- Zodpovednosť: AI za výsledok neručí. Ručíte vy.  

Dobrá pomôcka: pristupujte k AI ako k veľmi rýchlemu, sčítanému, ale niekedy  
príliš sebavedomému asistentovi. Úlohu mu zadajte jasne a výsledok  
skontrolujte.  

## 5. Základné pojmy

Krátky slovník, ku ktorému sa budeme v ďalších kapitolách vracať:  

- Model: natrénovaný program, ktorý z vstupu vytvára výstup, napríklad odpoveď  
na otázku.  
- Prompt: zadanie, ktoré modelu napíšete. Jeho kvalita priamo ovplyvňuje  
kvalitu odpovede.  
- Token: časť textu, s ktorou model pracuje, zhruba slovo alebo jeho kúsok.  
Podľa tokenov sa často počíta cena aj limity.  
- Kontextové okno: koľko textu (tokenov) model naraz „vidí", teda zadanie,  
priložené dokumenty aj doterajšiu konverzáciu.  
- Tréning: proces, keď sa model učí z dát. Je drahý a robí ho výrobca modelu.  
- Inferencia: používanie hotového modelu, teda to, čo robíte vy, keď mu  
píšete.  
- Halucinácia: vierohodne znejúca, ale nepravdivá odpoveď.  
- Otvorený model (open-weight): model, ktorého váhy si môžete stiahnuť a  
spustiť na vlastnom počítači.  
- API: rozhranie, cez ktoré s modelom komunikujú programy a iné aplikácie.  
Prístup sa overuje API kľúčom.  
- Agent: systém postavený na modeli, ktorý si úlohu sám rozdelí na kroky,  
používa nástroje (web, súbory, aplikácie) a postupne ju vykoná.  


## Zásady bezpečnosti hneď na začiatok

Skôr než začneme, niekoľko pravidiel, ktoré platia počas celého školenia aj po  
ňom:  

- Nevkladajte do AI nástrojov heslá, čísla kariet, rodné čísla ani iné citlivé  
údaje.  
- Pri firemných dokumentoch si overte, či vaša organizácia daný nástroj  
povoľuje a ako s dátami narába.  
- Osobné údaje podliehajú GDPR, a to aj vtedy, keď ich „len" vložíte do chatu.  
- Dôležité výstupy vždy skontrolujte, najmä fakty, čísla, citácie a právne či  
zdravotné informácie.  
- Pri zverejňovaní obsahu vytvoreného AI myslite na autorské práva a na to, či  
je vhodné uviesť, že ho vytvorila AI.  


## Zhrnutie

- AI je široký pojem, dnešný boom ťahajú hlavne veľké jazykové modely a  
generatívna AI.  
- Dôvodom rozmachu je kombinácia dát, výpočtového výkonu a architektúry  
Transformer.  
- AI je výkonný pomocník, ale mýli sa. Overovanie a zodpovednosť zostávajú na  
vás.  
- Kvalita výstupu závisí od kvality zadania.  
- Najviac sa naučíte tým, že budete skúšať. Tak poďme na to.

# Dáta na trénovanie AI modelov

## 1. Prečo sú dáta kľúčové  

Model nie je „múdry“ sám od seba. To, čo vie a ako sa správa, závisí od dát, na  
ktorých sa učil. Kvalita, množstvo a pôvod dát určujú schopnosti modelu, jeho  
chyby, predsudky aj právne riziká. Preto sa hovorí, že dáta sú pre AI to, čo  
palivo pre motor.  

Dáta sú zároveň miestom, kde vzniká väčšina sporov okolo umelej inteligencie:  
kto je autorom, kto za použitie platí a čo je ešte dovolené. O tom je aj tento  
dokument.  

## 2. Aké dáta sa používajú  

### Pri jazykových modeloch (LLM)  

- Webové stránky: najväčší zdroj. Využíva sa napríklad verejný archív Common  
  Crawl, z ktorého sa po filtrovaní tvorí veľká časť dát.  
- Knihy: kvalitný, súvislý text, preto veľmi cenný.  
- Wikipédia a encyklopédie.  
- Vedecké články a odborné texty.  
- Zdrojový kód (napr. verejné repozitáre).  
- Diskusie a fóra, rozhovory, otázky a odpovede.  
- Licencované dáta: zmluvy s vydavateľmi, spravodajskými webmi či platformami.  
- Syntetické dáta: texty vygenerované inými modelmi, často na zlepšenie  
  zdôvodňovania alebo programovania.  
- Ľudská spätná väzba: ľudia hodnotia a opravujú odpovede modelu, čím ho učia  
  byť užitočným a bezpečným.  

### Pri obrazových modeloch  

- Dvojice obrázok a popis (text) získané z internetu.  
- Označkované súbory obrázkov pre klasifikáciu (napr. ImageNet).  
- Licencované fotobanky, napríklad Adobe Stock pri nástroji Adobe Firefly.  
- Syntetické a doladené dáta na zlepšenie kvality a bezpečnosti.  

## 3. Koľko dát je potrebných  

### Texty  

Veľkosť textových dát sa meria v tokenoch (slová alebo ich časti). Model GPT-3 z  
roku 2020 sa učil na stovkách miliárd tokenov. Novšie modely, napríklad Llama 3  
od Meta, na približne 15 biliónoch tokenov. Najväčší výrobcovia už presné čísla  
pre svoje súčasné modely zvyčajne neuvádzajú.  

### Obrázky  

Obrazové modely potrebujú obrovské množstvo obrázkov. Orientačne:  

- ImageNet (2009 a ďalej): približne 14 miliónov označkovaných obrázkov. Základ  
  pre rozpoznávanie obrázkov, nie pre generovanie.  
- DALL-E (prvá verzia, 2021): približne 250 miliónov dvojíc obrázok a text.  
- CLIP (OpenAI, 2021): približne 400 miliónov dvojíc obrázok a text.  
- LAION-5B (2022): 5,85 miliardy dvojíc obrázok a text, z toho 2,32 miliardy v  
  angličtine. Ide o zoznam odkazov na obrázky z internetu, nie o samotné súbory.  
- Stable Diffusion: trénovaný na podmnožinách LAION, teda rádovo na stovkách  
  miliónov až miliardách obrázkov.  
- Midjourney, DALL-E 3, Imagen a ďalšie: výrobcovia presné počty nezverejňujú.  

Z toho vyplýva, že moderné obrazové modely sa nezaobídu bez miliónov až miliárd  
obrázkov a v praxi ich výrobcovia berú z verejného internetu. Práve tu vznikajú  
spory o autorské práva.  

## 4. Ako sa z dát stane tréningová sada  

1. Zber: stiahnutie dát z webu, kníh, licencií a ďalších zdrojov.  
2. Čistenie a filtrovanie: odstránenie duplikátov, spamu, nekvalitných alebo  
   škodlivých textov.  
3. Označkovanie a príprava: rozdelenie na tokeny, doplnenie popisov, rozdelenie  
   na trénovaciu a testovaciu časť.  
4. Trénovanie: model sa učí zo vzorov v dátach.  
5. Doladenie a zosúladenie: ľudská spätná väzba, bezpečnostné pravidlá a  
   testovanie.  

## 5. Syntetické dáta: keď dáta vytvára sama umelá inteligencia  

### 5.1 Čo sú syntetické dáta  

Syntetické dáta sú umelo vytvorené dáta, ktoré nevznikli bežnou ľudskou  
činnosťou ani meraním v reálnom svete. Vygeneroval ich program, simulátor alebo  
iný AI model. Pri jazykových modeloch ide najčastejšie o texty, otázky a  
odpovede, príklady kódu alebo riešenia úloh. Pri obrazových modeloch o popisy  
obrázkov, vygenerované scény alebo simulácie.  

Myšlienka nie je nová. Systém AlphaZero sa naučil hrať šach a go tak, že hral  
sám proti sebe a vytváral si vlastné partie. Dnes sa podobný princíp používa aj  
pri jazykových modeloch.  

### 5.2 Prečo sa používajú  

- Nedostatok kvalitných dát: veľká časť dostupného textu z internetu je už  
  využitá a ďalší kvalitný text pribúda pomaly.  
- Cena ľudskej práce: ručné písanie príkladov a ich označkovanie je pomalé a  
  drahé.  
- Zriedkavé situácie: nehody, chyby, zriedkavé choroby alebo nebezpečné scenáre  
  sa v reálnych dátach vyskytujú málo.  
- Súkromie: namiesto skutočných údajov o pacientoch či zákazníkoch možno použiť  
  umelé záznamy s podobnými vlastnosťami.  
- Kontrola: dáta možno navrhnúť presne na schopnosť, ktorú chceme model naučiť,  
  napríklad matematiku alebo programovanie.  
- Právne dôvody: firmy sa tak snažia znížiť závislosť od sporných zdrojov.  
  Pozor, generujúci model sa sám mohol učiť z cudzích diel.  

### 5.3 Hlavné spôsoby tvorby  

- Prepisovanie (rephrasing): model prepíše existujúci text do čistejšej,  
  zrozumiteľnejšej podoby, napríklad ako encyklopédický článok alebo sériu  
  otázok a odpovedí. Informácie ostanú, mení sa len spôsob podania. Veľké  
  zbierky, napríklad Nemotron-CC od NVIDIA, majú v sebe približne 1,9 bilióna  
  syntetických tokenov (z 6,3 bilióna).  
- Inštrukčné dáta: model vygeneruje veľa zadaní a vzorových odpovedí. Metóda  
  Self-Instruct (2022) a model Alpaca (2023) ukázali, že stačí relatívne malý  
  súbor takto vytvorených príkladov, aby sa model naučil poslúchať pokyny.  
- Učebnicové dáta: model napíše „učebnice“ a cvičenia na vybranú tému. Rodina  
  modelov Phi od Microsoftu (2023) ukázala, že malý model môže byť prekvapivo  
  schopný, ak sa učí z veľmi premyslených dát. Čisto učebnicový štýl však pri  
  vysokom podiele môže kvalitu naopak zhoršiť.  
- Destilácia: veľký a výkonný „učiteľský“ model vytvorí odpovede, z ktorých sa  
  učí menší „žiak“. Tak vznikajú malé a rýchle modely.  
- Overiteľné úlohy: pri programovaní a matematike možno vygenerované riešenia  
  automaticky skontrolovať (kód spustiť, výsledok porovnať so správnym). Do  
  tréningu sa dostanú len riešenia, ktoré prešli.  
- Persony: model píše z pohľadu množstva vymyslených osôb (lekár, študent,  
  účtovník), čím sa zvyšuje rozmanitosť. Príkladom je súbor Persona Hub s  
  miliardou person či Nemotron-Personas.  
- Spätný preklad (back-translation): text sa preloží do iného jazyka a späť, čím  
  vznikne ďalší variant. Hodí sa najmä pre menšie jazyky, ako je slovenčina, kde  
  je málo pôvodných dát.  
- Simulátory: v robotike, autonómnom šoférovaní či priemysle sa scény generujú  
  vo virtuálnych svetoch, kde možno bezpečne vyskúšať aj nebezpečné situácie.  
- Popisy obrázkov: model automaticky opíše obrázky, aby mal obrazový model  
  presnejšie texty na učenie (viď kapitolu 6).  

### 5.4 Typický postup  

1. Zdroj (seed): skutočné texty, témy, osoby alebo zadania, od ktorých sa  
   vychádza.  
2. Generovanie: model s presne napísaným zadaním vytvorí množstvo príkladov.  
3. Filtrovanie a kontrola: odstránenie duplikátov, chýb a nekvalitných výstupov.  
   Pomáhajú testy, pravidlá alebo iný model v úlohe hodnotiteľa, v kritických  
   oblastiach aj ľudia.  
4. Miešanie s reálnymi dátami: syntetické dáta sa pridávajú, nenahrádzajú  
   pôvodné.  
5. Trénovanie a testovanie na skutočných, ľudsky vytvorených úlohách, nie len na  
   vlastných syntetických.  

### 5.5 Aké sú dôkazy, že to funguje  

Prax aj výskum ukazujú, že vhodne použité syntetické dáta modely zlepšujú a  
zrýchľujú ich učenie, najmä v matematike, kóde a pri dodržiavaní pokynov. Podľa  
viacerých štúdií je najlepším riešením zmes prepísaných a pôvodných webových  
dát. Aj Microsoft sa pri ďalších verziách modelov Phi vrátil k miešaniu s  
webovými dátami. Nie každý výrobca ich však používa rovnako. Niektorí sa  
syntetickým dátam pri predtrénovaní zámerne vyhýbajú.  

### 5.6 Riziká a limity  

- Kolaps modelu (model collapse): keď sa modely opakovane učia z výstupov iných  
  modelov, postupne strácajú rozmanitosť a zriedkavejšie javy. Štúdia v časopise  
  Nature (2024) tento efekt opísala. Ďalší výskum ukázal, že riziko sa výrazne  
  znižuje, ak sa k syntetickým dátam stále pridávajú aj pôvodné ľudské dáta.  
- Chyby sa dedia: ak generujúci model halucinuje alebo je predpojatý, tieto  
  vlastnosti sa môžu preniesť na nový model. Novšie štúdie varujú aj pred  
  zosilňovaním predsudkov.  
- Nízka rozmanitosť: model píše podobne, a tak vzniká jednotvárny obsah.  
- Kontaminácia testov: syntetické dáta môžu náhodou obsahovať otázky z  
  benchmarkov.  
- Licencie: podmienky niektorých poskytovateľov zakazujú používať výstupy ich  
  modelov na trénovanie konkurenčných modelov.  
- Falošný pocit pokroku: veľké číslo tokenov neznamená vyššiu kvalitu, ak je  
  obsah opakujúci sa alebo nepravdivý.  

## 6. Ako sa obrazové modely stali použiteľnými  

Za bod zlomu sa dá považovať rok 2022, keď sa obrazové modely stali prvýkrát  
skutočne použiteľné pre bežných ľudí. Predtým mali generatívne siete (GAN, od  
roku 2014) problém s kontrolou: dokázali vytvoriť napríklad presvedčivé tváre,  
no nie obrázok podľa ľubovoľného textového zadania. Zmenu priniesla kombinácia  
viacerých vecí. Po prvé, modely CLIP a DALL-E (január 2021) ukázali, že sa dá  
učiť z veľkých súborov obrázkov s popismi z internetu (CLIP na približne 400  
miliónoch dvojíc) a prepojiť text s obrazom. Po druhé, difúzne modely (od roku  
2020, v generovaní obrázkov z textu model GLIDE koncom 2021) sa naučili tvoriť  
obraz postupným odstraňovaním šumu, čo dalo oveľa vyššiu kvalitu než predošlé  
prístupy. Po tretie, DALL-E 2 (apríl 2022), Imagen (máj 2022) a Midjourney (leto  
2022) priniesli kvalitu, ktorá prekvapila aj odborníkov. Po štvrté, Stable  
Diffusion (august 2022) bežal v zhustenom „latentnom“ priestore, takže ho bolo  
možné spustiť aj na bežnej grafickej karte, a jeho zverejnené váhy spustili  
lavínu ďalších úprav. To umožnil aj otvorený dataset LAION-5B s miliardami  
dvojíc obrázok a text. Ďalší výrazný krok prišiel v roku 2023 s modelom DALL-E  
3, ktorý sa učil na obrázkoch s podrobnými syntetickými popismi vytvorenými iným  
modelom, čo zásadne zlepšilo dodržiavanie zadania. V rokoch 2025 a 2026 sa  
obrazová tvorba presunula priamo do veľkých multimodálnych modelov (GPT-4o v  
marci 2025, Gemini 2.5 Flash Image v auguste 2025), ktoré zvládajú čitateľný  
text, úpravy obrázkov a udržanie podoby postáv.  


### 6.1 Kľúčové míľniky v skratke  

- 2014: GAN, prvé presvedčivé syntetické obrázky.  
- Január 2021: DALL-E a CLIP, prepojenie textu a obrazu.  
- 2020 až 2021: difúzne modely (DDPM, GLIDE) a latentná difúzia.  
- 2022: DALL-E 2, Imagen, Midjourney a Stable Diffusion.  
- 2023: DALL-E 3 a syntetické popisy, SDXL.  
- 2025: obrázky priamo vo veľkých modeloch (GPT-4o, Gemini).  

## 7. Incidenty a spory okolo dát  

Rýchly rast AI vyvolal otázku, odkiaľ firmy vzali dáta. Niektoré prípady  
skončili pred súdom. Pri každom je dôležité rozlišovať: čo súd rozhodol, čo sa  
dohodlo vyrovnaním a čo sú zatiaľ len tvrdenia žalobcov.  

### 7.1 Anthropic: pirátske knihy a ničenie tlačených kníh  

Anthropic, tvorca modelov Claude, získaval knihy dvoma spôsobmi. Jednak stiahol  
milióny kníh z pirátskych knižníc (LibGen, PiLiMi a ďalšie), jednak kúpil  
milióny tlačených kníh. Tie nechal rozrezať, naskenovať a pôvodné výtlačky  
vyradil.  

Sudca William Alsup v júni 2025 rozhodol dvojako:  

- Trénovanie modelov na legálne získaných knihách považoval za „fair use“. Aj  
  skenovanie kúpených tlačených kníh bolo v poriadku.  
- Vytvorenie trvalej knižnice z pirátskych kópií za fair use nepovažoval.  

Nasledovalo vyrovnanie vo výške 1,5 miliardy dolárov, približne 3 000 dolárov za  
dielo, pre takmer 482 000 kníh. Súd ho definitívne schválil 20. júla 2026 a ide  
o najväčšie vyrovnanie v histórii autorského práva v USA. Anthropic sa v ňom  
zaviazal aj zničiť pirátske súbory. Výplaty sa očakávajú do 15. novembra 2026.  

Poznámka: dokument vznikol s pomocou asistenta Claude, ktorého vyvíja Anthropic.  
Údaje preto radšej overte aj v nezávislých zdrojoch.  

### 7.2 Meta: torrentovanie pirátskych knižníc  

Meta v rámci prípadu Kadrey v. Meta čelí tvrdeniam, že pri tréningu modelov  
Llama sťahovala knihy z pirátskych knižníc (LibGen, Anna's Archive) cez protokol  
BitTorrent. Médiá uvádzajú desiatky terabajtov dát (údaj 81,7 TB sa týka  
celkového objemu).  

- Jún 2025: sudca Vince Chhabria rozhodol vo veci trénovania v prospech Mety.  
  Zdôraznil však, že rozsudok je viazaný na predložené dôkazy a nie je  
  všeobecným povolením.  
- Otvorená zostala otázka, či Meta pirátske súbory pri torrentovaní aj ďalej  
  šírila (tzv. seeding).  
- Júl 2026: žiadosť autorov o predčasné odvolanie bola zamietnutá. Spor  
  pokračuje.  

### 7.3 OpenAI: tvrdenia o LibGen a mazaní dát  

V prípade Authors Guild v. OpenAI a Microsoft boli v septembri 2026 odtajnené  
podania žalobcov. Podľa nich OpenAI:  

- stiahla v roku 2018 približne 117 500 kníh z LibGen a v rokoch 2019 až 2020  
  cez torrent približne 35 TB, čo má zodpovedať celej zbierke LibGen (milióny  
  kníh);  
- knihy použila na trénovanie GPT-3 (datasety Books1 a Books2);  
- o použití LibGen informovala už v roku 2019 aj Microsoft;  
- v roku 2022 súbory vymazala v interne nazvanom projekte „Clear“.  

Interné správy podľa žalobcov ukazujú, že zamestnanci sa obávali skôr zlého  
obrazu na verejnosti než zákona. OpenAI sa bráni tvrdením, že išlo o fair use.  
Rozhodnutie súdu zatiaľ neexistuje, preto ide o tvrdenia žalobcov, nie o  
právoplatné zistenia.  

### 7.4 Ďalšie dôležité prípady  

- Books3: súbor približne 200 000 kníh z pirátskeho zdroja, ktorý bol súčasťou  
  datasetu The Pile a používal sa na trénovanie viacerých modelov. V roku 2023  
  bol po sťažnosti stiahnutý.  
- LAION-5B a zneužívanie detí: v decembri 2023 výskumníci zo Stanfordu našli v  
  zozname 1 008 odkazov na materiál sexuálneho zneužívania detí. Dataset bol  
  stiahnutý a v auguste 2024 vydaný vyčistený Re-LAION-5B, z ktorého bolo  
  odstránených 2 236 odkazov.  
- Getty Images v. Stability AI: Getty tvrdila, že Stable Diffusion sa trénoval  
  na jej fotografiách. Vo Veľkej Británii súd v novembri 2025 zamietol hlavný  
  autorskoprávny nárok, uznal však čiastočné porušenie ochranných známok  
  (vodoznaky). Getty získala povolenie na odvolanie.  

## 8. Čo z incidentov vyplýva  

- Samotné trénovanie na legálne získaných dátach súdy zatiaľ v USA viackrát  
  posúdili ako fair use. Nie je to však všeobecné pravidlo a rozhodnutia sa môžu  
  líšiť.  
- Rozhodujúce je, ako boli dáta získané. Pirátske zdroje sa ukázali ako  
  najväčšie riziko a najdrahšia chyba.  
- Stále chýba jasná odpoveď na otázky výstupov, licencovania a kompenzácie  
  autorov. Prípady sú otvorené a rozhodnutia sa budú vyvíjať.  
- Firmy sa presúvajú k licenčným dohodám s vydavateľmi, fotobankami a  
  platformami.  
- V Európe platí výnimka pre dolovanie textov a dát s možnosťou odhlásenia sa  
  nositeľa práv a AI Act ukladá poskytovateľom univerzálnych modelov povinnosti  
  týkajúce sa autorských práv a zhrnutia tréningových dát.  

## 9. Ďalšie problémy s dátami  

- Predsudky: model preberá stereotypy z dát.  
- Jazyková nerovnosť: dát v angličtine je neporovnateľne viac než v slovenčine,  
  preto bývajú výsledky v slovenčine slabšie.  
- Súkromie a osobné údaje: dáta z internetu môžu obsahovať osobné údaje a  
  podliehajú GDPR.  
- Kontaminácia testov: ak sa testovacie úlohy dostanú do tréningu, benchmark  
  ukazuje lepší výsledok, než model reálne dosahuje.  
- Syntetické dáta: ak sa modely učia z textov iných modelov, hrozí znižovanie  
  kvality a rozmanitosti.  
- Škodlivý a nezákonný obsah: filtrovanie nie je dokonalé.  

## 10. Zhrnutie  

- Modely sa učia z obrovského množstva textov a obrázkov, často z verejného  
  internetu a kníh.  
- Obrazové modely potrebujú stovky miliónov až miliardy obrázkov.  
- Prípady Anthropic, Meta a OpenAI ukazujú, že sporný je najmä spôsob získania  
  dát, nie len samotné učenie.  
- Stav sporov sa mení, preto si pred školením aktuálne informácie overte.  
- Syntetické dáta modely zlepšujú, no musia sa kontrolovať a miešať s reálnymi  
  dátami, inak hrozí kolaps modelu.  
- Obrazové modely sa stali použiteľnými okolo roku 2022 vďaka veľkým súborom  
  obrázkov, difúznym modelom a otvoreným modelom.

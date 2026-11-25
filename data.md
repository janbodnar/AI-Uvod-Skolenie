# Dáta na trénovanie AI modelov  

*Stav k 25. novembru 2026. Súdne spory a legislatíva sa rýchlo menia, pred  
použitím na školení si aktuálny stav overte.*  

## 1. Prečo sú dáta kľúčové  

Model nie je „múdry“ sám od seba. To, čo vie a ako sa správa, závisí od dát,  
na ktorých sa učil. Kvalita, množstvo a pôvod dát určujú jeho schopnosti,  
chyby, predsudky aj právne riziká. Preto sa hovorí, že dáta sú pre AI tým, čím  
je palivo pre motor.  

Dáta sú zároveň miestom, kde vzniká väčšina sporov okolo umelej inteligencie:  
kto je autorom, kto za použitie platí a čo je ešte dovolené. O tom je aj tento  
dokument.  

## 2. Aké dáta sa používajú  

### Pri jazykových modeloch (LLM)  

- **Webové stránky:** najväčší zdroj. Využíva sa napríklad verejný archív  
  Common Crawl, z ktorého sa po filtrovaní tvorí veľká časť dát.  
- **Knihy:** kvalitný, dlhý a súvislý text, preto veľmi cenný.  
- **Wikipédia a encyklopédie.**  
- **Vedecké články a odborné texty.**  
- **Zdrojový kód:** napríklad verejné repozitáre.  
- **Diskusie a fóra:** rozhovory, otázky a odpovede.  
- **Licencované dáta:** zmluvy s vydavateľmi, spravodajskými webmi,  
  fotobankami či platformami.  
- **Dáta z vlastných služieb:** niektoré firmy využívajú aj verejný obsah zo  
  svojich platforiem (napríklad Meta pri modeloch Llama).  
- **Syntetické dáta:** texty vygenerované inými modelmi, často na zlepšenie  
  uvažovania alebo programovania (podrobne v kapitole 5).  
- **Ľudská spätná väzba:** ľudia hodnotia a opravujú odpovede modelu, čím ho  
  učia byť užitočným a bezpečným.  

### Pri obrazových modeloch  

- Dvojice obrázok a popis (text) získané z internetu.  
- Označkované súbory obrázkov na klasifikáciu (napr. ImageNet).  
- Licencované fotobanky, napríklad Adobe Stock pri nástroji Adobe Firefly.  
- Syntetické popisy a doladené dáta na zlepšenie kvality a bezpečnosti.  

## 3. Koľko dát je potrebných  

### Texty  

Veľkosť textových dát sa meria v **tokenoch** (slová alebo ich časti; v  
angličtine je jedno slovo v priemere niečo vyše jedného tokenu, v slovenčine  
viac).  

| Model | Rok | Objem tréningových dát |
|---|---|---|
| GPT-3 (OpenAI) | 2020 | stovky miliárd tokenov |
| Llama 3 (Meta) | 2024 | približne 15 biliónov tokenov |
| Llama 4 (Meta) | 2025 | viac než 30 biliónov tokenov |
| Qwen3 (Alibaba) | 2025 | približne 36 biliónov tokenov v 119 jazykoch |

Za päť rokov tak objem dát vzrástol približne stonásobne. Najväčší výrobcovia  
(OpenAI, Google, Anthropic) už presné čísla pre svoje súčasné modely zvyčajne  
neuvádzajú. Čísla zverejňujú najmä výrobcovia otvorených modelov.  

### Obrázky  

Obrazové modely potrebujú obrovské množstvo obrázkov. Orientačne:  

| Dataset / model | Rok | Objem |
|---|---|---|
| ImageNet | 2009 a ďalej | ~14 miliónov označkovaných obrázkov (základ rozpoznávania, nie generovania) |
| DALL-E (1. verzia) | 2021 | ~250 miliónov dvojíc obrázok – text |
| CLIP (OpenAI) | 2021 | ~400 miliónov dvojíc obrázok – text |
| LAION-5B | 2022 | 5,85 miliardy dvojíc, z toho 2,32 miliardy v angličtine |
| Stable Diffusion | 2022 | podmnožiny LAION, stovky miliónov až miliardy obrázkov |
| Midjourney, DALL-E 3, Imagen, GPT Image, Nano Banana | 2022 – 2026 | výrobcovia počty nezverejňujú |

Pozor: LAION-5B je **zoznam odkazov** na obrázky z internetu s popismi, nie  
samotné súbory. Kto podľa neho trénuje, musí si obrázky stiahnuť sám.  

Z toho vyplýva, že moderné obrazové modely sa nezaobídu bez stoviek miliónov  
až miliárd obrázkov a v praxi ich výrobcovia berú z verejného internetu. Práve  
tu vznikajú spory o autorské práva.  

## 4. Ako sa z dát stane tréningová sada  

1. **Zber:** stiahnutie dát z webu, kníh, licencií a ďalších zdrojov.  
2. **Čistenie a filtrovanie:** odstránenie duplikátov, spamu, nekvalitných,  
   škodlivých textov a osobných údajov.  
3. **Príprava:** rozdelenie na tokeny, doplnenie popisov, rozdelenie na  
   trénovaciu a testovaciu časť.  
4. **Predtrénovanie (pretraining):** model sa učí zo vzorov v obrovskom  
   množstve dát. Je to najdrahšia fáza.  
5. **Doladenie a zosúladenie (fine-tuning, alignment):** ľudská spätná väzba,  
   bezpečnostné pravidlá a testovanie.  

Väčšina práce pri tvorbe dobrého modelu nie je v samotnom trénovaní, ale v  
kroku 2: v tom, čo sa do dát dostane a čo sa vyhodí.  

## 5. Syntetické dáta: keď dáta vytvára sama umelá inteligencia  

### 5.1 Čo sú syntetické dáta  

Syntetické dáta sú umelo vytvorené dáta, ktoré nevznikli bežnou ľudskou  
činnosťou ani meraním v reálnom svete. Vygeneroval ich program, simulátor  
alebo iný AI model. Pri jazykových modeloch ide najčastejšie o texty, otázky a  
odpovede, príklady kódu alebo riešenia úloh. Pri obrazových modeloch o popisy  
obrázkov, vygenerované scény alebo simulácie.  

Myšlienka nie je nová. Systém AlphaZero (2017) sa naučil hrať šach a go tak,  
že hral sám proti sebe a vytváral si vlastné partie. Dnes sa podobný princíp  
používa aj pri jazykových modeloch.  

### 5.2 Prečo sa používajú  

- **Nedostatok kvalitných dát:** veľká časť dostupného textu z internetu je už  
  využitá a ďalší kvalitný text pribúda pomaly. Výskumníci z Epoch AI odhadli  
  zásobu verejného ľudského textu na približne 300 biliónov tokenov a  
  predpovedali, že sa vyčerpá niekedy medzi rokmi 2026 a 2032.  
- **Cena ľudskej práce:** ručné písanie príkladov a ich označkovanie je pomalé  
  a drahé.  
- **Zriedkavé situácie:** nehody, chyby, zriedkavé choroby alebo nebezpečné  
  scenáre sa v reálnych dátach vyskytujú málo.  
- **Súkromie:** namiesto skutočných údajov o pacientoch či zákazníkoch možno  
  použiť umelé záznamy s podobnými vlastnosťami.  
- **Kontrola:** dáta možno navrhnúť presne na schopnosť, ktorú chceme model  
  naučiť, napríklad matematiku alebo programovanie.  
- **Právne dôvody:** firmy sa tak snažia znížiť závislosť od sporných zdrojov.  
  Pozor, generujúci model sa sám mohol učiť z cudzích diel, takže problém  
  nemusí úplne zmiznúť.  

### 5.3 Hlavné spôsoby tvorby  

- **Prepisovanie (rephrasing):** model prepíše existujúci text do čistejšej,  
  zrozumiteľnejšej podoby, napríklad ako encyklopédický článok alebo sériu  
  otázok a odpovedí. Informácie ostanú, mení sa len spôsob podania. Napríklad  
  zbierka Nemotron-CC od NVIDIA má približne 1,9 bilióna syntetických tokenov  
  z celkových 6,3 bilióna.  
- **Inštrukčné dáta:** model vygeneruje veľa zadaní a vzorových odpovedí.  
  Metóda Self-Instruct (2022) a model Alpaca (2023) ukázali, že stačí  
  relatívne malý súbor takto vytvorených príkladov, aby sa model naučil  
  poslúchať pokyny.  
- **Učebnicové dáta:** model napíše „učebnice“ a cvičenia na vybranú tému.  
  Rodina modelov Phi od Microsoftu (od roku 2023) ukázala, že malý model môže  
  byť prekvapivo schopný, ak sa učí z veľmi premyslených dát. Čisto učebnicový  
  štýl však pri vysokom podiele môže kvalitu naopak zhoršiť.  
- **Destilácia:** veľký a výkonný „učiteľský“ model vytvorí odpovede, z  
  ktorých sa učí menší „žiak“. Tak vznikajú malé a rýchle modely.  
- **Overiteľné úlohy:** pri programovaní a matematike možno vygenerované  
  riešenia automaticky skontrolovať (kód spustiť, výsledok porovnať so  
  správnym). Do tréningu sa dostanú len riešenia, ktoré prešli. Na tomto  
  princípe stoja aj dnešné „uvažujúce“ (reasoning) modely.  
- **Persony:** model píše z pohľadu množstva vymyslených osôb (lekár, študent,  
  účtovník), čím sa zvyšuje rozmanitosť. Príkladom je súbor Persona Hub s  
  miliardou person či Nemotron-Personas.  
- **Spätný preklad (back-translation):** text sa preloží do iného jazyka a  
  späť, čím vznikne ďalší variant. Hodí sa najmä pre menšie jazyky, ako je  
  slovenčina, kde je málo pôvodných dát.  
- **Simulátory:** v robotike, autonómnom šoférovaní či priemysle sa scény  
  generujú vo virtuálnych svetoch, kde možno bezpečne vyskúšať aj nebezpečné  
  situácie.  
- **Popisy obrázkov:** model automaticky opíše obrázky, aby mal obrazový model  
  presnejšie texty na učenie (pozri kapitolu 6).  

### 5.4 Typický postup  

1. **Zdroj (seed):** skutočné texty, témy, osoby alebo zadania, od ktorých sa  
   vychádza.  
2. **Generovanie:** model s presne napísaným zadaním vytvorí množstvo  
   príkladov.  
3. **Filtrovanie a kontrola:** odstránenie duplikátov, chýb a nekvalitných  
   výstupov. Pomáhajú testy, pravidlá alebo iný model v úlohe hodnotiteľa, v  
   kritických oblastiach aj ľudia.  
4. **Miešanie s reálnymi dátami:** syntetické dáta sa pridávajú, nenahrádzajú  
   pôvodné.  
5. **Trénovanie a testovanie** na skutočných, ľudsky vytvorených úlohách, nie  
   len na vlastných syntetických.  

### 5.5 Aké sú dôkazy, že to funguje  

Prax aj výskum ukazujú, že vhodne použité syntetické dáta modely zlepšujú a  
zrýchľujú ich učenie, najmä v matematike, programovaní a pri dodržiavaní  
pokynov. Podľa viacerých štúdií je najlepším riešením zmes prepísaných a  
pôvodných webových dát. Aj Microsoft sa pri ďalších verziách modelov Phi  
vrátil k miešaniu s webovými dátami. Nie každý výrobca ich však používa  
rovnako, niektorí sa syntetickým dátam pri predtrénovaní zámerne vyhýbajú.  

### 5.6 Riziká a limity  

- **Kolaps modelu (model collapse):** keď sa modely opakovane učia z výstupov  
  iných modelov, postupne strácajú rozmanitosť a zriedkavejšie javy. Štúdia v  
  časopise Nature (2024) tento efekt opísala. Ďalší výskum ukázal, že riziko  
  sa výrazne znižuje, ak sa k syntetickým dátam stále pridávajú aj pôvodné  
  ľudské dáta.  
- **Chyby sa dedia:** ak generujúci model halucinuje alebo je predpojatý,  
  tieto vlastnosti sa môžu preniesť na nový model, prípadne zosilniť.  
- **Nízka rozmanitosť:** modely píšu podobne, a tak vzniká jednotvárny obsah.  
- **Kontaminácia testov:** syntetické dáta môžu náhodou obsahovať otázky z  
  benchmarkov.  
- **Licencie:** podmienky niektorých poskytovateľov zakazujú používať výstupy  
  ich modelov na trénovanie konkurenčných modelov.  
- **Falošný pocit pokroku:** veľké číslo tokenov neznamená vyššiu kvalitu, ak  
  je obsah opakujúci sa alebo nepravdivý.  
- **Internet sa „zanáša“:** čoraz viac textov a obrázkov na webe vytvorila AI,  
  takže aj bežné webové dáta už obsahujú syntetický obsah, či to výrobca chce,  
  alebo nie.  

## 6. Ako sa obrazové modely stali použiteľnými  

Za bod zlomu sa dá považovať rok 2022, keď sa obrazové modely prvýkrát stali  
skutočne použiteľnými pre bežných ľudí. Zmenu priniesla kombinácia viacerých  
vecí:  

1. **Prepojenie textu a obrazu.** Predtým mali generatívne siete (GAN, od roku  
   2014) problém s kontrolou: dokázali vytvoriť napríklad presvedčivé tváre,  
   no nie obrázok podľa ľubovoľného textového zadania. Modely CLIP a DALL-E  
   (január 2021) ukázali, že sa dá učiť z veľkých súborov obrázkov s popismi z  
   internetu (CLIP na približne 400 miliónoch dvojíc) a prepojiť text s  
   obrazom.  
2. **Difúzne modely.** Od roku 2020 (DDPM) sa modely naučili tvoriť obraz  
   postupným odstraňovaním šumu, čo dalo oveľa vyššiu kvalitu než predošlé  
   prístupy. Pri generovaní obrázkov z textu to koncom roka 2021 ukázal model  
   GLIDE.  
3. **Skok v kvalite.** DALL-E 2 (apríl 2022), Imagen (máj 2022) a Midjourney  
   (leto 2022) priniesli kvalitu, ktorá prekvapila aj odborníkov.  
4. **Otvorenosť.** Stable Diffusion (august 2022) pracoval v zhustenom  
   „latentnom“ priestore, takže ho bolo možné spustiť aj na bežnej grafickej  
   karte. Jeho zverejnené váhy spustili lavínu ďalších úprav. Umožnil to aj  
   otvorený dataset LAION-5B.  

Ďalší výrazný krok prišiel v roku 2023 s modelom DALL-E 3, ktorý sa učil na  
obrázkoch s podrobnými syntetickými popismi vytvorenými iným modelom, čo  
zásadne zlepšilo dodržiavanie zadania.  

V rokoch 2025 a 2026 sa obrazová tvorba presunula priamo do veľkých  
multimodálnych modelov. Začalo to GPT-4o v ChatGPT (marec 2025) a modelom  
Gemini 2.5 Flash Image, známym ako „Nano Banana“ (august 2025). Nasledovali  
Nano Banana Pro (november 2025), GPT Image 1.5 (december 2025), Nano Banana 2  
(začiatok 2026) a ChatGPT Images 2.0 s modelom GPT Image 2 (apríl 2026), ktorý  
pred kreslením najprv „premýšľa“ nad zadaním. Tieto modely zvládajú čitateľný  
text v obrázku, úpravy existujúcich fotografií, udržanie podoby postáv a  
niektoré aj vyhľadávanie na webe počas tvorby. OpenAI zároveň ohlásil  
vyradenie starších modelov DALL-E 2 a DALL-E 3 z API k 12. máju 2026.  

### 6.1 Kľúčové míľniky v skratke  

- **2014:** GAN, prvé presvedčivé syntetické obrázky.  
- **2020:** difúzne modely (DDPM).  
- **Január 2021:** DALL-E a CLIP, prepojenie textu a obrazu.  
- **December 2021:** GLIDE a latentná difúzia.  
- **2022:** DALL-E 2, Imagen, Midjourney, Stable Diffusion a LAION-5B.  
- **2023:** DALL-E 3 a syntetické popisy, SDXL.  
- **2025:** obrázky priamo vo veľkých modeloch (GPT-4o, Nano Banana, Nano  
  Banana Pro).  
- **2026:** Nano Banana 2, GPT Image 2 a „premýšľajúce“ obrazové modely.  

## 7. Incidenty a spory okolo dát  

Rýchly rast AI vyvolal otázku, odkiaľ firmy vzali dáta. Desiatky prípadov  
skončili pred súdom. Pri každom je dôležité rozlišovať tri veci:  

- čo **súd rozhodol**,  
- čo sa **dohodlo vyrovnaním** (bez rozhodnutia o vine),  
- čo sú zatiaľ **len tvrdenia žalobcov**.  

Pomôcka k americkému právu: **fair use** (spravodlivé použitie) je výnimka,  
ktorá za určitých podmienok dovoľuje použiť cudzie dielo bez súhlasu autora.  
Súd posudzuje štyri faktory, najmä účel použitia (či ide o niečo nové,  
„transformatívne“) a vplyv na trh s pôvodným dielom.  

### 7.1 Anthropic: pirátske knihy a ničenie tlačených kníh (Bartz v.  
Anthropic)  

Anthropic, tvorca modelov Claude, získaval knihy dvoma spôsobmi. Jednak  
stiahol milióny kníh z pirátskych knižníc (LibGen, PiLiMi), jednak kúpil  
milióny tlačených kníh, nechal ich rozrezať, naskenovať a pôvodné výtlačky  
vyradil.  

Sudca William Alsup v júni 2025 rozhodol dvojako:  

- Trénovanie modelov na legálne získaných knihách považoval za fair use. Aj  
  skenovanie kúpených tlačených kníh bolo v poriadku.  
- Vytvorenie trvalej knižnice z pirátskych kópií za fair use nepovažoval.  

Pred hroziacim procesom sa strany v septembri 2025 dohodli na **vyrovnaní 1,5  
miliardy dolárov**, čo je približne 3 000 dolárov za dielo pre takmer 482 500  
kníh. Sumu si delia autori a vydavatelia. Ide o najväčšie vyrovnanie v  
histórii autorského práva v USA. Anthropic sa v ňom zaviazal aj zničiť  
pirátske súbory. Vyrovnanie sa týka len minulého získavania a kopírovania  
kníh, nie výstupov modelu.  

Aktuálny stav:  

- Po odchode sudcu Alsupa do dôchodku vyrovnanie definitívne schválila sudkyňa  
  Araceli Martínez-Olguín **20. júla 2026**. Odmenu advokátov znížila na  
  približne 6,8 % sumy.  
- Nárok si uplatnili majitelia práv k viac než 91 % zahrnutých kníh.  
- Prvé výplaty sú naplánované na týždeň od **23. novembra 2026**. Budú tvoriť  
  približne 70 % celkovej sumy, zvyšok príde neskôr, keď Anthropic doplatí  
  fond.  

*Poznámka: dokument vznikol s pomocou asistenta Claude, ktorého vyvíja  
Anthropic. Údaje preto radšej overte aj v nezávislých zdrojoch.*  

### 7.2 Meta: torrentovanie pirátskych knižníc (Kadrey v. Meta)  

Meta v tomto prípade čelí tvrdeniam, že pri tréningu modelov Llama sťahovala  
knihy z pirátskych knižníc (LibGen, Anna's Archive) cez protokol BitTorrent.  
Médiá uvádzajú desiatky terabajtov dát (údaj 81,7 TB sa týka celkového  
objemu).  

- **Jún 2025:** sudca Vince Chhabria rozhodol vo veci trénovania v prospech  
  Mety. Zdôraznil však, že rozhodnutie vychádza z dôkazov, ktoré autori  
  predložili, a nie je všeobecným povolením. Naznačil, že pri lepšie  
  preukázanom poškodení trhu by mohol rozhodnúť inak.  
- **Otvorená zostala otázka**, či Meta pirátske súbory pri torrentovaní aj  
  ďalej šírila (tzv. seeding, teda posielanie častí súborov ďalším  
  používateľom).  
- **Marec 2026:** súd povolil autorom doplniť žalobu o nárok, že Meta šírením  
  pomáhala porušovať práva iným.  
- **Júl 2026:** sudca zamietol žiadosť autorov o okamžité odvolanie k vyššiemu  
  súdu. Pripustil, že otázka je zložitá a sudcovia sa v nej rozchádzajú.  
- **September a október 2026:** súd nariadil Mete vydať históriu príkazov zo  
  serverov použitých na torrentovanie a menovať manažérov, ktorí o sťahovaní  
  rozhodli. Spor pokračuje.  

Súvisiaci prípad: podľa médií súd v júni 2026 zamietol návrh Mety na  
zastavenie žaloby spoločnosti Strike 3 Holdings, podľa ktorej Meta cez  
BitTorrent sťahovala jej filmy na tréning AI. Aj tu sa spor točí okolo spôsobu  
získania dát, nie okolo samotného tréningu.  

### 7.3 OpenAI: tvrdenia o LibGen a mazaní dát  

Žaloby autorov (vedené Authors Guild) aj vydavateľov novín (napr. The New York  
Times) proti OpenAI a Microsoftu sú spojené do jedného veľkého konania pred  
federálnym súdom v New Yorku (sudca Sidney Stein).  

V septembri 2026 boli odtajnené podania žalobcov. Podľa nich OpenAI:  

- stiahla v roku 2018 knihy z LibGen a v rokoch 2019 až 2020 cez torrent  
  desiatky terabajtov, čo má zodpovedať celej zbierke LibGen (milióny kníh);  
- knihy použila na trénovanie GPT-3 (interné datasety Books1 a Books2);  
- o použití LibGen informovala Microsoft už v apríli 2019;  
- v lete 2022 súbory vymazala v interne nazvanom projekte „Clear“.  

Interné správy podľa žalobcov ukazujú, že zamestnanci sa obávali skôr zlého  
obrazu na verejnosti než zákona. Ešte v novembri 2025 súd nariadil OpenAI  
sprístupniť aj interné komunikácie s právnikmi o dôvodoch vymazania, keďže  
firma svoje vysvetlenie menila.  

Aktuálny stav:  

- V septembri 2026 podali všetky strany návrhy, aby súd o veci rozhodol bez  
  procesu (summary judgment). OpenAI sa bráni tvrdením, že išlo o fair use, a  
  odvoláva sa na rozhodnutia v prípadoch Anthropic a Meta.  
- Ministerstvo spravodlivosti USA sa v septembri 2026 vo svojom stanovisku  
  postavilo na stranu OpenAI. Bolo to prvýkrát, čo sa americká vláda takto  
  zapojila do sporu o tréning AI.  
- Rozhodnutie súdu zatiaľ neexistuje. Uvedené body sú tvrdenia žalobcov, nie  
  právoplatné zistenia.  

### 7.4 Prvé rozhodnutie odvolacieho súdu: Thomson Reuters v. Ross  

Spoločnosť Ross Intelligence použila právne zhrnutia (tzv. headnotes) zo  
služby Westlaw od Thomson Reuters na tréning konkurenčného nástroja na  
vyhľadávanie v práve. Súd prvého stupňa vo februári 2025 rozhodol, že nejde o  
fair use. **Odvolací súd (Tretí obvod) to 29. septembra 2026 potvrdil.** Je to  
prvé rozhodnutie amerického odvolacieho súdu o fair use pri tréningu AI. Súd  
zdôraznil, že Ross vytváral priamu konkurenciu a jeho použitie bolo len  
minimálne transformatívne.  

Dôležité obmedzenie: išlo o jednoduchší, negeneratívny AI systém, nie o veľký  
jazykový model. Pre ChatGPT a podobné modely preto rozhodnutie nemusí platiť  
priamo, no ukazuje, že fair use nie je pri AI automatický.  

### 7.5 Európa  

- **GEMA v. OpenAI (Nemecko):** krajinský súd v Mníchove v novembri 2025  
  rozhodol, že ChatGPT porušil autorské práva k textom deviatich nemeckých  
  piesní. Model ich mal „zapamätané“ a vedel ich takmer doslovne zopakovať.  
  Súd uznal, že takéto zapamätanie v modeli je rozmnoženinou diela a výnimka  
  na dolovanie textov a dát naň nestačí. Rozhodnutie nie je právoplatné.  
- **Like Company v. Google (Súdny dvor EÚ, C-250/25):** prvý prípad  
  generatívnej AI pred Súdnym dvorom EÚ. Maďarský vydavateľ tvrdí, že chatbot  
  Gemini preberal a zhrnoval jeho články. Generálny advokát Szpunar v novembri  
  2026 navrhol otázky o trénovaní modelov odmietnuť ako hypotetické, pretože  
  nebolo preukázané, že sa na článkoch vydavateľa trénovalo. Rozsudok sa ešte  
  len očakáva.  
- **Kneschke v. LAION (Nemecko):** prvostupňový súd v Hamburgu v roku 2024  
  rozhodol, že tvorba datasetu LAION spadala pod výnimku na vedecký výskum.  

### 7.6 Getty Images v. Stability AI (Veľká Británia)  

Getty tvrdila, že Stable Diffusion sa trénoval na jej fotografiách. Súd v  
Londýne v novembri 2025 zamietol hlavný autorskoprávny nárok: samotný model  
podľa neho neobsahuje kópie fotografií, a teda nie je „porušujúcou kópiou“.  
Uznal však čiastočné porušenie ochranných známok pri starších modeloch  
(napodobnené vodoznaky Getty). Getty získala povolenie na odvolanie.  
**Odvolací súd prípad prejednal v novembri 2026**, rozhodnutie sa očakáva v  
roku 2027.  

### 7.7 Ďalšie dôležité prípady  

- **Books3:** súbor približne 200 000 kníh z pirátskeho zdroja, ktorý bol  
  súčasťou datasetu The Pile a používal sa na trénovanie viacerých modelov. V  
  roku 2023 bol po sťažnosti stiahnutý.  
- **LAION-5B a zneužívanie detí:** v decembri 2023 výskumníci zo Stanfordu  
  našli v zozname 1 008 potvrdených odkazov na materiál sexuálneho zneužívania  
  detí. Dataset bol stiahnutý a v auguste 2024 vydaný vyčistený Re-LAION-5B, z  
  ktorého bolo odstránených 2 236 podozrivých odkazov. Prípad ukazuje, že ani  
  filtrovanie veľkých datasetov nie je dokonalé.  
- **Disney a Universal v. Midjourney (USA, jún 2025):** prvá žaloba veľkých  
  hollywoodskych štúdií proti AI firme. Štúdiá tvrdia, že Midjourney sa  
  trénoval na ich dielach a ľahko vytvára obrázky ich postáv.  
- **Hudba (Suno, Udio):** veľké vydavateľstvá žalovali v roku 2024 generátory  
  hudby Suno a Udio. Koncom roka 2025 sa Universal a Warner s Udio a Warner so  
  Suno vyrovnali a namiesto sporu uzavreli licenčné dohody na nové platformy  
  trénované na licencovanej hudbe.  

### 7.8 Prehľad prípadov  

| Prípad | Krajina | Stav (november 2026) |
|---|---|---|
| Bartz v. Anthropic | USA | vyrovnanie 1,5 mld. USD schválené, prebiehajú výplaty |
| Kadrey v. Meta | USA | tréning = fair use (2025), spor o torrentovanie pokračuje |
| Authors Guild / NYT v. OpenAI a Microsoft | USA | návrhy na rozhodnutie bez procesu, čaká sa na súd |
| Thomson Reuters v. Ross | USA | odvolací súd: nie je fair use (2026) |
| Disney a Universal v. Midjourney | USA | prebieha |
| GEMA v. OpenAI | Nemecko | OpenAI prehrala v 1. stupni (2025), neprávoplatné |
| Like Company v. Google | EÚ | stanovisko generálneho advokáta, čaká sa na rozsudok |
| Getty Images v. Stability AI | Veľká Británia | Getty v 1. stupni prehrala hlavný nárok, odvolanie prejednané |
| Labely v. Suno a Udio | USA | čiastočne vyrovnané licenčnými dohodami |

## 8. Čo z incidentov vyplýva  

- **Samotné trénovanie** na legálne získaných dátach súdy v USA zatiaľ dvakrát  
  (Anthropic, Meta) posúdili ako fair use. Odvolací súd v prípade Ross však  
  ukázal, že pri priamej konkurencii to neplatí automaticky. Rozhodnutia sa  
  líšia a záväzné stanovisko najvyšších súdov zatiaľ chýba.  
- **Rozhodujúce je, ako boli dáta získané.** Pirátske zdroje sa ukázali ako  
  najväčšie riziko a najdrahšia chyba. Ťažisko sporov sa presúva od otázky  
  „smie sa trénovať?“ k otázke „odkiaľ ste dáta vzali?“.  
- **Zapamätanie a výstupy** sú ďalším rizikom. Ak model dokáže dielo doslovne  
  zopakovať (texty piesní, články, postavy), súdy sú voči AI firmám  
  prísnejšie.  
- **Firmy sa presúvajú k licenčným dohodám** s vydavateľmi, fotobankami,  
  hudobnými vydavateľstvami a platformami. Spory sa často končia dohodou  
  namiesto rozsudku.  
- **Stále chýba jasná odpoveď** na otázky výstupov, licencovania a kompenzácie  
  autorov. Prípady sú otvorené a rozhodnutia sa budú vyvíjať.  

### Pravidlá v Európe  

- **Výnimka na dolovanie textov a dát (TDM):** smernica EÚ o autorskom práve z  
  roku 2019 dovoľuje automatizovanú analýzu verejne dostupných diel, pokiaľ si  
  to nositeľ práv výslovne nezakázal (tzv. opt-out, napríklad strojovo  
  čitateľným spôsobom na webe). Slovensko ju prebralo do autorského zákona. Či  
  sa výnimka vzťahuje aj na trénovanie generatívnych modelov, ešte nie je s  
  konečnou platnosťou rozhodnuté.  
- **AI Act:** od 2. augusta 2025 platia povinnosti pre poskytovateľov  
  univerzálnych modelov (GPAI). Musia mať politiku dodržiavania autorského  
  práva, rešpektovať opt-out a zverejniť zhrnutie tréningových dát podľa vzoru  
  Európskej komisie. Úrad pre AI môže tieto povinnosti vymáhať od 2. augusta  
  2026.  
- **Digitálny omnibus o AI:** nariadenie (EÚ) 2026/1744 platné od 27. júla  
  2026 posunulo termíny najmä pre vysokorizikové systémy a posilnilo právomoci  
  Úradu pre AI. Základná štruktúra AI Act vrátane povinností pre univerzálne  
  modely zostala zachovaná.  

## 9. Ďalšie problémy s dátami  

- **Predsudky:** model preberá stereotypy z dát.  
- **Jazyková nerovnosť:** dát v angličtine je neporovnateľne viac než v  
  slovenčine, preto bývajú výsledky v slovenčine slabšie. Novšie modely však  
  pokrývajú čoraz viac jazykov (Qwen3 uvádza 119).  
- **Súkromie a osobné údaje:** dáta z internetu môžu obsahovať osobné údaje a  
  v EÚ podliehajú GDPR. Taliansky dozorný úrad napríklad v decembri 2024  
  pokutoval OpenAI sumou 15 miliónov eur. Meta od mája 2025 trénuje na  
  verejných príspevkoch používateľov z EÚ, ktorí môžu podať námietku.  
- **Kontaminácia testov:** ak sa testovacie úlohy dostanú do tréningu,  
  benchmark ukazuje lepší výsledok, než model reálne dosahuje.  
- **Syntetické dáta:** ak sa modely učia z textov iných modelov, hrozí  
  znižovanie kvality a rozmanitosti.  
- **Škodlivý a nezákonný obsah:** filtrovanie nie je dokonalé, ako ukázal  
  prípad LAION-5B.  
- **Netransparentnosť:** najväčší výrobcovia nezverejňujú, na čom presne  
  trénovali, čo sťažuje kontrolu aj uplatňovanie práv autorov.  

## 10. Čo z toho pre prax  

**Pre autorov a firmy, ktoré publikujú obsah:**  

- Ak nechcete, aby sa na vašom obsahu trénovalo, nastavte opt-out (napríklad  
  zákaz pre AI roboty v súbore robots.txt a vyhlásenie v podmienkach  
  používania webu).  
- Sledujte licenčné ponuky a hromadné vyrovnania. Americké vyrovnania sa však  
  zvyčajne týkajú len diel registrovaných na americkom Úrade pre autorské  
  práva, takže väčšina slovenských kníh do nich nespadá.  

**Pre firmy, ktoré AI používajú:**  

- Uprednostnite nástroje s jasnou licenčnou politikou a právnou ochranou  
  zákazníka (niektorí poskytovatelia ručia za spory o autorské práva vo  
  výstupoch).  
- Nevkladajte do verejných AI nástrojov citlivé a osobné údaje. Zistite, či  
  poskytovateľ používa vaše vstupy na ďalší tréning, a ak áno, vypnite to.  
- Pri obrázkoch a textoch na komerčné použitie kontrolujte, či výstup  
  nenapodobňuje konkrétne chránené dielo, postavu alebo značku.  

## 11. Slovník pojmov  

- **Token:** základná jednotka textu pre model, slovo alebo jeho časť.  
- **Predtrénovanie:** prvá, najdrahšia fáza učenia na obrovskom množstve dát.  
- **Doladenie (fine-tuning):** dodatočné učenie na menšom, cielenom súbore  
  dát.  
- **Syntetické dáta:** dáta vytvorené programom alebo iným AI modelom.  
- **Destilácia:** učenie malého modelu z odpovedí veľkého modelu.  
- **Benchmark:** štandardizovaný test na porovnanie modelov.  
- **Fair use:** americká výnimka z autorského práva pre „spravodlivé použitie“  
  diela.  
- **TDM (text and data mining):** európska výnimka na automatizovanú analýzu  
  textov a dát.  
- **Opt-out:** výslovný zákaz nositeľa práv používať jeho dielo na dolovanie  
  dát či trénovanie.  
- **Seeding:** pri torrentovaní posielanie stiahnutých súborov ďalším  
  používateľom.  
- **Vyrovnanie (settlement):** dohoda strán, ktorá ukončí spor bez rozsudku o  
  vine.  
- **GPAI:** univerzálny AI model (general-purpose AI) podľa AI Act.  

## 12. Zhrnutie  

- Modely sa učia z obrovského množstva textov a obrázkov, často z verejného  
  internetu a kníh. Najväčšie otvorené jazykové modely dnes používajú 30 až 40  
  biliónov tokenov.  
- Obrazové modely potrebujú stovky miliónov až miliardy obrázkov.  
- Syntetické dáta modely zlepšujú, no musia sa kontrolovať a miešať s reálnymi  
  dátami, inak hrozí kolaps modelu.  
- Obrazové modely sa stali použiteľnými okolo roku 2022 vďaka veľkým súborom  
  obrázkov, difúznym modelom a otvoreným modelom. Od roku 2025 sú súčasťou  
  veľkých multimodálnych modelov.  
- Prípady Anthropic, Meta a OpenAI ukazujú, že sporný je najmä spôsob získania  
  dát, nie len samotné učenie. Prípady Ross a GEMA ukazujú, že súdy môžu  
  rozhodnúť aj proti AI firmám.  
- Odvetvie sa posúva od sporov k licenčným dohodám, no mnohé zásadné otázky  
  zostávajú otvorené.  
- Stav sporov sa mení, preto si pred školením aktuálne informácie overte.

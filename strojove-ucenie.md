# Úvod do strojového učenia

Pracovný materiál k školeniu Úvod do AI. Cieľom je pochopiť, čo strojové  
učenie je, ako funguje a kde sa s ním v praxi stretávame, bez potreby  
programovania alebo matematiky.  

## 1. Čo je strojové učenie

Strojové učenie (angl. machine learning, ML) je oblasť umelej inteligencie, v  
ktorej sa počítač učí vzory z dát namiesto toho, aby mu človek ručne napísal  
všetky pravidlá.  

Klasický príklad: nechceme programátorovi vysvetľovať, ako vyzerá mačka na  
fotke. Ukážeme systému tisíce fotiek označených ako mačka alebo nie mačka a  
necháme ho, aby si rozdiely našiel sám.  

![Strojové učenie](strojove-ucenie.jpg)

## 2. Klasické programovanie vs. strojové učenie

- Klasické programovanie: človek napíše pravidlá, počítač ich aplikuje na dáta  
  a vráti odpoveď.  
- Strojové učenie: človek dodá dáta a správne odpovede, počítač z nich odvodí  
  pravidlá (model), ktoré potom použije na nové dáta.  

Výhoda ML: zvláda úlohy, kde sú pravidlá príliš zložité alebo ich nevieme  
presne opísať, napríklad rozpoznávanie reči, obrazu alebo spamu.  

## 3. Tri hlavné typy učenia

### Učenie s učiteľom (supervised learning)

Model dostane príklady so správnou odpoveďou (štítkom). Učí sa predpovedať  
odpoveď pre nové príklady. Použitie: filter spamu, odhad ceny nehnuteľnosti,  
diagnostika z obrazových snímok.  

### Učenie bez učiteľa (unsupervised learning)

Dáta nemajú štítky. Model sám hľadá štruktúru, napríklad skupiny podobných  
zákazníkov alebo neobvyklé transakcie. Použitie: segmentácia zákazníkov,  
detekcia anomálií.  

### Posilňované učenie (reinforcement learning)

Model sa učí pokusom a omylom. Za dobré kroky dostáva odmenu, za zlé trest.  
Použitie: hranie hier, robotika, optimalizácia riadenia.  

## 4. Ako prebieha trénovanie modelu

1. Zber a príprava dát: dáta treba vyčistiť, doplniť chýbajúce hodnoty a  
   odstrániť chyby.  
2. Rozdelenie dát: väčšina sa použije na trénovanie, zvyšok na testovanie.  
   Testovacie dáta model počas učenia nevidí.  
3. Trénovanie: model opakovane porovnáva svoje odpovede so správnymi a  
   upravuje svoje vnútorné parametre, aby robil menej chýb.  
4. Vyhodnotenie: na testovacích dátach zmeriame, ako dobre model funguje na  
   príkladoch, ktoré ešte nevidel.  
5. Nasadenie a sledovanie: model používame v praxi a pravidelne kontrolujeme,  
   či jeho kvalita neklesá.  

## 5. Dáta sú základ

Kvalita modelu závisí najmä od kvality dát. Platí známe pravidlo: garbage in,  
garbage out. Ak sú dáta chybné, neúplné alebo zaujaté, bude také aj správanie  
modelu.  

- Množstvo: viac rozmanitých dát zvyčajne znamená lepší model.  
- Kvalita: správne označené, aktuálne a konzistentné dáta.  
- Reprezentatívnosť: dáta musia pokrývať situácie, v ktorých sa bude model  
  používať.  

## 6. Typické problémy

- Preučenie (overfitting): model si dáta zapamätá namiesto toho, aby sa naučil  
  všeobecné vzory. Na trénovacích dátach je skvelý, na nových zlyháva.  
- Podučenie (underfitting): model je príliš jednoduchý a vzory nezachytí.  
- Skreslenie (bias): ak dáta odrážajú predsudky, model ich prevezme a môže ich  
  zosilniť.  
- Posun dát (data drift): svet sa mení a model trénovaný na starých dátach  
  postupne zastaráva.  

## 7. Neurónové siete a hlboké učenie

Neurónová sieť je model inšpirovaný mozgom. Skladá sa z veľkého počtu  
jednoduchých výpočtových jednotiek usporiadaných do vrstiev. Každá vrstva  
spracuje vstup a pošle ho ďalej.  

Hlboké učenie (deep learning) používa siete s mnohými vrstvami. Vďaka nim sa  
dosiahol veľký pokrok v rozpoznávaní obrazu, reči a v spracovaní prirodzeného  
jazyka.  

## 8. Od strojového učenia k veľkým jazykovým modelom

Veľké jazykové modely (LLM), na ktorých stoja nástroje ako Claude alebo  
ChatGPT, sú špeciálny typ neurónových sietí. Trénujú sa na obrovskom množstve  
textu a učia sa predpovedať, aký text nasleduje.  

Z tejto jednoduchej úlohy vzniká schopnosť písať, sumarizovať, prekladať či  
odpovedať na otázky. Model však nerozumie svetu ako človek a môže sa mýliť,  
preto je potrebné jeho výstupy overovať.  

## 9. Kde sa s ML stretávame každý deň

- Odporúčania filmov, hudby a produktov.  
- Filtre nevyžiadanej pošty a detekcia podvodov v platbách.  
- Rozpoznávanie reči a hlasoví asistenti.  
- Navigácia a odhad času príchodu.  
- Automatický preklad a prepis textu.  
- Rozpoznávanie tvárí a objektov vo fotografiách.  

## 10. Obmedzenia a zodpovednosť

ML model nie je neomylný. Je to štatistický nástroj, ktorý pracuje s  
pravdepodobnosťami. Pri dôležitých rozhodnutiach by mal človek zostať v  
procese a výstupy kontrolovať.  

- Chyby: aj dobrý model sa občas mýli, niekedy sebavedomo.  
- Vysvetliteľnosť: nie vždy vieme povedať, prečo model rozhodol práve takto.  
- Ochrana súkromia: dáta na trénovanie môžu obsahovať osobné údaje.  
- Spravodlivosť: je potrebné testovať, či model nediskriminuje skupiny ľudí.  

## 11. Kľúčové pojmy

- Model: naučená funkcia, ktorá z vstupu vyrobí výstup.  
- Trénovanie: proces, v ktorom sa model učí z dát.  
- Príznak (feature): vstupná vlastnosť dát, napríklad vek či cena.  
- Štítok (label): správna odpoveď pre daný príklad.  
- Predikcia (inferencia): použitie hotového modelu na nové dáta.  
- Presnosť (accuracy): podiel správnych odpovedí modelu.  

## 12. Otázky na diskusiu

1. Kde vo vašej práci opakujete rozhodnutia, ktoré sa riadia vzormi?  
2. Aké dáta máte k dispozícii a ako kvalitné sú?  
3. Ktoré rozhodnutia by ste automatizácii nikdy neprenechali a prečo?  
4. Ako by ste zistili, že model prestal fungovať správne?

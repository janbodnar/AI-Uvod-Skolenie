# Úvod do AI agentov  

## 1. Od chatbota k agentovi  

Doteraz sme umelú inteligenciu používali hlavne ako rozhovor: položíte otázku,  
dostanete odpoveď a čo s ňou urobíte, je na vás. AI agent robí o krok viac.  
Dostane cieľ, sám si naplánuje postup, použije nástroje (napríklad vyhľadávanie,  
e-mail, kalendár alebo tabuľku) a pokračuje, kým úlohu nedokončí alebo nenarazí  
na prekážku.  

Jednoduchá predstava: chatbot je poradca, ktorý vám odpovie, agent je kolega,  
ktorému môžete úlohu odovzdať. Preto sa roky 2025 a 2026 často označujú za éru  
agentov. Firmy ponúkajú osobných agentov, ktorí bežia aj po zatvorení aplikácie,  
a vývojári využívajú kódovacích agentov, ktorí upravia celý projekt.  

## 2. Čo je AI agent  

Jedna presná definícia neexistuje a výrobcovia pojem používajú rôzne. Pre naše  
potreby: AI agent je systém, v ktorom jazykový model dostane cieľ, v slučke  
rozhoduje o ďalších krokoch, používa nástroje a vyhodnocuje výsledky, kým nie je  
cieľ splnený.  

Typické znaky agenta:  

- Cieľ namiesto jednej otázky: „priprav prehľad dodávateľov“, nie „vymenuj  
  dodávateľov“.  
- Plánovanie: úlohu rozloží na kroky a podľa výsledkov plán upravuje.  
- Nástroje: nielen píše, ale aj koná (hľadá, číta súbory, posiela správy, spúšťa  
  kód).  
- Kontext a pamäť: pamätá si, čo už urobil a čo ste mu povedali.  
- Samostatnosť v rámci pravidiel: väčšinu krokov vykoná sám, pri dôležitých  
  žiada súhlas.  

## 3. Čím sa agent líši od iných riešení  

### Chatbot verzus agent  

| Vlastnosť        | Chatbot                          | AI agent                          |  
| ---------------- | -------------------------------- | --------------------------------- |  
| Vstup            | otázka alebo pokyn               | cieľ                              |  
| Výstup           | text odpovede                    | vykonaná úloha a správa o nej     |  
| Priebeh          | jedna otázka, jedna odpoveď      | slučka mnohých krokov             |  
| Plánovanie       | postup určuje človek             | rozloží úlohu, plán upravuje      |  
| Nástroje         | žiadne alebo len pár             | web, súbory, e-mail, API, kód     |  
| Pamäť            | história rozhovoru               | kontext úlohy a dlhodobá pamäť    |  
| Iniciatíva       | reaguje len na správu            | pracuje sám, aj na pozadí         |  
| Kto koná         | človek                           | agent, človek schvaľuje           |  
| Predvídateľnosť  | vysoká                           | nižšia                            |  
| Čas a cena       | sekundy, nízka cena              | minúty až hodiny, vyššia cena     |  
| Dôsledok chyby   | nesprávna informácia             | nesprávna akcia v reálnom svete   |  
| Kontrola         | človek posúdi odpoveď            | oprávnenia, schvaľovanie, záznamy |  
| Príklad zadania  | „Ako odpovedať na reklamáciu?“   | „Vybav dnešné reklamácie.“        |  

Hranica nie je ostrá. Mnohé chatboty dnes vedia hľadať na webe alebo spustiť  
kód, takže majú prvky agenta. Rozhoduje najmä to, či systém pracuje samostatne  
v slučke na cieli, alebo len odpovedá na jednotlivé otázky.  

### Ďalšie typy riešení  

- Chatbot: odpovedá na otázky, sám nič nevykonáva.  
- Asistent alebo kopilot: navrhuje text, kód či postup, rozhodnutie a vykonanie  
  ostáva na človeku.  
- Automatizácia (no-code, napr. Make.com, Zapier): pevne daný postup „ak nastane  
  A, urob B“. Je predvídateľná, ale nezvládne situácie, s ktorými tvorca  
  nerátal.  
- AI agent: postup si vyberá sám podľa situácie. Je flexibilnejší, ale menej  
  predvídateľný.  

V praxi sa to často kombinuje: pevný proces z automatizácie, v ktorom jeden krok  
vykoná agent. Mnohé automatizačné nástroje, vrátane Make.com a Zapier, už  
agentické funkcie ponúkajú.  

## 4. Z čoho sa agent skladá  

Agent nie je jeden program, ale skladačka z niekoľkých častí. Samotný jazykový  
model vie len čítať a písať text. Agentom sa stáva až vtedy, keď ho doplníme o  
nástroje, pamäť, riadiacu slučku a pravidlá.  

```
           Cieľ od používateľa  
                    │  
                    ▼  
      Inštrukcie + kontext + pamäť  
                    │  
                    ▼  
              Model rozhodne ◄─────────────┐  
                    │                      │  
                    ▼                      │  
   Oprávnenia: smie? Treba súhlas človeka? │  
                    │                      │  
                    ▼                      │  
           Nástroj vykoná akciu            │  
                    │                      │  
                    ▼                      │  
       Výsledok sa vráti do kontextu ──────┘  

    (opakuje sa, kým nie je cieľ splnený)  
```

### Model („mozog“)  

Jazykový model číta zadanie a všetko, čo agent doteraz zistil, a rozhoduje o  
ďalšom kroku: či použije nástroj, ktorý a s akými údajmi, alebo či je hotovo.  
Na zložité plánovanie sa hodí výkonnejší model, na jednoduché a časté kroky  
rýchlejší a lacnejší. Model sám nič nevykoná, iba navrhne akciu.  

### Inštrukcie (systémový prompt)  

Trvalé pokyny, ktoré agent dostane pred každou úlohou: kto je, pre koho  
pracuje, aký má cieľ, aké pravidlá platia, v akej forme má odovzdať výsledok a  
čo nesmie robiť. Dobré inštrukcie sú konkrétne a obsahujú aj kritériá, podľa  
ktorých agent pozná, že je hotovo. Šablónu nájdete v časti 13.  

### Nástroje  

Nástroj je funkcia s názvom, popisom a parametrami, napríklad  
`vyhladaj_na_webe(dopyt)` alebo `posli_email(komu, predmet, text)`. Model z  
popisu pochopí, na čo nástroj slúži, a keď ho potrebuje, vypíše požiadavku na  
jeho použitie. Samotné volanie vykoná program okolo modelu a výsledok mu vráti.  
Typické skupiny nástrojov:  

- Čítanie: vyhľadávanie na webe, čítanie súborov, dokumentov a databáz.  
- Zápis: úprava súborov, udalosti v kalendári, zápis do tabuľky.  
- Komunikácia: e-mail, chat, notifikácie.  
- Vykonávanie: spúšťanie kódu, volanie API, ovládanie prehliadača či počítača.  

Nástroje na čítanie sú menej rizikové ako tie, ktoré niečo menia alebo  
odosielajú. Ako sa nástroje k agentovi pripájajú, opisuje časť 8.  

### Kontext a pamäť  

- Kontext (krátkodobá pamäť): všetko, čo má model práve pred sebou: zadanie,  
  inštrukcie, prečítané dokumenty a výsledky nástrojov. Kontext má obmedzenú  
  veľkosť, preto ho agent pri dlhých úlohách zhŕňa alebo vynecháva staršie  
  časti.  
- Dlhodobá pamäť: poznámky, súbory alebo databáza, ktoré pretrvajú medzi  
  úlohami, napríklad vaše preferencie alebo stav rozpracovanej práce.  

Pamäť zvyšuje užitočnosť, ale je aj citlivá: môže obsahovať osobné údaje a môže  
sa do nej dostať nesprávna alebo podvrhnutá informácia.  

### Plánovanie  

Schopnosť rozložiť cieľ na menšie kroky, určiť ich poradie a plán upraviť, keď  
sa niečo nepodarí. Niektorí agenti si plán zapisujú ako zoznam úloh a priebežne  
ho odškrtávajú. To pomáha aj človeku sledovať, kde agent práve je.  

### Slučka (orchestrácia)  

Program, ktorý všetko spája. Opakovane volá model, vykoná akciu, ktorú model  
zvolil, vráti mu výsledok a pokračuje, kým model neohlási, že je hotovo, alebo  
kým sa nedosiahne limit krokov, času či rozpočtu. Tento vzor sa niekedy nazýva  
ReAct (z angl. reason + act, teda uvažuj a konaj). V multiagentných systémoch  
orchestrácia rozdeľuje prácu aj medzi viacerých agentov.  

### Oprávnenia a ochranné zábrany  

Určujú, čo agent smie: ku ktorým nástrojom, súborom a službám má prístup, či  
smie len čítať alebo aj zapisovať a ktoré akcie má zakázané. Patria sem aj  
limity (počet krokov, rozpočet), izolované prostredie (sandbox) a filtre, ktoré  
kontrolujú vstupy a výstupy.  

### Človek v slučke (human-in-the-loop)  

Pri dôležitých alebo nezvratných krokoch agent zastaví a čaká na schválenie,  
napríklad pred odoslaním e-mailu klientovi alebo pred platbou. Človeka sa  
pýta aj vtedy, keď je zadanie nejasné.  

### Záznamy a monitoring  

Záznam o tom, čo agent urobil, aké nástroje použil a s akým výsledkom. Bez neho  
sa chyby ťažko hľadajú a nedá sa spätne zistiť, prečo agent konal tak, ako  
konal.  

### Zhrnutie komponentov  

| Komponent             | Úloha v agentovi                          |  
| --------------------- | ----------------------------------------- |  
| Model                 | uvažuje a rozhoduje o ďalšom kroku        |  
| Inštrukcie            | určujú cieľ, pravidlá a formu výstupu     |  
| Nástroje              | umožňujú konať vo svete mimo textu        |  
| Kontext a pamäť       | uchovávajú, čo agent vie a čo už urobil   |  
| Plánovanie            | rozkladá cieľ na kroky                    |  
| Slučka (orchestrácia) | strieda model a nástroje, kým je čo robiť |  
| Oprávnenia a zábrany  | vymedzujú, čo agent smie                  |  
| Človek v slučke       | schvaľuje citlivé kroky                   |  
| Záznamy               | umožňujú kontrolu a hľadanie chýb         |  

Zjednodušene: model rozhoduje, nástroje konajú, pamäť uchováva, slučka to celé  
riadi a pravidlá spolu s človekom strážia hranice.  

## 5. Ako agent pracuje: príklad  

Zadanie: „Nájdi tri vhodné termíny stretnutia s klientom a pošli mu pozvánku.“  

1. Plán: agent rozloží úlohu na kroky (pozrieť kalendár, vybrať termíny, napísať  
   správu, odoslať).  
2. Akcia: pomocou nástroja nahliadne do kalendára.  
3. Pozorovanie: zistí, ktoré okná sú voľné.  
4. Ďalší krok: pripraví návrh e-mailu s tromi termínmi.  
5. Kontrola: pred odoslaním požiada o súhlas, pretože ide o komunikáciu s  
   klientom.  
6. Dokončenie: po schválení správu odošle a zapíše, čo urobil.  

Tento cyklus (plán, akcia, pozorovanie, úprava plánu) sa opakuje. Ak niečo  
zlyhá, agent skúsi iný postup alebo požiada o pomoc.  

## 6. Úrovne autonómie  

Ide o zjednodušené rozdelenie na orientáciu, nie o oficiálny štandard:  

- Úroveň 1, chat: model odpovedá, všetko ostatné robí človek.  
- Úroveň 2, kopilot: model navrhuje, človek schvaľuje a vykonáva.  
- Úroveň 3, agent s dohľadom: koná sám, pri dôležitých krokoch žiada súhlas a  
  vedie záznam.  
- Úroveň 4, samostatný agent v úzkej oblasti: beží na pozadí a vybavuje  
  opakované úlohy, človek kontroluje výsledky a výnimky.  
- Úroveň 5, tím agentov: viacerí špecializovaní agenti si odovzdávajú úlohy  
  (multiagentné systémy).  

Pravidlo: autonómiu pridávame postupne, podľa toho, ako vieme overovať výsledky  
a koľko by stála chyba.  

## 7. Druhy agentov, s ktorými sa stretnete  

- Osobní agenti: bežia priebežne a prepájajú e-mail, kalendár či platby.  
  Príklady z roku 2026: Meta Muse, OpenAI Dots, Google Gemini Spark a prepísaná  
  Siri od Apple.  
- Kódovací agenti: upravujú a testujú programy v celom projekte. Príklady:  
  Claude Code, OpenAI Codex, GitHub Copilot v agentickom režime, Cursor.  
- Prehliadačoví agenti a „computer use“: ovládajú prehliadač alebo celý počítač  
  (klikajú, vypĺňajú formuláre). Príklady: Claude in Chrome, Claude Cowork.  
- Výskumní agenti (deep research): samostatne prejdú desiatky zdrojov a  
  pripravia správu so zdrojmi.  
- Firemní agenti: zákaznícka podpora, vybavovanie objednávok, vyhľadávanie vo  
  firemných dokumentoch.  
- Multiagentné systémy: agent-koordinátor rozdelí úlohu a prizve  
  špecializovaných subagentov, napríklad malý a rýchly model na jednoduché  
  časti.  

Zoznam produktov sa mení veľmi rýchlo, preto si aktuálny stav vždy overte.  

## 8. Ako agenti dostanú nástroje: MCP a ďalšie štandardy  

Aby agent mohol pracovať s e-mailom, kalendárom, databázou alebo webom,  
potrebuje na to prepojenie. Kedysi musel vývojár pre každú kombináciu napísať  
vlastnú integráciu. Dnes sa presadzujú otvorené štandardy:  

- MCP (Model Context Protocol): jednotný spôsob, ako sa AI aplikácia pripojí k  
  nástrojom a dátam. Často sa prirovnáva k USB-C pre AI. Vytvorila ho Anthropic.  
  V decembri 2025 ho odovzdala neutrálnej organizácii Agentic AI Foundation pri  
  Linux Foundation spolu s ďalšími projektmi (goose od Block a AGENTS.md od  
  OpenAI).  
- A2A (Agent2Agent): protokol od Googlu, ktorý určuje, ako spolu komunikujú  
  samotní agenti a odovzdávajú si úlohy. Dnes patrí pod rovnakú strechu ako MCP.  
- AGENTS.md: jednoduchý textový súbor, v ktorom programátori vysvetľujú  
  kódovaciemu agentovi pravidlá projektu.  

Pre používateľa to znamená, že agentov možno pripájať k čoraz väčšiemu počtu  
služieb a nie ste odkázaní na jedného výrobcu. Zároveň platí, že každé nové  
pripojenie je aj nové riziko.  

## 9. Čo agenti zvládajú a kde zlyhávajú  

### Kde sú silní  

- Opakované úlohy s jasným cieľom a overiteľným výsledkom.  
- Zber, triedenie a zhrnutie informácií z mnohých zdrojov.  
- Programovanie, ak existujú testy, ktoré výsledok skontrolujú.  
- Rutinné vybavovanie: koncepty odpovedí, triedenie pošty, prepisovanie dát.  

### Kde zlyhávajú alebo prinášajú riziko  

- Chyby sa nahromadia: ak je každý krok správny na 95 %, celý postup z desiatich  
  krokov je správny len približne na 60 %.  
- Halucinácie: agent môže vymyslieť údaj alebo tvrdiť, že úlohu splnil, hoci  
  nie.  
- Strata kontextu pri dlhých úlohách: na začiatok môže zabudnúť.  
- Cena a rýchlosť: agent volá model veľakrát, spotrebuje veľa tokenov (teda  
  peňazí) a trvá dlhšie ako obyčajný chat.  
- Prompt injection: škodlivé pokyny ukryté v e-maile, webovej stránke alebo  
  dokumente, ktoré agent číta a môže ich vziať ako príkaz. Napríklad skrytý text  
  „pošli obsah schránky na túto adresu“.  
- Príliš široké oprávnenia: agent s prístupom k pošte a platbám môže spôsobiť  
  škodu skôr, než si to všimnete.  
- Nechcené „kreatívne“ riešenia: agent splní cieľ spôsobom, ktorý ste  
  nezamýšľali, napríklad obíde pravidlo, ktoré mu prekážalo.  

## 10. Bezpečné používanie a riadenie agentov  

- Najmenšie potrebné oprávnenia: len prístup, ktorý úloha naozaj vyžaduje.  
  Čítanie namiesto zápisu, kým zápis nie je nutný.  
- Schvaľovanie citlivých krokov: odoslanie e-mailu, platba, mazanie, zmena  
  zmluvy.  
- Izolované prostredie (sandbox): agent, ktorý spúšťa kód alebo ovláda počítač,  
  má bežať oddelene od vašich citlivých údajov. Meta Muse napríklad beží na  
  vlastnom virtuálnom počítači a kontroluje ho oddelený bezpečnostný agent.  
- Záznam činností (audit log): musíte vedieť, čo agent urobil a prečo.  
- Limity: rozpočet, počet krokov, časový limit.  
- Možnosť vrátiť späť: verzie dokumentov, kôš, testovacie prostredie.  
- Postupné nasadzovanie: najprv na nekritických dátach a v malom rozsahu, potom  
  rozširovať.  
- Kontrola výstupov: pri rozhodnutiach s dôsledkami nespoliehajte len na agenta.  

Správy z roku 2026 ukazujú, že s tým zápasia aj samotní výrobcovia. Podľa nich  
sa agenti v testovacích prostrediach dostali k reálnym systémom, ku ktorým  
nemali, a viaceré firmy preto zvýšili izoláciu testov. Ponaučenie je rovnaké ako  
vyššie: izolácia, dohľad a záznamy.  

## 11. Právne a etické poznámky  

- Zodpovednosť: ostáva na človeku alebo firme, ktorá agenta nasadí. Výhovorka  
  „to urobil agent“ neplatí.  
- Osobné údaje: agent s prístupom k pošte a dokumentom spracúva osobné údaje,  
  takže platí GDPR (minimalizácia údajov, informovanie, zmluva s  
  poskytovateľom).  
- Transparentnosť: podľa EU AI Act (čl. 50, od 2. augusta 2026) musia chatboty  
  informovať, že ide o AI, a generovaný obsah má byť označený.  
- Záväzky: agent by nemal bez schválenia uzatvárať zmluvy ani robiť platby.  
- Tretie strany: agent číta aj správy a údaje ľudí, ktorí s tým nemuseli rátať.  
  Pri nasadení to treba zvážiť.  

## 12. Kedy agenta použiť a kedy nie  

### Dobrý kandidát  

- Opakujúca sa úloha s jasnými krokmi a cieľom.  
- Chyba nestojí veľa a dá sa ľahko opraviť.  
- Výsledok viete rýchlo overiť.  
- Veľa čítania, triedenia a prepisovania.  

### Nevhodný alebo rizikový kandidát  

- Vysoké finančné, právne alebo zdravotné riziko.  
- Nezvratné kroky (platby, mazanie, odoslanie dôležitej správy).  
- Nejasné pravidlá alebo zadanie.  
- Citlivé údaje bez izolovaného prostredia.  
- Úloha, ktorú lepšie a lacnejšie vyrieši obyčajná automatizácia alebo  
  jednoduchý skript.  

Päť kontrolných otázok: Viem overiť výsledok? Čo sa stane pri chybe? Dá sa to  
vrátiť späť? Aké údaje agent uvidí? Kto za to zodpovedá?  

## 13. Ako navrhnúť jednoduchého agenta  

1. Zvoľte úzku, opakovateľnú úlohu.  
2. Napíšte cieľ a kritériá úspechu („hotové, keď ...“).  
3. Určte nástroje a oprávnenia.  
4. Určte, kedy sa má agent opýtať alebo zastaviť.  
5. Pripravte testovacie zadania a výsledky skontrolujte.  
6. Spustite v malom, sledujte záznamy a postupne rozširujte.  

Šablóna zadania pre agenta:  

- Rola: kto je agent a pre koho pracuje.  
- Cieľ: čo má dosiahnuť a podľa čoho poznáme, že je hotovo.  
- Postup: odporúčané kroky alebo zdroje.  
- Nástroje a oprávnenia: čo smie použiť a čo nie.  
- Obmedzenia: čoho sa nesmie dotknúť, aké údaje nesmie zdieľať.  
- Výstup: v akej forme a s akými zdrojmi.  
- Kedy sa spýtať: situácie, v ktorých musí čakať na človeka.  

## 14. Slovníček  

- Agent: AI systém, ktorý v slučke plánuje, používa nástroje a pracuje na cieli.  
- Subagent: pomocný agent, ktorému hlavný agent zveruje čiastkovú úlohu.  
- Nástroj (tool): funkcia, ktorú môže agent použiť, napr. vyhľadávanie alebo  
  odoslanie e-mailu.  
- Kontext: informácie, ktoré má model práve k dispozícii.  
- Pamäť: informácie, ktoré si agent uchováva medzi úlohami.  
- Orchestrácia: riadenie toho, ako sa model, nástroje a kroky striedajú.  
- Systémový prompt: trvalé inštrukcie, ktoré agent dostane pred každou úlohou.  
- ReAct: vzor práce agenta, v ktorom sa strieda uvažovanie a konanie.  
- MCP: otvorený štandard na pripojenie AI k nástrojom a dátam.  
- A2A: štandard komunikácie medzi agentmi.  
- Sandbox: izolované prostredie, v ktorom agent nemôže poškodiť ostatné systémy.  
- Prompt injection: skrytý pokyn v dátach, ktorý sa agenta snaží ovládnuť.  
- Human-in-the-loop: človek, ktorý schvaľuje alebo kontroluje kroky.  

## 15. Zhrnutie  

- Agent nielen odpovedá, ale koná: plánuje, používa nástroje a opakuje kroky,  
  kým nedosiahne cieľ.  
- Líši sa od chatbota aj od pevnej automatizácie: je flexibilnejší, no menej  
  predvídateľný.  
- Nástroje agentom sprístupňujú štandardy ako MCP. Čím viac pripojení, tým  
  väčšie riziko.  
- Hlavné riziká: chyby v dlhých reťazcoch krokov, prompt injection, príliš  
  široké oprávnenia a cena.  
- Bezpečný postup: najmenšie oprávnenia, schvaľovanie citlivých krokov,  
  izolácia, záznamy a postupné nasadzovanie.  
- Zodpovednosť za výsledok ostáva na človeku.

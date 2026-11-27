# OpenCode: otvorený agent harness pre AI modely  

Keď sa povie „AI agent na programovanie", väčšina ľudí si predstaví jazykový  
model – Claude, GPT či Gemini. Model však sám nevie otvoriť súbor, spustiť  
príkaz ani skontrolovať výsledok. Vie len čítať text a písať text. Agentom sa  
stáva až vtedy, keď ho obalí program, ktorý mu dodá nástroje, pamäť, pravidlá  
a slučku práce. Takémuto programu sa hovorí **agent harness**.  

**OpenCode** je presne takýto harness – a navyše **otvorený a nezávislý od  
modelu**. Je to open-source agent, ktorý prepája AI model s vaším projektom,  
terminálom a nástrojmi. Model si vyberáte sami: od Claude a GPT cez Gemini až  
po otvorené modely bežiace na vlastnom počítači.  

> 🔑 **Hlavná myšlienka kapitoly:** OpenCode nie je AI model. Je to **agent  
> harness** – „postroj", ktorý z ľubovoľného modelu urobí agenta. Model dodáva  
> inteligenciu, harness dodáva ruky, oči a pravidlá.  

*Stav k novembru 2026 (OpenCode 2.x). Nástroj sa vyvíja veľmi rýchlo, preto si  
pri inštalácii vždy overte aktuálnu dokumentáciu.*  

**Po tejto kapitole budete vedieť:**  

* vysvetliť, čo je agent harness a prečo je rovnako dôležitý ako model  
* nainštalovať OpenCode a pripojiť k nemu model  
* pracovať s agentmi Build a Plan a so súborom `AGENTS.md`  
* nastaviť povolenia tak, aby agent nerobil nič bez vášho súhlasu  
* rozšíriť OpenCode o vlastné príkazy, skills a MCP servery  

## Čo je agent harness  

Anglické slovo *harness* znamená **postroj** – výstroj, ktorou sa kôň  
zapriahne do voza. Kôň má silu, ale bez postroja, opratí a voza ju nevie  
užitočne využiť. Pri AI je to rovnaké:  

* **model** (LLM) je kôň – má „inteligenciu", ale sám nič nevykoná;  
* **harness** je postroj, opraty a voz – určuje, čo model vidí, aké nástroje  
  smie použiť, kam smie ísť a kto drží opraty.  

V odbornej komunite sa ustálila jednoduchá rovnica:  

```
Agent = Model + Harness
```  

Často sa k nej pridáva veta: **„Ak nie ste model, ste harness."** Harness je  
teda všetko okrem modelu – každý kus kódu, konfigurácie a logiky, ktorá  
z modelu robí agenta.  

### Čo všetko harness robí  

| Časť harnessu | Čo robí | Ako to rieši OpenCode |  
| :--- | :--- | :--- |  
| **Pokyny** | Hovoria modelu, kto je a ako má pracovať | systémový prompt, `AGENTS.md`, agenti |  
| **Nástroje** | Dávajú modelu „ruky" | čítanie, úprava súborov, shell, web, MCP |  
| **Slučka** | Opakuje kroky, kým nie je úloha hotová | agentová slučka „mysli → konaj → pozoruj" |  
| **Pamäť** | Uchováva históriu a stav práce | relácie (sessions), zhusťovanie kontextu |  
| **Povolenia** | Určujú, čo smie agent urobiť bez opýtania | pravidlá `allow` / `ask` / `deny` |  
| **Delegovanie** | Rozdelí veľkú úlohu medzi viac agentov | subagenti (general, explore) |  
| **Rozhrania** | Spôsob, ako s agentom komunikujete | terminál, desktopová aplikácia, web, SDK |  

### Ako vyzerá jeden krok agenta  

Najdôležitejšie pochopiť toto: **model sa nikdy priamo nedotkne vášho  
počítača.** Model iba napíše textovú požiadavku („chcem prečítať súbor  
`index.html`"). Harness ju skontroluje, vykoná a výsledok mu vráti.  

```
Váš prompt
    │
    ▼
OpenCode poskladá kontext: systémový prompt + AGENTS.md
+ história rozhovoru + zoznam dostupných nástrojov
    │
    ▼
MODEL navrhne ďalší krok ──► úloha hotová? ──► odpoveď vám
    │
    │ (model chce použiť nástroj)
    ▼
OpenCode skontroluje povolenia: allow / ask / deny
    │
    ▼
OpenCode spustí nástroj: čítaj, uprav, shell, web, MCP
    │
    ▼
výsledok sa vráti do kontextu ──► znova MODEL
```  

Táto slučka sa pri jednej úlohe zopakuje aj desiatky krát. Model rozhoduje,  
**čo** urobiť. Harness rozhoduje, **či a ako** sa to stane.  

### Prečo na harnesse záleží  

* **Rovnaký model, rôzne výsledky.** Ten istý model dosahuje v rôznych  
  harnessoch rozdielne výsledky. Dobrý model v dobrom harnesse často porazí  
  lepší model v zlom harnesse.  
* **Chyba agenta nemusí byť chyba modelu.** Agent nepoznal pravidlo projektu?  
  Doplňte ho do `AGENTS.md`. Spustil nebezpečný príkaz? Upravte povolenia.  
  Väčšinu problémov opravíte v harnesse, nie čakaním na nový model.  
* **Harness si môžete prispôsobiť.** Časť harnessu je zabudovaná vo výrobcovom  
  nástroji (systémový prompt, nástroje). Druhú časť tvoríte vy: súbory  
  s pokynmi, povolenia, vlastné príkazy či skills.  

### OpenCode medzi ostatnými harnessmi  

Všetky známe programovacie nástroje s AI sú harnessy. Líšia sa najmä tým, kto  
ich vyvíja a s akými modelmi fungujú:  

| Harness | Výrobca | Zdrojový kód | Modely |  
| :--- | :--- | :--- | :--- |  
| **OpenCode** | Anomaly | otvorený (MIT) | ľubovoľné, aj lokálne |  
| **Claude Code** | Anthropic | uzavretý | Claude |  
| **Codex CLI** | OpenAI | otvorený | najmä GPT |  
| **Gemini CLI** | Google | otvorený | Gemini |  
| **GitHub Copilot** | GitHub (Microsoft) | uzavretý | výber modelov viacerých firiem |  

Hlavná výhoda OpenCode: **harness a model sú oddelené**. Ak zajtra vyjde lepší  
model od inej firmy, nemusíte meniť nástroj, zvyky ani nastavenia – len  
prepnete model.  

## OpenCode v skratke  

* **Výrobca:** firma **Anomaly** – tím, ktorý stojí za frameworkom SST  
  a obchodom terminal.shop.  
* **Licencia:** MIT, zdrojový kód je na GitHube (`anomalyco/opencode`).  
* **Popularita:** v máji 2026 prekročil 160 000 hviezdičiek na GitHube.  
  Thoughtworks Technology Radar ho v novembri 2026 označil za jeden  
  z najvýznamnejších open-source harnessov pre programovacích agentov.  
* **Rozhrania:** terminálové rozhranie (TUI), desktopová aplikácia pre  
  Windows, macOS a Linux, webové rozhranie a príkazový riadok pre skripty.  
* **Modely:** desiatky poskytovateľov (Anthropic, OpenAI, Google, OpenRouter…)  
  aj lokálne modely, napr. cez Ollama.  

### OpenCode 2.0  

V októbri 2026 sa hlavnou verziou stal **OpenCode 2.0** – výrobca ho označil  
za veľkú prestavbu. Najdôležitejšie zmeny:  

* **spoločná služba na pozadí** – terminál, desktopová aplikácia aj web sa  
  pripájajú k tej istej relácii, takže prácu môžete začať v termináli  
  a dokončiť v prehliadači;  
* **Code Mode** – agent zavolá viac nástrojov MCP naraz cez krátky JavaScript,  
  namiesto mnohých samostatných krokov modelu;  
* **práca na pozadí** – subagenti a príkazy shellu môžu bežať súbežne;  
* **nové API a SDK** – OpenCode sa dá vložiť do vlastných aplikácií.  

> ⚠️ Na internete nájdete veľa návodov pre OpenCode 1.x. Niektoré príkazy,  
> konfigurácia a inštalácia sa vo verzii 2 zmenili. Pri nejasnostiach má  
> prednosť oficiálna dokumentácia na opencode.ai/docs.  

## Inštalácia  

### Desktopová aplikácia (odporúčané pre začiatočníkov)  

Najjednoduchšia cesta: stiahnite si inštalátor z **opencode.ai/download**. Pre  
Windows je k dispozícii `.exe` (x64 aj ARM64), pre macOS `.dmg` a pre Linux  
balíky `.deb`, `.rpm` a AppImage.  

### Terminálová verzia  

macOS a Linux – inštalačný skript:  

```bash
curl -fsSL https://opencode.ai/v2/install | bash
```  

Ak máte Node.js, môžete použiť aj npm:  

```bash
npm install -g @opencode/cli
```  

Windows: OpenCode 2 sa neinštaluje cez správcov balíkov (Scoop, Chocolatey).  
Stiahnite si samostatný ZIP s programom `opencode.exe` zo stránky  
s inštaláciou alebo použite desktopovú aplikáciu.  

> ⚠️ Staršie návody uvádzajú `npm install -g opencode-ai`, `choco install  
> opencode` alebo `scoop install opencode`. Tieto spôsoby inštalujú **OpenCode  
> 1** a môžu sa s verziou 2 pobiť.  

## Prvé spustenie  

### 1. Spustenie v priečinku projektu  

OpenCode pracuje vždy v konkrétnom priečinku. Ten je jeho „pracoviskom":  

```powershell
cd C:\Projekty\moj-web
opencode
```  

> 💡 Nikdy nespúšťajte agenta v koreni disku ani v domovskom priečinku.  
> Vytvorte si na kurz samostatný priečinok, napr. `C:\Projekty\kurz-ai`.  

### 2. Pripojenie modelu: `/connect`  

V rozhraní napíšte `/connect` a vyberte poskytovateľa. Máte tri hlavné  
možnosti:  

| Možnosť | Pre koho | Poznámka |  
| :--- | :--- | :--- |  
| **OpenCode Go** | začiatočníci | predplatné od 10 $ mesačne, otvorené modely a niektoré komerčné |  
| **Vlastný API kľúč** | kto už má účet | Anthropic, OpenAI, Google a ďalší; platíte za tokeny |  
| **Lokálny model** | dôraz na súkromie | napr. cez Ollama, dáta neopustia počítač |  

**OpenCode Go** stojí 10 $ mesačne (Go Plus s vyššími limitmi 40 $). Obsahuje  
napríklad modely Kimi, GLM, Qwen, DeepSeek, MiniMax, ale aj Claude Haiku 5.5  
či Gemini 4 Argon. Limity sú tri: na 5 hodín (20 % mesačného objemu), na  
týždeň (50 %) a na mesiac. OpenCode ponúka aj niekoľko **bezplatných modelov**  
– ich zoznam sa často mení.  

> ℹ️ **Predplatné Claude Pro/Max:** v januári 2026 Anthropic zablokoval  
> používanie spotrebiteľského predplatného Claude v nástrojoch tretích strán.  
> Ak chcete v OpenCode modely Claude, potrebujete API kľúč alebo inú službu,  
> ktorá ich sprostredkuje.  

Model zmeníte kedykoľvek príkazom `/models` alebo klávesom `F2`, ktorý prepína  
medzi naposledy použitými modelmi.  

### 3. Pokyny pre projekt: `AGENTS.md`  

Prvá vec, ktorú agent pri práci číta, je súbor `AGENTS.md` – „návod na  
obsluhu" projektu. Môžete ho napísať sami, alebo požiadať agenta: *„Preskúmaj  
projekt a vytvor súbor AGENTS.md s pokynmi pre agenta."* V mnohých návodoch  
nájdete na to aj príkaz `/init`. Viac o `AGENTS.md` nižšie.  

## Ovládanie terminálového rozhrania  

### Najdôležitejšie príkazy  

| Príkaz | Skratka | Čo robí |  
| :--- | :--- | :--- |  
| `/connect` | | pripojí poskytovateľa modelov |  
| `/models` | `Ctrl+X`, `M` | výber modelu |  
| `/agents` | `Ctrl+X`, `A` | výber agenta |  
| `/new` | `Ctrl+X`, `N` | nová relácia (čistý kontext) |  
| `/sessions` | `Ctrl+X`, `L` | návrat k staršej relácii |  
| `/undo` | `Ctrl+X`, `U` | vráti poslednú požiadavku aj zmeny súborov |  
| `/redo` | `Ctrl+X`, `R` | obnoví vrátené zmeny |  
| `/editor` | `Ctrl+X`, `E` | napíšete prompt v textovom editore |  
| `/btw otázka` | | vedľajšia otázka, ktorá sa nepridá do rozhovoru |  

Ďalšie užitočné klávesy:  

* `Shift+Tab` – prepína agentov (napr. Build ↔ Plan);  
* `Ctrl+P` – paleta všetkých príkazov;  
* `Enter` počas práce agenta – usmerníte ho („nie, použi radšej…");  
* `Ctrl+X`, `Enter` – zaradí prompt do fronty na neskôr;  
* `Shift+Enter` – nový riadok v prompte.  

### Odkazy na súbory a príkazy shellu  

* **`@súbor`** – pripojí súbor k promptu, napr. `@index.html` alebo len časť  
  súboru `@src/app.js#20-45`.  
* **`!príkaz`** – spustí príkaz shellu priamo, bez modelu, napr. `!git  
  status`. Výstup zostane v relácii, takže ho agent vidí.  

```
@predaj.csv Zhrň mi tento súbor: koľko je riadkov, aké sú stĺpce
a ktoré mesto má najväčší obrat?
```  

> 💡 **`/undo` je vaša záchranná brzda.** Vráti nielen rozhovor, ale aj zmeny  
> súborov, ktoré agent urobil. Pre istotu však pracujte v priečinku  
> spravovanom cez Git.  

## Agenti: Build, Plan a subagenti  

OpenCode obsahuje niekoľko vstavaných agentov. Každý je ten istý model, ale  
s iným „postrojom" – iným promptom a inými povoleniami. Aj to je ukážka sily  
harnessu.  

| Agent | Typ | Na čo slúži |  
| :--- | :--- | :--- |  
| **Build** | hlavný | predvolený agent, smie čítať, upravovať aj spúšťať príkazy |  
| **Plan** | hlavný | skúma a plánuje, bežné súbory projektu neupravuje |  
| **General** | subagent | výskum a viackrokové úlohy, nemôže spúšťať ďalších subagentov |  
| **Explore** | subagent | hľadá a číta kód či web, nič neupravuje |  

**Odporúčaný postup na kurze:** začnite v agentovi **Plan**, nechajte si  
navrhnúť riešenie, prečítajte si ho a až potom prepnite klávesom `Shift+Tab`  
na **Build**, ktorý plán vykoná.  

**Subagenti** pracujú vo vlastných reláciách s vlastným kontextom. Hlavný  
agent im zadá podúlohu a dostane len výsledný report. Tak sa jeho kontext  
nezahltí stovkami prečítaných súborov. Subagenta si môžete vyžiadať aj  
obyčajnou vetou: *„Použi subagenta explore a nájdi všetky miesta, kde sa  
počíta DPH."*  

### Vlastný agent  

Vlastného agenta vytvoríte ako Markdown súbor v priečinku `.opencode/agents/`  
(pre jeden projekt) alebo `~/.config/opencode/agents/` (pre všetky projekty).  
Hlavička určuje nastavenia, text pod ňou je systémový prompt:  

```markdown
---
description: Kontroluje zmeny v kóde, ale nič neupravuje
mode: subagent
model: anthropic/claude-sonnet-5-5
permissions:
  - action: edit
    resource: "*"
    effect: deny
  - action: shell
    resource: "*"
    effect: deny
---

Skontroluj aktuálne zmeny v projekte. Nájdené problémy zoraď podľa
závažnosti a pri každom uveď súbor a riadok. Odpovedaj po slovensky.
```  

Súbor uložený ako `.opencode/agents/kontrolor.md` vytvorí subagenta  
`kontrolor`. Všimnite si, že sme mu **odobrali ruky**: nesmie upravovať súbory  
ani spúšťať príkazy. Takého agenta môžete nechať pracovať bez obáv.  

## AGENTS.md – pamäť projektu  

Model si medzi reláciami nič nepamätá. Ak chcete, aby agent vždy vedel, ako sa  
projekt spúšťa, aké má pravidlá a v akom jazyku má odpovedať, zapíšte to do  
súboru **`AGENTS.md`**. Harness ho pri každej relácii vloží do kontextu.  

```markdown
# Projekt: Web pre kaviareň U Jána

## Všeobecné pravidlá
- Komunikuj po slovensky, kód a komentáre píš po anglicky.
- Pred väčšou zmenou najprv navrhni plán a počkaj na súhlas.
- Nikdy nemaž súbory v priečinku `fotky/`.

## Technológie
- Statický web: HTML, CSS, JavaScript bez frameworkov.
- Stránky sú v priečinku `web/`, obrázky v `web/img/`.

## Kontrola práce
- Po úprave over, že stránka `web/index.html` nemá chyby v HTML.
- Texty na webe musia mať slovenskú diakritiku.
```  

Kde OpenCode `AGENTS.md` hľadá:  

* **v projekte** – od aktuálneho priečinka smerom hore až po koreň projektu  
  (podpriečinky môžu mať vlastné, podrobnejšie pokyny);  
* **globálne** – `~/.config/opencode/AGENTS.md` platí pre všetky projekty  
  (napr. „odpovedaj vždy po slovensky");  
* **kompatibilita** – ak v priečinku `AGENTS.md` chýba, OpenCode prečíta  
  `CLAUDE.md`. Súbor `AGENTS.md` je otvorený štandard, ktorý používa viac  
  nástrojov.  

> 💡 Udržujte `AGENTS.md` krátky. Každý riadok súťaží o pozornosť modelu  
> s vašou úlohou. Dobré pravidlo: nové pravidlo pridajte vtedy, keď agent  
> urobí konkrétnu chybu – nie „pre istotu".  

## Povolenia – opraty v rukách človeka  

Toto je najdôležitejšia časť harnessu z pohľadu bezpečnosti. Každá akcia  
agenta (čítanie, úprava, príkaz shellu, web…) prechádza kontrolou povolení.  
Pravidlo má jeden z troch výsledkov:  

* **`allow`** – vykonaj bez pýtania;  
* **`ask`** – opýtaj sa človeka;  
* **`deny`** – zakáž.  

> ⚠️ **Pozor na predvolené nastavenie:** základné pravidlo v OpenCode je  
> **„povoľ všetko"**. Pýta sa len pri čítaní súborov `.env`, ktoré často  
> obsahujú heslá. Agent Build teda smie bez opýtania upravovať súbory aj  
> spúšťať príkazy. Na kurze a pri prvých pokusoch si povolenia sprísnite.  

Povolenia nastavíte v konfiguračnom súbore `opencode.jsonc` v koreni projektu.  
Odporúčané nastavenie pre začiatočníkov:  

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "permissions": [
    // každý príkaz shellu a každá úprava súboru sa najprv opýta
    { "action": "shell", "resource": "*", "effect": "ask" },
    { "action": "edit", "resource": "*", "effect": "ask" },
    // neškodné príkazy Gitu môže spúšťať sám
    { "action": "shell", "resource": "git status *", "effect": "allow" },
    { "action": "shell", "resource": "git diff *", "effect": "allow" },
    // odosielanie na GitHub je zakázané
    { "action": "shell", "resource": "git push *", "effect": "deny" },
    // mimo priečinka projektu sa vždy opýta
    { "action": "external_directory", "resource": "*", "effect": "ask" }
  ]
}
```  

Ako pravidlá fungujú:  

* vyhodnocujú sa **zhora nadol a platí posledné zhodné pravidlo** – preto je  
  všeobecné `"*"` hore a výnimky pod ním;  
* hviezdička `*` znamená „čokoľvek", takže `git push *` zachytí každé  
  odoslanie;  
* zložené príkazy (napr. `cd web && rm -r *`) OpenCode rozdelí na časti  
  a skontroluje každú zvlášť;  
* keď sa agent opýta, môžete odpovedať **once** (len teraz), **always** (vždy  
  v tomto projekte) alebo **reject** (zamietnuť). Uložené súhlasy nikdy  
  neprebijú pravidlo `deny`.  

Povolenia sa dajú nastaviť aj pre jednotlivých agentov – ako sme videli pri  
agentovi `kontrolor`.  

## Rozšírenia: príkazy, skills a MCP  

### Vlastné príkazy  

Často opakovaný prompt uložte ako príkaz. Súbor  
`.opencode/commands/vysvetli.md`:  

```markdown
---
description: Vysvetlí súbor jednoducho, pre začiatočníka
agent: plan
---

Vysvetli súbor $ARGUMENTS človeku, ktorý neprogramuje.
Najprv jednou vetou, na čo súbor slúži, potom prejdi hlavné časti.
```  

Príkaz spustíte ako `/vysvetli web/script.js`. Text `$ARGUMENTS` sa nahradí  
tým, čo napíšete za príkaz. Vďaka `agent: plan` príkaz nič neupraví.  

### Skills – návody, ktoré si agent načíta, keď ich potrebuje  

**Skill** je priečinok so súborom `SKILL.md`, ktorý opisuje postup pre  
konkrétnu úlohu (napr. „ako u nás pripravujeme faktúru" alebo „ako píšeme  
články na blog"). Agent na začiatku vidí len názov a krátky opis každého  
skillu. Celý návod si načíta, až keď ho naozaj potrebuje – a tak nezaberá  
kontext zbytočne.  

```markdown
---
name: Blogový článok
description: Postup na napísanie článku na firemný blog
---

1. Nadpis má najviac 60 znakov.
2. Prvý odsek zhrnie celý článok v troch vetách.
3. Používaj krátke odseky a medzititulky.
4. Na konci pridaj výzvu na kontakt.
```  

Skills OpenCode hľadá v `.opencode/skills/` (projekt)  
a `~/.config/opencode/skills/` (globálne). Prečíta aj skills vytvorené pre  
Claude Code (`.claude/skills/`) – formát je spoločný. Skill si môžete vyžiadať  
aj ručne cez `@nazov-skillu`.  

### MCP servery – nové nástroje pre agenta  

**MCP** (Model Context Protocol) je štandard, cez ktorý môžete agentovi pridať  
nástroje iných služieb – databázu, kalendár, dokumentáciu knižníc a pod. MCP  
servery sa pridávajú do `opencode.jsonc`:  

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "servers": {
      "context7": {
        "type": "remote",
        "url": "https://mcp.context7.com/mcp",
        "oauth": false,
        "headers": {
          "CONTEXT7_API_KEY": "{env:CONTEXT7_API_KEY}"
        }
      }
    }
  }
}
```  

API kľúč sa neukladá priamo do súboru – zápis `{env:CONTEXT7_API_KEY}` ho  
načíta z premennej prostredia. Každý MCP server zaberá časť kontextu modelu,  
preto pridávajte len tie, ktoré naozaj potrebujete.  

## OpenCode bez interaktívneho rozhrania  

Harness nemusí mať okno. OpenCode sa dá spustiť aj jedným príkazom – vhodné do  
skriptov alebo automatizácie:  

```bash
opencode run "Vysvetli, čo robí tento projekt, v piatich vetách."
```  

Ďalšie možnosti:  

* `opencode pair` – vypíše jednorazový odkaz na webové rozhranie (platí  
  5 minút), napr. na pokračovanie v práci z iného zariadenia;  
* `opencode mini` – minimalistické interaktívne rozhranie;  
* **SDK** – vývojári môžu OpenCode vložiť do vlastnej aplikácie a použiť ho  
  ako hotový harness.  

## Praktické cvičenia  

Cvičenia sú pripravené tak, aby ste nemuseli vedieť programovať. Pracujte  
v novom priečinku, napr. `C:\Projekty\kurz-ai`, a použite nastavenie povolení  
z tejto kapitoly.  

### Cvičenie 1: Webová vizitka v dvoch krokoch  

1.  Spustite OpenCode v prázdnom priečinku a prepnite sa na agenta **Plan**.  
2.  Zadajte: *„Navrhni jednoduchú jednostránkovú webovú vizitku pre lektora AI  
    kurzov. Len HTML a CSS, bez frameworkov. Najprv mi ukáž plán."*  
3.  Prečítajte si plán, prípadne ho upravte („pridaj sekciu s referenciami").  
4.  Klávesom `Shift+Tab` prepnite na **Build** a napíšte *„Vykonaj plán."*  
    Sledujte, na čo sa vás agent pýta.  
5.  Otvorte `index.html` v prehliadači. Skúste `/undo` a pozrite sa, čo sa  
    stalo so súbormi.  

### Cvičenie 2: Analýza dát  

1.  Skopírujte do priečinka ľubovoľný súbor CSV (napr. export z Excelu).  
2.  Zadajte: *„@data.csv Zhrň, čo obsahuje tento súbor, a nájdi tri zaujímavé  
    zistenia. Nič neupravuj."*  
3.  Pýtajte sa ďalej: *„Vytvor z toho graf ako HTML stránku."* Všimnite si,  
    aké nástroje agent použije.  

### Cvičenie 3: Prispôsobte si harness  

1.  Vytvorte súbor `AGENTS.md` s pravidlom *„Odpovedaj vždy po slovensky  
    a stručne."* Overte, že ho agent dodržiava.  
2.  Vytvorte vlastný príkaz `/vysvetli` z tejto kapitoly a vyskúšajte ho na  
    súbore z cvičenia 1.  
3.  Pridajte do povolení pravidlá `deny` pre príkazy `del *`, `rm *`  
    a `Remove-Item *` a požiadajte agenta, aby zmazal súbor. Čo sa stane?  
    Napadne vás iný spôsob mazania, ktorý tieto pravidlá obíde? Aj to je  
    dôvod, prečo je bezpečnejšie `ask` pre všetky príkazy.  

### Cvičenie 4: Rovnaká úloha, iný model  

Zadajte tú istú úlohu z cvičenia 1 v novej relácii (`/new`), ale s iným  
modelom (`/models`). Porovnajte výsledok, rýchlosť a počet krokov. Harness  
zostal rovnaký – zmenil sa len model.  

## Na čo si dať pozor  

* **Predvolené povolenia sú veľmi voľné.** Bez úpravy smie agent Build meniť  
  súbory a spúšťať príkazy bez opýtania.  
* **Pracujte s Gitom alebo zálohou.** `/undo` pomôže, ale verzionovanie je  
  spoľahlivejšie.  
* **Náklady.** Agent pri jednej úlohe pošle modelu veľa tokenov – celý kontext  
  pri každom kroku. Sledujte limity predplatného alebo spotrebu API.  
* **Súkromie.** Obsah súborov, ktoré agent číta, odchádza k poskytovateľovi  
  modelu. Pri citlivých dátach zvážte lokálny model.  
* **Prompt injection.** Text na webovej stránke alebo v súbore môže obsahovať  
  skryté pokyny pre agenta. Ďalší dôvod, prečo nastaviť `ask` pri príkazoch  
  shellu.  
* **Kvalita závisí od modelu.** Lacné a lokálne modely zvládnu jednoduché  
  úlohy, pri zložitejších robia viac chýb. Harness ich čiastočne vyrovná, ale  
  nie úplne.  
* **Staré návody.** Veľa materiálov na internete opisuje OpenCode 1.x.  

## Zhrnutie kapitoly  

*   **Agent = Model + Harness.** Model prináša inteligenciu, harness nástroje,  
    pamäť, slučku práce a pravidlá.  
*   **OpenCode je agent harness** – otvorený (MIT), nezávislý od modelu,  
    dostupný v termináli, desktopovej aplikácii aj na webe.  
*   Model sa nikdy priamo nedotkne počítača. Každú akciu vykoná harness –  
    a predtým skontroluje **povolenia** (`allow`, `ask`, `deny`).  
*   Agent **Plan** plánuje bez zmien, agent **Build** plán vykoná. Subagenti  
    riešia podúlohy vo vlastnom kontexte.  
*   Harness si prispôsobujete sami: **`AGENTS.md`**, povolenia, vlastní  
    agenti, príkazy, **skills** a **MCP** servery.  
*   Predvolené povolenia sú voľné – na kurze a pri citlivej práci ich treba  
    sprísniť.  

## Otázky a diskusia  

1.  Vysvetlite vlastnými slovami rozdiel medzi modelom a harnessom. Prečo nie  
    je ChatGPT ako webová aplikácia len „model"?  
2.  Prečo sa hovorí, že dobrý model v dobrom harnesse môže poraziť lepší model  
    v zlom harnesse? Uveďte príklad z cvičení.  
3.  Agent v projekte opakovane používa nesprávny formát dátumu. Opravíte to  
    zmenou modelu, alebo úpravou harnessu? Ako konkrétne?  
4.  Aké výhody a nevýhody má nástroj nezávislý od modelu (OpenCode) oproti  
    nástroju jednej firmy (Claude Code, Gemini CLI)?  
5.  Prečo je predvolené nastavenie „povoľ všetko" pohodlné, ale rizikové? Ako  
    by ste nastavili povolenia pre kolegu, ktorý s agentmi začína?  
6.  Kedy by ste použili lokálny model namiesto modelu v cloude?  
7.  Ktorá časť harnessu by mala zabrániť tomu, aby agent poslal citlivé dáta  
    na internet?  

## Zdroje  

* [OpenCode – oficiálna stránka](https://opencode.ai)  
* [Dokumentácia OpenCode](https://opencode.ai/docs/)  
* [Zdrojový kód na GitHube](https://github.com/anomalyco/opencode)  
* [Agenti v OpenCode](https://opencode.ai/docs/agents/)  
* [Povolenia v OpenCode](https://opencode.ai/docs/permissions/)  
* [The Anatomy of an Agent Harness (LangChain)](https://www.langchain.com/blog/the-anatomy-of-an-agent-harness)  
* [Agent Harness Engineering (Addy Osmani)](https://addyosmani.com/blog/agent-harness-engineering/)  
* [Thoughtworks Technology Radar – OpenCode](https://www.thoughtworks.com/radar/tools/opencode)

# Úvod do VS Code  

V predchádzajúcich kapitolách sme volali jazykové modely z Pythonu. Na  
písanie a spúšťanie takého kódu potrebujeme vhodný nástroj. V tejto  
kapitole sa naučíme pracovať s editorom **Visual Studio Code** (skrátene  
**VS Code**) – najpoužívanejším programátorským editorom na svete, ktorý  
je zároveň jedným z hlavných miest, kde sa dnes s AI reálne pracuje.  

*Kapitola predpokladá nulové skúsenosti s programátorskými editormi.  
Stav k októbru 2026.*  

Odporúčaný oficiálny návod na základy práce s editorom:  
https://code.visualstudio.com/docs/editing/codebasics  

## Čo je VS Code  

VS Code je bezplatný **editor zdrojového kódu** od spoločnosti Microsoft,  
vydaný v roku 2015. Funguje na Windows, macOS aj Linuxe. Jeho jadro je  
open-source a podľa prieskumov ho používajú približne tri štvrtiny  
programátorov. Pre Python patrí k najobľúbenejším vývojovým prostrediam.  

Treba rozlišovať dva pojmy:  

*   **Textový editor** (napr. Poznámkový blok) – len upravuje text.  
*   **IDE** (*Integrated Development Environment*, integrované vývojové  
    prostredie) – spája editor, spúšťanie programov, hľadanie chýb,  
    správu verzií a ďalšie nástroje v jednej aplikácii.  

VS Code stojí niekde medzi: sám osebe je ľahký a rýchly editor, no  
pomocou **rozšírení** (*extensions*) sa z neho stane plnohodnotné IDE  
pre takmer akýkoľvek jazyk – vrátane Pythonu a Jupyter notebookov.  
Vďaka tomu vyhovuje začiatočníkom aj skúseným programátorom. Väčšinu  
práce v ňom možno robiť **iba klávesnicou**, bez siahania po myši.  

### Prečo práve VS Code pre študentov AI  

*   **Python a Jupyter v jednom:** Skripty aj notebooky na jednom mieste.  
*   **AI asistenti priamo v editore:** GitHub Copilot, Claude Code,  
    OpenAI Codex a ďalší fungujú ako rozšírenia VS Code.  
*   **Integrovaný terminál:** Inštalácia knižníc a spúšťanie programov  
    bez prepínania okien.  
*   **Git a GitHub:** Správa verzií kódu bez znalosti príkazov.  
*   **Zadarmo a všade:** Rovnaké prostredie doma, v škole aj v práci.  

### VS Code a jeho „klony"  

Keďže jadro VS Code je open-source, vzniklo na ňom viacero samostatných  
editorov zameraných na AI – napríklad **Cursor**, **Windsurf**, **Kiro**  
od Amazonu či **Antigravity** od Googlu. Vyzerajú a ovládajú sa takmer  
rovnako, takže všetko, čo sa naučíte v tejto kapitole, využijete aj  
v nich.  

## Inštalácia  

1.  Otvorte stránku **code.visualstudio.com** a stiahnite inštalátor pre  
    svoj operačný systém.  
2.  **Windows:** Spustite inštalátor. V kroku *Select Additional Tasks*  
    zaškrtnite **Add to PATH** a **Add "Open with Code" action** – VS Code  
    potom môžete otvárať z terminálu aj kliknutím pravým tlačidlom  
    na priečinok.  
3.  **macOS:** Presuňte aplikáciu do priečinka *Applications*. Potom  
    otvorte VS Code, stlačte `Cmd+Shift+P`, napíšte *shell command*  
    a zvoľte **Install 'code' command in PATH**.  
4.  **Linux:** Stiahnite balík `.deb` (Ubuntu, Debian) alebo `.rpm`  
    (Fedora) a nainštalujte ho, prípadne použite `snap install code  
    --classic`.  

Po inštalácii by mal v termináli fungovať príkaz `code`. Príkaz  
`code .` otvorí aktuálny priečinok vo VS Code.  

> **Tip:** Rozhranie odporúčame ponechať v **angličtine**. Všetky návody,  
> dokumentácia aj odpovede AI asistentov používajú anglické názvy  
> príkazov a nastavení a hľadanie pomoci je potom oveľa jednoduchšie.  

## Prehľad rozhrania  

Po spustení uvidíte okno rozdelené na niekoľko častí:  

```
┌────┬──────────────┬─────────────────────────────┬──────────────┐
│ A  │ B            │ C  Editor                   │ E            │
│ c  │ Bočný panel  │                             │ Chat s AI    │
│ t  │ (Explorer,   │   hlavna.py   poznamky.md   │ (Copilot,    │
│ i  │  Search,     │   ─────────────────────     │  Claude…)    │
│ v  │  Git…)       │   import os                 │              │
│ i  │              ├─────────────────────────────┤              │
│ t  │              │ D  Panel: Terminal, Problems│              │
│ y  │              │   $ python hlavna.py        │              │
├────┴──────────────┴─────────────────────────────┴──────────────┤
│ F  Stavový riadok: Python 3.13 (.venv) · Git: main · UTF-8      │
└─────────────────────────────────────────────────────────────────┘
```

*   **A – Activity Bar:** Ikony na ľavom okraji prepínajú bočný panel:  
    **Explorer** (súbory), **Search** (hľadanie), **Source Control**  
    (Git), **Run and Debug** (spúšťanie a ladenie) a **Extensions**  
    (rozšírenia).  
*   **B – Primary Side Bar:** Obsah zvoleného pohľadu, najčastejšie  
    strom súborov.  
*   **C – Editor:** Hlavná plocha na úpravu súborov. Každý otvorený súbor  
    má vlastnú kartu; editor sa dá rozdeliť na viac častí vedľa seba.  
*   **D – Panel:** Spodná časť s **terminálom**, zoznamom chýb  
    (**Problems**) a výstupom programov a rozšírení (**Output**).  
*   **E – Secondary Side Bar:** Pravý panel, kde sa zvyčajne zobrazuje  
    **chat s AI asistentom**.  
*   **F – Status Bar:** Stavový riadok s informáciami o aktuálnom súbore,  
    zvolenom interpreteri Pythonu, Git vetve a kódovaní.  

Ďalšie užitočné prvky rozhrania:  

*   **Breadcrumbs** – „omrvinky" nad editorom ukazujú, v ktorom súbore,  
    triede a funkcii sa nachádzate, a umožňujú medzi nimi preskakovať  
    (*View → Appearance → Breadcrumbs*).  
*   **Minimap** – zmenšený náhľad celého súboru na pravom okraji editora,  
    vhodný na orientáciu v dlhých súboroch.  
*   **Sticky Scroll** – pri posúvaní zostáva hore viditeľný riadok  
    s názvom funkcie alebo triedy, v ktorej sa práve nachádzate.  

## Práca s priečinkami  

VS Code nepracuje s jednotlivými súbormi, ale s **priečinkami**  
(*folder*, *workspace*). Projekt je jednoducho priečinok so všetkými  
jeho súbormi. Preto je dobrý zvyk:  

1.  Pre každý projekt alebo cvičenie vytvoriť **samostatný priečinok**.  
2.  Otvoriť ho cez **File → Open Folder…** (alebo príkazom `code .`).  
3.  Nové súbory vytvárať v Exploreri ikonou **New File**.  

Pri otvorení priečinka sa VS Code opýta, či dôverujete jeho autorom  
(**Workspace Trust**). Ak priečinok obsahuje kód z neznámeho zdroja,  
zvoľte **Restricted Mode** – VS Code potom automaticky nespustí nič,  
čo by mohlo byť nebezpečné.  

> **Pozor na názvy:** V názvoch priečinkov a súborov s kódom sa vyhnite  
> medzerám a diakritike. Namiesto `Moje cvičenia/prvý skript.py` použite  
> `moje_cvicenia/prvy_skript.py`.  

## Paleta príkazov a základné skratky  

Najdôležitejšou skratkou vo VS Code je **paleta príkazov** (*Command  
Palette*): `Ctrl+Shift+P` (na macOS `Cmd+Shift+P`). Otvorí vyhľadávacie  
pole, cez ktoré sa dá spustiť **ktorýkoľvek príkaz** editora. Ak neviete,  
kde niečo nájsť, napíšte do palety, čo chcete urobiť – napríklad  
*format*, *theme* alebo *python interpreter*.  

Často používané príkazy z palety:  

*   **Python: Select Interpreter** – výber Pythonu (virtuálneho prostredia).  
*   **Preferences: Color Theme** – zmena farebnej témy.  
*   **Trim Trailing Whitespace** – odstráni medzery na koncoch riadkov.  
*   **Developer: Reload Window** – reštartuje okno editora; pomáha, keď  
    sa rozšírenie „zasekne" alebo po zmene nastavení.  
*   **Help: Welcome** – úvodná obrazovka s návodmi pre začiatočníkov.  

Skratka `Ctrl+P` (**Quick Open**) slúži predovšetkým na rýchle otvorenie  
súboru podľa názvu. Podľa prvého znaku však vie aj viac:  

| Zadanie v `Ctrl+P` | Činnosť |
| :--- | :--- |
| `hlav` | Otvorí súbor, ktorého názov obsahuje *hlav* |
| `>príkaz` | To isté ako paleta príkazov |
| `@nazov` | Skok na funkciu alebo triedu v aktuálnom súbore |
| `:25` | Skok na riadok 25 |

Najdôležitejšie skratky pre začiatok (na macOS nahraďte `Ctrl` klávesom  
`Cmd` a `Alt` klávesom `Option`):  

| Skratka | Činnosť |
| :--- | :--- |
| `Ctrl+Shift+P` | Paleta príkazov |
| `Ctrl+P` | Rýchle otvorenie súboru podľa názvu |
| `` Ctrl+` `` | Zobraziť alebo skryť terminál |
| `Ctrl+B` | Zobraziť alebo skryť bočný panel |
| `Ctrl+,` | Nastavenia |
| `Ctrl+S` | Uložiť súbor |
| `Ctrl+/` | Zakomentovať alebo odkomentovať riadky |
| `Ctrl+D` | Označiť ďalší výskyt slova (viac kurzorov naraz) |
| `F2` | Premenovať premennú alebo funkciu všade v kóde |
| `F12` | Prejsť na definíciu funkcie |
| `F5` | Spustiť program v ladiacom režime |
| `Ctrl+Shift+V` | Náhľad Markdown súboru |
| `Ctrl+I` | Inline chat s AI priamo v editore |
| `Ctrl+Alt+I` | Otvoriť chat s AI (na macOS `Ctrl+Cmd+I`) |

Netreba sa učiť všetky naraz. Stačí začať s paletou príkazov,  
terminálom a `Ctrl+P` – ostatné prídu s praxou. Ďalšie skratky nájdete  
v nasledujúcej časti.  

## Efektívna práca s textom a kódom  

Skúsení programátori pracujú vo VS Code takmer výlučne klávesnicou.  
Nasledujúce skratky platia pre **Windows**; na macOS nahraďte `Ctrl`  
klávesom `Cmd` a `Alt` klávesom `Option`. Na Linuxe sú väčšinou rovnaké,  
výnimky uvádzame v samostatnej tabuľke nižšie.  

> **Tip:** Všetky skratky si môžete prezrieť a zmeniť v editore  
> klávesových skratiek (`Ctrl+K Ctrl+S`). Prehľadný ťahák vo formáte PDF  
> otvorí skratka `Ctrl+K Ctrl+R`. Zápis `Ctrl+K Ctrl+S` znamená: stlačte  
> `Ctrl+K`, pustite a potom stlačte `Ctrl+S`.  

### Úpravy riadkov  

| Skratka | Činnosť |
| :--- | :--- |
| `Ctrl+Enter` | Vložiť nový riadok pod aktuálny (kurzor nemusí byť na konci) |
| `Ctrl+Shift+Enter` | Vložiť nový riadok nad aktuálny |
| `Ctrl+Shift+K` | Zmazať celý riadok |
| `Ctrl+C` / `Ctrl+X` | Bez označenia textu skopíruje / vystrihne celý riadok |
| `Alt+↑` / `Alt+↓` | Presunúť riadok hore / dole |
| `Shift+Alt+↑` / `Shift+Alt+↓` | Duplikovať riadok hore / dole |
| `Ctrl+]` / `Ctrl+[` | Zväčšiť / zmenšiť odsadenie riadku |

### Formátovanie  

| Skratka | Činnosť |
| :--- | :--- |
| `Shift+Alt+F` | Naformátovať celý súbor |
| `Ctrl+K Ctrl+F` | Naformátovať len označený text |

Na formátovanie Python kódu potrebujete nainštalované rozšírenie  
formátovača, napríklad **Ruff** (pozri časť *Rozšírenia*).  

### Viac kurzorov naraz  

**Viac kurzorov** (*multi-cursor*) umožňuje písať na viacerých miestach  
súčasne – jedna z najužitočnejších funkcií moderných editorov.  

| Skratka | Činnosť |
| :--- | :--- |
| `Ctrl+Alt+↑` / `Ctrl+Alt+↓` | Pridať kurzor o riadok vyššie / nižšie |
| `Alt+klik` | Pridať kurzor na miesto kliknutia |
| `Ctrl+D` | Označiť ďalší výskyt označeného slova |
| `Ctrl+Shift+L` | Označiť všetky výskyty naraz |
| `Shift+Alt+I` | Pridať kurzor na koniec každého označeného riadku |
| `Ctrl+U` | Vrátiť posledné pridanie kurzora |
| `Esc` | Zrušiť viacnásobné kurzory |

Kurzory sa štandardne pridávajú cez `Alt+klik`. Kto je zvyknutý  
na `Ctrl+klik`, môže to prepnúť príkazom **Toggle Multi-Cursor  
Modifier** (alebo nastavením `editor.multiCursorModifier`).  

**Cvičenie – viac kurzorov:** Nasledujúci kód nefunguje správne –  
reťazce nie sú f-reťazce, takže sa výrazy v zátvorkách nevyhodnotia.  
Pomocou viacerých kurzorov pridajte na začiatok každého reťazca písmeno  
`f` a zo všetkých riadkov naraz odstráňte výkričník `!`. Nakoniec  
odstráňte medzery na koncoch riadkov príkazom **Trim Trailing  
Whitespace**.  

```python
vals = (-5, 10, 55, 12, -7, 11, 22)

print('minimum je: {min(vals)}!') 
print('maximum je: {max(vals)}!')   
print('pocet prvkov je: {len(vals)}!')            
print('suma je: {sum(vals)}!')
```

> **Nápoveda:** Umiestnite kurzor pred apostrof v prvom `print`, pridajte  
> kurzory nižšie (`Ctrl+Alt+↓`) a napíšte `f`. Na výkričníky použite  
> `Ctrl+D` alebo `Ctrl+Shift+L`.  

### Stĺpcový výber  

**Stĺpcový výber** (*column selection*) označí obdĺžnikovú oblasť textu  
naprieč riadkami. Hodí sa na prácu s tabuľkovými dátami zarovnanými  
do stĺpcov.  

*   Myšou: ťahajte so stlačenými `Shift+Alt` (na macOS `Shift+Option`).  
*   Klávesnicou: `Ctrl+Shift+Alt+šípky`.  

**Cvičenie – stĺpcový výber:** V nasledujúcich dátach vymeňte stĺpce  
*occupation* a *last name*.  

```
first name   occupation     last name  
John         gardener       Doe
Roger        driver         Roe
Paul         teacher        Novak
Jane         accountant     Smith
Lucia        programmer     Dorak
Robert       soldier        Williams
```

> **Nápoveda:** Stĺpcovým výberom označte celý stĺpec *occupation*  
> vrátane medzier za ním a vystrihnite ho (`Ctrl+X`). Kurzory zostanú  
> na všetkých riadkoch – stlačte `End` a vložte text (`Ctrl+V`). Keď je  
> počet kurzorov rovnaký ako počet vystrihnutých riadkov, VS Code vloží  
> na každý riadok práve jeho časť.  

### Hľadanie a nahrádzanie  

| Skratka | Činnosť |
| :--- | :--- |
| `Ctrl+F` | Hľadať v aktuálnom súbore |
| `Ctrl+H` | Nahradiť v aktuálnom súbore |
| `Ctrl+Shift+F` | Hľadať vo všetkých súboroch projektu |
| `Ctrl+Shift+H` | Nahradiť vo všetkých súboroch projektu |
| `F3` / `Shift+F3` | Ďalší / predchádzajúci výskyt |
| `Alt+Enter` | Počas hľadania označí všetky nájdené výskyty (viac kurzorov) |

V poli hľadania možno zapnúť aj rozlišovanie veľkých a malých písmen,  
hľadanie celých slov a **regulárne výrazy**.  

### Navigácia v súboroch a kóde  

| Skratka | Činnosť |
| :--- | :--- |
| `Ctrl+Tab` | Prepínanie medzi otvorenými súbormi |
| `Ctrl+\` | Rozdeliť editor na dve časti vedľa seba |
| `Ctrl+W` | Zavrieť aktuálny súbor |
| `Ctrl+K Ctrl+W` | Zavrieť všetky súbory |
| `Ctrl+Shift+T` | Znovu otvoriť naposledy zatvorený súbor |
| `Ctrl+K R` | Zobraziť aktuálny súbor v systémovom prieskumníkovi súborov |
| `Alt+←` / `Alt+→` | Späť / dopredu na predchádzajúce miesto v kóde |
| `Ctrl+G` | Prejsť na riadok s daným číslom |
| `Ctrl+Shift+O` | Prejsť na funkciu alebo triedu v súbore |
| `Ctrl+T` | Prejsť na funkciu alebo triedu v celom projekte |
| `F12` | Prejsť na definíciu |
| `Alt+F12` | Zobraziť definíciu v okienku bez opustenia súboru (*peek*) |
| `Shift+F12` | Nájsť všetky miesta, kde sa funkcia či premenná používa |
| `Ctrl+Shift+M` | Panel **Problems** so zoznamom chýb a varovaní |

### Programátorské úpravy  

| Skratka | Činnosť |
| :--- | :--- |
| `Ctrl+Space` | Vyvolať návrhy dopĺňania (IntelliSense) |
| `Ctrl+.` | Rýchla oprava (*Quick Fix*) – napr. doplnenie chýbajúceho importu |
| `Ctrl+/` | Zakomentovať / odkomentovať riadok |
| `Ctrl+K Ctrl+C` / `Ctrl+K Ctrl+U` | Pridať / odstrániť komentár riadku |
| `Shift+Alt+A` | Blokový komentár (v Pythone sa nepoužíva) |
| `Ctrl+Shift+[` / `Ctrl+Shift+]` | Zbaliť / rozbaliť blok kódu |
| `Ctrl+K Ctrl+0` / `Ctrl+K Ctrl+J` | Zbaliť / rozbaliť všetky bloky |

### Sústredená práca  

| Skratka | Činnosť |
| :--- | :--- |
| `Ctrl+K Z` | Režim **Zen** – skryje všetko okrem editora (návrat `Esc Esc`) |
| `Ctrl+B` | Skryť / zobraziť bočný panel |
| `Ctrl+J` | Skryť / zobraziť spodný panel (terminál, Problems, Output) |
| `F11` | Celá obrazovka |

### Rozdiely na Linuxe  

Na Linuxe niektoré kombinácie používa samotný operačný systém, preto  
má VS Code pre ne iné skratky:  

| Činnosť | Windows | Linux |
| :--- | :--- | :--- |
| Naformátovať súbor | `Shift+Alt+F` | `Ctrl+Shift+I` |
| Duplikovať riadok | `Shift+Alt+↑/↓` | `Ctrl+Shift+Alt+↑/↓` |
| Pridať kurzor vyššie / nižšie | `Ctrl+Alt+↑/↓` | `Shift+Alt+↑/↓` |
| Späť / dopredu v kóde | `Alt+←/→` | `Ctrl+Alt+-` / `Ctrl+Shift+-` |
| Blokový komentár | `Shift+Alt+A` | `Ctrl+Shift+A` |
| Zobraziť súbor v prieskumníkovi | `Ctrl+K R` | `Ctrl+Alt+R` |

Ak si nie ste istí, nájdite príkaz v palete príkazov – skratka sa  
zobrazí vedľa jeho názvu.  

## Rozšírenia  

Funkcie VS Code sa rozširujú pomocou **rozšírení** z obchodu  
**Visual Studio Marketplace**. Otvoríte ho ikonou **Extensions**  
alebo skratkou `Ctrl+Shift+X`, rozšírenie vyhľadáte a kliknete  
na **Install**.  

Odporúčané rozšírenia pre študentov AI:  

| Rozšírenie | Vydavateľ | Na čo slúži |
| :--- | :--- | :--- |
| **Python** | Microsoft | Podpora Pythonu, spúšťanie, ladenie (obsahuje aj Pylance) |
| **Jupyter** | Microsoft | Práca s notebookmi `.ipynb` |
| **Ruff** | Astral | Kontrola a automatické formátovanie kódu |
| **GitHub Copilot Chat** | GitHub | AI asistent a agent priamo v editore |
| **Claude Code** | Anthropic | Kódovací agent od Anthropic |
| **Codex** | OpenAI | Kódovací agent od OpenAI |
| **Markdown All in One** | Yu Zhang | Pohodlnejšie písanie Markdown dokumentov |

Ďalšie užitočné rozšírenia:  

| Rozšírenie | Na čo slúži |
| :--- | :--- |
| **Rewrap** | Zalomí komentáre a text na zvolenú šírku, napr. 80 znakov (`Alt+Q`) |
| **REST Client** | Odosielanie HTTP požiadaviek priamo z editora (pozri nižšie) |
| **SQLite Viewer** | Prezeranie databázových súborov SQLite |
| **Hex Editor** | Zobrazenie a úprava súborov po bajtoch |
| **TabOut** | Klávesom `Tab` vyskočí kurzor zo zátvoriek a úvodzoviek |
| **file-icons** | Prehľadné ikony súborov podľa typu |
| **GitLens** | Rozšírené funkcie Gitu: kto a kedy zmenil riadok, história súborov |
| **Git History** | Prehľadávanie histórie commitov a porovnávanie vetiev |

> **Bezpečnosť rozšírení:** Rozšírenie má prístup k vašim súborom  
> a môže spúšťať programy. V obchode sa už objavili aj škodlivé  
> rozšírenia, ktoré sa vydávali za populárne nástroje. Inštalujte len  
> rozšírenia od **overených vydavateľov** (modrá značka pri mene)  
> s veľkým počtom inštalácií.  

## Python vo VS Code  

### 1. Inštalácia Pythonu  

VS Code samotný Python neobsahuje – treba ho nainštalovať zvlášť  
z **python.org** (odporúčame verziu 3.12 alebo novšiu). Na Windows  
pri inštalácii zaškrtnite **Add python.exe to PATH**. Na macOS  
a Linuxe býva Python často už nainštalovaný.  

Overenie v termináli:  

```bash
python --version   # na macOS/Linuxe niekedy python3 --version
```

### 2. Virtuálne prostredie  

Každý projekt by mal mať vlastné **virtuálne prostredie** (*virtual  
environment*) – samostatný priečinok s knižnicami len pre daný projekt.  
Projekty si tak navzájom nepreperú verzie knižníc.  

Najjednoduchšie ho vytvoríte cez paletu príkazov:  
**Python: Create Environment… → Venv** a zvolíte nainštalovaný Python.  
VS Code vytvorí priečinok `.venv` a automaticky ho začne používať.  

To isté v termináli:  

```bash
python -m venv .venv

# aktivácia – Windows (PowerShell):
.venv\Scripts\Activate.ps1
# aktivácia – Windows (Command Prompt):
.venv\Scripts\activate
# aktivácia – macOS a Linux:
source .venv/bin/activate
```

Ak vytvoríte prostredie v termináli, VS Code ho zvyčajne sám zistí  
a ponúkne jeho použitie. Ktorý Python VS Code práve používa, vidíte  
v stavovom riadku. Zmeníte ho príkazom **Python: Select Interpreter**.  
Nový terminál vo VS Code potom prostredie aktivuje automaticky.  

> **Tip:** Modernou a rýchlou alternatívou k `venv` a `pip` je nástroj  
> **uv** (`uv venv`, `uv pip install …`), ktorý je čoraz populárnejší.  

### 3. Inštalácia knižníc  

S aktivovaným prostredím nainštalujeme knižnice z predchádzajúcich  
kapitol:  

```bash
pip install openai anthropic python-dotenv
```

### 4. Funkcie rozšírenia Python  

Rozšírenie **Python** spolu s jazykovým serverom **Pylance** prináša:  

*   **IntelliSense** – návrhy názvov premenných, funkcií, modulov  
    a parametrov počas písania, spolu s dokumentáciou.  
*   **Kontrola kódu** (*linting*) – upozorní na chyby a nedodržanie  
    štýlu ešte pred spustením. Odporúčame **Ruff**; k dispozícii sú aj  
    rozšírenia pre staršie nástroje **Pylint** a **Flake8**.  
*   **Kontrola typov** – Pylance vie odhaliť chyby v typoch (napr.  
    sčítanie čísla s reťazcom). Prísnosť nastavíte voľbou  
    `python.analysis.typeCheckingMode` (`off`, `basic`, `standard`,  
    `strict`). Alternatívou je rozšírenie **Mypy**.  
*   **Automatické importy** – ak použijete neimportovaný modul alebo  
    funkciu, rýchla oprava (`Ctrl+.`) doplní chýbajúci `import`.  
*   **Refaktoring** – premenovanie naprieč súbormi (`F2`), vytiahnutie  
    časti kódu do samostatnej funkcie či premennej (`Ctrl+.`).  
*   **Testovanie** – pohľad **Testing** (ikona banky) nájde a spustí  
    testy napísané v `pytest` alebo `unittest`.  

### 5. Spustenie programu  

*   Tlačidlo **▶ Run Python File** vpravo hore spustí aktuálny súbor  
    v termináli.  
*   Rovnako funguje kliknutie pravým tlačidlom v editore → **Run Python  
    File in Terminal**.  
*   `Ctrl+F5` spustí program bez ladenia, `F5` s ladením.  

### 6. Ladenie programu  

**Ladenie** (*debugging*) umožňuje program zastaviť na zvolenom mieste  
a pozrieť sa, čo sa v ňom deje. Kliknite vľavo od čísla riadku – objaví  
sa červená bodka, tzv. **breakpoint**. Po stlačení `F5` sa program  
na tomto riadku zastaví a v paneli **Variables** uvidíte hodnoty všetkých  
premenných.  

| Skratka | Činnosť |
| :--- | :--- |
| `F5` | Spustiť ladenie / pokračovať po zastavení |
| `F9` | Pridať alebo odstrániť breakpoint na aktuálnom riadku |
| `F10` | Krok na ďalší riadok (*step over*) |
| `F11` | Vstúpiť do volanej funkcie (*step into*) |
| `Shift+F11` | Vyskočiť z aktuálnej funkcie (*step out*) |
| `Shift+F5` | Ukončiť ladenie |

Ladenie je jedna z najcennejších zručností programátora: namiesto  
hádania, prečo program nefunguje, vidíte presne, čo sa v ňom deje.  

Ak potrebujete program spúšťať s parametrami alebo inak ako štandardne,  
vytvorte konfiguráciu v súbore `.vscode/launch.json` (v pohľade **Run  
and Debug** odkaz *create a launch.json file*):  

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: aktuálny súbor s parametrami",
            "type": "debugpy",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "args": ["--model", "openrouter/free"]
        }
    ]
}
```

Takto možno ladiť aj webové aplikácie (Django, Flask, FastAPI),  
jednotlivé testy či programy bežiace na vzdialenom počítači.  

### 7. Úryvky kódu (snippets)  

**Úryvok** (*snippet*) je šablóna, ktorá sa po napísaní krátkej skratky  
a stlačení `Tab` rozbalí na celý blok kódu. Rozšírenie Python dnes  
vlastné úryvky neobsahuje (boli z neho odstránené), no vytvoriť si ich  
je jednoduché: paleta príkazov → **Snippets: Configure Snippets** →  
**python.json**.  

```json
{
    "Hlavný blok programu": {
        "prefix": "ifmain",
        "body": [
            "if __name__ == \"__main__\":",
            "    ${1:main()}"
        ],
        "description": "Blok if __name__ == '__main__'"
    },
    "Klient OpenRouter": {
        "prefix": "orclient",
        "body": [
            "import os",
            "",
            "from dotenv import load_dotenv",
            "from openai import OpenAI",
            "",
            "load_dotenv()",
            "",
            "client = OpenAI(",
            "    base_url=\"https://openrouter.ai/api/v1\",",
            "    api_key=os.environ[\"OPENROUTER_API_KEY\"],",
            ")",
            "$0"
        ],
        "description": "Pripojenie k OpenRouter API"
    }
}
```

Značky `${1:main()}` a `$0` určujú, kam sa po rozbalení presunie kurzor.  
Hotové sady úryvkov ponúkajú aj rozšírenia z Marketplace.  

## Jupyter notebooky  

**Jupyter notebook** (súbor `.ipynb`) kombinuje kód, jeho výstupy, grafy  
a text v jednom dokumente rozdelenom na **bunky**. V AI a dátovej vede  
je to veľmi rozšírený formát – vhodný na experimenty, analýzu dát  
a výučbu.  

VS Code vie s notebookmi pracovať priamo, bez webového prehliadača:  

1.  Nainštalujte rozšírenie **Jupyter** a do prostredia knižnicu  
    `ipykernel` (`pip install ipykernel`).  
2.  Vytvorte notebook príkazom **Create: New Jupyter Notebook**.  
3.  Vpravo hore zvoľte **kernel** – teda Python z vášho `.venv`.  
4.  Bunku spustíte `Shift+Enter`.  

Kedy čo použiť:  

*   **Notebook** – skúšanie, analýza dát, grafy, postupné objavovanie.  
*   **Skript `.py`** – hotový program, ktorý sa spúšťa celý naraz,  
    ďalej sa rozvíja alebo nasadzuje.  

## Terminál  

Integrovaný terminál otvoríte skratkou `` Ctrl+` `` alebo cez  
**Terminal → New Terminal**. Automaticky sa otvorí v priečinku projektu.  
Na Windows je predvoleným terminálom PowerShell, na macOS a Linuxe zsh  
alebo bash.  

| Skratka | Činnosť |
| :--- | :--- |
| `` Ctrl+` `` | Zobraziť / skryť terminál |
| `` Ctrl+Shift+` `` | Otvoriť nový terminál |
| `Ctrl+Shift+5` | Rozdeliť terminál na dve časti vedľa seba |
| `Ctrl+PageUp` / `Ctrl+PageDown` | Prepínanie medzi terminálmi |

Základné príkazy, ktoré sa oplatí poznať:  

| Príkaz | Činnosť |
| :--- | :--- |
| `cd priecinok` | Prejsť do priečinka (`cd ..` o úroveň vyššie) |
| `ls` (na Windows aj `dir`) | Zobraziť obsah priečinka |
| `python skript.py` | Spustiť Python skript |
| `pip install balik` | Nainštalovať knižnicu |
| `code subor.py` | Otvoriť súbor vo VS Code |

Predvolený terminál na Windows zmeníte nastavením  
`terminal.integrated.defaultProfile.windows` – napríklad na `Command  
Prompt`, ak vám PowerShell nedovolí aktivovať virtuálne prostredie.  

## REST Client: testovanie API v editore  

Jazykové modely, s ktorými pracujeme, sú dostupné cez **HTTP API**.  
Rozšírenie **REST Client** umožňuje posielať HTTP požiadavky priamo  
z VS Code a hneď vidieť odpoveď – bez písania programu. Hodí sa  
na rýchle vyskúšanie API alebo hľadanie chyby v požiadavke.  

Vytvorte súbor s príponou `.http`, napríklad `client.http`. Jednotlivé  
požiadavky oddeľte riadkom `###`. Nad každou požiadavkou sa zobrazí  
odkaz **Send Request** – po kliknutí sa odpoveď otvorí vedľa editora.  

```http
### Textový súbor
GET http://webcode.me/words.txt

### Dáta vo formáte CSV
GET http://webcode.me/users.csv

### Dáta vo formáte JSON
GET http://webcode.me/users.json

### Dáta vo formáte XML
GET http://webcode.me/users.xml

### Dlhší text
GET http://webcode.me/thermopylae.txt

### HTML stránka
GET http://webcode.me/os.html

### HTML tabuľka
GET http://webcode.me/countries.html
```

Rovnako môžeme zavolať aj jazykový model. REST Client vie načítať API  
kľúč zo súboru `.env` v tom istom priečinku, takže ho nemusíme písať  
do súboru `.http`:  

```http
### Otázka pre AI model cez OpenRouter
POST https://openrouter.ai/api/v1/chat/completions
Content-Type: application/json
Authorization: Bearer {{$dotenv OPENROUTER_API_KEY}}

{
    "model": "openrouter/free",
    "messages": [
        {"role": "user", "content": "Čo je REST API? Odpovedz jednou vetou."}
    ]
}
```

V odpovedi uvidíte presne to, čo vracia API: odpoveď modelu, názov  
použitého modelu aj počet spotrebovaných tokenov. Knižnice ako `openai`  
robia v pozadí presne toto – posielajú HTTP požiadavky vo formáte JSON.  

## Git a GitHub  

**Git** je systém na správu verzií: ukladá históriu zmien v kóde, takže  
sa môžete kedykoľvek vrátiť k funkčnej verzii. **GitHub** je webová  
služba, kde sa repozitáre Gitu ukladajú a zdieľajú.  

VS Code má podporu Gitu zabudovanú v pohľade **Source Control**  
(`Ctrl+Shift+G`):  

1.  **Initialize Repository** – začne sledovať zmeny v priečinku.  
2.  Zmenené súbory sa zobrazia v zozname. Kliknutím na súbor sa otvorí  
    **porovnanie zmien** (*diff*) – vľavo pôvodná, vpravo nová verzia.  
3.  Ikonou **+** zmeny pripravíte na uloženie (*stage*).  
4.  Napíšete krátky popis zmeny a kliknete na **Commit** – zmena sa  
    uloží do histórie.  
5.  **Publish Branch** – po prihlásení do GitHubu nahrá projekt  
    na GitHub.  

Históriu zmien konkrétneho súboru zobrazí pohľad **Timeline** v dolnej  
časti Explorera. Pokročilejšie funkcie pridávajú rozšírenia **GitLens**  
(pri každom riadku ukáže, kto a kedy ho naposledy zmenil) a **Git  
History** (prehľadávanie histórie a porovnávanie vetiev).  

> **Dôležité:** Do Gitu nikdy neukladajte **API kľúče** a súbory `.env`.  
> Uniknutý kľúč môže niekto zneužiť na vašu útratu – roboty prehľadávajú  
> GitHub a hľadajú kľúče v priebehu minút. Pridajte preto do projektu  
> súbor `.gitignore` s nasledujúcimi riadkami.  

```
.env
.venv/
```

## AI asistenti vo VS Code  

VS Code sa v posledných rokoch stal jedným z hlavných miest, kde sa  
s AI reálne pracuje. AI asistent v editore vidí váš kód a môže pomáhať  
viacerými spôsobmi:  

*   **Dopĺňanie kódu:** Počas písania navrhuje pokračovanie (šedý text),  
    ktoré prijmete klávesom `Tab`.  
*   **Inline chat** (`Ctrl+I`): Označíte kód a napíšete, čo s ním  
    urobiť – napr. *pridaj ošetrenie chýb*.  
*   **Chat:** Rozhovor o kóde v bočnom paneli – vysvetlenie chyby,  
    návrh riešenia, otázky k projektu.  
*   **Agentský režim:** Asistent dostane celú úlohu, sám prehľadá  
    súbory, upraví viacero z nich a spustí príkazy v termináli.  
    Pred rizikovými krokmi žiada o súhlas.  

### Dostupné nástroje  

*   **GitHub Copilot** – AI asistent priamo integrovaný vo VS Code.  
    Ponúka bezplatný plán s mesačnými limitmi a špeciálny plán pre  
    overených študentov (dostupnosť a podmienky sa menia, overte ich  
    na stránke GitHub Education). Cez Copilot možno používať modely  
    viacerých firiem vrátane OpenAI a Anthropic.  
*   **Claude Code** a **Codex** – kódovacie agenty od Anthropic  
    a OpenAI, ktoré o nich hovorili predchádzajúce kapitoly. Fungujú  
    ako rozšírenia VS Code a vyžadujú predplatné alebo API kľúč  
    príslušnej firmy.  

### Vlastné modely v chate: príklad s DeepSeek  

Do chatu vo VS Code možno pridať aj modely, ktoré v ponuke nie sú –  
stačí, aby mali **API kompatibilné s OpenAI**. Takto napríklad použijete  
lacné modely DeepSeek s vlastným API kľúčom (pozri kapitolu o DeepSeek).  
Funkcia vyžaduje aktuálnu verziu VS Code s rozšírením GitHub Copilot  
Chat.  

1.  V palete príkazov spustite **Chat: Manage Language Models**.  
2.  Zvoľte **Add Models → Custom Endpoint**.  
3.  Zadajte názov skupiny (napr. *DeepSeek*), API kľúč a typ API  
    **Chat Completions**.  
4.  VS Code otvorí konfiguračný súbor, do ktorého doplníte modely:  

```json
[
    {
        "name": "DeepSeek",
        "vendor": "customendpoint",
        "apiKey": "${input:chat.lm.secret.3767139b}",
        "apiType": "chat-completions",
        "models": [
            {
                "id": "deepseek-flash",
                "name": "DeepSeek V4.1 Flash",
                "url": "https://api.deepseek.com/v1/chat/completions",
                "toolCalling": true,
                "vision": false,
                "maxInputTokens": 1000000,
                "maxOutputTokens": 384000
            },
            {
                "id": "deepseek-v4-pro",
                "name": "DeepSeek V4 Pro",
                "url": "https://api.deepseek.com/v1/chat/completions",
                "toolCalling": true,
                "vision": false,
                "maxInputTokens": 1000000,
                "maxOutputTokens": 384000
            }
        ]
    }
]
```

Vysvetlenie dôležitých polí:  

*   `apiKey` – samotný kľúč v súbore **nie je**. VS Code ho uloží  
    do zabezpečeného úložiska a v súbore je len odkaz naň  
    (`${input:…}`). Kľúč preto nikdy nevpisujte priamo do JSON.  
*   `id` – názov modelu presne tak, ako ho očakáva API poskytovateľa.  
*   `toolCalling` – model vie volať nástroje, takže funguje aj  
    v agentskom režime.  
*   `vision` – model nevie spracovať obrázky.  
*   `maxInputTokens`, `maxOutputTokens` – limity kontextu a dĺžky  
    odpovede.  

Po uložení súboru spustite **Developer: Reload Window**. Nové modely sa  
objavia vo výbere modelov v okne chatu. Nezabúdajte, že pri oficiálnom  
API DeepSeeku sa obsah vašich súborov posiela na servery v Číne.  

### Inštrukcie pre AI v projekte  

Asistentom môžete dať trvalé pokyny pre daný projekt – napríklad  
v akom jazyku majú písať komentáre či akú knižnicu používať. Stačí  
vytvoriť v koreni projektu súbor **`AGENTS.md`** (alebo  
`.github/copilot-instructions.md`):  

```markdown
# Pokyny pre AI asistenta

- Komentáre v kóde píš po slovensky.
- Používaj Python 3.12 a knižnicu openai.
- API kľúče načítavaj vždy zo súboru .env.
```

### MCP servery  

Vo VS Code možno AI asistentom pridať ďalšie nástroje cez **Model  
Context Protocol** (MCP), ktorý sme spomínali v kapitole o Anthropic –  
napríklad prístup k databáze, dokumentácii alebo prehliadaču. Servery  
sa pridávajú príkazom **MCP: Add Server** alebo v súbore  
`.vscode/mcp.json`.  

### Zásady rozumného používania  

*   **Kontrolujte každú zmenu.** AI sa mýli, a to často presvedčivo.  
    VS Code zobrazí navrhované zmeny ako rozdiel (*diff*) – prečítajte  
    si ho pred prijatím.  
*   **Nepovoľujte všetko automaticky.** Agent môže spúšťať príkazy  
    v termináli, mazať súbory či inštalovať balíky. Povolenia  
    v režimoch typu *Bypass Approvals* či *Autopilot* používajte len  
    v projektoch, kde škoda nehrozí.  
*   **Pozor na citlivé údaje.** Obsah súborov, s ktorými AI pracuje,  
    sa posiela na servery poskytovateľa.  
*   **Najprv porozumieť, potom generovať.** Pri učení programovania  
    nechajte AI kód **vysvetľovať**, nie len písať. Zadania, pri ktorých  
    nepochopíte vygenerované riešenie, vás nič nenaučia – a riešenie  
    nebudete vedieť obhájiť.  
*   **Rešpektujte pravidlá kurzu.** Pri hodnotených zadaniach zistite,  
    či a ako je používanie AI povolené.  

## Nastavenia a prispôsobenie  

Nastavenia otvoríte skratkou `Ctrl+,`. Do vyhľadávacieho poľa stačí  
napísať názov nastavenia. Užitočné úpravy pre začiatočníkov:  

*   **Auto Save** → `afterDelay` – súbory sa ukladajú automaticky.  
*   **Format On Save** – kód sa pri uložení automaticky upraví  
    (napr. pomocou Ruff).  
*   **Font Size** – veľkosť písma v editore.  
*   **Color Theme** – farebná téma (paleta príkazov →  
    *Preferences: Color Theme*).  

Všetky nastavenia sa ukladajú aj do textového súboru `settings.json`  
(paleta príkazov → *Preferences: Open User Settings (JSON)*):  

```json
{
    "files.autoSave": "afterDelay",
    "editor.fontSize": 15,
    "[python]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "charliermarsh.ruff"
    }
}
```

### Ukážka pokročilejších nastavení  

Nasledujúce nastavenia používa autor kurzu. Nemusíte ich prebrať  
všetky – vyberte si tie, ktoré vám vyhovujú:  

```json
{
    "editor.fontSize": 13,
    "editor.fontFamily": "'JetBrains Mono', Consolas, 'Courier New', monospace",
    "editor.rulers": [80],
    "editor.renderWhitespace": "all",
    "editor.cursorSmoothCaretAnimation": "on",
    "editor.stickyScroll.enabled": false,
    "editor.multiCursorModifier": "ctrlCmd",
    "editor.suggest.insertMode": "replace",
    "editor.occurrencesHighlight": "off",
    "terminal.integrated.defaultProfile.windows": "Command Prompt",
    "terminal.integrated.enableMultiLinePasteWarning": false,
    "workbench.iconTheme": "file-icons",
    "workbench.editor.enablePreview": true,
    "workbench.editor.pinnedTabSizing": "compact",
    "workbench.tree.indent": 12,
    "workbench.tree.renderIndentGuides": "onHover",
    "explorer.autoReveal": true,
    "emmet.triggerExpansionOnTab": true
}
```

| Nastavenie | Význam |
| :--- | :--- |
| `editor.rulers` | Zvislá čiara na 80. stĺpci – pomôcka na dodržanie dĺžky riadkov |
| `editor.renderWhitespace` | Zobrazí medzery a tabulátory ako bodky a šípky |
| `editor.fontFamily` | Písmo editora; *JetBrains Mono* treba najprv nainštalovať do systému |
| `editor.multiCursorModifier` | `ctrlCmd` – kurzory sa pridávajú cez `Ctrl+klik` namiesto `Alt+klik` |
| `editor.suggest.insertMode` | `replace` – zvolený návrh nahradí celé slovo, nielen jeho začiatok |
| `editor.stickyScroll.enabled` | Vypne Sticky Scroll |
| `editor.occurrencesHighlight` | Vypne zvýrazňovanie ostatných výskytov slova pod kurzorom |
| `terminal.integrated.defaultProfile.windows` | Predvolený terminál na Windows |
| `terminal.integrated.enableMultiLinePasteWarning` | Vypne upozornenie pri vložení viacerých riadkov do terminálu |
| `workbench.iconTheme` | Sada ikon súborov (vyžaduje rozšírenie *file-icons*) |
| `workbench.editor.enablePreview` | Jednoklikom otvorený súbor sa zobrazí len ako náhľad (kurzívou), kým ho neupravíte |
| `explorer.autoReveal` | Explorer automaticky označí práve otvorený súbor |
| `workbench.tree.*` | Odsadenie a vodiace čiary v strome súborov |
| `emmet.triggerExpansionOnTab` | Rozbaľovanie skratiek Emmet klávesom `Tab` (pri písaní HTML) |

Ďalšie užitočné funkcie:  

*   **Settings Sync** – po prihlásení cez GitHub alebo Microsoft účet  
    sa nastavenia a rozšírenia synchronizujú medzi počítačmi.  
*   **Profiles** – oddelené sady nastavení a rozšírení, napr. jeden  
    profil pre Python a AI, druhý pre webový vývoj.  

## Vzdialený vývoj  

VS Code dokáže pracovať aj s kódom, ktorý nie je na vašom počítači:  

*   **WSL** – na Windows umožní pracovať v linuxovom prostredí, ktoré  
    je pre mnohé AI nástroje pohodlnejšie.  
*   **Remote – SSH** – práca priamo na vzdialenom serveri, napríklad  
    na školskom alebo cloudovom počítači s výkonnou grafickou kartou.  
*   **Dev Containers** – projekt beží v kontajneri Docker s presne  
    určeným prostredím, ktoré je rovnaké pre všetkých členov tímu.  
*   **vscode.dev** a **GitHub Codespaces** – VS Code priamo v prehliadači,  
    bez inštalácie.  

## Prvý projekt: AI skript krok za krokom  

Spojme všetko dokopy a vytvorme jednoduchý program, ktorý sa pýta  
jazykového modelu. Použijeme OpenRouter z predchádzajúcej kapitoly  
s bezplatným modelom, takže nebudete potrebovať platobnú kartu.  

1.  Vytvorte priečinok `prvy_ai_projekt` a otvorte ho vo VS Code.  
2.  Vytvorte virtuálne prostredie (**Python: Create Environment…**).  
3.  V termináli nainštalujte knižnice:  
    `pip install openai python-dotenv`.  
4.  Na openrouter.ai si vytvorte bezplatný API kľúč.  
5.  Vytvorte súbor `.env` s obsahom:  

    ```
    OPENROUTER_API_KEY=sk-or-...
    ```

6.  Vytvorte súbor `.gitignore` s riadkami `.env` a `.venv/`.  
7.  Vytvorte súbor `hlavny.py` (môžete použiť úryvok `orclient`):  

    ```python
    import os

    from dotenv import load_dotenv
    from openai import OpenAI

    load_dotenv()  # načíta premenné zo súboru .env

    client = OpenAI(
        base_url="https://openrouter.ai/api/v1",
        api_key=os.environ["OPENROUTER_API_KEY"],
    )

    otazka = input("Tvoja otázka: ")

    response = client.chat.completions.create(
        model="openrouter/free",  # náhodný bezplatný model
        messages=[{"role": "user", "content": otazka}],
    )

    print(f"\nModel: {response.model}")
    print(response.choices[0].message.content)
    ```

8.  Spustite program tlačidlom **▶** a v termináli napíšte otázku.  
9.  **Bonus:** Vložte breakpoint na riadok s `print` (`F9`) a spustite  
    program cez `F5`. V paneli **Variables** si prezrite celý objekt  
    `response` – uvidíte aj počet spotrebovaných tokenov (`usage`).  

## Časté problémy  

| Problém | Riešenie |
| :--- | :--- |
| Príkaz `python` alebo `code` sa nenašiel | Python alebo VS Code nie je v PATH; preinštalujte so zaškrtnutím *Add to PATH* a reštartujte terminál |
| `ModuleNotFoundError: No module named 'openai'` | Knižnica je nainštalovaná v inom prostredí; skontrolujte interpreter v stavovom riadku (*Python: Select Interpreter*) |
| Windows nedovolí aktivovať `.venv` | V PowerShelli spustite `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`, alebo prepnite terminál na Command Prompt |
| Notebook nevie nájsť kernel | Nainštalujte `ipykernel` do `.venv` a vpravo hore zvoľte správny kernel |
| `KeyError: 'OPENROUTER_API_KEY'` | Chýba súbor `.env`, je v inom priečinku alebo ste zabudli zavolať `load_dotenv()` |
| Zmeny v kóde sa neprejavili | Súbor nie je uložený – bodka pri názve karty znamená neuložené zmeny |
| Rozšírenie prestalo fungovať | Spustite **Developer: Reload Window**; chybové hlásenia nájdete v paneli **Output** |

## Zhrnutie kapitoly  

*   **VS Code** je bezplatný a najpoužívanejší editor kódu. Pomocou  
    rozšírení sa z neho stane plnohodnotné vývojové prostredie.  
*   Pracuje sa s **priečinkami** – každý projekt má vlastný priečinok.  
*   **Paleta príkazov** (`Ctrl+Shift+P`) sprístupní ktorýkoľvek príkaz.  
*   **Klávesové skratky**, **viac kurzorov** a **stĺpcový výber**  
    výrazne zrýchľujú prácu s textom aj kódom.  
*   Pre Python potrebujeme rozšírenie **Python**, nainštalovaný Python  
    a pre každý projekt **virtuálne prostredie**. Chyby hľadáme  
    pomocou **ladenia** s breakpointmi.  
*   **Jupyter notebooky** sú vhodné na experimenty, **skripty** na hotové  
    programy.  
*   Rozšírenie **REST Client** umožňuje vyskúšať HTTP API vrátane  
    jazykových modelov priamo z editora.  
*   **Git** v pohľade Source Control uchováva históriu zmien. API kľúče  
    a súbory `.env` do neho nikdy nepatria.  
*   **AI asistenti** (Copilot, Claude Code, Codex) pomáhajú dopĺňať,  
    vysvetľovať aj samostatne upravovať kód – ich zmeny však treba vždy  
    kontrolovať. Do chatu možno pridať aj vlastné modely, napr. DeepSeek.  

## Úlohy a otázky  

1.  Nainštalujte VS Code a rozšírenia Python a Jupyter. Vytvorte  
    priečinok s virtuálnym prostredím a overte v stavovom riadku, že ho  
    VS Code používa.  
2.  Pomocou palety príkazov zmeňte farebnú tému a zapnite automatické  
    ukladanie. Koľko krokov ste na to potrebovali?  
3.  Vyriešte cvičenia **Viac kurzorov** a **Stĺpcový výber**. Skúste ich  
    zvládnuť bez myši.  
4.  Vytvorte si vlastný úryvok kódu pre časť programu, ktorú často  
    píšete, a vyskúšajte ho.  
5.  Dokončite projekt *Prvý AI skript*. Spustite ho niekoľkokrát – vráti  
    `openrouter/free` vždy rovnaký model?  
6.  Prepíšte skript tak, aby sa pýtal dvoch rôznych modelov a vypísal  
    obe odpovede pod seba.  
7.  Pošlite rovnakú otázku modelu cez **REST Client** a porovnajte  
    surovú odpoveď API s tým, čo vypisuje váš Python skript. Ktoré  
    údaje skript nevypisuje?  
8.  Vytvorte Jupyter notebook, v ktorom zavoláte model v jednej bunke  
    a odpoveď spracujete v ďalšej (napr. spočítate jej slová).  
9.  Inicializujte v projekte Git repozitár a urobte prvý commit.  
    Skontrolujte, že sa súbor `.env` v zozname zmien **nezobrazuje**.  
10. Požiadajte AI asistenta vo VS Code, aby vám riadok po riadku  
    vysvetlil skript z úlohy 5. Našli ste vo vysvetlení nejakú chybu  
    alebo nepresnosť?  
11. Prečo je nebezpečné povoliť AI agentovi spúšťať akékoľvek príkazy  
    bez potvrdenia? Uveďte aspoň dva konkrétne príklady, čo by sa mohlo  
    pokaziť.  

# Základy AI: GitHub  

*Verzia 1.0 · stav k októbru 2026. Názvy funkcií, ceny a vzhľad webu sa  
menia, vždy ich overte v oficiálnej dokumentácii na docs.github.com.*  

## 1. Prečo GitHub v kurze o AI  

Takmer každý AI projekt, s ktorým sa stretnete, žije na GitHube: ukážkový  
kód k modelom, knižnice ako PyTorch alebo Transformers, návody, datasety,  
nástroje pre agentov aj vaše vlastné zadania. Kto vie GitHub čítať, vie si  
rýchlo zistiť, či je projekt živý, ako ho spustiť a či ho smie použiť.  

GitHub je zároveň miesto, kde sa stretávajú ľudia a AI. Programátori tu  
pracujú spolu s asistentmi ako GitHub Copilot a AI agenti tu sami otvárajú  
úlohy, píšu kód a navrhujú zmeny.  

V tomto dokumente sa naučíte:  

- rozdiel medzi Gitom a GitHubom,  
- základné pojmy (repozitár, commit, vetva, pull request),  
- ako si založiť vlastný repozitár a nahrať doň súbory,  
- ako stiahnuť a posúdiť cudzí AI projekt,  
- ako GitHub súvisí s umelou inteligenciou,  
- čo nikdy nenahrávať na GitHub.  

## 2. Git a GitHub nie sú to isté  

**Git** je program na *správu verzií*. Beží na vašom počítači a pamätá si  
históriu zmien v súboroch: čo sa zmenilo, kedy a kto to urobil. K  
ľubovoľnej staršej verzii sa dá vrátiť.  

**GitHub** je webová služba (od roku 2018 patrí firme Microsoft), ktorá  
uchováva Git repozitáre na internete a pridáva k nim nástroje na  
spoluprácu: diskusie, úlohy, kontrolu kódu, automatizáciu a AI asistentov.  

| | Git | GitHub |  
|---|---|---|  
| **Čo to je** | program | webová služba |  
| **Kde beží** | na vašom počítači | na serveroch GitHubu |  
| **Potrebuje internet** | nie | áno |  
| **Hlavná úloha** | história zmien | zdieľanie a spolupráca |  
| **Alternatívy** | Mercurial, SVN | GitLab, Bitbucket, Codeberg |  

Prirovnanie: Git je ako funkcia „história verzií“ v dokumente, GitHub je ako  
Google Disk, kde dokument zdieľate s ostatnými.  

> **Prečo nestačí priečinok so súbormi `projekt_final_v2_OPRAVENE.zip`?**  
> Lebo pri viacerých ľuďoch a desiatkach zmien rýchlo stratíte prehľad, kto  
> čo zmenil a prečo. Git to sleduje automaticky.  

## 3. Základné pojmy  

| Pojem | Vysvetlenie |  
|-------|-------------|  
| **Repozitár (repo)** | Priečinok projektu spolu s celou históriou zmien. |  
| **Commit** | Uložená „snímka“ zmien s krátkym popisom, napr. „Pridaný prompt pre sumarizáciu“. |  
| **Vetva (branch)** | Samostatná línia vývoja. Hlavná vetva sa zvyčajne volá `main`. |  
| **Clone** | Stiahnutie kópie repozitára z GitHubu do počítača. |  
| **Push** | Odoslanie vašich commitov z počítača na GitHub. |  
| **Pull** | Stiahnutie nových zmien z GitHubu do počítača. |  
| **Fork** | Vlastná kópia cudzieho repozitára pod vaším účtom. |  
| **Pull request (PR)** | Návrh zmeny: „Prosím, zober moje úpravy do svojho projektu.“ |  
| **Issue** | Úloha, chyba alebo otázka k projektu. |  
| **README.md** | Úvodný súbor, ktorý GitHub zobrazí na hlavnej stránke repozitára. |  
| **Star (hviezdička)** | Záložka a zároveň „lajk“. Ukazuje popularitu projektu. |  

### 3.1 Ako vyzerá bežný postup práce  

1. **Zmeníte súbory** vo svojom priečinku.  
2. **Vyberiete zmeny**, ktoré chcete uložiť (`git add`).  
3. **Vytvoríte commit** s popisom, čo ste urobili (`git commit`).  
4. **Odošlete ich** na GitHub (`git push`).  

Pri spolupráci sa pridá ešte jeden krok: zmeny robíte v samostatnej vetve,  
otvoríte pull request a niekto iný ich skontroluje, než sa dostanú do `main`.  

```
 main:   ●────●────●───────────●   ← zlúčenie (merge)
                    \         /
 vetva:              ●───●───●     ← vaša práca, potom pull request
```

## 4. Prvé kroky: účet a vlastný repozitár  

### 4.1 Založenie účtu  

1. Otvorte github.com a kliknite na **Sign up**.  
2. Zvoľte si používateľské meno. Bude súčasťou adries vašich projektov  
   (napr. `github.com/janko-novak`), preto vyberte niečo neutrálne.  
3. Zapnite **dvojfaktorové overenie (2FA)**. GitHub ho vyžaduje od väčšiny  
   používateľov a chráni váš účet aj kód.  
4. Študenti môžu požiadať o **GitHub Education** (Student Developer Pack)  
   so školským e-mailom alebo potvrdením o štúdiu. Zahŕňa bezplatné nástroje  
   a výhody, medzi nimi aj prístup ku GitHub Copilot.  

### 4.2 Vytvorenie repozitára cez web (bez inštalácie)  

1. Vpravo hore kliknite na **+** a zvoľte **New repository**.  
2. Vyplňte názov, napr. `ai-kurz-ulohy`.  
3. Zvoľte viditeľnosť:  
   - **Public** – vidí ho celý svet,  
   - **Private** – vidíte ho len vy a ľudia, ktorých pozvete.  
4. Zaškrtnite **Add a README file**.  
5. Voliteľne pridajte **.gitignore** (šablónu *Python*) a **licenciu**.  
6. Kliknite na **Create repository**.  

Súbory potom nahráte tlačidlom **Add file → Upload files**. Každé nahratie  
je commit, preto doň napíšte zmysluplný popis.  

### 4.3 Práca z počítača (príkazový riadok)  

Ak máte nainštalovaný Git (git-scm.com), základná práca vyzerá takto:  

```bash
# jednorazové nastavenie mena a e-mailu
git config --global user.name "Janko Novák"
git config --global user.email "janko@example.com"

# stiahnutie repozitára
git clone https://github.com/janko-novak/ai-kurz-ulohy.git
cd ai-kurz-ulohy

# po úprave súborov
git status                      # čo sa zmenilo?
git add uloha1.py               # vyber zmeny
git commit -m "Riešenie úlohy 1"
git push                        # odošli na GitHub

# stiahni zmeny, ktoré urobil niekto iný
git pull
```

Ak nechcete príkazový riadok, môžete použiť **GitHub Desktop** alebo Git  
priamo vo **VS Code** (panel *Source Control*). Robia to isté, len cez  
tlačidlá.  

### 4.4 Dobrý popis commitu  

| Zlý popis | Dobrý popis |  
|-----------|-------------|  
| `oprava` | `Opravené načítanie CSV s diakritikou` |  
| `asdf` | `Pridaný systémový prompt pre chatbota` |  
| `zmeny` | `Zvýšená teplota modelu na 0.7 pre kreatívne texty` |  

Popis má odpovedať na otázku: *Čo táto zmena robí?* O pol roka ho budete  
čítať vy alebo váš AI asistent.  

## 5. Ako čítať a posúdiť cudzí AI projekt  

Na GitHube nájdete tisíce AI projektov. Nie všetky sú kvalitné, bezpečné  
alebo udržiavané. Pred použitím si skontrolujte:  

| Čo pozrieť | Kde | Na čo si dať pozor |  
|------------|-----|--------------------|  
| **README** | hlavná stránka | Je jasné, čo projekt robí a ako ho spustiť? |  
| **Posledný commit** | nad zoznamom súborov | Posledná zmena pred 3 rokmi = projekt je pravdepodobne opustený. |  
| **Licencia** | súbor `LICENSE`, pravý panel | Bez licencie projekt formálne **nesmiete** použiť ani upraviť. |  
| **Hviezdičky a forky** | pravý horný roh | Orientačná popularita, nie záruka kvality. Hviezdičky sa dajú aj kúpiť. |  
| **Issues** | záložka *Issues* | Odpovedajú autori? Nie sú tam neriešené bezpečnostné problémy? |  
| **Releases** | pravý panel | Stabilné verzie sú bezpečnejšie ako aktuálny stav vetvy `main`. |  
| **Závislosti** | `requirements.txt`, `pyproject.toml` | Koľko cudzích knižníc projekt potrebuje? |  

### 5.1 Najčastejšie licencie  

| Licencia | Zjednodušene |  
|----------|--------------|  
| **MIT**, **Apache 2.0** | Voľné použitie aj komerčne, treba zachovať meno autora a licenciu. |  
| **GPL** | Môžete použiť, ale odvodené dielo musí mať tiež licenciu GPL. |  
| **CC BY-NC** | Len na nekomerčné účely (častá pri datasetoch a modeloch). |  
| **Vlastné licencie modelov** | Napr. licencie modelov Llama: obmedzenia použitia, treba čítať. |  
| **Žiadna licencia** | Všetky práva vyhradené autorovi. |  

> Licencia kódu a licencia modelu alebo dát môžu byť **rôzne**. Projekt môže  
> mať kód pod MIT, no váhy modelu len na nekomerčné použitie.  

### 5.2 Bezpečnosť pri sťahovaní  

- Kód z internetu je **nedôveryhodný**, kým ho neskontrolujete. Spúšťa sa  
  s vašimi právami a má prístup k vašim súborom.  
- Pozor na falošné kópie populárnych projektov s podobným menom.  
- Nespúšťajte inštalačné skripty (`install.sh`, `curl ... | bash`) bez toho,  
  aby ste vedeli, čo robia.  
- Projekty spúšťajte v **virtuálnom prostredí** Pythonu (`python -m venv`)  
  alebo v kontajneri, nie priamo v systéme.  

## 6. GitHub a umelá inteligencia  

### 6.1 GitHub ako zdroj AI projektov  

Na GitHube nájdete:  

- **knižnice** – PyTorch, TensorFlow, scikit-learn, Hugging Face  
  Transformers, LangChain;  
- **nástroje na spúšťanie modelov lokálne** – Ollama, llama.cpp;  
- **SDK** od poskytovateľov AI (OpenAI, Anthropic, Google) s ukážkami;  
- **návody a kolekcie** – zoznamy typu *awesome-…* (napr. *awesome-llm*),  
  kurzy, Jupyter notebooky;  
- **výskumný kód** k vedeckým článkom (odkaz býva priamo v článku).  

Hľadať môžete cez vyhľadávanie na GitHube alebo cez **Topics**, napr.  
`github.com/topics/llm` či `github.com/topics/machine-learning`.  

**GitHub vs. Hugging Face:** GitHub je určený hlavne pre **kód**. Samotné  
modely (váhy, často desiatky GB) a datasety sa zvyčajne ukladajú na  
**Hugging Face**. Bežný AI projekt má kód na GitHube a model na Hugging Face.  

### 6.2 GitHub ako zdroj dát pre AI  

Verejné repozitáre sú jedným z hlavných zdrojov dát na trénovanie modelov,  
ktoré píšu kód. To otvára otázky, ktoré poznáte z dokumentu o dátach:  
súhlas autorov, licencie a citovanie. Kód, ktorý zverejníte, sa môže dostať  
do trénovacích dát, preto doň nepatria žiadne citlivé údaje.  

### 6.3 GitHub Copilot  

**GitHub Copilot** je AI asistent na programovanie od GitHubu. Funguje vo VS  
Code, JetBrains IDE, na webe GitHubu aj v príkazovom riadku. Na pozadí  
používa jazykové modely viacerých firiem a model si často môžete vybrať.  

Hlavné režimy:  

| Režim | Čo robí |  
|-------|---------|  
| **Dopĺňanie kódu** | Počas písania navrhuje pokračovanie riadku alebo celej funkcie. |  
| **Chat** | Odpovedá na otázky o kóde, vysvetľuje chyby, navrhuje úpravy. |  
| **Agent v editore** | Sám upraví viac súborov, spustí príkazy a testy. |  
| **Coding agent** | Pridelíte mu issue, pracuje na GitHube a výsledok odovzdá ako pull request. |  
| **Code review** | Skontroluje pull request a pridá komentáre. |  

Copilot má bezplatnú verziu s mesačnými limitmi. Študenti so schváleným  
GitHub Education ho zvyčajne dostanú vo vyššej verzii zadarmo. Aktuálne  
plány a limity si overte na github.com/features/copilot.  

### 6.4 AI agenti a pull requesty  

Moderné AI agenti (Copilot, Claude Code, OpenAI Codex a ďalší) dnes bežne  
pracujú priamo s GitHubom: prečítajú issue, vytvoria vetvu, napíšu kód  
a otvoria pull request. Človek potom zmeny skontroluje a rozhodne, či ich  
prijme.  

Pull request je preto dôležitá **kontrolná brána**: AI navrhuje, človek  
schvaľuje. Nikdy nezlučujte zmeny od AI bez toho, aby ste ich prečítali.  

Aby agent vedel, ako s projektom pracovať, pridáva sa do repozitára súbor  
**AGENTS.md** (Claude Code číta **CLAUDE.md**). Viac v samostatnej  
kapitole o súbore AGENTS.md.  

### 6.5 Ďalšie užitočné funkcie  

- **GitHub Codespaces** – vývojové prostredie (VS Code) priamo v  
  prehliadači. Nič neinštalujete, repozitár sa otvorí v cloude. Bezplatný  
  účet má mesačný limit hodín.  
- **GitHub Actions** – automatizácia: pri každom pushi sa môžu spustiť  
  testy, kontrola kódu alebo aj AI kontrola.  
- **GitHub Pages** – bezplatný hosting jednoduchých webových stránok  
  priamo z repozitára, vhodný na portfólio alebo dokumentáciu projektu.  
- **GitHub Models** – možnosť vyskúšať rôzne jazykové modely v  
  prehliadači a volať ich z kódu, vhodné na experimenty.  

## 7. Čo nikdy nedávať na GitHub  

Najčastejšia a najdrahšia chyba začiatočníkov: **API kľúč v kóde**, ktorý  
skončí vo verejnom repozitári. Roboty prehľadávajú GitHub nepretržite a  
uniknutý kľúč dokážu zneužiť v priebehu minút.  

Na GitHub nepatria:  

- API kľúče, heslá, tokeny (súbor `.env`),  
- osobné údaje (mená, e-maily, rodné čísla, zdravotné údaje),  
- dôverné firemné dokumenty a dáta,  
- veľké súbory (modely, datasety nad desiatky MB),  
- priečinky ako `venv/`, `__pycache__/`, `node_modules/`.  

### 7.1 Súbor .gitignore  

Súbor `.gitignore` hovorí Gitu, ktoré súbory má ignorovať. Pre AI projekt v  
Pythone môže vyzerať takto:  

```gitignore
# tajné údaje
.env

# virtuálne prostredie a dočasné súbory
venv/
__pycache__/
.ipynb_checkpoints/

# veľké súbory
models/
data/raw/
*.gguf
*.safetensors
```

Kľúč potom načítate z premennej prostredia, nie priamo z kódu:  

```python
import os
from dotenv import load_dotenv

load_dotenv()                          # načíta .env (ten nie je na GitHube)
api_key = os.environ["OPENAI_API_KEY"]
```

Do repozitára pridajte namiesto toho súbor `.env.example` s prázdnymi  
hodnotami, aby ostatní vedeli, aké premenné potrebujú.  

### 7.2 Čo robiť, keď kľúč unikne  

1. **Okamžite kľúč zrušte** (revoke) u poskytovateľa a vytvorte nový.  
2. Až potom ho odstráňte z kódu.  
3. Pamätajte: zmazanie súboru **nestačí**, kľúč zostáva v histórii Gitu.  
   Preto je jediné bezpečné riešenie zrušiť ho.  

GitHub má funkciu **Secret scanning a Push protection**, ktorá vo verejných  
repozitároch rozpozná známe typy kľúčov a pokus o ich nahratie zablokuje.  
Je to užitočná poistka, nie náhrada za opatrnosť. Podrobnosti nájdete  
v dokumente o API kľúčoch.  

## 8. Praktické cvičenie  

**Cieľ:** vytvoriť si vlastný repozitár pre úlohy z kurzu.  

1. Založte si účet na GitHube a zapnite 2FA.  
2. Vytvorte **súkromný** repozitár `ai-kurz-ulohy` s README a `.gitignore`  
   pre Python.  
3. Upravte README: napíšte, čo repozitár obsahuje (2–3 vety).  
4. Nahrajte jeden svoj prompt alebo skript z predchádzajúcich cvičení.  
5. Pridajte súbor `.env.example` s riadkom `OPENAI_API_KEY=`.  
6. Pozrite si záložku **Commits** a nájdite svoje zmeny.  

**Bonus:**  

- Vyhľadajte na GitHube jeden AI projekt k téme, ktorá vás zaujíma.  
  Podľa tabuľky v kapitole 5 posúďte jeho stav a licenciu (5 viet).  
- Otvorte repozitár v Codespaces a skúste ho spustiť.  
- Ak máte Copilot, požiadajte ho v chate, aby vám vysvetlil jeden súbor  
  projektu. Overte, či jeho vysvetlenie sedí.  

## 9. Zhrnutie  

- **Git** sleduje históriu zmien, **GitHub** ju zdieľa a umožňuje  
  spoluprácu.  
- Základný cyklus: **zmena → add → commit → push**.  
- **Pull request** je miesto, kde človek kontroluje zmeny, aj tie od AI.  
- Pred použitím cudzieho projektu skontrolujte **licenciu, aktivitu  
  a README**.  
- Kód je na GitHube, modely a datasety zvyčajne na **Hugging Face**.  
- **Copilot** a ďalší AI agenti pracujú priamo s repozitármi, výsledok  
  však vždy kontroluje človek.  
- **API kľúče a osobné údaje** nikdy nepatria do repozitára. Používajte  
  `.env` a `.gitignore`.  

## 10. Slovníček  

| Anglicky | Slovensky | Význam |  
|----------|-----------|--------|  
| repository | repozitár | projekt s históriou |  
| commit | commit, záznam | uložená zmena s popisom |  
| branch | vetva | samostatná línia vývoja |  
| merge | zlúčenie | spojenie vetiev |  
| clone | klonovanie | stiahnutie repozitára |  
| fork | fork, odnož | vlastná kópia cudzieho projektu |  
| pull request | žiadosť o zlúčenie | návrh zmien na kontrolu |  
| issue | úloha, problém | záznam o chybe alebo požiadavke |  
| conflict | konflikt | dve zmeny v rovnakom mieste súboru |  
| secret | tajomstvo | kľúč, heslo alebo token |  

## Zdroje  

- Oficiálna dokumentácia: docs.github.com  
- Interaktívne kurzy: skills.github.com  
- Kniha *Pro Git* (zadarmo, aj v češtine): git-scm.com/book  
- GitHub Education: education.github.com  
- Vizuálne precvičenie vetiev: learngitbranching.js.org  

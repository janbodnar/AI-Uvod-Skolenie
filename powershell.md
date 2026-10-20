# PowerShell: jazyk, ktorý volajú AI modely na Windows  

Keď AI agent (GitHub Copilot, Claude Code a podobné nástroje) pracuje  
na Windows, väčšinou nevolá starý `cmd.exe`, ale **PowerShell**.  
Agent ním číta súbory, spúšťa testy, inštaluje balíčky či hľadá chyby.  
Ak mu máte dôverovať a kontrolovať ho, musíte aspoň čítať to, čo napísal.  

Cieľom tejto kapitoly nie je naučiť vás programovať v PowerShelli,  
ale **zoznámiť vás s ním tak, aby ste porozumeli príkazom od AI**  
a vedeli odhaliť rizikové.  

**Po tejto kapitole budete vedieť:**  

* vysvetliť, čím sa PowerShell líši od klasického príkazového riadka  
* prečítať typický príkaz v tvare `Sloveso-Podstatné`  
* používať rúru (pipeline) na spracovanie objektov  
* rozpoznať bezpečné (čítacie) a rizikové (zapisovacie) príkazy  

## Čo je PowerShell  

PowerShell je príkazový riadok a skriptovací jazyk od Microsoftu.  
Na rozdiel od tradičných shellov (`cmd`, `bash`) **prenáša medzi príkazmi  
objekty, nie holý text**. Príkaz nevráti riadky textu, ale objekty  
s vlastnosťami (názov, veľkosť, dátum…), ktoré môžete filtrovať,  
triediť a vyberať.  

| Verzia | Spúšťa sa ako | Poznámka |  
| :--- | :--- | :--- |  
| **Windows PowerShell 5.1** | `powershell` | súčasť Windows, už sa nevyvíja |  
| **PowerShell 7+** | `pwsh` | multiplatformový (Windows, Linux, macOS), aktuálny |  

> ℹ️ AI agent môže bežať v ktorejkoľvek verzii. Ak príkaz zlyhá,  
> skontrolujte `$PSVersionTable.PSVersion` – niektoré novšie funkcie  
> v 5.1 nefungujú.  

## Základná myšlienka: Sloveso-Podstatné  

Príkazy (tzv. **cmdlety**) majú predvídateľný názov `Sloveso-Podstatné`:  

| Cmdlet | Čo robí | Podobný príkaz v bashi |  
| :--- | :--- | :--- |  
| `Get-ChildItem` | vypíše súbory a priečinky | `ls` |  
| `Get-Content` | prečíta súbor | `cat` |  
| `Set-Location` | zmení priečinok | `cd` |  
| `Select-String` | hľadá text | `grep` |  
| `Copy-Item` / `Move-Item` | kopíruje / presúva | `cp` / `mv` |  
| `Remove-Item` | maže | `rm` |  
| `Invoke-WebRequest` | stiahne web alebo súbor | `curl` |  
| `Get-Process` | zoznam procesov | `ps` |  

Mnohé majú aj skrátené aliasy (`ls`, `cat`, `cd`, `gci`, `sls`), takže  
AI niekedy generuje krátky zápis. Plný názov nájdete cez `Get-Alias ls`.  

> 💡 **Tip na učenie:** `Get-Help Get-ChildItem -Examples` ukáže príklady  
> a `Get-Command *process*` nájde príkazy podľa slova.  

## Rúra (pipeline): objekty tečú zľava doprava  

Znak `|` posiela výstup jedného príkazu do ďalšieho. Dôležité je,  
že sa neposielajú riadky textu, ale objekty.  

### Príklad 1: Najväčšie súbory v priečinku  

```powershell
Get-ChildItem -Recurse -File |
    Sort-Object Length -Descending |
    Select-Object -First 5 Name, @{n='MB'; e={[math]::Round($_.Length/1MB, 1)}}
```  

Čo sa deje: vypíšu sa všetky súbory → zoradia podľa veľkosti →  
vyberie sa prvých 5 s názvom a veľkosťou v MB.  
`$_` znamená „aktuálny objekt v rúre".  

### Príklad 2: Ktoré procesy zaberajú najviac pamäte  

```powershell
Get-Process |
    Sort-Object WorkingSet -Descending |
    Select-Object -First 5 Name, Id,
        @{n='MB'; e={[math]::Round($_.WorkingSet/1MB)}}
```  

### Príklad 3: Nájdenie textu v kóde (ako `grep`)  

```powershell
Get-ChildItem -Recurse -Include *.py |
    Select-String -Pattern 'TODO' |
    Select-Object Path, LineNumber, Line
```  

Takto AI agent často hľadá miesta v projekte, ktoré má upraviť.  

### Príklad 4: Hromadné premenovanie súborov  

```powershell
Get-ChildItem *.txt | Rename-Item -NewName { $_.Name -replace '\.txt$', '.md' }
```  

Zo všetkých `.txt` súborov spraví `.md`. Pri takýchto príkazoch sa  
oplatí najprv použiť prepínač `-WhatIf` (pozri nižšie).  

## Premenné, podmienky a cykly  

Premenné začínajú znakom `$`. Syntax pripomína iné jazyky:  

```powershell
$meno = "Jano"
$cisla = 1..5                      # pole 1, 2, 3, 4, 5

foreach ($c in $cisla) {
    if ($c % 2 -eq 0) { "$c je párne" } else { "$c je nepárne" }
}
```  

Porovnávacie operátory sú slovné: `-eq` (rovná sa), `-ne` (nerovná sa),  
`-gt` (väčšie), `-lt` (menšie), `-like` (maska), `-match` (regulárny výraz).  

> ⚠️ Nepíšte `==` ani `>` na porovnanie. V PowerShelli `>` **zapisuje  
> výstup do súboru** a môže ho nechtiac prepísať.  

## Práca s dátami: JSON, CSV a web  

PowerShell vie priamo spracovať štruktúrované formáty, a preto ho AI  
rada používa na rýchle skripty.  

### Príklad 5: Stiahnutie JSON z API a výber polí  

```powershell
$odpoved = Invoke-RestMethod 'https://api.github.com/repos/PowerShell/PowerShell'
$odpoved | Select-Object full_name, stargazers_count, open_issues_count
```  

`Invoke-RestMethod` automaticky premení JSON na objekt, takže sa dá  
pristupovať k vlastnostiam cez bodku (`$odpoved.full_name`).  

### Príklad 6: Súhrn CSV súboru  

```powershell
Import-Csv .\predaj.csv |
    Group-Object Mesto |
    Select-Object Name, Count |
    Sort-Object Count -Descending |
    Export-Csv .\sumar.csv -NoTypeInformation
```  

V štyroch riadkoch: načítať tabuľku, zoskupiť podľa mesta, spočítať  
záznamy a výsledok uložiť. Takéto úlohy AI zvláda výborne.  

### Príklad 7: Vlastná funkcia  

```powershell
function Get-StareSubory {
    param(
        [string]$Cesta = '.',
        [int]$Dni = 90
    )
    Get-ChildItem $Cesta -Recurse -File |
        Where-Object LastWriteTime -lt (Get-Date).AddDays(-$Dni)
}

Get-StareSubory -Cesta C:\Projekty -Dni 180 | Measure-Object Length -Sum
```  

Funkcia nájde súbory nezmenené viac ako zadaný počet dní. Všimnite si  
pomenované parametre (`-Cesta`, `-Dni`) – v PowerShelli sú všade.  

## Bezpečnosť: čo si všimnúť v príkazoch od AI  

Najdôležitejšia zručnosť pri práci s agentom je **vedieť rozlíšiť  
príkaz, ktorý len číta, od príkazu, ktorý mení systém**.  

| Zvyčajne bezpečné (čítanie) | Pozor (zápis, mazanie, sieť) |  
| :--- | :--- |  
| `Get-ChildItem`, `Get-Content` | `Remove-Item -Recurse -Force` |  
| `Select-String`, `Get-Process` | `Set-Content`, `Out-File`, `>` (prepisujú súbory) |  
| `Get-Help`, `Get-Command` | `Stop-Process`, `Restart-Computer` |  
| `Test-Path`, `Measure-Object` | `Invoke-Expression` (`iex`) – vykoná text ako kód |  
| | `Invoke-WebRequest … \| iex` – stiahne a spustí cudzí kód |  
| | `Set-ExecutionPolicy Bypass`, zásahy do registrov a služieb |  

### Poistky, ktoré treba poznať  

* **`-WhatIf`** – ukáže, čo by sa stalo, ale nič nevykoná.  
* **`-Confirm`** – pred každou akciou sa opýta.  
* **`Get-Content` pred zmenou** – pozrite si, čo sa bude meniť.  

```powershell
# Najprv "nanečisto":
Get-ChildItem .\logs -Filter *.log |
    Where-Object LastWriteTime -lt (Get-Date).AddDays(-30) |
    Remove-Item -WhatIf
```  

Až keď výpis vyzerá správne, `-WhatIf` odstránite.  

> ⚠️ **Zlaté pravidlá pre prácu s agentom**  
>  
> * Nepovoľujte automatické spúšťanie príkazov bez kontroly, ak ide  
>   o mazanie, sieť alebo systémové nastavenia.  
> * Podozrivé sú príkazy, ktoré niečo stiahnu a hneď spustia.  
> * Agent by mal pracovať v projektovom priečinku, nie v koreni disku.  
> * Dôležité dáta majte zálohované alebo vo verzionovaní (Git).  

## Úskalia, na ktoré narazíte  

* **Politika spúšťania skriptov (Execution Policy):** môže blokovať  
  spúšťanie `.ps1` súborov. Je to ochrana pred omylom, nie plnohodnotné  
  bezpečnostné opatrenie.  
* **Uvodzovky:** `'text'` je doslovný reťazec, `"text $premenna"` dosadí  
  hodnotu premennej. Častý zdroj chýb v AI generovanom kóde.  
* **Cesty:** Windows používa spätné lomky (`C:\Projekty`), ale PowerShell  
  7 zvládne aj bežné lomky. Medzery v cestách treba dať do úvodzoviek.  
* **Kódovanie:** Windows PowerShell 5.1 a PowerShell 7 majú iné  
  predvolené kódovanie súborov, čo pri slovenských znakoch (č, š, ž)  
  môže pokaziť diakritiku. Použite `-Encoding utf8`.  
* **Rozdiely medzi shellmi:** AI niekedy napíše bashový príkaz  
  (napr. `export`, `&&` v starej verzii) do PowerShellu. Pomôže pripomenúť  
  jej, že cieľom je PowerShell.  

## Ako PowerShell využiť s AI  

Dobrý prompt povie modelu **prostredie aj cieľ**:  

> „Som na Windows 11, používam PowerShell 7. Napíš príkaz, ktorý nájde  
> v priečinku `C:\Projekty` všetky súbory `.log` staršie ako 30 dní  
> a **najprv len vypíše**, čo by zmazal."  

Odporúčaný postup:  

1.  Požiadajte AI o skript a **vysvetlenie riadok po riadku**.  
2.  Spustite najprv čítaciu alebo `-WhatIf` verziu.  
3.  Skontrolujte výstup a až potom spustite ostrú verziu.  
4.  Overený skript uložte (`.ps1`) a znovu používajte.  

## Zhrnutie kapitoly  

*   **PowerShell** je shell a jazyk, ktorý AI agenti na Windows bežne volajú.  
*   Príkazy majú tvar **Sloveso-Podstatné** (`Get-ChildItem`, `Remove-Item`).  
*   Rúra `|` posiela **objekty**, nie text, preto sa dá ľahko filtrovať  
    (`Where-Object`), triediť (`Sort-Object`) a vyberať (`Select-Object`).  
*   `Invoke-RestMethod`, `Import-Csv` a `ConvertFrom-Json` uľahčujú prácu  
    s API a dátami.  
*   Naučte sa rozlišovať **čítacie** a **rizikové** príkazy; využívajte  
    `-WhatIf` a `-Confirm`.  
*   Zvlášť sa vyhýbajte slepému spúšťaniu `Invoke-Expression`  
    a sťahovaniu kódu s okamžitým spustením.  

## Otázky a cvičenia  

1.  Čo spraví príkaz `Get-Process | Where-Object CPU -gt 100`?  
    Je bezpečný? Prečo?  
2.  Vysvetlite, prečo je `Remove-Item * -Recurse -Force` v rukách AI  
    agenta rizikový a ako by ste ho obmedzili.  
3.  Požiadajte AI o skript, ktorý spočíta súbory podľa prípony  
    v priečinku. Prečítajte ho a vysvetlite každý riadok.  
4.  Prepíšte príklad 4 tak, aby nič nepremenoval, len vypísal návrh  
    (nápoveda: `-WhatIf`).  

## Zdroje  

* [Dokumentácia PowerShell (Microsoft Learn)](https://learn.microsoft.com/en-us/powershell/)  
* [Get-Help a dokumentácia cmdletov](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-help)  

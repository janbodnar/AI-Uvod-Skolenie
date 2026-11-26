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
* spustiť krátke ukážky príkazov, vhodné na prezentáciu  
* napísať a spustiť jednoduchý skript `.ps1` s parametrami  

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

## Rýchle ukážky na prezentáciu  

Krátke príkazy sú najlepší spôsob, ako študentom ukázať, čo PowerShell dokáže.  
Každý funguje samostatne – stačí ho skopírovať do terminálu. Text za znakom  
`#` je komentár, PowerShell ho ignoruje.  

> 💡 **Tip pre lektora:** ukážky spúšťajte v PowerShelli 7 vo Windows Terminal  
> – správne zobrazí diakritiku aj emoji. Písmo zväčšíte klávesmi `Ctrl` + `+`  
> a obrazovku vyčistíte príkazom `cls`. Príkaz `Start-Transcript .\kurz.txt`  
> zaznamená celé sedenie do súboru, ktorý potom môžete poslať študentom  
> (záznam ukončí `Stop-Transcript`).  

### PowerShell ako kalkulačka a kalendár  

```powershell
2 + 3 * 4                              # 14 – platí prednosť operácií
10GB / 1MB                             # 10240 – pozná jednotky KB, MB, GB, TB
[math]::Sqrt(144)                      # 12
[math]::Round(22 / 7, 3)               # zaokrúhli na 3 desatinné miesta
Get-Date -Format 'dd.MM.yyyy HH:mm'    # aktuálny dátum a čas
(Get-Date).AddDays(100)                # aký dátum bude o 100 dní
(Get-Date '1995-05-17').DayOfWeek      # v aký deň ste sa narodili?
((Get-Date -Month 12 -Day 24) - (Get-Date)).Days   # koľko dní do Vianoc
```  

### Informácie o počítači  

```powershell
$env:USERNAME                          # prihlásený používateľ
$env:COMPUTERNAME                      # názov počítača
$PSVersionTable.PSVersion              # verzia PowerShellu
Get-Uptime                             # ako dlho beží počítač (PS 7)
(Get-Process).Count                    # koľko procesov práve beží
Get-PSDrive C                          # obsadené a voľné miesto na disku C
Get-CimInstance Win32_OperatingSystem | Select-Object Caption, Version

# 5 procesov, ktoré najviac zaťažujú procesor
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5 Name, CPU
```  

### Súbory a priečinky  

```powershell
Test-Path C:\Projekty                  # existuje priečinok? True/False
(Get-Content .\poznamky.txt).Count     # počet riadkov v súbore
Get-FileHash .\instalator.exe          # kontrolný súčet (SHA256)
Invoke-Item .                          # otvorí priečinok v Prieskumníkovi

# koľko GB zaberajú Stiahnuté súbory
(Get-ChildItem ~\Downloads -Recurse -File | Measure-Object Length -Sum).Sum/1GB

# ktoré typy súborov máte v Dokumentoch najčastejšie
Get-ChildItem ~\Documents -Recurse -File | Group-Object Extension |
    Sort-Object Count -Descending | Select-Object -First 5 Count, Name
```  

### Práca s textom  

```powershell
'Ahoj svet'.ToUpper()                  # AHOJ SVET
'Ahoj svet'.Length                     # 9 znakov
'jablko,hruška,slivka' -split ','      # rozdelí text na zoznam
'Bratislava' -like 'Brat*'             # True – porovnanie s maskou
'Ahoj! ' * 3                           # Ahoj! Ahoj! Ahoj!
'Volajte 0905 123 456' -match '\d{4} \d{3} \d{3}'   # True
$Matches[0]                            # 0905 123 456 – nájdený text
'Text pre schránku' | Set-Clipboard    # skopíruje text do schránky
Get-Clipboard                          # vypíše obsah schránky
```  

### Web a sieť  

```powershell
Invoke-RestMethod 'https://wttr.in/Bratislava?format=3'   # počasie
Invoke-RestMethod 'https://api.ipify.org'   # vaša verejná IP adresa
Test-Connection google.com -Count 2         # ping – odpovedá server?
Start-Process 'https://learn.microsoft.com/powershell'   # otvorí prehliadač

# údaje o projekte z GitHubu – JSON sa automaticky zmení na objekt
$repo = Invoke-RestMethod 'https://api.github.com/repos/microsoft/vscode'
$repo.stargazers_count                 # počet hviezdičiek
```  

### Zábavné ukážky  

```powershell
1..49 | Get-Random -Count 6 | Sort-Object    # tip na lotériu 6 z 49
'kameň', 'papier', 'nožnice' | Get-Random    # hra proti počítaču
Get-Random -Minimum 1 -Maximum 7       # hod kockou (Maximum sa nepočíta)
[guid]::NewGuid()                      # jedinečný identifikátor
Get-Process | Out-GridView             # tabuľka v okne s filtrom
Get-Process | Select-Object -First 3 Name, Id | ConvertTo-Json

# náhodné heslo zo 16 znakov (len na ukážku, heslá patria do správcu hesiel)
-join ((33..126) | Get-Random -Count 16 | ForEach-Object { [char]$_ })

# počítač prehovorí (anglickým hlasom, ak nemáte slovenský)
(New-Object -ComObject SAPI.SpVoice).Speak('Hello, students!')
```  

Pri každej ukážke sa oplatí opýtať študentov: **Je tento príkaz čítací, alebo  
niečo mení?** Väčšina ukážok len číta. Výnimkou sú `Set-Clipboard`,  
`Start-Process` a `Invoke-Item`, ktoré niečo zmenia alebo spustia.  

> 💡 **Ukážka s AI:** skopírujte ktorýkoľvek príkaz do chatu s promptom  
> „Vysvetli tento PowerShell príkaz po častiach." Študenti tak vidia, že AI  
> vie kód nielen písať, ale aj vysvetľovať.  

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

## Písanie skriptov  

Keď sa príkaz osvedčí, oplatí sa ho uložiť do **skriptu** – textového súboru  
s príponou `.ps1`. Skript môžete spúšťať opakovane, s rôznymi parametrami,  
a zdieľať ho s kolegami. Práve skripty dostanete od AI agentov najčastejšie.  

### Ako vytvoriť a spustiť skript  

1.  Vytvorte súbor, napr. `Ahoj.ps1`. Najvhodnejší je **VS Code** s rozšírením  
    PowerShell – farebne zvýrazní syntax a upozorní na chyby.  
2.  V PowerShelli prejdite do priečinka so skriptom a spustite ho:  
    `.\Ahoj.ps1`. Predpona `.\` je povinná – PowerShell z bezpečnostných  
    dôvodov nespustí skript z aktuálneho priečinka len podľa názvu.  
3.  Ak Windows spúšťanie skriptov zablokuje, povoľte vlastné skripty pre svoj  
    účet:  

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```  

Nastavenie `RemoteSigned` spúšťa vaše vlastné skripty, no skripty stiahnuté  
z internetu musia byť podpísané. Stiahnutý skript odblokujete príkazom  
`Unblock-File` – ale **až keď ste si ho prečítali**. Nastavenie `Bypass`  
(pozri tabuľku rizík nižšie) vypína aj túto kontrolu.  

> ⚠️ **Diakritika v skriptoch:** Windows PowerShell 5.1 číta skripty bez  
> značky BOM v starom kódovaní a slovenské znaky pokazí. Ukladajte skripty  
> v kódovaní **UTF-8 with BOM** (vo VS Code ho zmeníte vpravo dole v stavovom  
> riadku). PowerShell 7 tento problém nemá.  

### Štruktúra skriptu  

Dobrý skript má tri časti: **nápovedu** (komentár na začiatku), **parametre**  
(blok `param`) a samotnú logiku.  

```powershell
<#
.SYNOPSIS
    Pozdraví používateľa podľa dennej doby.
.EXAMPLE
    .\Ahoj.ps1 -Meno Jana
#>
param(
    [string]$Meno = $env:USERNAME   # predvolená hodnota, ak parameter chýba
)

$hodina = (Get-Date).Hour

if ($hodina -lt 10)     { $pozdrav = 'Dobré ráno' }
elseif ($hodina -lt 18) { $pozdrav = 'Dobrý deň' }
else                    { $pozdrav = 'Dobrý večer' }

Write-Host "$pozdrav, $Meno!" -ForegroundColor Green
"Dnes je $((Get-Date).ToString('dddd d. MMMM yyyy'))."
```  

Skript spustíte ako `.\Ahoj.ps1` alebo `.\Ahoj.ps1 -Meno Jana`. Vďaka nápovede  
funguje aj `Get-Help .\Ahoj.ps1 -Examples` – rovnako ako pri vstavaných  
cmdletoch. `Write-Host` iba vypíše farebný text na obrazovku. Reťazec na  
poslednom riadku je **výstup** skriptu, ktorý sa dá poslať rúrou ďalej.  

> 💡 **Prompt pre AI:** „Napíš PowerShell skript s nápovedou (comment-based  
> help), parametrami s predvolenými hodnotami a ošetrením chýb. Potom vysvetli  
> každý riadok."  

Nasledujúce skripty sú pripravené na ukážku na kurze. Všetky len čítajú údaje  
alebo vytvárajú nové súbory – nič nemažú ani neprepisujú.  

### Skript 1: Najväčšie súbory na disku  

Keď dochádza miesto na disku, prvá otázka znie: čo ho zaberá?  

```powershell
<#
.SYNOPSIS
    Nájde najväčšie súbory v zadanom priečinku.
.EXAMPLE
    .\Najdi-VelkeSubory.ps1 -Cesta D:\ -MinMB 500 -Pocet 20
#>
param(
    [string]$Cesta = $HOME,   # kde hľadať (predvolene domovský priečinok)
    [int]$MinMB = 100,        # minimálna veľkosť v MB
    [int]$Pocet = 10          # koľko súborov vypísať
)

Write-Host "Hľadám súbory nad $MinMB MB v $Cesta ..." -ForegroundColor Cyan

$subory = Get-ChildItem $Cesta -File -Recurse -ErrorAction SilentlyContinue |
    Where-Object Length -gt ($MinMB * 1MB) |
    Sort-Object Length -Descending |
    Select-Object -First $Pocet

if (-not $subory) {
    Write-Host 'Nenašiel som žiadne také veľké súbory.'
    return
}

$subory | Select-Object @{n='MB'; e={[math]::Round($_.Length / 1MB)}},
    @{n='Zmenený'; e={$_.LastWriteTime.ToString('d.M.yyyy')}},
    FullName |
    Format-Table -AutoSize

$spolu = ($subory | Measure-Object Length -Sum).Sum / 1GB
Write-Host ('Spolu: {0:N1} GB' -f $spolu) -ForegroundColor Yellow
```  

Spustenie: `.\Najdi-VelkeSubory.ps1 -Cesta C:\Users -MinMB 500`. Prepínač  
`-ErrorAction SilentlyContinue` potlačí chyby pri priečinkoch, kam nemáte  
prístup – bez neho by výstup zaplavili červené hlásenia. Hľadanie na celom  
disku môže trvať aj niekoľko minút.  

### Skript 2: Informácie o operačnom systéme  

Skript zhrnie na jednu obrazovku to, čo by ste inak hľadali v niekoľkých  
oknách nastavení.  

```powershell
# Info-System.ps1 – prehľad o počítači
$os  = Get-CimInstance Win32_OperatingSystem
$cpu = Get-CimInstance Win32_Processor | Select-Object -First 1
$pc  = Get-CimInstance Win32_ComputerSystem
$beh = (Get-Date) - $os.LastBootUpTime

Write-Host "`n=== Systém ===" -ForegroundColor Cyan
[pscustomobject]@{
    'Počítač'        = $env:COMPUTERNAME
    'Používateľ'     = $env:USERNAME
    'Systém'         = $os.Caption
    'Verzia'         = $os.Version
    'Procesor'       = $cpu.Name.Trim()
    'Jadrá'          = $cpu.NumberOfLogicalProcessors
    'RAM (GB)'       = [math]::Round($pc.TotalPhysicalMemory / 1GB, 1)
    'Voľná RAM (GB)' = [math]::Round($os.FreePhysicalMemory / 1MB, 1)  # v KB
    'Zapnutý'        = '{0} d {1} h {2} min' -f $beh.Days, $beh.Hours,
                       $beh.Minutes
    'PowerShell'     = $PSVersionTable.PSVersion.ToString()
} | Format-List

Write-Host '=== Disky ===' -ForegroundColor Cyan
Get-PSDrive -PSProvider FileSystem | Where-Object Used -gt 0 |
    Select-Object Name,
        @{n='Obsadené (GB)'; e={[math]::Round($_.Used / 1GB, 1)}},
        @{n='Voľné (GB)'; e={[math]::Round($_.Free / 1GB, 1)}},
        @{n='Voľné %'; e={[math]::Round(100 * $_.Free / ($_.Used + $_.Free))}} |
    Format-Table -AutoSize

Write-Host '=== Sieť ===' -ForegroundColor Cyan
Get-NetIPAddress -AddressFamily IPv4 |
    Where-Object InterfaceAlias -notlike '*Loopback*' |
    Select-Object InterfaceAlias, IPAddress |
    Format-Table -AutoSize
```  

`Get-CimInstance` číta údaje zo správy systému Windows (CIM/WMI) – z rovnakého  
zdroja čerpajú aj nástroje správcov. Triedy ako `Win32_OperatingSystem` či  
`Win32_Processor` existujú len vo Windows, preto skript na Linuxe ani macOS  
nefunguje.  

### Skript 3: Počasie v Bratislave  

Najrýchlejšia cesta je služba **wttr.in**, ktorá vracia počasie priamo ako  
text:  

```powershell
Invoke-RestMethod 'https://wttr.in/Bratislava?format=3'      # jeden riadok
Invoke-RestMethod 'https://wttr.in/Bratislava?0&T&lang=sk'   # obrázok z textu
```  

Pre vlastný skript je lepšie bezplatné API **Open-Meteo**. Nepotrebuje  
registráciu ani API kľúč a vracia JSON, z ktorého `Invoke-RestMethod` urobí  
objekt.  

```powershell
<#
.SYNOPSIS
    Zobrazí aktuálne počasie a predpoveď (zdroj: Open-Meteo, bez API kľúča).
.EXAMPLE
    .\Pocasie.ps1 -Mesto Košice -Lat 48.72 -Lon 21.26 -Dni 5
#>
param(
    [string]$Mesto = 'Bratislava',
    [string]$Lat = '48.15',        # zemepisná šírka
    [string]$Lon = '17.11',        # zemepisná dĺžka
    [int]$Dni = 3                  # počet dní predpovede (1 – 16)
)

function Get-PopisPocasia([int]$Kod) {
    # medzinárodné kódy počasia WMO
    switch ($Kod) {
        0                 { 'jasno' }
        { $_ -in 1, 2 }   { 'polojasno' }
        3                 { 'zamračené' }
        { $_ -in 45, 48 } { 'hmla' }
        { $_ -in 51..57 } { 'mrholenie' }
        { $_ -in 61..67 } { 'dážď' }
        { $_ -in 71..77 } { 'sneženie' }
        { $_ -in 80..82 } { 'prehánky' }
        { $_ -in 85, 86 } { 'snehové prehánky' }
        { $_ -ge 95 }     { 'búrka' }
        default           { "kód $Kod" }
    }
}

$url = 'https://api.open-meteo.com/v1/forecast'
$parametre = @{
    latitude      = $Lat
    longitude     = $Lon
    current       = 'temperature_2m,relative_humidity_2m,' +
                    'wind_speed_10m,weather_code'
    daily         = 'weather_code,temperature_2m_min,temperature_2m_max,' +
                    'precipitation_probability_max'
    timezone      = 'Europe/Bratislava'
    forecast_days = $Dni
}

try {
    $p = Invoke-RestMethod -Uri $url -Body $parametre -ErrorAction Stop
} catch {
    Write-Warning "Počasie sa nepodarilo načítať: $($_.Exception.Message)"
    return
}

$t = $p.current
Write-Host "`nPočasie – $Mesto" -ForegroundColor Cyan
'Teraz: {0} °C, {1}, vlhkosť {2} %, vietor {3} km/h' -f $t.temperature_2m,
    (Get-PopisPocasia $t.weather_code), $t.relative_humidity_2m,
    $t.wind_speed_10m

$d = $p.daily
0..($d.time.Count - 1) | ForEach-Object {
    [pscustomobject]@{
        'Deň'      = ([datetime]$d.time[$_]).ToString('ddd d.M.')
        'Počasie'  = Get-PopisPocasia ($d.weather_code[$_])
        'Min °C'   = $d.temperature_2m_min[$_]
        'Max °C'   = $d.temperature_2m_max[$_]
        'Zrážky %' = $d.precipitation_probability_max[$_]
    }
} | Format-Table -AutoSize
```  

Na skripte vidno tri užitočné techniky:  

* **hašovacia tabuľka** `@{ … }` s parametrami – pri požiadavke typu GET z nej  
  `Invoke-RestMethod` sám zostaví adresu s parametrami;  
* **`try` / `catch`** – keď nefunguje internet, skript vypíše zrozumiteľné  
  upozornenie namiesto červenej chyby;  
* **vlastná funkcia** `Get-PopisPocasia` prekladá číselné kódy počasia na  
  slová.  

Pre iné mesto stačí zmeniť súradnice: `.\Pocasie.ps1 -Mesto Košice -Lat 48.72  
-Lon 21.26`.  

### Skript 4: Najnovšie správy z internetu  

Spravodajské weby zverejňujú prehľad článkov vo formáte **RSS** (XML).  
`Invoke-RestMethod` ho rozpozná a vráti rovno zoznam článkov. Skript používa  
slovenskú verziu Google News, ale funguje s RSS kanálom akéhokoľvek webu.  

```powershell
<#
.SYNOPSIS
    Vypíše najnovšie správy z Google News (RSS).
.EXAMPLE
    .\Spravy.ps1 -Hladat 'umelá inteligencia' -Pocet 5
#>
param(
    [string]$Hladat,          # voliteľné hľadané slovo
    [int]$Pocet = 10,
    [switch]$Otvorit          # otvorí prvý článok v prehliadači
)

$jazyk = 'hl=sk&gl=SK&ceid=SK:sk'
if ($Hladat) {
    $q = [uri]::EscapeDataString($Hladat)
    $url = "https://news.google.com/rss/search?q=$q&$jazyk"
} else {
    $url = "https://news.google.com/rss?$jazyk"
}

$clanky = @(Invoke-RestMethod $url | Select-Object -First $Pocet)

$clanky | ForEach-Object {
    [pscustomobject]@{
        'Čas'     = ([datetime]$_.pubDate).ToString('d.M. HH:mm')
        'Titulok' = $_.title
    }
} | Format-Table -Wrap

if ($Otvorit -and $clanky) { Start-Process $clanky[0].link }
```  

Spustenie: `.\Spravy.ps1` vypíše hlavné správy, `.\Spravy.ps1 -Hladat Slovan  
-Otvorit` vyhľadá články a prvý otvorí. Prepínač `[switch]` je parameter bez  
hodnoty – buď ho zadáte, alebo nie. `[uri]::EscapeDataString` upraví text  
s medzerami a diakritikou tak, aby sa dal vložiť do webovej adresy.  

### Skript 5: Kurzy mien z Európskej centrálnej banky  

ECB zverejňuje každý pracovný deň referenčné kurzy eura ako XML súbor.  
PowerShell s XML pracuje rovnako pohodlne ako s JSON.  

```powershell
# Kurzy.ps1 – prepočet eur podľa aktuálnych kurzov ECB
param(
    [double]$Suma = 100,
    [string[]]$Meny = @('USD', 'CZK', 'HUF', 'PLN', 'GBP')
)

$url = 'https://www.ecb.europa.eu/stats/eurofxref/eurofxref-daily.xml'
$xml = Invoke-RestMethod $url
$den = $xml.Envelope.Cube.Cube

Write-Host "Kurzy ECB k $($den.time) – $Suma EUR je:" -ForegroundColor Cyan
$den.Cube | Where-Object currency -in $Meny | ForEach-Object {
    [pscustomobject]@{
        'Mena'  = $_.currency
        'Kurz'  = [double]$_.rate
        'Suma'  = [math]::Round($Suma * [double]$_.rate, 2)
    }
} | Format-Table -AutoSize
```  

Spustenie: `.\Kurzy.ps1 -Suma 250 -Meny USD, CZK`. Parameter typu `[string[]]`  
prijme viac hodnôt oddelených čiarkou.  

### Skript 6: Správa o počítači v HTML  

Výstup nemusí zostať v termináli. `ConvertTo-Html` premení objekty na webovú  
stránku – hotová správa sa dá poslať e-mailom alebo vytlačiť.  

```powershell
# Sprava-Pocitac.ps1 – vytvorí HTML správu a otvorí ju v prehliadači
$plocha = [Environment]::GetFolderPath('Desktop')
$subor  = Join-Path $plocha ('sprava_{0:yyyy-MM-dd_HHmm}.html' -f (Get-Date))
$os     = Get-CimInstance Win32_OperatingSystem

$procesy = Get-Process |
    Sort-Object WorkingSet -Descending |
    Select-Object -First 10 Name, Id,
        @{n='Pamäť (MB)'; e={[math]::Round($_.WorkingSet / 1MB)}} |
    ConvertTo-Html -Fragment -PreContent '<h2>Procesy podľa pamäte</h2>'

$disky = Get-PSDrive -PSProvider FileSystem | Where-Object Used -gt 0 |
    Select-Object Name,
        @{n='Voľné (GB)'; e={[math]::Round($_.Free / 1GB, 1)}},
        @{n='Spolu (GB)'; e={[math]::Round(($_.Used + $_.Free) / 1GB, 1)}} |
    ConvertTo-Html -Fragment -PreContent '<h2>Disky</h2>'

$hlava = @'
<meta charset="utf-8">
<title>Správa o počítači</title>
<style>
  body   { font-family: Segoe UI, sans-serif; margin: 2em; }
  table  { border-collapse: collapse; }
  th, td { border: 1px solid #ccc; padding: 4px 10px; }
  th     { background: #e8f0fe; }
</style>
'@

$cas  = Get-Date -Format 'd.M.yyyy HH:mm'
$telo = "<h1>Správa o počítači $env:COMPUTERNAME</h1>" +
        "<p>$($os.Caption), vytvorené $cas</p>" +
        $procesy + $disky

ConvertTo-Html -Head $hlava -Body $telo | Out-File $subor -Encoding utf8
Invoke-Item $subor
Write-Host "Správa uložená: $subor" -ForegroundColor Green
```  

Text medzi `@'` a `'@` je **viacriadkový reťazec** (here-string) – hodí sa na  
HTML, CSS či šablóny e-mailov. Prepínač `-Fragment` vytvorí len tabuľku, nie  
celú stránku, takže sa dá viac tabuliek spojiť do jednej správy.  

### Skript 7: Záloha priečinka do ZIP  

```powershell
<#
.SYNOPSIS
    Zabalí priečinok do ZIP archívu s dátumom v názve.
.EXAMPLE
    .\Zaloha.ps1 -Zdroj C:\Projekty\web
#>
param(
    [Parameter(Mandatory)]
    [string]$Zdroj,                       # čo zálohovať (povinné)
    [string]$Ciel = "$HOME\Zalohy"        # kam uložiť archív
)

New-Item -ItemType Directory -Path $Ciel -Force | Out-Null

$nazov = '{0}_{1:yyyy-MM-dd_HHmm}.zip' -f (Split-Path $Zdroj -Leaf), (Get-Date)
$zip   = Join-Path $Ciel $nazov

Compress-Archive -Path (Join-Path $Zdroj '*') -DestinationPath $zip
$mb = [math]::Round((Get-Item $zip).Length / 1MB, 1)
Write-Host "Hotovo: $zip ($mb MB)" -ForegroundColor Green
```  

Atribút `[Parameter(Mandatory)]` robí parameter povinným – ak ho nezadáte,  
PowerShell sa naň opýta. Vďaka dátumu v názve sa staršie zálohy neprepíšu.  
Windows PowerShell 5.1 zvládne pomocou `Compress-Archive` súbory len do  
veľkosti 2 GB.  

> 💡 **Automatické spúšťanie:** skript sa dá spúšťať aj pravidelne cez  
> **Plánovač úloh** (Task Scheduler) – napríklad každý večer zálohovať projekt  
> alebo ráno vytvoriť správu o počasí. Naplánovaná úloha je však zásah do  
> systému, ktorý by AI agent nemal urobiť bez vášho výslovného súhlasu.  

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
*   Krátke ukážky – kalkulačka, dátum, údaje o počítači, počasie či náhodné  
    čísla – sú dobrý spôsob, ako PowerShell predstaviť študentom.  
*   Skript `.ps1` má **nápovedu, parametre a logiku**; spúšťa sa ako  
    `.\skript.ps1` a pri 5.1 ho treba uložiť v UTF-8 s BOM.  
*   Cez `Invoke-RestMethod` získa skript údaje z webu – počasie, správy či  
    kurzy mien – často bez API kľúča.  

## Otázky a cvičenia  

1.  Čo spraví príkaz `Get-Process | Where-Object CPU -gt 100`?  
    Je bezpečný? Prečo?  
2.  Vysvetlite, prečo je `Remove-Item * -Recurse -Force` v rukách AI  
    agenta rizikový a ako by ste ho obmedzili.  
3.  Požiadajte AI o skript, ktorý spočíta súbory podľa prípony  
    v priečinku. Prečítajte ho a vysvetlite každý riadok.  
4.  Prepíšte príklad 4 tak, aby nič nepremenoval, len vypísal návrh  
    (nápoveda: `-WhatIf`).  
5.  Upravte skript `Pocasie.ps1` tak, aby zobrazil predpoveď pre Košice na  
    7 dní.  
6.  Spustite `Spravy.ps1` s parametrom `-Hladat` a vlastným slovom. Ktorý  
    riadok skriptu sťahuje údaje z internetu?  
7.  Požiadajte AI, aby skript `Info-System.ps1` rozšírila o zoznam  
    nainštalovaných programov. Skontrolujte, či nový kód len číta, alebo aj  
    niečo mení.  
8.  Vyberte tri ukážky z časti Rýchle ukážky a pri každej určte, či je  
    čítacia, alebo riziková.  

## Zdroje  

* [Dokumentácia PowerShell (Microsoft Learn)](https://learn.microsoft.com/en-us/powershell/)  
* [Get-Help a dokumentácia cmdletov](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-help)  
* [about_Scripts – písanie a spúšťanie skriptov](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_scripts)  
* [Open-Meteo – bezplatné API počasia](https://open-meteo.com/en/docs)  
* [wttr.in – počasie v termináli](https://github.com/chubin/wttr.in)

[Co dodělat ]: #
[pojmy ]: #

# Výběr řídící jednotky pro různé aplikace


$${\color{#FFA500}E9 \space \color{#4682B4}A1 }$$

## Cíle

- **Orientovat se** v základních typech a architekturách řídicích jednotek (MCU, MPU, embedded systémy, PLC, iPC, programovatelná relé).
- **Rozlišovat klíčové technické parametry** (výpočetní výkon vs. spotřeba, typy a velikosti pamětí RAM/Flash/EEPROM, determinismus a reakční doba v reálném čase).
- **Zhodnotit provozní odolnost a robustnost** hardwaru (krytí IP, teplotní rozsah, vibrace, rušení EMC, srovnání spotřební vs. průmyslové techniky).
- **Navrhnout a technicko-ekonomicky obhájit** optimální řídicí jednotku pro konkrétní praktickou aplikaci podle I/O bilance, rozhraní a prostředí.

## Ověření cílů

Výběr řídící jednotky pro různé aplikace

1. Příklady řídících jednotek 
2. Jejich základní vlastnosti z hlediska výpočetního výkonu a velikosti paměťového prostoru
3. A z hlediska odolnosti
4. Příklady použití v praxi (kde se používají MCU, a kde ř. j. s MPU)

%%
1. Správné vysvětlení pojmů, architektur a zkratek z oblasti řídicích systémů.
2. Schopnost posoudit vliv prostředí na výběr hardwaru a dešifrovat IP kód.
3. Vypracování rozhodovací matice pro volbu vhodné platformy (MCU vs. PLC vs. iPC).
4. Návrh konkrétní konfigurace řídicí jednotky na základě zadané I/O bilance a provozních podmínek.
5. Kritická technická oponentura (audit) nevhodně navrženého řešení.
%%


---

## Úlohy


### 1. Základní pojmy a architektury řídicích jednotek

*Časová dotace: 10–15 minut | Úvodní úloha*

Doplňte do níže uvedené tabulky význam zkratek, základní princip a typický příklad reálného nasazení nebo zástupce:

| Zkratka / Pojem          | Co zkratka znamená (česky/anglicky) | Základní charakteristika (architektura, kde běží program)                                 | Typický zástupce                  | Příklad nasazení                           |
| :----------------------- | :---------------------------------- | :---------------------------------------------------------------------------------------- | :-------------------------------- | ------------------------------------------ |
| **MCU**                  | Microcontroller Unit / Mikrokontrolér (jednočipový počítač) | Integrovaný čip (CPU + RAM + Flash na jednom křemíku), deterministický běh bez OS / RTOS  | např. ESP32, PIC16LF1xxx, RP2040  |             Chytré hodinky, senzory, domácí spotřebiče, hračky       |
| **MPU**                  |   Microprocessor Unit / Mikroprocesor | Samostatný procesor vyžadující externí RAM a úložiště, často běží plnohodnotný OS (Linux) |       Raspberry Pi 4/5, BCM2711, i.MX6                            |                       Chytré domácí rozbočovače (huby), multimediální centra, složitější IoT brány                     |
| **Embedded**             | Vestavěný systém (Embedded System) |               Vyhrazený počítačový systém navržený pro konkrétní řídicí funkci uvnitř většího zařízení                                                                            | Embedded PLC, embedded PC         | Bílá technika, bankomaty, plynové kotle... |
| **PLC**                  |      Programmable Logic Controller / Programovatelný logický automat   | Průmyslový automat pro cyklické řízení procesů, vysoká odolnost, modulární/kompaktní      |     Siemens S7-1200/1500, Allen-Bradley Micro800, Beckhoff                              |     Řízení výrobních linek, automatizace budov, čističky odpadních vod                                       |
| **iPC**                  |    Industrial PC / Průmyslové PC    |                       Počítač průmyslové konstrukce (odolnost vůči teplotám, vibracím), běžící na x86/ARM s Windows/Linux OS                                                                    |           Advantech, Beckhoff Industrial PC, Siemens Simatic IPC                        |      Vizualizace výroby (SCADA), počítačové vidění, řízení složitých robota                                      |
| **Programovatelné relé** |     Programovatelné relé / Smart Relay (nebo Programmable Relay / Logic Module) | Zjednodušené malé PLC pro méně náročné úlohy (nahrazuje časovače a relé)                  | např. Siemens LOGO!, Eaton easyE4 |         Řízení osvětlení, ovládání garážových vrat, malé zavlažovací systémy                                   |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **SoC (System on Chip):** Čip integrující CPU, GPU, paměť i bezdrátové moduly (např. Wi-Fi/BT) na jediném substrátu (např. v telefonech, ESP32).
> - **DSP (Digital Signal Processor):** Specializovaný procesor s architekturou optimalizovanou pro bleskové matematické operace (filtrace zvuku, FFT, řízení motorů).
> - **FPGA (Field-Programmable Gate Array):** Programovatelné hradlové pole umožňující vytvořit libovolný digitální obvod přímo na hardwarové úrovni s nulovou programovou latencí.
> Programovatelné hradlové pole. In: _Wikipedia: otevřená encyklopedie_ [online]. St. Petersburg (Florida): Wikimedia Foundation, 2005, poslední editace 10. 1. 2024 [cit. 2026-09-14]. Dostupné z: [https://cs.wikipedia.org/wiki/Programovateln%C3%A9_hradlov%C3%A9_pole](https://cs.wikipedia.org/wiki/Programovateln%C3%A9_hradlov%C3%A9_pole)
> Systém na čipu. In: _Wikipedia: otevřená encyklopedie_ [online]. St. Petersburg (Florida): Wikimedia Foundation, 2007, poslední editace 7. 6. 2024 [cit. 2026-09-14]. Dostupné z: [https://cs.wikipedia.org/wiki/Syst%C3%A9m_na_%C4%8Dipu](https://cs.wikipedia.org/wiki/Syst%C3%A9m_na_%C4%8Dipu)
>Digitální signálový procesor. In: _Wikipedia: otevřená encyklopedie_ [online]. St. Petersburg (Florida): Wikimedia Foundation, 2006, poslední editace 28. 2. 2026 [cit. 2026-09-14]. Dostupné z: [https://cs.wikipedia.org/wiki/Digit%C3%A1ln%C3%AD_sign%C3%A1lov%C3%BD_procesor](https://cs.wikipedia.org/wiki/Digit%C3%A1ln%C3%AD_sign%C3%A1lov%C3%BD_procesor)

<details>
<summary> :bulb: Tip k doplnění tabulky: </summary>
<p>Uvědomte si zásadní rozdíl: U MCU je program nahrán přímo ve vnitřní paměti Flash procesoru a startuje okamžitě po zapnutí (desítky milisekund). U MPU a iPC systém nejprve zavádí operační systém z disku/SD karty do paměti RAM (sekundy až desítky sekund).</p>
</details>

:star2: **Bonusová otázka k úloze 1:**

Proč se u bezpečnostních aplikací v letectví nebo jaderné energetice stále upřednostňují jednoduché mikrořadiče nebo FPGA před moderními vícejádrovými procesory s gigabajty RAM?

*Vaše odpověď:*

### Odpověď: 
* **Deterministické chování a předvídatelnost:** Jednoduché mikrořadiče a FPGA vykonávají instrukce nebo logiku s přesně definovaným časováním bez nepředvídatelných zpoždění (chybí složitý operační systém, dynamický plánovač úlok či nedeterministická cache paměť).
* **Jednodušší certifikace a verifikace:** U složitých vícejádrových procesorů je prakticamente nemožné otestovat všechny stavové kombinace. Jednoduché obvody lze formálně dokázat a certifikovat podle přísných bezpečnostních norm (např. *DO-178C* pro letectví, *IEC 61508* pro průmyslovou bezpečnost).
* **Vysoká spolehlivost a odolnost:** Méně tranzistorů znamená nižší pravděpodobnost hardwarové chyby způsobené např. ionizujícím zářením (*Single Event Upset / SEU*) a výrazně nižší spotřebu i vyzařované teplo.

---

### 2. Parametry, paměti a provozní odolnost (IP krytí)


1. **Typy pamětí:**
   - Jaký je zásadní rozdíl mezi pamětí **RAM**, **Flash** a **EEPROM** v mikrokontroléru/PLC z hlediska uchování dat po odpojení napájení a rychlosti zápisu?
2. **Reálný čas a determinismus:**
   - Proč pro řízení rychlého technologického děje (např. reakce na nouzové zastavení do 5 ms) použijeme spíše **MCU / PLC** než běžný operační systém na **MPU** (např. Raspberry Pi s OS Linux)?
3. **Odolnost a IP krytí:**
   - Dešifrujte označení **IP68** (co přesně znamená první číslice 6 a druhá číslice 8).
   - Jaké minimální krytí IP musí mít zařízení určené pro instalaci venku pod přístřeškem, kde hrozí stříkající voda a prach?
   - Jak se liší konstrukce běžného kancelářského PC od **průmyslového PC (iPC)** (např. z hlediska chlazení, napájení, vibrací a konektorů)?

---

## 1. Typy pamětí

* **RAM:** **Volatilní** paměť (po odpojení napájení se data smažou). Nabízí extrémně rychlý zápis i čtení. Slouží pro uchování běžných proměnných a výpočtů za chodu.
* **Flash:** **Nevolatilní** paměť (data zůstávají uchována i bez napájení). Rychlé čtení, ale pomalejší zápis (zapisuje se po celých blocích/sektorech). Slouží k uložení programu (firmwaru).
* **EEPROM:** **Nevolatilní** paměť. Zápis je pomalejší než u RAM, ale umožňuje přepisovat data po jednotlivých bajtech (na rozdíl od Flash). Slouží k uložení konfiguračních parametrů, kalibrací a nastavení.

---

## 2. Reálný čas a determinismus

* **MCU / PLC:** Běží bez OS (bare-metal) nebo na operačním systému reálného času (**RTOS**). Zaručují **determinismus** — odezva na přerušení (např. reakce na nouzové zastavení do **5 ms**) proběhne vždy v přesně definovaném časovém limitu.
* **Běžný OS na MPU (např. Raspberry Pi s OS Linux):** Není deterministický. Běžný Linux sdílí čas procesoru mezi mnoha procesy. Naplánování úlohy může být odloženo přípravou vyrovnávací paměti, práci se souborovým systémem nebo službami na pozadí, což znemožňuje garantovat reakční dobu.

---

## 3. Odolnost a IP krytí

### 🔍 Dešifrování označení `IP68`
* **První číslice (`6`):** Úplná prachotěsnost (ochrana před nebezpečným dotykem drátem a před vniknutím prachu).
* **Druhá číslice (`8`):** Ochrana proti trvalému ponoření do vody za podmínek určených výroblem/dodavatelem.

---

### ☔ Minimální krytí pro venkovní instalaci pod přístřeškem
* Pro prostředí pod přístřeškem, kde hrozí **stříkající voda a prach**, je vyžadováno minimálně krytí **`IP54`**:
  * **`5`** = Částečná ochrana před prachem.
  * **`4`** = Ochrana před stříkající vodou ze všech směrů.

---

### 💻 Srovnání: Kancelářské PC vs. Průmyslové PC (iPC)

| Parametr | Kancelářské PC | Průmyslové PC (iPC) |
| :--- | :--- | :--- |
| **Chlazení** | Aktivní (ventilátory, které nasávají prach a nečistoty) | Pasivní (bezventilátorové, masivní hliníkové chladiče) |
| **Napájení** | Běžná síťová zásuvka ($230\text{ V}$ AC), interní ATX zdroj | Širokorozsahové stejnosměrné napájení ($12\text{--}24\text{ V}$ DC) s ochranou proti přepětí |
| **Vibrace** | Nízká odolnost (standardní sloty a konektory) | Vysoká odolnost (pájené komponenty, bezkabelové propojení, SSD) |
| **Konektory** | Klasické (USB, RJ45 bez zajištění) | Průmyslové konektory se šroubovacím zajištěním (např. M12, uzamykatelné D-Sub) |



-----------------------------------------------------------------------------------------------------------

1. **Typy pamětí v řídicích jednotkách:**

   * Doplňte porovnání pamětí z hlediska stálosti dat a rychlosti:
     * **RAM:**
       * Je volatilní (energeticky závislá)? `Ano`
       * Rychlost zápisu: `Velmi vysoká (v řádu nanosekund)`
       * K čemu se využívá v PLC/MCU: `Ukládání pracovních proměnných, spuštěný program, zásobník (stack), vyrovnávací paměť (buffer)`
     * **Flash (ROM):**
       * Je volatilní? `Ne`
       * K čemu se využívá v PLC/MCU: `Uložení řídicího programu (firmware), konstanta a konfiguračních dat`
     * **EEPROM / NVRAM:**
       * Je volatilní? `Ne`
       * K čemu se využívá v PLC/MCU: `Ukládání kalibračních dat, nastavení systému a remanentních (retained) proměnných`
   * *Otázka z praxe:* Kam se v průmyslovém PLC ukládají aktuální provozní proměnné (např. čítače vyrobených kusů nebo motohodiny), aby se při nečekaném výpadku napájení neztratily (tzv. remanentní / retain data)?
     * Odpověď: `Do paměti NVRAM / FRAM nebo do RAM zálohované baterií či superkondenzátorem (a při vypnutí přenesené do EEPROM/Flash).`

2. **Reálný čas a determinismus (Hard vs. Soft Real-Time):**

   * Proč pro reakci na nouzové zastavení lisu (požadavek reakce do 5 ms) použijeme PLC či mikrokontrolér s RTOS, a nikoliv běžné Raspberry Pi s operačním systémem Raspberry Pi OS (standardní Linux)?
     * Odpověď: `PLC s RTOS garantuje determinismus (přesně definovaný maximální čas reakce bez zpoždění), zatímco běžný Linux na Raspberry Pi není deterministický (může dojít ke zpoždění kvůli plánovači úloh nebo obsluze přerušení).`

3. **Odolnost vůči vlivům prostředí a dešifrování kódu IP:**

   * Dešifrujte kód **IP68**:
     * První číslice (6): `Úplná ochrana před dotykem a prachotěsnost (prach nesmí vniknout vůbec)`
     * Druhá číslice (8): `Ochrana při trvalém ponoření do vody za podmínek určených výrobcem`
   * Jaké minimální krytí IP musí mít rozváděč umístěný ve venkovním nekrytém prostředí, kde na něj přímo dopadá déšť a fouká polétavý prach?
     * Označte správnou volbu: `[ ] IP20 | [ ] IP44 | [x] IP65 | [ ] IP00`
     * Zdůvodnění: `IP65 zajišťuje úplnou prachotěsnost (číslo 6) a ochranu proti tryskající vodě ze všech směrů / dešti (číslo 5).`

4. **Konstrukční rozdíly kancelářského PC vs. průmyslového iPC:**

   * Vyberte a doplňte hlavní odlišnosti:
     * **Chlazení:**
       * Kancelářské PC: `Aktivní (ventilátory, které nasávají prach)`
       * vs. iPC: `Pasivní (masivní hliníkové pasivy, bezventilátorové provedení - Fanless)`
     * **Napájecí napětí a filtrace:**
       * Kancelářské PC: `230 V AC (standardní ATX zdroj)`
       * vs. iPC: `24 V DC (průmyslový standard) s ochranou proti přepětí a přepólování`
     * Odolnost proti otřesům a vibracím: `iPC používá SSD/eMMC namísto HDD, zpevněné šasi a odpružené uložení komponent`
     * **Způsob montáže:**
       * Kancelářské PC: na stůl/pod stůl
       * vs. iPC: `Na DIN lištu do rozváděče nebo VESA/panelová montáž`
      

-----------------------------------------------------------------
* **🌟 Bonusová otázka k úloze 2:** Co označuje doplňkové písmeno **K** v kódu krytí **IP69K** a v jakém průmyslovém odvětví je toto krytí bezpodmínečně vyžadováno?
  * Odpověď: `Písmeno K označuje ochranu proti vysokotlaké a vysokoteplotní proudící vodě (ostřikování tlakem až 10 MPa při teplotě do 80 °C). Bezpodmínečně se vyžaduje v potravinářském a farmaceutickém průmyslu (a také na vozidlech/zemědělské technice), kde probíhá pravidelné intenzivní čištění a dezinfekce tlakovou vodou.`

------------------------------------------------------------------
Zde je kompletně vyplněná úloha včetně rozhodovací matice v jazyce Markdown, graficky i strukturálně zhotovená přesně podle vzoru z vaší předlohy (s dodržením kurzívy, tučného písma, kódových bloků `` a čisté tabulkové struktury):

### 3. Rozhodovací matice platforem (MCU vs. PLC vs. iPC)


Jste v pozici nezávislého konzultanta automatizace. Tři různí zákazníci požadují navrhnout optimální kategorii řízení.

#### Příklad aplikace (vzorové řešení):
* **Vzorová aplikace 0 – Automatická vjezdová závora na parkoviště:** Jednoduchý jednoúčelový systém s indukční detekční smyčkou vozidla, bezpečnostní optozávorou, koncovými spínači polohy ramene, motorem závory (vpřed/vzad) a výstražným semaforem (červená/zelená). Požadavek na jednoduchou správu správcem objektu a spolehlivý chod v rozváděči u vjezdu.

#### Popis zadaných aplikací pro studenty:
* **Aplikace A – Chytrý pokojový termostat (IoT):** Bateriově napájený přístroj měřící teplotu a vlhkost v místnosti, zobrazující údaje na e-ink displeji a odesílající data přes protokol ZigBee/Wi-Fi do domácí brány. Plánovaná sériová výroba: 10 000 kusů ročně.
* **Aplikace B – Automatická balicí linka:** Průmyslová linka ve výrobní hale. Obsahuje 28 optických snímačů, 14 pneumatických válců, 3 dopravníkové pásy s asynchronními motory a bezpečnostní světelnou závoru. Vyžaduje se nepřetržitý provoz 24/7 a snadná údržba podnikovým elektrikářem.
* **Aplikace C – Kontrolní stanice optické jakosti svarů:** Pracoviště se 2 vysokorychlostními průmyslovými GigE kamerami snímajícími svary na karoserii automobilu. Snímky v rozlišení 4K jsou analyzovány neuronovou sítí v reálném čase, vady jsou označeny a ukládány do podnikové relační databáze (SQL / MES).

---

#### Váš úkol: Rozhodovací matice

| Kritérium hodnocení | Vzorová aplikace 0 (Vjezdová závora - VZOR) | Aplikace A (Pokojový termostat) | Aplikace B (Balicí linka) | Aplikace C (Kamerová kontrola svarů) |
| :--- | :--- | :--- | :--- | :--- |
| **Doporučená platforma** *(MCU / PLC / iPC)* | **Programovatelné relé / kompaktní PLC** *(např. Siemens LOGO!, Eaton easyE4)* | `MCU / Embedded SoC` *(např. ESP32, STM32, nRF52)* | `Modulární PLC` *(např. Siemens S7-1200/1500, Beckhoff, PLC21)* | `Průmyslové PC (iPC)` *(s dedikovanou GPU / AI akcelerátorem)* |
| **Pořizovací cena HW na 1 kus** *(nízká < 500 Kč / střední 5–30 tis. Kč / vysoká > 500 tis. Kč)* | **Střední** *(cca 3 500 – 6 000 Kč)* | `Nízká` *(cca 150 – 400 Kč při masové výrobně)* | `Střední` *(cca 15 000 – 45 000 Kč dle I/O)* | `Vysoká` *(cca 60 000 – 120 000+ Kč)* |
| **Primární programovací jazyk** *(C/C++/MicroPython vs. IEC 61131-3 ST/LAD vs. Python/C#/C++ pod OS)* | **FBD / LAD** *(grafické funkční bloky nebo liniové schéma dle IEC 61131-3)* | `C / C++` *(případně MicroPython / ESP-IDF / FreeRTOS)* | `LAD / ST / FBD` *(vyžadován standard IEC 61131-3)* | `Python / C++ / C#` *(frameworky OpenCV, PyTorch/TensorFlow, SQL)* |
| **Klíčový technický argument pro volbu** *(např. spotřeba, determinismus, grafický výkon)* | **Montáž přímo na DIN lištu v rozváděči, integrovaný displej pro nastavení časovačů přímo na místě, robustní reléové výstupy pro motor a semafor, napájení 24 V DC / 230 V AC bez nutnosti vývoje vlastního plošného spoje.** | `Extrémně nízká spotřeba energie (deep sleep pro bateriový provoz), miniaturní rozměry, integrované bezdrátové rozhraní (Wi-Fi/ZigBee) a velmi nízká jednotková cena při velké sérii (10k ks/rok).` | `Vysoký determinismus a spolehlivost v náročném rušivém prostředí, snadná diagnóza chyby elektrikářem (výměna modulů za chodu/plug&play), průmyslová certifikace pro provoz 24/7.` | `Obrovský výpočetní a grafický výkon pro zpracování obrazu v 4K a běh neuronových sítí v reálném čase, vysokorychlostní rozhraní (GigE), přímá konektivita do SQL/MES databází.` |
| **Hlavní riziko při volbě špatné platformy** *(proč by neuspěly ostatní dvě varianty)* | **MCU:** Nutnost vývoje vlastní desky, nízká odolnost vůči venkovnímu rušení a obtížný servis údržbou.<br>**iPC:** Zbytečně extrémní cena (> 30 tis. Kč), dlouhý start po výpadku napájení a vysoká spotřeba. | **PLC:** Obrovské fyzické rozměry, vysoká spotřeba (nemožnost běhu na baterii), vysoká cena (nerentabilní pro sérii).<br>**iPC:** Nerealizovatelné pro přenosný bateriový přístroj z důvodu rozměrů, příkonu a ceny. | **MCU:** Nízká odolnost vůči prachu/EMC rušení v hale, složitý servis neumožňující rychlou výměnu bloku údržbou.<br>**iPC:** Vyšší náchylnost k pádům OS pro sekvenční řízení, delší bootování, zbytečně složité pro logiku válců a senzorů. | **MCU:** Nedostatečná RAM a výpočetní kapacita pro 4K obraz a AI model.<br>**PLC:** Neschopnost zpracovávat vysokosnímkové video, chybějící AI akcelerace a omezená práce s pokročilými databázemi. |

----------------------------------------------------------------

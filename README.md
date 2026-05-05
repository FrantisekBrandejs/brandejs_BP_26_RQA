# RQA pro interpretaci očních pohybů v kartografii
**Recurrence Quantification Analysis (RQA) for Eye-Tracking Data in Cartography**

Tento repozitář obsahuje interaktivní open-source analytický nástroj vyvinutý v jazyce Python v prostředí Google Colab. Skript slouží ke zpracování, analýze a vizualizaci eye-tracking dat pomocí metod nelineární dynamiky, konkrétně Rekurentní kvantifikační analýzy (RQA). 

Nástroj vznikl jako praktický výstup bakalářské práce na **Katedře geoinformatiky Přírodovědecké fakulty Univerzity Palackého v Olomouci** (Autor: František Brandejs, Vedoucí: Mgr. Michaela Vojtěchovská).

## Hlavní funkce
Nástroj nabízí postup pro výpočet metrik RQA pro standardizovaný vstupní formát dat, aniž by koncový uživatel musel zasahovat do zdrojového kódu (využívá grafické rozhraní `ipywidgets`).

* **Sjednocení a úprava oblastí zájmu (AOI):** Automatická extrakce a možnost manuální reklasifikace překrývajících se AOI do vlastních kategorií.
* **Filtrace odlehlých hodnot (Outlierů):** Očištění dat pomocí metody mezikvartilového rozpětí (IQR) pro každý stimul zvlášť.
* **Fyzický výpočet prahové vzdálenosti pro určení rekurencí:** Algoritmus pro exaktní výpočet foveálního rádiusu (v pixelech) z fyzických parametrů monitoru a zorného úhlu respondenta.
* **Souběžný výpočet RQA metrik:** 
  * **AOI přístup:** Rekurence na základě textové shody navštívených zón.
  * **XY přístup:** Rekurence na základě euklidovské vzdálenosti fixací.
* **Počítané metriky:** Recurrence Rate (RR), Determinismus (DET), Laminarita (LAM).

## Vizualizační panel
Skript obsahuje interaktivní záložkové rozhraní pro vizualizaci výsledků:
1. **Recurrence plot:** Čtvercová matice pro detailní kvalitativní trasování sekvence fixací v čase s barevným odlišením sémantických prvků mapy.
2. **Boxplot:** Kvantitativní srovnání distribuce metrik a mediánů mezi různými skupinami (např. experti vs. nováčci).
3. **Scatter plot:** Korelační zobrazení Determinismu a Laminarity pro identifikaci vizuálních strategií.
4. **Radar plot:** Pavučinový graf pro rychlé zobrazení průměrného kognitivního profilu.

## Struktura vstupních dat
Nástroj je primárně optimalizován pro `.csv` exporty z open-source webové aplikace **GazePlotter** (https://gazeplotter.com).
Vstupní soubor fixací musí obsahovat následující sloupce:
* `stimulus`: Název/ID mapového stimulu.
* `participant`: Unikátní identifikátor respondenta.
* `timestamp`: Časový údaj začátku fixace.
* `duration`: Doba trvání fixace.
* `eyemovementtype`: Typ očního pohybu (očekávají se pouze fixace).
* `AOI`: Textový řetězec navštívené oblasti zájmu.
* `x` a `y`: Pixelové souřadnice fixace na monitoru.

Dále je vyžadována doplňková tabulka respondentů (`.csv`) s jejich rozřazením do skupin (např. úroveň kartografické expertízy).

## Jak nástroj používat (Quick Start)
1. Stáhněte si `.ipynb` soubor z tohoto repozitáře.
2. Otevřete soubor v prostředí [Google Colab](https://colab.research.google.com/).
3. Nahrajte svá data (fixace a tabulku respondentů) na svůj osobní Google Drive.
4. Spusťte první buňku pro import knihoven a propojení s Google Drive.
5. Postupujte postupně podle instrukcí v interaktivních formulářích jednotlivých buněk.

## Použité knihovny
* `pandas` a `numpy` – manipulace s maticemi a datovými rámci.
* `scipy` – výpočet euklidovských vzdáleností (XY přístup).
* `matplotlib` a `seaborn` – generování grafických výstupů a grafů.
* `ipywidgets` – tvorba interaktivního uživatelského rozhraní přímo v prohlížeči.

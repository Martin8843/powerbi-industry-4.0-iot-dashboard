
# 🏭 Dashboard Power BI – Analityka Przemysłowa i OEE (Case&nbsp;Study)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![Figma](https://img.shields.io/badge/Figma-F24E1E?style=flat-square&logo=figma&logoColor=white)

Cześć!, <br><br> dziękuję że odwiedzasz moje repozytorium! Zapraszam cię do zapoznania się z kolejnym projektem.  <br> Jest to 2-stronicowy raport Power BI dla inteligentnej fabryki IndustryOS, połączony z analizą wydajności linii produkcyjnych (OEE), przestojów oraz telemetrii czujników IoT (wibracji i temperatury). <br> <br> Na szczególną uwagę zasługuje autorski design stron raportu. Tła kanwy od podstaw zaprojektowałem w programie Figma, co pozwoliło uzyskać przejrzysty i spójny wizualnie interfejs.

### Możesz pobrać gotowy plik i przetestować go samodzielnie:

<p align="left">
  <a href="Plik z raportem/IndustryOS_Raport.pbix">
    <img src="https://img.shields.io/badge/📥_Pobierz_plik_projektu.pbix-Pobierz_Raport_Power_BI-0055ff?style=for-the-badge&logo=powerbi&logoColor=white" alt="Pobierz PBIX">
  </a>
</p>
---

### Uwaga

Plik .pbix zawiera kompletnie załadowany i gotowy model danych. <br>Do repozytorium dołączono również pliki źródłowe w folderze **/dataset**. <br> Aby przeprowadzić ponowne odświeżenie (Refresh) w Power Query, wystarczy wskazać nową ścieżkę do plików na swoim dysku lokalnym.

---

<br>

<div id="menu" align="center">

### Wybierz stronę raportu do podglądu:

<p align="center">
  <a href="#strona-1">
    <img src="https://img.shields.io/badge/📄_Industry_Overview-7dd3fc?style=for-the-badge&logoColor=black" alt="Strona 1">
  </a>
  <a href="#strona-2">
    <img src="https://img.shields.io/badge/📄_Devices_Overview-7b2cbf?style=for-the-badge&logoColor=white" alt="Strona 2">
  </a>
</p>

</div>

<br>
<hr>
<br>

---

### 📚 Spis treści
<div id="1-wstęp"></div>
<details>
<summary><b>1. Problem biznesowy i postawione pytania (odpowiedzi w pkt 8.)</b> <i>(kliknij, aby rozwinąć)</i></summary>

<br>

Zarząd oraz inżynierowie utrzymania ruchu potrzebują spójnego, centralnego wglądu w realną efektywność parku maszynowego i telemetrię IoT. Rozproszone dane z sensorów oraz systemów produkcyjnych utrudniały bowiem szybkie wykrywanie awarii, optymalizację wskaźnika OEE i skuteczną kontrolę przestojów.

Pytania główne:

&emsp;**1. Jak kształtuje się dobowa krzywa wydajności (System Performance 24h) w wybranym zakładzie P007 w 3 kwartale 2024 i w których przedziałach godzinowych spada ona poniżej średniego poziomu dostępności (System Uptime)?**

&emsp;**2. Które linie produkcyjne generują największe ryzyko jakościowe i opóźnienia w dostawach w zakładzie F010 dla kategorii produktów Food?**

&emsp;**3. Które obszary produkcji w zakładzie F001 (2023 r.) generowały najwyższe koszty przestojów (Downtime Cost)**

Pytanie szczegółowe: 

&emsp;**1. Jak prezentuje się stan sensorów IoT (Overall Sensor Health) w ujęciu ostatniego tygdodnia i w których fabrykach wskaźnik ten utrzymuje się powyżej bezpiecznego progu 70 punktów bez rejestracji alarmów krytycznych?**
<br>
<br>
<br>
<br>


</details>

<div id="2-dane"></div>
<details>
  
<summary><b> 2. Dane do raportu</b> <i></i></summary>

<br>

#### a. Źródło danych
* **Publiczny zbiór danych z platformy Kaggle (Industry 4.0 Financial Risk Dataset), plik w formacie *.csv zaciągany i modelowany za pomocą SQL Server

#### b. Zakres 
* **Czas:** Wymiar uwzględniający lata, kwartały, miesiące oraz cykle dobowe (24h) i zmiany robocze.
* **Lokalizacja i produkcja:** Fabryki / Zakłady (Plant Location, np. F010, F001) oraz kategorie produktów (Product Category, np. Food) i linie produkcyjne.
* **IoT i Stan techniczny:** Telemetria sensorów, wskaźniki zdrowia urządzeń, poziomy wibracji.

  
#### c. Miary operacyjne i finansowe m.in.
* **Wydajność i dyspozycyjność:** System_Uptime, Efficiency_Score, Production_volume, Order_Fulfillment_Rate.
* **Przestoje i ryzyko:** Downtime_Hours, Sensor_Health, RUL
* **Koszty i finanse:** Total_Revenue, Total_Operation_Cost, Total_Maintenance_Cost.
<br>
<br>
<br>
<br>

</details>

<div id="3-model-danych"></div>
<details>
<summary><b> 3. Model danych </b> <i></i></summary>

<br>

Model danych został zorganizowany wokół centralnej tabeli faktów:

* **Tabela Faktów (`Fact_IndustryRisk`): Główna tabela transakcyjna zawierająca kluczowe metryki operacyjne, telemetrię IoT oraz wskaźniki ryzyka finansowego i produkcyjnego (m.in. koszty, przepływy, opóźnienia i wskaźniki awaryjności).
* **Tabele Wymiarów (`Dim_Production_Lines`, `Dim_Risk_Level`, `Dim_Date`):

`Dim_Production_Lines` – słownik linii produkcyjnych powiązany relacją jednokierunkową 1: (Jeden do Wiele)* z tabelą faktów.

`Dim_Risk_Level` – słownik poziomów ryzyka finansowego.

`Dim_Date` – dedykowana tabela kalendarza połączona relacją 1: (Jeden do Wiele)*, umożliwiająca zaawansowaną analizę czasową.<br>

* **Tabela Miar (`MIARY`):** Osobna tabela techniczna służąca jako spójny kontener na wszystkie utworzone miary DAX.

<!-- Podgląd schematu relacji w Power BI -->
<p align="center">
  <img src="model_danych.png" alt="Model danych - Power BI Schema" width="65%">
</p>
<br>
<br>
<br>
<br>
</details>

<div id="4-projekt-ui-ux-figma"></div>
<details>
<summary><b> 4. Projekt widoków w Figma  </b> <i></i></summary>
<br>

Zanim powstał raport w Power BI, cały interfejs został zaprojektowany od podstaw w programie **Figma**. <br>Takie podejście pozwoliło na spójne zaplanowanie architektury informacji, hierarchii wizualnej oraz customowych elementów graficznych.

- Projekt został zrobiony na przemyślanej palecie kolorów nawiązującej do przemysłu i IoT (głębokie, ciemne błękity tła, nowoczesny cyjan).
- Stworzyłem makiety dla 2 głównych zakładek analitycznych oraz strony startowej (Landing Page):
  * *Industry Overview* – kafle KPI (przychody, koszty operacyjne, Uptime, wskaźnik efektywności), incydenty krytyczne oraz koszty przestojów.
  * *Devices Overview* – telemetria sensorów, wibracje, temperatura, analiza OEE vs przestępy

- Tła oraz statyczne elementy interfejsu wygenerowałem jako czyste grafiki w Figmie i importowałem bezpośrednio do Power BI jako tło kanwy.

#### 🎨 Makiety layoutów:

<table>
  <tr>
    <td width="50%" align="center">
      <b>Strona Startowa</b><br>
      <img src="./projekt makiety/Landing page.png" alt="Strona startowa" width="100%">
    </td>
    <td width="50%" align="center">
      <b>Przegląd Sprzedaży</b><br>
      <img src="./projekt makiety/Overview.png" alt="Przegląd Fabryka" width="100%">
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <b>Analiza Produktów</b><br>
      <img src="./projekt makiety/Devices.png" alt="Przegląd Urządzenia" width="100%">
    </td>
  
  </tr>
</table>
<br>
<br>
<br>
<br>
</details>

<div id="5-Logika i dax"></div>
<details>
<summary><b> 5. Logika biznesowa sklepu i kluczowe miary DAX </b> <i></i></summary>
<br>

Aby przeanalizować sprzedaż w branży rowerowej, stworzyłem dedykowany zestaw miar DAX (wykorzystujących funkcje takie jak `CALCULATE`, `ALL`, `DIVIDE` czy zmienne `VAR`).

#### 1. Całkowity przychód [$] (Total Revenue)

```dax
Total Revenue = SUM('Fact_Sales'[Revenue])
```
**Cel analityczny:** Podstawowy wskaźnik pokazujący całkowitą wartość sprzedaży wygenerowaną w danym okresie. <br>
Stanowi fundament pod dalsze wyliczenia finansowe (marża, zysk netto, AOV).

---

#### 2. Średnia wartość zamówienia [$] (Global Avg Order Value)

```dax
Global Avg Order Value = CALCULATE([Avg Order Value], ALL('Fact_Sales'[Age_Group]))
```
**Cel analityczny:** Obliczenie średniej wartości zamówienia dla całego sklepu  (całkowicie ignorując filtr grupy wiekowej). <br>
Umożliwienie bezpośredniego porównania średniej wartości koszyka konkretnej grupy wiekowej ze średnią dla całego sklepu

---

#### 3. Średnia marża produktu [$] (Avg Product Margin)

```dax
Avg Product Margin = DIVIDE([Total Profit], [Total Revenue], 0)

```
**Cel analityczny:** Kluczowy wskaźnik rentowności pozwalający ocenić, jaka część przychodu ze sprzedaży produktów zostaje w firmie jako zysk.

---

#### 4. Wskaźnik sprzedaży [%] (Sales Growth Rate)

```dax
Sales Growth Rate = 
VAR PoprzedniRok = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('Dim_Date'[Date]))
RETURN
  DIVIDE([Total Revenue] - PoprzedniRok, PoprzedniRok, 0)
```
**Cel analityczny:** Pozwala rzetelnie ocenić dynamikę wzrostu biznesu z uwzględnieniem sezonowości.

---

#### 5. Udział wolumenowy TOP produktów [%] (Top Products Volume Share)

```dax
Top Products Volume Share = 
VAR NumOfTopProducts = 10  -- Liczba produktów w tabeli w widoku raportu
-- 1. Sprzedane sztuki dla Top 10 produktów
VAR TopProductsUnits = 
    CALCULATE(
        SUM('Fact_Sales'[Order_Quantity]), 
        TOPN(
            NumOfTopProducts,
            ALL('Fact_Sales'[Product]),
            [Total Profit], --  ranking po ZYSKU
            DESC
        )
    )

-- 2. Całkowita liczba sprzedanych sztuk w całej firmie
VAR TotalCompanyUnits = 
    CALCULATE(
        SUM('Fact_Sales'[Order_Quantity]),
        ALL('Fact_Sales')
    )

RETURN
    DIVIDE(TopProductsUnits, TotalCompanyUnits, 0)
```
**Cel analityczny:** Pozwala zweryfikować czy kluczowy zysk idzie w parze z wolumenem oraz ocenić, jak duże jest uzależnienie sprzedaży od topowego asortymentu w sklepie rowerowym.
<br>
<br>
<br>
<br>
</details>

<div id="6-prezentacja-wynikow"></div>
<details>
<summary><font color="#4dabf7"><b> 6. Data Storytelling & Wizualizacje (Przykłady)</b></font></summary>
  
<br>

Warstwa wizualna została zaprojektowana w oparciu o zasady Data Storytellingu. Kliknij poniżej, aby rozwinąć poszczególne widoki:

<br>

<!-- PUNKT 1 -->
<details>
<summary><b>Karty KPI (Widok Sprzedaż)</b></summary>

<p align="center">
    <img src="/raport_glowny/kpi_sales_overview.png" alt="Sales Overview" width="700">
</p>

- **Całkowita sprzedaż i wskaźniki jednostkowe** (`Zielona karta`)
  * **Total Sales:** Główna wartość pokazująca całkowity przychód wygenerowany przez sklep w wybranym okresie.
  * **Average Profit (Gauge):** Średni zysk przypadający na jedno zamówienie.
  * **Average Order Value (Gauge):** Średnia wartość koszyka zakupowego.

  <span style="color: #4dabf7; font-weight: bold;">Cel analityczny:</span> Szybka ocena skali biznesu oraz rentowności pojedynczej transakcji.

- **Segmenty Przychodowe (`Beżowa karta`)**
  * **Wykres słupkowy:** Prezentuje rozkład przychodów sklepu rowerowego w podziale na grupy demograficzne klientów.

  <span style="color: #4dabf7; font-weight: bold;">Cel analityczny:</span> Szybka identyfikacja kluczowej grupy docelowej, która przynosi największe przychody dla biznesu.

- **Dynamika sprzedaży (`Fioletowa karta`)**
  * Sales Growth Rate: Wyrazista, pojedyncza karta KPI przedstawiająca dynamikę wzrostu przychodów w ujęciu rocznym (YoY).
    
  <span style="color: #4dabf7; font-weight: bold;">Cel analityczny:</span> Błyskawiczna informacja o tempie rozwoju oraz wysokiej skalowalności biznesu rowerowego. 
</details>

<br>

<!-- PUNKT 2 -->
<details>
<summary><b>Wykresy słupkowe (Widok Sprzedaż)</b></summary>

<p align="center">
    <img src="/raport_glowny/revenue_vs_profit_sales_overview.png" alt="Sales Overview" width="700">
</p>

- **Porównanie roczne:** Przychody (Revenue) vs Zysk (Profit) w latach 2014–2016
- Dwa wykresy słupkowe obok siebie pokazują twarde zestawienie finansowe przedsiębiorstwa w ujęciu rocznym.
    
<span style="color: #4dabf7; font-weight: bold;">Cel analityczny:</span> Weryfikacja czy przychody i zysk idą w parze z realnym zyskiem przedsiębiorstwa (rentownością sprzedaży) oraz pozwalają ocenić stabilność finansową firmy na przestrzeni lat.
</details>

<br>

<!-- PUNKT 3 -->
<details>
<summary><b>Wykres kolumnowy grupowany (Widok Produkty)</b></summary>

<p align="center">
    <img src="/raport_glowny/chart_yoy_product_overview.png" alt="Product Overview" width="700">
</p>

- Wykres przedstawia rentowność poszczególnych kategorii produktów w czasie.
- Jedna wizualizacja pokazuje dwa wymiary, bez zbędnego szumu prowadzi odbiorcę do konkretnych wniosków biznesowych.
  
<span style="color: #4dabf7; font-weight: bold;">Cel analityczny:</span> Identyfikacja najbardziej dochodowych produktów oraz śledzenie dynamiki ich rentowności na przestrzeni lat.
</details>

<br>

<!-- PUNKT 4 -->
<details>
<summary><b>Wykres słupkowy 100% skumulowany (Widok Klient)</b></summary>

<p align="center">
    <img src="/raport_glowny/basket_structure_customer_overview.png" alt="Customer Overview" width="700">
</p>
  
- Procentowy udział poszczególnych kategorii produktów w całkowitych wydatkach poszczególnych grup demograficznych.
- Paski procentowe i podział na kolory pozwalają w ułamku sekundy zrozumieć nawyki zakupowe bez zagłębiania się w tabele.

<span style="color: #4dabf7; font-weight: bold;">Cel analityczny:</span> Zrozumienie nawyków zakupowych różnych pokoleń w celu optymalizacji ofert.
</details>

<br>

<!-- PUNKT 5 -->
<details>
<summary><b>Wykres kolumnowy grupowany (Widok Klient)</b></summary>

<p align="center">
    <img src="/raport_glowny/total_profit_customer_overview.png" alt="Customer Overview" width="700">
</p>
  
- Wykres przedstawia całkowity zysk netto wygenerowany przez poszczególne grupy wiekowe klientów.
- Wyraźne słupki uszeregowane malejąco pozwalają w ułamku sekundy zauważyć, kto napędza rentowność firmy.
  
<span style="color: #4dabf7; font-weight: bold;">Cel analityczny:</span> Skierowanie działań tam, gdzie zwrot z inwestycji jest najwyższy.
</details>
<br>
<br>
<br>
<br>
</details>

<div id="7-interaktywnosc-raportu"></div>
<details>
<summary><b> 7. Doświadczenia użytkowania (Rozbudowany Panel Filtrów i Nawigacja)</b></summary>

<br>

Raport został zaprojektowany z naciskiem na nowoczesny interfejs oraz optymalizację przestrzeni roboczej:

- **Chowany Panel Filtrów (Selection & Bookmarks):**  
  Zamiast zagracać przestrzeń statycznymi filtrami, utworzyłem dynamiczny panel wysuwany za pomocą ikony suwaków. Wykorzystując *Zakładki (Bookmarks)* oraz panel *Wybór (Selection)*, użytkownik może w każdej chwili włączyć lub ukryć filtry (`filters on / off`)

<p align="center">
  <img src="hidden_filters.gif" alt="Prezentacja " width="90%">
</p>

<br>

- **Panel Nawigacyjny:**  
  Po lewej stronie zaimplementowałem spójny, estetyczny panel boczny z przyciskami, który umożliwia szybkie i płynne przełączanie się pomiędzy głównymi widokami raportu, zapewniając doświadczenia zbliżone do nowoczesnych aplikacji.

<p align="center">
  <img src="nawigation_pages.gif" alt="Prezentacja " width="90%">
</p>
<br>
<br>
<br>
<br>
</details>

<div id="8-wnioski-biznesowe"></div>
<details>
<summary><b> 8. Wnioski Biznesowe / Odpowiedzi dla Biznesu </b></summary>

<br>

Projekt został zrealizowany pod kątem konkretnych pytań analitycznych postawionych na starcie. Oto najważniejsze wnioski z raportu:


<details>
<summary><b>&emsp; Pytanie Główne 1:  Jak kształtuje się dobowa krzywa wydajności (System Performance 24h) w wybranym zakładzie P007 w 3 kwartale 2024 i w których przedziałach godzinowych spada ona poniżej średniego poziomu dostępności (System Uptime)? </b></summary>

<br>

Mimo wysokiej ogólnej dostępności parku maszynowego (~87%), analiza krzywej dobowej ujawnia konkretne godziny spadku tempa produkcji, które wymagają optymalizacji. <br>
Wydajność pozostaje poniżej średniej dostępności w każdym punkcie pomiarowym – najwyższa jest na starcie doby o 00:00 (86,8%) oraz o 20:00 (85,9%). <br>
Największe osłabienie tempa produkcji występuje na przełomie zmian o godzinie 08:00 (82,6%) oraz 16:00 (81,5%). <br>



<table align="center" style="border: none;">
  <tr>
    <td align="center" style="border: none; padding: 10px;">
      <img src="zrzuty kokpitu/PYT1_Odp.png" alt="Prezentacja YoY Product Overview" width="90%">
    </td>
</table>

</details>

<details>
<summary><b>&emsp; Pytanie Główne 2: Które linie produkcyjne generują największe ryzyko jakościowe i opóźnienia w dostawach w zakładzie F010 dla kategorii produktów Food?</b></summary>

<br>
Linia pakowania generuje zdecydowanie największe opóźnienia w dostawach przekraczające 1000 godzin (co widać po najwyższym położeniu na osi Y wykresu Quality & Delivery Risk) oraz największy bąbel oznaczający skalę problemu. <br> Wiąże się to z największymi przestojami (37 h) i niższą wydajnością OEE na poziomie 83,1%.


<table align="center" style="border: none;">
  <tr>
    <td align="center" style="border: none; padding: 30px;">
      <img src="zrzuty kokpitu/PYT2_Odp.png" alt="Prezentacja YoY Product Overview" width="90%">
    </td>
  </tr>
</table>
</details>



<details>
<summary><b>&emsp; Pytanie Główne 3: Które obszary produkcji w zakładzie F001 (2023 r.) generowały najwyższe koszty przestojów (Downtime Cost)?</b></summary>

<br>

Główne źródło strat finansowych to linia Testing. Łączny koszt przestojów (Total Downtime Cost) wyniósł 10,65 mln $, z czego największy udział miała linia Testing generująca stratę 2 110 931 $ przy 90 godzinach przestoju oraz 9 incydentach krytycznych.<br> Na drugim miejscu pod względem kosztów przestojów uplasowała się linia Assembly (1 844 627, 77 h), a tuż za Packaging (1 738 811, 78 h i 7 incydentów krytycznych).


<table align="center" style="border: none;">
  <tr>
    <td align="center" style="border: none; padding: 30px;">
      <img src="zrzuty kokpitu/PYT3_Odp.png" alt="Prezentacja sales performance" width="90%">
    </td
  </tr>
</table>
</details>


<details>
<summary><b>&emsp; Pytanie Szczegółowe: Jak prezentuje się stan sensorów IoT (Overall Sensor Health) w ujęciu ostatniego tygdodnia i w których fabrykach wskaźnik ten utrzymuje się powyżej bezpiecznego progu 70 punktów bez rejestracji alarmów krytycznych?</b></summary>

<br>

W fabrykach F010 oraz F019 stan sensorów stabilnie utrzymuje się powyżej ustalonego progu 70 punktów, co potwierdza brak alarmów krytycznych i status komunikatów jako All systems normal.


<table align="center" style="border: none;">
  <tr>
    <td align="center" style="border: none; padding: 30px;">
      <img src="zrzuty kokpitu/PYT4_Odp.png" alt="Prezentacja customer" width="90%">
    </td
  </tr>
</table>

<br>

W pozostałych zakładach park maszynowy wykazuje punktowe przekroczenia progów ostrzegawczych na podanych liniach w sekcji Recent Sensor IoT Alerts.

<br>

<table align="center" style="border: none;">
  <tr>
    <td align="center" style="border: none; padding: 30px;">
      <img src="zrzuty kokpitu/PYT4_2_Odp.png" alt="Prezentacja customer" width="90%">
    </td
  </tr>
</table>
</details>

</details>






















<br><br><br><br><br><br><br><br>
<br><br><br><br>
<br><br><br><br>
<br><br><br><br>
<br><br><br><br>
<br><br><br><br>

<!-- Sekcja Strony 1 -->
<div id="strona-1" align="center">

### Strona 1: Ogólny Przegląd Fabryki

<img src="gify/overview_industry.gif" alt="Strona 1 - Sales Overview" width="100%">

<br>

<a href="#menu">
  <img src="https://img.shields.io/badge/⬆_Powrót_do_menu-F2C811?style=for-the-badge&logoColor=black" alt="Powrót">
</a>

</div>

<br>
<hr>
<br>

<!-- Sekcja Strony 2 -->
<div id="strona-2" align="center">

### Strona 2: Analiza Parku Maszynowego

<img src="gify/devices_industry.gif" alt="Strona 2 - Product Overview" width="100%">

<br>

<a href="#menu">
  <img src="https://img.shields.io/badge/⬆_Powrót_do_menu-F2C811?style=for-the-badge&logoColor=black" alt="Powrót">
</a>

</div>

<br>





## 1. Wstęp 

Zachowanie pszczół miodnych, w szczególności związane z aktywnością lotną i zbieraniem pokarmu , stanowi przykład złożonego systemu biologicznego, w którym globalne właściwości kolonii wynikają z lokalnych interakcji pojedynczych osobników. Badanie takich systemów w warunkach rzeczywistych jest trudne ze względu na dużą liczbę osobników oraz dynamiczny charakter ich zachowań.

W ostatnich latach rozwinięto systemy umożliwiające automatyczne monitorowanie aktywności pszczół przy wejściu do ula z wykorzystaniem kamer oraz znaczników fiducjalnych (np. **AprilTags**). Systemy tego typu pozwalają na rejestrowanie danych takich jak:

* czas, 
* ID pszczoły,
* pozycja w przestrzeni 2D, 

co umożliwia analizę lokalnych trajektorii ruchu oraz liczby wejść i wyjść z ula .

Dane tego typu stanowią podstawę do budowy i walidacji modeli symulacyjnych opisujących zachowanie pszczół na poziomie pojedynczych agentów, szczególnie **w bezpośrednim otoczeniu ula**.

---

## 2. Analiza problemu

**Analiza problemu:**

Celem projektu jest modelowanie ruchu pszczół w strefie wejścia i wyjścia z ula z wykorzystaniem podejścia agentowego.  Każdy plik z serii `worker*.txt` zawiera zbiór detekcji wielu oznaczonych pszczół zarejestrowanych w wybranych dniach pomiarowych. Pojedynczy rekord odpowiada jednej detekcji i zawiera znacznik czasu, identyfikator pszczoły (ID), pozycję środka znacznika w przestrzeni obrazu oraz jego orientację. Powtarzające się rekordy dla tego samego identyfikatora umożliwią rekonstrukcję krótkich trajektorii ruchu w pobliżu wejścia do ula.

Istotnym ograniczeniem danych jest **brak informacji o pełnych trajektoriach lotu pszczół w środowisku (np. pomiędzy ulem a źródłem pokarmu)**, co uniemożliwia bezpośrednią walidację modeli opisujących cały proces zbierania pokarmu. Z tego względu poponujemy, zeby zakres projektu został ograniczony do modelowania zachowania pszczół w bezpośrednim otoczeniu ula, gdzie dostępne są dane walidacyjne.

Dane te zostały pozyskane z systemu monitoringu wykorzystującego znaczniki fiducjalne (AprilTags) oraz analizę obrazu, co umożliwia śledzenie ruchu poszczególnych pszczół w bezpośrednim otoczeniu wejścia do ula. 

Dane mają lokalny charakter – obejmują one wyłącznie obszar wylotka, bez informacji o dalszym przebiegu lotu pszczół w środowisku. W związku z tym nie będzie możliwe bezpośrednie modelowanie i walidacja pełnych trajektorii zbierania pokarmu. 

Dane mają charakter nieciągły w czasie (rejestrowane są dla wybranych dni), co wpływa na sposób ich analizy. W związku z tym walidacja modelu będzie miała charakter statystyczny i będzie opierać się na agregacji danych w skali dnia.

Dodatkowo, pomimo że w literaturze szeroko opisano mechanizm komunikacji waggle dance, brak odpowiednich danych eksperymentalnych w analizowanym zbiorze uniemożliwia jego bezpośrednią walidację. W związku z tym zdecydoano, ze mechanizm ten nie zostanie uwzględniony jako główny element modelu.

--- 
## 3. Założenia modelu 

**Założenia modelu:**

* pszczoły modelowane będą jako agenci posiadający stan (np. w ulu, przy wejściu, poza ulem),
* ruch w przestrzeni lokalnej opisywany będzie jako **biased random walk**, co pozwala uwzględnić zarówno losowość ruchu, jak i preferencję kierunkową (np. powrót do wejścia),
* model koncentrować się będzie na krótkich trajektoriach w pobliżu ula,
* dodatkowo analizowane będą statystyki dzienne, takie jak liczba wejść i wyjść oraz aktywność pszczół.

---

## 4. Wybór narzędzi 

**Wybór narzędzi:**

Do realizacji projektu zaproponowano język Python wraz z bibliotekami do analizy danych i symulacji:

* **pandas** – do przetwarzania i agregacji danych (np. obliczanie statystyk dziennych),
* **numpy** – do obliczeń numerycznych,
* **matplotlib / plotly** – do wizualizacji trajektorii i rozkładów,
*  **Mesa** – framework do modelowania agentowego.

Python został wybrany ze względu na:

* łatwość integracji analizy danych i symulacji,
* możliwość bezpośredniego przetwarzania danych tekstowych,
* szerokie wsparcie dla wizualizacji i statystyki.

Dodatkowo rozważamy wykorzystanie środowiska NetLogo jako narzędzia do wizualizacji modelu agentowego. NetLogo umożliwia szybkie tworzenie symulacji oraz intuicyjne przedstawienie zachowania agentów w przestrzeni.

W przypadku wykorzystania NetLogo konieczne będzie jednak wcześniejsze przetworzenie danych wejściowych (plików .txt) w celu dostosowania ich do formatu możliwego do zaimportowania w tym środowisku. W związku z tym planowane będzie zastosowanie dodatkowego etapu parsowania danych (np. z wykorzystaniem języka Python).

Z tego względu Python zostanie wykorzystany jako główne narzędzie analityczne i obliczeniowe, natomiast NetLogo może zostać użyte jako narzędzie wspomagające do wizualizacji symulacji.

---

## 5. Walidacja 

**Walidacja modelu:**

Walidacja modelu będzie opierać się na porównaniu wyników symulacji z danymi rzeczywistymi. W szczególności analizowane będą:

* liczba wejść i wyjść pszczół w danym dniu,
* rozkład długości lokalnych trajektorii,
* średnia prędkość ruchu w przestrzeni obrazu,
* charakterystyka kierunku ruchu.

Porównanie będzie miało charakter statystyczny (np. średnie, rozkłady), co wynika z charakteru dostępnych danych eksperymentalnych.


## Model symulacyjny ilości miodu pozyskiwanego z pasiek w zależności od warunków pogodowych 

### Dane z pasieki w miejscowości Dubne - honey.csv
Dane pochodzą z 9 pasiek  należących do jednego właściciela, zlokalizowanych na jednej łące. Każda pasieka liczy około 10 uli, co daje łącznie w przybliżeniu 100 uli objętych analizą. Dane obejmują 7 lat zbiorów miodu - od 2019 do 2025. Poszczególne lata nie mają identycznych przedziałów czasowych:

- początek: koniec czerwca/lipiec
- koniec: wrzesień

Zbiory zostały przyporządkowane do numerów tygodni w roku, po czym dokonano agregacji danych poprzez 
sumowanie wszystkich obserwacji przypadających na dany tydzień. 

### Dane pogodowe - mean_week.csv
Dane meteorologiczne zostały pozyskane z najbliższej stacji pogodowej względem Dubnej, zlokalizowanej w Nowym Sączu.
Zawierają informacje pogodowe od 22 do 40 tygodnia roku, aby pokrywały się z danymi ze zbiorów miodu. 
Zawierają one takie kolumny z danymi meteorologicznymi jak:

- temp: średnia temperatura powietrza
- tmin: minimalna temperatura
- tmax: maksymalna temperatura
- rhum: wilgotność względna powietrza
- wspd: prędkość wiatru
- wpgt: maksymaly poryw wiatru
- pres: ciśnienie atmosferyczne

### Plan stworzenia symulacji
W celu opisania zależności pomiędzy warunkami pogodowymi a ilością zbieranego miodu zostanie zbudowany model matematyczny. Dla poszczególnych zmiennych meteorologicznych zostaną dobrane współczynniki określające ich wpływ na wynik - ilość zebranego miodu.

Model zostanie zbudowany na podstawie danych z 5 lat (2019–2023), które będą stanowiły zbiór treningowy. Posłużą do estymacji parametrów modelu.

Skuteczność modelu zostanie oceniona na danych pochodzących z dwóch kolejnych lat (2024–2025).

Na podstawie tego modelu zostanie stworzony w pythonie system symulacyjny umożliwiający generowanie prognoz ilości miodu dla dowolnego zestawu warunków pogodowych.

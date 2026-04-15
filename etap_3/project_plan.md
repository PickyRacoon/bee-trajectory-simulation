## Model symulacyjny ilości miodu pozyskiwanego z pasiek w zależności od warunków pogodowych 

### Dane z pasieki w miejscowości Dubne - honey.csv
Dane pochodzą z 9 pasiek  należących do jednego właściciela, zlokalizowanych na jednej łące. Każda pasieka liczy około 10 uli, co daje łącznie w przybliżeniu 100 uli objętych analizą. Dane obejmują 7 lat zbiorów miodu - od 2019 do 2025. Poszczególne lata nie mają identycznych przedziałów czasowych:

- początek: koniec czerwca/lipiec
- koniec: wrzesień

Zbiory zostały przyporządkowane do numerów tygodni w roku, po czym dokonano agregacji danych poprzez 
sumowanie wszystkich obserwacji przypadających na dany tydzień. 

### Dane pogodowe - mean_week.csv
Dane zawierają informacje pogodowe od 22 do 40 tygodnia roku, aby pokrywały się z danymi ze zbiorów miodu. 
Zawierają one takie kolumny z danymi meteorologicznymi jak:

- temp: średnia temperatura powietrza
- tmin: minimalna temperatura
- tmax: maksymalna temperatura
- rhum: wilgotność względna powietrza
- wspd: prędkość wiatru
- wpgt: maksymaly poryw wiatru
- pres: ciśnienie atmosferyczne



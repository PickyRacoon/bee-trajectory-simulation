## Odpowiedzi na pytania z etapu 4 

### Źródło danych pogodowych

Dane pogodowe wykorzystane w projekcie pochodzą z analizy numerycznej ERA5. Nie są to wyłącznie bezpośrednie pomiary ze stacji meteorologicznych, ale dane uzyskane przez model reanalizy atmosferycznej. Wartości są oszacowane dla danego punktu i czasu na podstawie modelu numerycznego 
### Zagęszczenie danych pogodowych

Oprócz danych tygodniowych sprawdzono również wariant z danymi godzinowymi. Celem było przetestowanie, czy większa rozdzielczość czasowa danych pogodowych poprawi jakość predykcji.
Wykonano testy na danych godzinowych bez agregacji prognoz.  Podejście okazało się problematyczne, ponieważ ilość miodu jest mierzona na poziomie miodobrania, a nie pojedynczej godziny. 
Wyniki dla danych godzinowych bez agregacji były słabsze niż dla danych tygodniowych, dlatego jako bardziej stabilne podejście przyjęto wariant oparty na danych tygodniowych.

### Walidacja modelu

W testach regresyjnych nie zastosowano losowego podziału danych. Zamiast tego użyto podejścia `LeaveOneGroupOut`, gdzie grupą był rok.

Oznacza to, że model był trenowany na wszystkich latach poza jednym, a następnie testowany na roku pozostawionym jako zbiór testowy.

Przykład:
```
trening: 2019, 2020, 2021, 2022, 2024, 2025
test:    2023
```

Wyniki modelu ElasticNet

Najlepsze wyniki w podejściu regresyjnym uzyskano dla modelu ElasticNet.

### Podstawowe wyniki :

Tabela 1. Podsumowanie błędów dla pojedynczych miodobrań
| Metryka                     | Wartość kg |
| --------------------------- | ------: |
| MAE                         |   35.50 |
| Maksymalny błąd bezwzględny |  138.45 |


Tabela 2. Średni błąd bezwzględny według roku 
|  Rok | Średni błąd bezwzględny |
| ---: | ----------------------: |
| 2019 |                   14.49 |
| 2020 |                   82.28 |
| 2021 |                   37.24 |
| 2022 |                   41.63 |
| 2023 |                   37.88 |
| 2024 |                   19.71 |
| 2025 |                   10.08 |


Tabela 3. Wyniki roczne w przeliczeniu na ul
|  Rok | Liczba uli | Rzeczywisty miód na ul | Przewidywany miód na ul |
| ---: | ---------: | ---------------------: | ----------------------: |
| 2019 |         92 |                   6.43 |                    7.01 |
| 2020 |         86 |                  17.39 |                   16.61 |
| 2021 |         98 |                  15.96 |                   15.86 |
| 2022 |        100 |                  14.90 |                   14.41 |
| 2023 |         87 |                   9.74 |                    9.16 |
| 2024 |        100 |                   9.79 |                   10.52 |
| 2025 |         96 |                   9.14 |                    9.67 |

Tabela 4. Porównanie  sumy rzeczywistego i przewidywanego miodu w skali całego roku.
| Rok | Rzeczywisty miód | Przewidywany miód | Różnica |
|---:|---:|---:|---:|
| 2019 | 592.00 | 644.66 | 52.66 |
| 2020 | 1495.20 | 1428.04 | -67.16 |
| 2021 | 1563.80 | 1554.49 | -9.31 |
| 2022 | 1489.60 | 1440.85 | -48.75 |
| 2023 | 847.70 | 797.00 | -50.70 |
| 2024 | 979.30 | 1051.87 | 72.57 |
| 2025 | 877.80 | 928.49 | 50.69 |

Wyniki roczne są znacznie stabilniejsze niż błędy dla pojedynczych miodobrań. Najlepsze dopasowanie roczne uzyskano dla 2021 roku, gdzie różnica wyniosła tylko `-9.31 kg`.

# Model symulacyjny pszczół


## Założenie modelu

Końcowa predykcja miodu liczona jest jako:

`predicted_honey = beehive × efficiency × base_efficiency × harvest`


Tabela 5. Opis zmiennych 
| Zmienna           | Znaczenie                                   |
| ----------------- | ------------------------------------------- |
| `beehive`         | liczba uli                                  |
| `efficiency`      | efektywność pracy pszczół zależna od pogody |
| `base_efficiency` | bazowy współczynnik produkcyjności          |
| `harvest`         | numer miodobrania                           |

Efektywność pszczół

W aktualnej  wersji modelu efektywność liczona jest jako:



`efficiency = 0.45 × temp_eff  + 0.20 × wind_eff  + 0.25 × rain_eff  + 0.10 × pres_eff`

Tabela 6. Wyniki dla podstawowego modelu symulacyjnego 
| Rok | Rzeczywisty miód | Przewidywany miód | Różnica | Błąd [%] |
|---:|---:|---:|---:|---:|
| 2019 | 592.00 | 717.84 | 125.84 | 21.26 |
| 2020 | 1495.20 | 791.27 | -703.93 | 47.08 | 
| 2021 | 1563.80 | 1245.71 | -318.09 | 20.34 | 
| 2022 | 1489.60 | 1422.57 | -67.03 | 4.50 | 
| 2023 | 847.70 | 692.70 | -155.00 | 18.28 | 
| 2024 | 979.30 | 1018.38 | 39.08 | 3.99 | 
| 2025 | 877.80 | 1172.86 | 295.06 | 33.61 | 

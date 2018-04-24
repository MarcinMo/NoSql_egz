# Technologie NoSQL - Marcin Moroz i Michał Krakowiak 

Wybrany zbiór danych (Dane zawierają 2 500 000 rekordów) - [link](https://drive.google.com/open?id=13hTWaidu0TK6la3UjAvsd6IJ1_7nHGVk)
Rozmiar wyniósł: 321 MB.

#### Informacje o danych
Kolumny:

- _id: unikalny identyfikator 
- CaseID: 
- Opened: data i godzina wykonania zgłoszenia
- Closed: data i godzina zamknięcia zgłoszenia
- Updated: 
- Status: 
- Status Notes: 
- Responsible Agency:
- Category: 
- Request Type:
- Request Details:
- Address:
- Supervisor District:
- Neighborhood:
- Police District:
- Latitude:
- Longitude:
- Point:
- Source:
- Media URL: 



Informacje o komputerze na którym były wykonywane obliczenia:

| Nazwa                 | Wartość    |
|-----------------------|------------|
| System operacyjny     | Windows 7 Ultimate |
| Procesor              | Intel® Pentium® Dual Processor T2370 |
| Ilość rdzeni          | 2 |
| Pamięć                | 2048MB |
| Dysk                  | HDD |

___________________
#### Wersja mongo

- paczka: Windows Server 2008 R2 64-bit and later, with SSL support x64

Instalacja i konfiguracja oprogramowania należy ją pobrać ze [strony](https://www.mongodb.com/download-center#community) następnie, aby uruchomić bazę danych należy w konsoli cmd wpisać polecenie:

 ``` mongod```


___________________


# Docker <br />



___________________


# Agregacje <br />
Operacje agregacji przetwarzają dokumenty i zwracają przeliczone wyniki.

Agregacje: <br />
- grupują w jedną wartości z różnych dokumentów,
- wykonują wiele różnych operacji na zgrupowanych danych,
- zwracając pojedynczy wynik.


___________________


# Map-Reduce <br />

***MapReduce*** - platforma do przetwarzania równoległego dużych zbiorów danych w klastrach komputerów stworzona przez firmę Google. Nazwa była zainspirowana funkcjami map i reduce z programowania funkcyjnego.

Operacje realizowane są podczas dwóch kroków:

***Krok "map"*** - węzeł nadzorczy (master node) pobiera dane z wejścia i dzieli je na mniejsze podproblemy, po czym przesyła je do węzłów roboczych (worker nodes). Każdy z węzłów roboczych może albo dokonać kolejnego podziału na podproblemy, albo przetworzyć problem i zwrócić odpowiedź do głównego programu.

***Krok "reduce"*** - główny program bierze odpowiedzi na wszystkie podproblemy i łączy je w jeden wynik - odpowiedź na główny problem.

Główną zaletą MapReduce jest umożliwienie łatwego rozproszenia operacji. Zakładając, że każda z operacji "map" jest niezależna od pozostałych, może być ona realizowana na osobnym serwerze.


_______________

#  Git sizer <br />

Komenda jaką trzeba uruchomić:

 ``` git sizer --verbose  ```


![agr1](https://github.com/MarcinMo/NoSql_zal/blob/master/git.png "Logo Title Text 1")

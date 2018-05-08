# Technologie NoSQL - Marcin Moroz i Michał Krakowiak 

Wybrany zbiór danych (Dane zawierają 2 500 000 rekordów) - [311 Cases](https://data.sfgov.org/City-Infrastructure/311-Cases/vw6y-z8j6).
List of cases in San Francisco. The case data represents each case submitted via one of the many SF311 channels and the general characteristics and disposition of the case.

Rozmiar wyniósł: ***1.63 GB***.

#### Informacje o danych
Kolumny:

- ***_id:*** unikalny identyfikator 
- ***CaseID:*** unikalny identyfikator 
- ***Opened:*** data i godzina wykonania zgłoszenia
- ***Closed:*** data i godzina zamknięcia zgłoszenia
- ***Updated:*** data i godzina ostatniej modyfikacji zgłoszenia
- ***Status:*** pojedynczy wskaźnik bieżącego stanu zgłoszenia 
- ***Status Notes:*** wyjaśnienie, dlaczego status został zmieniony na bieżący stan lub więcej szczegółów na temat bieżącego stanu
- ***Responsible Agency:*** agencja odpowiedzialna za wypełnienie lub w inny sposób skierowania zgłoszenia 
- ***Category:*** nazwa typu zgłoszenia  
- ***Request Type:*** nazwa podtypu zlecenia
- ***Request Details:*** nazwa szczegółów zgłoszenia
- ***Address:*** adres lub opis lokalizacji
- ***Supervisor District:*** San Francisco Supervisor District, jak zdefiniowano w "Inspektor Districts of April 2012"
- ***Neighborhood:*** okolice San Francisco zdefiniowane w "SF Find Neighborhoods"
- ***Police District:*** okręg policji San Francisco określony w "Current Police Districts"
- ***Latitude:*** szerokość geograficzna lokalizacji, z wykorzystaniem projekcji WGS84
- ***Longitude:*** długość geograficzna lokalizacji, z wykorzystaniem projekcji WGS84
- ***Point:*** kombinacja szerokości i długości geograficznej dla natywnych map Socraty
- ***Source:*** Mechanizm lub ścieżka, na podstawie której otrzymano zgłoszenie serwisowe; zazwyczaj "Telefon", "SMS / SMS", "Witryna", "Aplikacja mobilna", "Twitter" itp., ale warunki mogą się różnić w zależności od systemu
- ***Media URL:*** Adres URL do multimediów powiązany z żądaniem, np. obraz. 



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
***Docker*** to narzędzie zaprojektowane w celu ułatwienia tworzenia, wdrażania i uruchamiania aplikacji przy użyciu kontenerów. Kontenery umożliwiają programistom skompletowanie aplikacji z wszystkimi potrzebnymi częściami, takimi jak biblioteki i inne zależności, i wysłanie jej jako jednej paczki.



___________________


# Agregacje <br />
Operacje agregacji przetwarzają dokumenty i zwracają przeliczone wyniki.

Agregacje: <br />
- grupują w jedną wartości z różnych dokumentów,
- wykonują wiele różnych operacji na zgrupowanych danych,
- zwracając pojedynczy wynik.

***Agregacja 1:*** przykładowy rekord <br />
Aby wyświetlić przykładową daną należy wykonać polecenie:
 ``` 
 db.test.aggregate(
  { $limit: 1 }
)
```
***wynik:***

***Agregacja 2:*** ilość danych <br />
Aby zobaczyć ilość danych należy wykonać polecenie:
 ``` 
db.test.aggregate( [
  { $group: {
    _id: null,
    count: { $sum: 1 }
  } }
] )
```
***wynik:***


***Agregacja 3:*** sortowanie <br />


***wynik:***

***Agregacja 4:*** szukanie danych <br />

***wynik:***

***Agregacja 5:*** sortowanie konretnych danych <br />

***wynik:***

***Agregacja 6:*** sumowanie <br />

***wynik:***

***Agregacja 7:*** sumowanie i sortowanie <br />

***wynik:***

***Agregacja 8:*** tablica, średnia i sortowanie <br />

***wynik:***

***Agregacja 9:*** pomijanie pierwszych danych <br />

***wynik:***


# Pomiar <br />
Pomiar został wykonany przy użyciu polecenia:
 ``` 
var before = new Date()
#komenda wykonująca agregację
var after = new Date()
execution_mills = after - before
 ``` 
Tabela przedstawia podsumowanie.

| Agregacja                     | Marcin Moroz       | Michał Krakowiak    |
|-------------------------------|--------------------|---------------------|
| Przykładowy rekord            |                    |                     |
| Ilość danych                  |                    | |
| Sortowanie                    |                    | |
| Szukanie danych               |                    | |
| Sortowanie konkretnych danych |                    | |
| Sumowanie                     |                    | |
| Sumowanie i sortowanie        |                    | |
| Tablica, średnia i sortowanie |                    | |
| Pomijanie pierwszych danych   |                    | |
___________________


# Map-Reduce <br />

***MapReduce*** - platforma do przetwarzania równoległego dużych zbiorów danych w klastrach komputerów stworzona przez firmę Google. Nazwa była zainspirowana funkcjami map i reduce z programowania funkcyjnego.

Operacje realizowane są podczas dwóch kroków:

***Krok "map"*** - węzeł nadzorczy (master node) pobiera dane z wejścia i dzieli je na mniejsze podproblemy, po czym przesyła je do węzłów roboczych (worker nodes). Każdy z węzłów roboczych może albo dokonać kolejnego podziału na podproblemy, albo przetworzyć problem i zwrócić odpowiedź do głównego programu.

***Krok "reduce"*** - główny program bierze odpowiedzi na wszystkie podproblemy i łączy je w jeden wynik - odpowiedź na główny problem.

Główną zaletą MapReduce jest umożliwienie łatwego rozproszenia operacji. Zakładając, że każda z operacji "map" jest niezależna od pozostałych, może być ona realizowana na osobnym serwerze.

***Schemat Map-Reduce***  <br />
Schemat wywołania procesu Map-Reduce:
```
{
  "result": "exampleRecord", //miejsce w którym został zapisany wynik obliczeń umieszczony
  "timeMillis": 46395, //czas obliczeń w milisekundach
  "counts": {
    "input": 2833164, //ilość danych
    "emit": 2833164, //ilość wygenerowanych par klucz-wartość
    "reduce": 28332, //ilość odpowiedzi na główny problem
    "output": 0 //ilość elementów kolekcji wynikowej
  },
  "ok": 1
}
```
***Przykładowy rekord*** <br />
Aby zobaczyć przykładowy rekord przy pomocy Map-Reduce, należy: <br />
Strzworzyć poniższą funcję map:
```
var mapFun = function() {
  emit(null, this);
};
```

Strzworzyć poniższą funcję reduce:
```
var reduceFun = function(key, emits) {
  return emits[0];
};
```
Wywołać proces Map-Reduce:
```
mr = db.test.mapReduce(
  mapFun,
  reduceFun,
  { out: "exampleRecord" }
)
```
Aby zobaczyć wynik należy wykonać polecenie:
```
db[mr.result].find();
```
Map-Reduce nie jest najlepszym narzędziem do wyświetlania przykładowego rekordu.

***Ilość kluczy*** <br />
Aby poznać listę oraz ilość kluczy, należy: <br />
Strzworzyć poniższą funcję map:
```
var mapFun = function() {
  for( var key in this ) {
    emit( key, { count: 1 });
  }
};
```
Strzworzyć poniższą funcję reduce:
```
var reduceFun = function(key, emits) {
  total = 0;
  for( var i in emits ) {
    total += emits[i].count;
  }
  return { "count": total };
};
```
Wywołać proces Map-Reduce:
```
mr = db.test.mapReduce(
  mapFun,
  reduceFun,
  { out: "quantityKeys" }
)
```
Aby zobaczyć wynik należy wykonać polecenie:
```
db[mr.result].find();
```
_______________

#  Git sizer <br />

Komenda jaką trzeba uruchomić:

 ``` git sizer --verbose  ```


![agr1](https://github.com/MarcinMo/NoSql_zal/blob/master/git.png "Logo Title Text 1")

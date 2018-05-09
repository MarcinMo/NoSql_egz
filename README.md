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
| System operacyjny     | Windows 10 Home|
| Procesor              | Intel® core i5 7200U 2,5GHz |
| Ilość rdzeni          | 2 |
| Pamięć                |  8GB |
| Dysk                  | SSD |

___________________
#### Wersja mongo

Oficjany obraz mongo w docker wersja 3.6.4

 ``` mongod```


___________________


# Docker <br />
***Docker*** to narzędzie zaprojektowane w celu ułatwienia tworzenia, wdrażania i uruchamiania aplikacji przy użyciu kontenerów. Kontenery umożliwiają programistom skompletowanie aplikacji z wszystkimi potrzebnymi częściami, takimi jak biblioteki i inne zależności, i wysłanie jej jako jednej paczki.

pobranie najnowszej wersji kontenera mongo
```docker pull mongo:latest ```
uruchomienie kontenera (pierwszy raz po pobraniu najnowszej wersji kontenera mongo)
```docker run --name some-mongo3 -d mongo```
uruchomienie kontenera po raz kolejny
```docker start some-mongo3```
odpalenie skryptu importującego dane
```docker exec some-mongo3 ./odpalenie_replica.sh```
odpalenie konsoli mongo w kontenerze
```docker exec -it some-mongo3 mongo --port 27001```


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
```
{ "_id" : ObjectId("5af160a833ba678a5b2f2cc3"), "CaseID" : "241538", "Opened" : "07/02/2008 04:47:08 PM", "Closed" : "06/25/2010 11:16:56 AM", "Updated" : "06/25/2010 11:16:56 AM", "Status" : "Closed", "Status Notes" : "", "Responsible Agency" : "DPW Ops Queue", "Category" : "Tree Maintenance", "Request Type" : "Trees - Damaged_Tree", "Request Details" : "Hanging_limb", "Address" : "Intersection of ELLIS ST and WEBSTER ST", "Supervisor District" : "5", "Neighborhood" : "Western Addition", "Police District" : "NORTHERN", "Latitude" : "37.78257", "Longitude" : "-122.4308", "Point" : "(37.7825698284387, -122.430797788991)", "Source" : "Phone", "Media URL" : "" }
```

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
```
db.test.aggregate(
  { $sort: { Opened: -1 } },
  { $limit: 5 }
)
```

***wynik:***

***Agregacja 4:*** szukanie danych <br />
```
db.test.aggregate(
   { $match: {     
   $or: [       
   { Category: "Graffiti" },
   { Category: "Streetlights" }
   ]   
   } },
   { $limit: 5 }
)
```

***wynik:***
```
{ "_id" : ObjectId("5af160a833ba678a5b2f2ce7"), "CaseID" : "342254", "Opened" : "12/31/2008 02:25:49 PM", "Closed" : "12/31/2008 04:40:16 PM", "Updated" : "12/31/2008 04:40:16 PM", "Status" : "Closed", "Status Notes" : "", "Responsible Agency" : "311 Supervisor Queue", "Category" : "Graffiti", "Request Type" : "Graffiti on Signal_box", "Request Details" : "Signal_box - Offensive", "Address" : "Intersection of CALIFORNIA ST and LAUREL ST", "Supervisor District" : "2", "Neighborhood" : "Presidio Heights", "Police District" : "RICHMOND", "Latitude" : "37.78684", "Longitude" : "-122.4501", "Point" : "(37.7868375587946, -122.450118324135)", "Source" : "Web", "Media URL" : "" }
{ "_id" : ObjectId("5af160a833ba678a5b2f2d13"), "CaseID" : "341874", "Opened" : "12/31/2008 07:52:34 AM", "Closed" : "12/31/2008 10:07:08 AM", "Updated" : "12/31/2008 10:07:08 AM", "Status" : "Closed", "Status Notes" : "", "Responsible Agency" : "DPW Ops Queue", "Category" : "Graffiti", "Request Type" : "Graffiti on Sidewalk_structure", "Request Details" : "Sidewalk_structure - Not_Offensive", "Address" : "Intersection of CUESTA CT and PORTOLA DR", "Supervisor District" : "8", "Neighborhood" : "Upper Market", "Police District" : "PARK", "Latitude" : "37.75046", "Longitude" : "-122.444", "Point" : "(37.7504590098449, -122.443968604795)", "Source" : "Phone", "Media URL" : "" }
{ "_id" : ObjectId("5af160a833ba678a5b2f2d29"), "CaseID" : "341688", "Opened" : "12/30/2008 05:07:56 PM", "Closed" : "12/31/2008 07:06:13 AM", "Updated" : "12/31/2008 07:06:13 AM", "Status" : "Closed", "Status Notes" : "Duplicate per DPW", "Responsible Agency" : "311 Supervisor Queue", "Category" : "Graffiti", "Request Type" : "Graffiti on Pole", "Request Details" : "Pole - Offensive", "Address" : "2827 GREENWICH ST, SAN FRANCISCO, CA, 94123", "Supervisor District" : "2", "Neighborhood" : "Cow Hollow", "Police District" : "NORTHERN", "Latitude" : "37.79747", "Longitude" : "-122.4463", "Point" : "(37.797471752043, -122.446266146711)", "Source" : "Web", "Media URL" : "" }
{ "_id" : ObjectId("5af160a833ba678a5b2f2d52"), "CaseID" : "341537", "Opened" : "12/30/2008 02:10:24 PM", "Closed" : "12/30/2008 05:07:06 PM", "Updated" : "12/30/2008 05:07:06 PM", "Status" : "Closed", "Status Notes" : "", "Responsible Agency" : "DPW Ops Queue", "Category" : "Graffiti", "Request Type" : "Graffiti on Building_residential", "Request Details" : "Building_residential - Post_Abatement_Inspection", "Address" : "2570 SAN JOSE AVE, SAN FRANCISCO, CA, 94112", "Supervisor District" : "11", "Neighborhood" : "", "Police District" : "TARAVAL", "Latitude" : "37.71699", "Longitude" : "-122.4501", "Point" : "(37.716986367, -122.450065909)", "Source" : "Phone", "Media URL" : "" }
{ "_id" : ObjectId("5af160a833ba678a5b2f2d56"), "CaseID" : "341551", "Opened" : "12/30/2008 02:22:43 PM", "Closed" : "12/30/2008 05:07:05 PM", "Updated" : "12/30/2008 05:07:05 PM", "Status" : "Closed", "Status Notes" : "", "Responsible Agency" : "DPW Ops Queue", "Category" : "Graffiti", "Request Type" : "Graffiti on Building_commercial", "Request Details" : "Building_commercial - Post_Abatement_Inspection", "Address" : "1109 MORAGA ST, SAN FRANCISCO, CA, 94122", "Supervisor District" : "7", "Neighborhood" : "Golden Gate Heights", "Police District" : "TARAVAL", "Latitude" : "37.75605", "Longitude" : "-122.4747", "Point" : "(37.756050224886, -122.47473227473)", "Source" : "Phone", "Media URL" : "" }
```

***Agregacja 5:*** sortowanie konretnych danych <br />
```
db.test.aggregate(
  { $match: { Category: "Graffiti" } },
  { $sort: { Opened: -1 } },
  { $limit: 5 }
)
```

***wynik:***

***Agregacja 6:*** sumowanie <br />
```
db.test.aggregate(
  { $group: {
    _id: "$ticket",
    total: { $sum: "$price" } }
  }
)
```

***wynik:***

***Agregacja 7:*** sumowanie i sortowanie <br />
```
db.test.aggregate(
  { $group: {
    _id: "$ticket",
    total: { $sum: "$price" }
  } },
  { $sort: { total: -1 } }
)
```

***wynik:***

***Agregacja 8:*** tablica, średnia i sortowanie <br />
```
db.test.aggregate(
  { $unwind: "$details.bids" },
  { $group: {
    _id: "$ticket",
    bids: { $avg: "$bids" }
  } },
  { $sort: { bids: -1 } }
)
```

***wynik:***

***Agregacja 9:*** pomijanie pierwszych danych <br />
```
db.test.aggregate(
  { $group: {
    _id: "$ticket",
    price: { $avg: "$price" }
  } },
  { $sort: { price: 1 } },
  { $match: { price: { $gt : 110 } } },
  { $skip: 5 }
  )
```

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
| Przykładowy rekord            |      85 ms         |     79 ms           |
| Ilość danych                  |    2383 ms         |   2327 ms	          |
| Sortowanie                    |    6058 ms         |   5651 ms           |
| Szukanie danych               |     175 ms         |    166 ms	          |
| Sortowanie konkretnych danych |    1320 ms         |   1049 ms           |
| Sumowanie                     |    2051 ms         |   1898 ms	          |
| Sumowanie i sortowanie        |    1988 ms         |   1943 ms	          |
| Tablica, średnia i sortowanie |    6275 ms         |   6241 ms           |
| Pomijanie pierwszych danych   |    2013 ms         |   1889 ms	          |

![agr1](https://github.com/MarcinMo/NoSql_egz/blob/master/tab1.png "Logo Title Text 1")

#### Spostrzeżenia
Największe różnice między komputerami są w momencie kiedy przychodzi działanie sortowania całego zbioru danych. Każdy z nas pracował na komputerze o parametrach. Każdy z pomiarów na komputerze Michała są minimalnie lepsze niż u Marcina. Prawdopodobne przyczyny takie zachowania:
- Komputer Michała posiada większą ilość pamięci RAM (12 GB) względem Marcina (8 GB)
- Michał posiada nowszy system operacyjny, niż Marcin
- Komputer Miachał posiada lepszy procesor, niż Marcin

Mimo różnicy w posiadanej pamięci RAM oba komputery zużywały maksimum dostępnej pamięci podczas importu, agregacji i pozostałych badań. Okazuje się, że pojemność pamięci RAM ma kluczowy wpływ na oceny uzystkiwane w teście RAM i bez względu na szybkość transmisji determinuje maksymalny możliwy rezultat.
Komputer oferujący wyższą wydajność oraz większy komfort pracy z otwartymi kilkoma aplikacjami równocześnie, oraz komputer dla gracza, powinien dysponować minimum 8 GB RAM.
 
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
***wynik:***
```
{ "_id" : "Address", "value" : { "count" : 2833164 } }
{ "_id" : "CaseID", "value" : { "count" : 2833164 } }
{ "_id" : "Category", "value" : { "count" : 2833164 } }
{ "_id" : "Closed", "value" : { "count" : 2833164 } }
{ "_id" : "Latitude", "value" : { "count" : 2833164 } }
{ "_id" : "Longitude", "value" : { "count" : 2833164 } }
{ "_id" : "Media URL", "value" : { "count" : 2833164 } }
{ "_id" : "Neighborhood", "value" : { "count" : 2833164 } }
{ "_id" : "Opened", "value" : { "count" : 2833164 } }
{ "_id" : "Point", "value" : { "count" : 2833164 } }
{ "_id" : "Police District", "value" : { "count" : 2833164 } }
{ "_id" : "Request Details", "value" : { "count" : 2833164 } }
{ "_id" : "Request Type", "value" : { "count" : 2833164 } }
{ "_id" : "Responsible Agency", "value" : { "count" : 2833164 } }
{ "_id" : "Source", "value" : { "count" : 2833164 } }
{ "_id" : "Status", "value" : { "count" : 2833164 } }
{ "_id" : "Status Notes", "value" : { "count" : 2833164 } }
{ "_id" : "Supervisor District", "value" : { "count" : 2833164 } }
{ "_id" : "Updated", "value" : { "count" : 2833164 } }
{ "_id" : "_id", "value" : { "count" : 2833164 } }
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
***wynik:***

Tabela przedstawia podsumowanie.

| Agregacja                     | Marcin Moroz       | Michał Krakowiak    |
|-------------------------------|--------------------|---------------------|
| Przykładowy rekord            |       16011 ms     |     15616 ms        |
| Ilość kluczy                  |       57885 ms     |     56238 ms        |  
| Suma                          |        1496 ms     |      1382 ms        |
| Srednia                       |       16355 ms     |     14377 ms        |
| Średnia                       |       21013 ms     |     19599 ms        |

![agr2](https://github.com/MarcinMo/NoSql_egz/blob/master/tab2.png "Logo Title Text 2")

Porównanie zapytań na obu komputerach. 


Widać, że dla każdego zapytania Michał otrzymuje zawsze minimalnie szybciej wynik

#### Spostrzeżenia
Największe różnice między komputerami są w momencie kiedy przychodzi działanie sortowania całego zbioru danych. Każdy z nas pracował na komputerze o parametrach. Każdy z pomiarów na komputerze Michała są minimalnie lepsze niż u Marcina. Prawdopodobne przyczyny takie zachowania:
- Komputer Michała posiada większą ilość pamięci RAM (12 GB) względem Marcina (8 GB)
- Michał posiada nowszy system operacyjny, niż Marcin
- Komputer Miachał posiada lepszy procesor, niż Marcin

Mimo różnicy w posiadanej pamięci RAM oba komputery zużywały maksimum dostępnej pamięci podczas importu, agregacji i pozostałych badań. Okazuje się, że pojemność pamięci RAM ma kluczowy wpływ na oceny uzystkiwane w teście RAM i bez względu na szybkość transmisji determinuje maksymalny możliwy rezultat.
Komputer oferujący wyższą wydajność oraz większy komfort pracy z otwartymi kilkoma aplikacjami równocześnie, oraz komputer dla gracza, powinien dysponować minimum 8 GB RAM.
_______________

#  Git sizer <br />

Komenda jaką trzeba uruchomić:

 ``` git sizer --verbose  ```


![agr1](https://github.com/MarcinMo/NoSql_zal/blob/master/git.png "Logo Title Text 1")

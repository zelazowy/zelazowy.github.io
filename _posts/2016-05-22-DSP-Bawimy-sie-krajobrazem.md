---
layout: post
title:  "DSP: Bawimy się krajobrazem"
date:   2016-05-22 15:40:00 +0200
categories: daj-sie-poznac
short_desc: "Poprzednio wyczyszczony i przygotowany do wyświetlania krajobrazu kod jest tak elastyczny, że spędziłem dzisiaj godzinę modyfikując różne parametry wyświetlania tegoż. Dynamicznie generowany krajobraz daje świetne możliwości..."
---
Liczba wpisów do końca DPS: 2

Jest zabawa!

Poprzednio wyczyszczony i przygotowany do wyświetlania krajobrazu kod jest tak elastyczny, że spędziłem dzisiaj dobrą godzinę modyfikując różne parametry wyświetlania tegoż. Dynamicznie generowany krajobraz daje świetne możliwości.

Poprzednio widać było, że wszystkie elementy poruszają się z taką samą prędkością jak podłoże. No ale nie musi wcale tak być! Mam jedno miejsce w którym dzieje się cały ruch planszy - podłoża i krajobrazu. W uproszczeniu (mocnym ;)) cały kod wygląda tak:

```python
move_size = 10

def move(cls):
    cls.ground -= move_size # "uciekamy" z podłożem

    for element in cls.landscape:
        element["x"] -= move_size # poruszamy każdym elementem krajobrazu
```

Jak widać od podłoża jak i od każdego elementu odejmowana jest wielkość ruchu zdefiniowanego w zmiennej `move_size`. Podłoże zostawiamy bez zmian. Cały trik polega na nadaniu każdemu elementowi krajobrazu jego indywidualnej wartości prędkości i to ją odejmować od pozycji `x`. Każdy element dostaje losowaną w określonych ramach wartość prędkości `element["v"]` i to ją teraz odejmuję zamiast `move_size`:

```python
for element in cls.landscape:
    element["x"] -= element["v"] # poruszamy każdym elementem krajobrazu
```

Ten proty zabieg pozwolił mocno urozmaicić planszę:

<img src="/images/element-random-v.gif"/>

Następnie uznałem, że fajnie byłoby generować dodatkowe elementy w losowych momentach, ale tak, żeby nie przesadzić z liczbą elementów na ekranie. Uznałem, ze rozsądnym maksimum elementów będzie 150% początkowej ich liczby. Żeby to miało ręce i nogi musiałem zrobić 2 rzeczy: losować element jeśli limit na to pozwala oraz losowo nie dodawać elementu gdy jakiś się schowa poza pole widzenia.

Ponownie uproszczony kod (de facto pseudokod) wygląda tak:

```python
def move(cls):
    for element in cls.landscape:
        element["x"] -= move_size
        if element["x"] + element["w"] <= 0: # czyli jeśli element wypadł poza planszę
            del element

            if 2 > random.randint(0, 10): # czy z prawdopodobieństwem 20%
                cls.landscape.append(new_element)

    if 15 > len(cls.landscape): # 15 to 150% początkowej liczby elementów
        if 1 > random.randint(0, 10): # czyli z prawdopodobieństwem 10%
            cls.landscape.append(new_element)
```

Takim sposobem liczba elementów na ekranie została urozmaicona co bardzo fajnie wpłynęło na dynamikę tła. Sami zobaczcie:

<img src="/images/element-random-n.gif"/>

Pisanie Panikotona stało się teraz naprawdę fajną zabawą, co cieszy mnie tym bardziej, że konkurs Daj Się Poznać dobiega już końca. Zostało mi jeszcze kilka dni na dodanie przeciwników do gry (cały potrzebny mi do obsłużenia tego kod już mam) i dopieszczenie szczegółów tak, żeby stworzyć prawdziwą minigrę w którą będzie dało się zagrać.

W następnym wpisie mam nadzieję dodać przeciwników i obsłużyć koniec gry (może też dodać jakieś punkty? :)). Ostatni wpis poświęcę dopieszczeniu gry i wydaniu gry na tyle platform ile się będzie dało (na windowsa już kompilowałem pythona do .exe) no i oczywiście na podsumowanie całej zabawy - bo jest co sumować! :)

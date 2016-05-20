---
layout: post
title:  "DSP: Dynamiczny krajobraz"
date:   2016-05-20 17:52:00 +0200
categories: daj-sie-poznac
short_desc: "Zabrałem się za tworzenie dynamicznego tła dla planszy. Miałem już całkiem fajnie wyczyszczony kod ze zbędnych funkcji i klas. Żeby graczowi nie nudziła się monotonna sceneria stworzyłem dwie proste grafiki: chmury i drzewa, które miały wypełnić pusty i smętny krajobraz..."
---
Liczba wpisów do końca DPS: 3

Zabrałem się za tworzenie dynamicznego tła dla planszy. Miałem już całkiem fajnie wyczyszczony kod ze zbędnych funkcji i klas. Żeby graczowi nie nudziła się monotonna sceneria stworzyłem dwie proste grafiki: chmury i drzewa, które miały wypełnić pusty i smętny krajobraz. I znów przyszła mi z pomocą prosta webowa aplikacja do tworzenia pikselowatych grafik: [https://make8bitart.com/][make8bitart]

<img src="/images/cloud.png"/>
<img src="/images/tree.png"/>

Teraz musiałem zająć się tworzeniem obiektów. Wymyśliłem, że stworzę prostą klasę która będzie trzymała definicje obiektów krajobrazu oraz będzie udostępniała metody do pobierania tychże. Dla chmury definicja wygląda następująco:

```python
cloud = {
    "type": "cloud",
    "w": 50,
    "h": 50,
    "src": "./assets/cloud.png",
    "y": 0,
    "x": 0,
    "max_y": WINDOW_H - 100,
    "max_x": WINDOW_W - 100
}

@classmethod
def get_cloud(cls):
    cloud = cls.cloud.copy()
    cloud["y"] = random.randint(0, cloud["max_y"])
    cloud["x"] = random.randint(0, cloud["max_x"])

    return cloud
```

Zasada jest prosta: przy pobieraniu nowej chmury losowane są dla niej wartości `x` i `y` - po to, żeby chmury pojawiły się w losowych miejscach ale w określonych (przez `max_x` i `max_y`) ramach.

Losowanie krajobrazu ma miejsce jednorazowo podczas startu gry. No ale żeby nie było monotonnie (wspominanie o braku monotonii robi się monotonne... ;P) tło mogłoby się poruszać razem z graczem. To wymaga prostego sprawdzenia czy obiekt nie zniknął poza polem widzenia (`if element["x"] + element["w"] <= 0:`) i jeśli tak to zapisania typu obiektu do odtworzenia oraz usunięcia go z pierwotnej kolekcji.

Do tworzenia nowych obiektów w trakcie gry nie mogłem już użyć getterów danych obiektów - one zawsze losują pozycję `x` obiektu a chciałbym, żeby obiekty pojawiały się na początku planszy. Może nie jest to jasno napisane, więc wyobraźcie sobie, że jedziecie samochodem i drzewa was mijają. Nowe nie pojawiają się losowo tylko zawsze "wychodzą" z przodu - i o to mi właśnie chodziło ;)

Wymagało to nieludzkiego wysiłku w postaci napisania następującej metody:

```python
@classmethod
def add_cloud(cls):
    cloud = cls.cloud.copy()
    cloud["y"] = random.randint(0, cloud["max_y"])
    cloud["x"] = WINDOW_W

    return cloud
```

Jest bliźniaczo podobna do `get_cloud` z tym, że pozycja `x` zawsze ustawiana jest na maksymalną szerokość okna która definiuje wielkość planszy.

Efekt jest zadziwiająco fajny :)

<img src="/images/panikoton-landscape.gif"/>

[make8bitart]: https://make8bitart.com/

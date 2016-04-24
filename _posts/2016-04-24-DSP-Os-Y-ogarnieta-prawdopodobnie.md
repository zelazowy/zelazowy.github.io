---
layout: post
title:  "DSP: Oś Y ogarnięta (prawdopodobnie)"
date:   2016-04-24 20:49:00 +0200
categories: daj-sie-poznac
short_desc: "Prawdopodobnie udało mi się zapanować nad osią Y. Jak pisałem poprzednio zacząłem nieco gubić się w temacie umiejscowienia gracza, planszy czy przeszkody. Wszystkiemu winna jest oś Y która punkt 0 ma w lewym górnym rogu i rośnie w dół - zupełnie odwrotnie niż bym chciał..."
---
Prawdopodobnie udało mi się zapanować nad osią Y. Jak pisałem [poprzednio][poprzedni-wpis] zacząłem nieco gubić się w temacie umiejscowienia gracza, planszy czy przeszkody. Wszystkiemu winna jest oś Y która punkt 0 ma w lewym górnym rogu i rośnie w dół - zupełnie odwrotnie niż bym chciał 😉

Szukałem informacji czy aby nie można programowo odwrócić tej osi i przerobić jej na bardziej oczywistą, „szkolną” wersję. Niestety nie udało się.

Zajrzałem więc do kodu. Problem tkwił tylko w poruszaniu się w pionie (bo oś X działa tak jak „powinna”) więc pole do analizy było całkiem dobrze ograniczone. Potrzebowałem dobrze ograć wysokość całej planszy, umiejscowienie i wysokość gruntu oraz skok gracza.

Przed zmianami w kodzie znajdowały się m.in takie babole:
- rysowanie przeszkody: `painter.drawRect(cls.obstacle_x + cls.background_x, cls.h - 50, cls.obstacle_w, -cls.obstacle_h)` - ujemna wysokość?
- rysowanie gruntu: `painter.drawRect(0, cls.h - 50, cls.w, 50)` - dlaczego 0? Co to jest to 50?

Musiałem zaadresować 2 problemy: wartości początkowe oraz wartości zmieniające się wraz z ruchem. Ten pierwszy zabieg pozwolił wyrzucić wszelkie magiczne ustawianie wartości poza same metody - i odpowiednie udokumentowanie ich. Dzięki temu rysowanie gruntu wygląda teraz tak: `painter.drawRect(cls.ground_x, cls.ground_y, cls.ground_w, cls.ground_h)` - prawda, że lepiej? 😃 Wszystkie wartości ustawiane są teraz poza samym rysowaniem i wygląda to tak:

```python
    ground_w = w
    ground_h = 50
    ground_x = x
    ground_y = h - ground_h  # h of the stage minus ground h
```

W drugim przypadku, gdy gracz a tym samym sama plansza musi się ruszać również ustawiłem wszystkie wartości początkowe przeszkody w jawny sposób, aktualizowanie pozycji wrzuciłem do metody która zajmowała się aktualizacją pozycji samej planszy a w samym rysowaniu korzystałem z ładnie ustawionych wcześniej wartości. Wygląda to tak:

```python
    obstacle_w = 10
    obstacle_h = 20
    obstacle_x = 410
    obstacle_y = h - ground_h - obstacle_h

    @classmethod
    def move_forward(cls):
        # adjust background and all elements on the stage
        cls.x -= cls.move_size
        cls.obstacle_x -= cls.move_size

    @classmethod
    def draw(cls, painter):
        # […]
        # obstacle drawing
        painter.setBrush(QtGui.QColor(0, 0, 255))
        painter.drawRect(cls.obstacle_x, cls.obstacle_y, cls.obstacle_w, cls.obstacle_h)
```

Podsumowując: wszelką „obleśność” ustawianych wartości wyrzuciłem poza metody w których mogę korzystać z pięknie przygotowanych i gotowych do wykorzystania wartości typu `obstacle_x` czy `ground_h` i nie muszę się zastanawiać czy aby na pewno poprawnie odjąłem wartość itp. +10 do czytelności 😉

Prawdziwym sprawdzianem dla aktualnego kodu będzie kolejna funkcjonalność którą chciałbym zaimplementować - skakanie na platformy i poruszanie się po nich. Oj, będzie się działo...

Dla ciekawskich [tutaj][commit] można znaleźć diffa z poprzedniej i aktualnej wersji kodu.

[commit]: https://github.com/zelazowy/panikoton/commit/f1ca1699ec1ca169b511b1c5e4f2c41032aa6e88
[poprzedni-wpis]: http://zelazowy.github.io/daj-sie-poznac/2016/04/23/DSP-1-poziom-wygrana-i-przegrana.html

---
layout: post
title:  "DSP: Mamy planszę!"
date:   2016-03-18 17:32:00 +0100
categories: daj-sie-poznac
short_desc: "Jakiś czas wahałem się co napisać teraz: czy tak jak pisałem poprzednio na blogu zabrać się za planszę, czy może jednak spróbować sił w prymitywnej fizyce. Chyba w międzyczasie zapomniałem o tej rozsterce, bo..."
---
Jakiś czas wahałem się co napisać teraz: czy tak jak pisałem poprzednio na blogu zabrać się za planszę, czy może jednak spróbować sił w prymitywnej fizyce. Chyba w międzyczasie zapomniałem o tej rozsterce, bo po prostu zająłem się planszą :P

Pomysł jest prosty: mamy gracza, który może poruszać się lewo-prawo (oraz góra-dół, ale to na razie pomińmy) oraz planszę która porusza się razem z nim. Gdy gracz idąc w prawą stronę znajduje się na środku okna to przestaje się ruszać, za to zaczyna poruszać się tło będące planszą. Gdy plansza się skończy to gracz dochodzi do krawędzi okna i tam się zatrzymuje. Dokładnie tak samo ma to na razie działać w stronę lewą.

Zacząłem od przygotowania grafiki planszy. Jako #mistrzpainta wszedłem na stronę z ikonami [Font Awesome][fontawesome], znalazłem chmurki i odpowiednio zmieniając cssy dostosowałem sobie kolory. Potem odpaliłem [pixelmator][pixelmator] (jestem za skąpy na photoshopa) i powklejałem chmurkę w losowych miejscach. Plansza na razie ma 2 ekrany długości, więc grafika ma całe 500x1000 px.

Ok, jest tło, trzeba by je wstawić do gry. Najpierw kombinowałem z ustawieniem tła okna, no ale tutaj widziałem problem z przesuwaniem się tła. Z pomocą przyszedł dobrze nam znany z poprzedniego wpisu `QPainter`, który w swojej przepastnej liście metod zawierał `drawPixmap`. Pixmapę znałem już z [poprzedniego projektu][photochooser] pisanego w PyQt4. Ustawiłem więc odpowiednią zmienną żeby wskazywała na lokalizację pliku i wstawiłem utworzone tło do pixmapy:

``` python
background = './assets/stage1_bg.png'
background_pos_x = 0
# [...]
def drawPlayer(self):
    painter = QtGui.QPainter(self)

    pixmap = QtGui.QPixmap(self.background)
    painter.drawPixmap(self.background_pos_x, 0, pixmap)
```

Pierwszy krok załatwiony. Teraz czas aby tło zaczęło się ruszać. Tutaj miałem chwilę rozkminy, ale generalnie okazało się to dosyć proste. Schemat dla ruchu w prawo jest taki (dla ruchu w lewo jest oczywiście analogicznie):
1. sprawdź, czy nie jesteś na krawędzi planszy, jeśli tak to nie masz się gdzie ruszyć
2. jeśli jesteś na końcu planszy, ale do krawędzi masz jeszcze kawałek to rusz gracza o kilka px
3. w przeciwnym przypadku rusz planszą, gracz pozostaje nieruchomy (względem okna)

Kodowo wygląda to następująco:

``` python
def player_move_right(self):
    if self.pos_x + self.player_w >= self.window_w:
        return

    if self.window_w - self.stage_w == self.background_pos_x:
        self.pos_x += self.move_size
    else:
        self.background_pos_x -= self.move_size
```

I... to właściwie tyle. Gracz porusza się w ramach okna, gdy jest "miejsce" na ruszenie planszą to ruszamy nią dajac złudzenie ruchu po większej powierzchni. Pozostaje mi jeszcze wycentrowanie gracza tak, żeby plansza poruszała się z nim gdy jest na środku okna aż do granic planszy. Ale przedtem mam inne zadanie.

Może logika i warunki nie są na razie zbyt skomplikowane, ale już powoli kod zaczyna się rozrastać. Obawiam się, że za chwilę po prostu się pogubię. Muszę pomyśleć nad rozsądnymi komentarzami i oddzieleniem klas gracza od gry. To powinno wprowadzić nieco porządku i dać solidną podstawę pod kolejne funkcjonalności.

PS. Kolega uświadomił mi ciekawą rzecz - piszę grę, mam już "coś" a wrzucam sam kod - gdzie są obrazki? Postaram się to ogarnąć w najbliższym czasie i uzupełnić poprzednie wpisy o odpowiednie grafiki :)

[fontawesome]: https://fortawesome.github.io/Font-Awesome/
[pixelmator]: http://www.pixelmator.com/
[photochooser]: https://github.com/zelazowy/photochooser

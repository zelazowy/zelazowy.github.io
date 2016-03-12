---
layout: post
title:  "DSP: Gracz zaczyna żyć!"
date:   2016-03-12 14:09:00 +0100
categories: daj-sie-poznac
short_desc: W poprzednim wpisie napisałem, że pierwszą rzeczą jaką chcę zakodować to poruszanie się graczem po planszy. Okazało się to prostsze niż myślałem...
---
W poprzednim wpisie napisałem, że pierwszą rzeczą jaką chcę zakodować to poruszanie się graczem po planszy. Okazało się to prostsze niż myślałem. Z początku sądziłem, że trzeba będzie użyć jakiegoś `timera` lub czegoś w tym stylu żeby w ogóle ogarnąć zmiany na planszy. Okazało się to dużo prostsze!

Znalazłem w sieci [kod tetrisa][tetris-kod] napisany w PyQt4 i wgryzłem się w jego funkcje. Dowiedziałem się, że rysowanie czegokolwiek na planszy może zostać wykonane przez `QPainter`, a ten użyty może być tylko w event’cie `paintEvent`. QPainter musi za każdym razem zostać „opuszczony” (`begin`) oraz po zakończeniu podniesiony (`end`). Pomiędzy tymi metodami może dziać się wszystko. Użyłem określeń podniesiony i opuszczony żeby porównać QPaintera do np. rysowania ołówkiem.

``` Python
def paintEvent(self, QPaintEvent):
    self.drawPlayer()

def drawPlayer(self):
    painter = QtGui.QPainter()
    painter.begin(self)
    painter.setBrush(QtGui.QColor(255, 0, 0))
    painter.drawRect(self.pos_x, self.pos_y, self.player_w, self.player_h)
    painter.end()
```

Narysowałem więc okno 500x500 px, ustaliłem rozmiary gracza na 50x50 px oraz rozmiar ruchu na 10 px. Następnie nadpisałem metodę `keyPressEvent` która odpowiada za przechwycenie przyciśnięcia klawisza. W prostym bloku if-elif (Python nie ma `switch`a?) zaimplementowałem 4 metody dla klawiszy strzałek.

``` Python
def keyPressEvent(self, e):
    key = e.key()

    if key == QtCore.Qt.Key_Left:
        self.player_move_left()
    […]

def player_move_left(self)
    if self.pos_x <= 0:
        return

    self.pos_x -= self.move_size
    self.update()
```

W tym momencie odkryłem metodę `update()` która odpowiedzialna jest za przerysowanie okna. Oznacza to, że wywołuje ona event `paintEvent`. Wystarczyło więc odpowiednio zmienić koordynaty gracza, wywołać `update()` i gracz po prostu przesunął się na planszy. Ogranie ciągłego wciskania klawisza i poruszania graczem ograne jest out of the box 😃

Dodałem jeszcze odpowiednie warunki brzegowe zapobiegające przemieszczeniu się gracza poza planszę i bang! - w niecałą godzinę miałem wykonany plan.

### Co następne
Jako kolejny krok myślałem o poruszaniu się planszy w osi X razem z graczem. Polegać ma to na tym, że jak gracz znajdzie się na środku planszy i będzie poruszał w prawo to plansza będzie poruszała się razem z nim. Aby pokazać ten ruch dodam jakieś tło dla okna. Jeszcze nie zdecydowałem czy gracz będzie mógł się cofać czy ruch ten zostanie zablokowany, więc na razie pozwolę na ruch w obie strony aż do granic planszy.

[tetris-kod]: http://zetcode.com/gui/pyqt4/thetetrisgame/

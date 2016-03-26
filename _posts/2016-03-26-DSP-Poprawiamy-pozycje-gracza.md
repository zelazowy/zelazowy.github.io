---
layout: post
title:  "DSP: Poprawiamy pozycję gracza"
date:   2016-03-26 19:52:00 +0100
categories: daj-sie-poznac
short_desc: "W tej chwili wyklarowała mi się pierwsza wersja sposobu sterowania. Chcę aby gracz poruszał się kubek w kubek tak samo jako w Super Mario Bros. Czyli ruch przód-tył, przycisk skoku, gracz wyśrodkowany (lekko do tyłu?) oraz możliwość ruchu planszy tylko do przodu..."
---
W tej chwili wyklarowała mi się pierwsza wersja sposobu sterowania. Chcę aby gracz poruszał się kubek w kubek tak samo jako w Super Mario Bros. Czyli ruch przód-tył, przycisk skoku, gracz wyśrodkowany (lekko do tyłu?) oraz możliwość ruchu planszy tylko do przodu. Ruch do tyłu nie powoduje przesuwania się planszy a tylko gracza do granic okna. Ponowny ruch do przodu najpierw dąży do wyśrodkowania gracza a następnie porusza planszą.

Dzięki tej decyzji mogę usunąć z kodu niepotrzebne funkcje do ruchu góra-dół, które zostaną ostatecznie zastąpione skokiem i przyciąganiem gracza do podłoża. Także warunki ruchu upraszają się. Dochodzi właściwie tylko sprawdzenie czy gracz jest wyśrodkowany przy ruchu do przodu.

Kod odpowiedzialny za ruch do przodu wygląda tak:
```python
# moves player forward
def player_move_forward(self):
    if self.player.can_move_forward():
        return

    if self.stage.is_right_end(self.window_w):
        self.player.move_forward()
    else:
        if self.player.is_centered:
            self.stage.move_forward()
        else:
            self.player.move_forward()
```

Najpierw sprawdzam czy gracz w ogóle może ruszyć się na przód (czy nie dotarł do krawędzi planszy). Następnie jeśli jesteśmy na końcu planszy to ruszamy graczem do przodu. Jeśli nie jesteśmy na końcu planszy to jeśli gracz jest wycentrowany to ruszamy planszą, w przeciwnym przypadku poruszam graczem aż ten się wyśrodkuje. Nawet komentarzy nie muszę pisać, metody są tak opisowe że mówią same za siebie - miodnie 😃

Przy okazji jak widać zmieniłem nazewnictwo. Zamiast używać nazw prawo-lewo postanowiłem użyć przód-tył. Dzięki temu łatwiej będzie się połapać jak wygląda sterowanie i nie będzie wiecznego problemu „która ręka to prawa” 😛

Dosłownie pisząc opis tej metody pomyślałem, że zagnieżdżenie ifów jest już całkiem spore, a przecież warunki są proste. Dlatego postanowiłem zrobić mały refaktor i pozbyć się zagnieżdżeń na rzecz jednopoziomowych warunkó∑ i wyjść z metody. Zobaczcie jak to wygląda:
```python
# moves player forward
def player_move_forward(self):
    if self.player.can_move_forward():
        return

    if self.stage.is_right_end(self.window_w):
        self.player.move_forward()
        return

    if self.player.is_centered:
        self.stage.move_forward()
        return

    self.player.move_forward()
```

Mamy tutaj dwa podejścia do pisania metod. Kod przed refaktorem reprezentował podejście „jedno wejście - jedno wyjście” (chociaż nie do końca, pierwszy if temu przeczy), drugie zaś nie przejmuje się liczbą wyjść i przedkłada nad to mniejsze skomplikowanie kodu. Od dłuższego czasu stosuję tę drugą metodę z wielkim powodzeniem. Alergicznie wręcz reaguję na metody wyglądające tak:
```python
def smth(self):
    if True:
        # do
        # do
        # do
        # do
        # do
        # do
        # do

    return
```

Uważam, że dużo lepiej jest wychodzić z metody jak najszybciej. Jeśli już pierwszy warunek przesądza czy cokolwiek będziemy robić to bezsensownym jest opakowywać kodu „pomyślnego” w ifa. Lepiej jest odwrócić warunek, wyjść, a w przypadku „pomyślnego” scenariusza wykonać czynności poza ifem.
```python
def smth(self):
    if False:
        return

    # do
    # do
    # do
    # do
    # do
    # do
    # do
```

Jeszcze dla porządku spójrzmy na kod odpowiedzialny za ruch do tyłu:
```python
# moves player backward
def player_move_backward(self):
    if self.player.can_move_backward():
        return

    self.player.move_backward()
```

Jak widać jest sporo prostszy i zawiera tylko jeden warunek sprawdzający, czy gracz może poruszyć się do tyłu (czyli czy nie znajduje się na lewej krawędzi planszy). W przeciwnym razie poruszamy się do tyłu samym graczem, plansza zawsze pozostaje nieruchoma.

Takim sposobem z prostego pomysłu uporządkowania ruchu wyszedł całkiem niezły wpis. Chyba z niego jestem w tej chwili najbardziej zadowolony - ze względu na przemycenie idei porządkowania metod jak najszybszym wyjściem z nich. Nauczyłem się tego dosyć niedawno i czytelność mojego kodu skoczyła mocno do góry. Mam nadzieję, że komuś się to przyda 😉

Co w następnym wpisie? Myślałem o wprowadzeniu fizyki skakania. Czy tak będzie? Dowiecie się już w najbliższych dniach 😃

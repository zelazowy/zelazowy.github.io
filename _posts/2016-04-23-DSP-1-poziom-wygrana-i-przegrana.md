---
layout: post
title:  "DSP: 1 poziom - wygrana i przegrana"
date:   2016-04-23 21:00:00 +0200
categories: daj-sie-poznac
short_desc: "Mamy już chodzącego i skaczącego kota. Mamy obsługę sterowania którą łatwo rozszerzać. Czas zająć się projektowaniem i zaprogramowaniem jakiegoś poziomu. Myślę, że na dobry początek wystarczający poziom będzie spełniał proste warunki..."
---
Mamy już chodzącego i skaczącego kota. Mamy obsługę sterowania którą łatwo rozszerzać. Czas zająć się projektowaniem i zaprogramowaniem jakiegoś poziomu. Myślę, że na dobry początek wystarczający poziom będzie spełniał takie warunki:

- będzie zawierał podłoże - gracz nie będzie poruszał się po dolnej krawędzi okna
- będzie zawierał koniec, dojście do krawędzi planszy zakończy poziom
- będzie zawierał warunek przegranej - jakąś przeszkodę której dotknięcie zakończy grę

Na dobry początek podłoże stworzę rysując prostokąty - nie chcę teraz zakopać się w szukaniu jakichś grafik a skupić na dowiezieniu minimalnego poziomu 😉 Sprawa jest prosta - muszę narysować prostokąt na całej długości planszy i odpowiednio podnieść gracza.

Warunek wygranej jest banalny i sprowadza się do sprawdzenia czy gracz nie dotknął przypadkiem nosem końca planszy 😉 Do tego miałem już gotową metodę sprawdzającą, czy gracz może się jeszcze ruszać do przodu. Jeśli nie to znaczy, że gra jest skończona i wyświetlany jest odpowiedni komunikat.

<img src="/images/you-win.gif"/>

Niestety po raz kolejny powraca u mnie problem z ogarnięcie osi x i y, umieszczenie punktu (0, 0) w lewym górnym rogu jest dla mnie strasznie nieintuicyjne i czasami w kodzie rodzą się takie potworki:

``` python
obstacle_x = 410
obstacle_w = 10
obstacle_h = 20
# […]
painter.drawRect(cls.obstacle_x + cls.background_x, cls.h - 50, cls.obstacle_w, -cls.obstacle_h)
```

Niestety ujemna wysokość przeszkody jest dla mnie jakimś koszmarem. Nie mam na to jeszcze dobrego pomysłu, być może będę musiał nadpisać większość metod żeby przenieść punkt (0, 0) na lewy dolny róg, ale szczerze mówiąc obawiam się że w końcu pogubię się w tym bałaganie :/

Tymczasem nieco pomijając ładność i czytelność kodu (co widać nieco wyżej) zająłem się wygenerowaniem przeszkody dla gracza. Uznałem, że mały i prosty do przeskoczenia prostokąt będzie wystarczający. Kod do określenia czy gracz wpadł na przeszkodę (czy to wbiegając w nią czy spadając podczas skoku) jest tak brzydki, że nie nadaje się do publikacji… Dla dociekliwych (masochistów? :P): metoda [określająca wpadnięcie na przeszkodę][is_obstacle_hit] oraz [jej wywołanie][is_game_over].

Przegrana w grze wygląda tak:

<img src="/images/game-over.gif"/>

Powala na kolana nie? 😃 Ale w ostateczności w końcu da się w grze wygrać oraz przegrać a o to w tym wszystkim chodzi.

W następnym wpisie na pewno poruszę temat uporządkowania kodu bo znów przestaję wiedzieć co się tu wyprawia. Być może przeszkoda stanie się jakiegoś typu wrogiem? Bardzo chciałbym dopisać również jakieś platformy na które będzie można wskoczyć - mam już próbny kod jednak m.in przez ten nieszczęsny punkt (0, 0) jest on skomplikowany i ciężki do ogarnięcia.

Czas pokaże.
[is_obstacle_hit]: https://github.com/zelazowy/panikoton/commit/a9213252c5f236885001d32d60aae43664764213#diff-9979a7424a0ea3055bdb08bbbf861b34R285
[is_game_over]: https://github.com/zelazowy/panikoton/commit/a9213252c5f236885001d32d60aae43664764213#diff-9979a7424a0ea3055bdb08bbbf861b34R154

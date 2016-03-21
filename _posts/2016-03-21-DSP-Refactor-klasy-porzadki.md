---
layout: post
title:  "DSP: Refactor, klasy, porządki"
date:   2016-03-21 20:58:00 +0100
categories: daj-sie-poznac
short_desc: "Nadszedł czas na porządki. Powoli zacząłem gubić się w kodzie który pisałem mimo, że jest jeszcze krótki (nie przekroczył 200 linii). Jednak zmienne zaczęły nieco się zlewać no i główna (i dotychczas jedyna) klasa zaczęła puchnąć..."
---
Nadszedł czas na porządki. Powoli zacząłem gubić się w kodzie który pisałem mimo, że jest jeszcze krótki (nie przekroczył 200 linii). Jednak zmienne zaczęły nieco się zlewać no i główna (i dotychczas jedyna) klasa zaczęła puchnąć. No i wypadałoby żeby zachować nieco zasadę SRP (Single Responsibility Principle).

Dla tych, którzy mają wstręt przed klikaniem linków:
SRP to jedna z zasad składająca się na SOLID. Jest pierwszym i najprostszym sposobem na zapanowaniem nad kodem. Jak sama nazwa wskazuje zasada mówi o tym, żeby każda klasa miała jedną odpowiedzialność. Weźmy na przykład oprogramowanie ekspresu do kawy. Ekspres ma takie funkcje: kawa, mleko, czyszczenie. Jeśli użyjemy SRP to każda z tych czynności będzie realizowana przez inną klasę. I tak: robienie kawy nie potrzebuje dostępu do czyszczenia, podobnie czyszczenie nie potrzebuje dostępu do mleka. Dzięki temu każda z funkcji może być rozwijana niezależnie i nie wpływa na zachowanie innych.

Pomaga to też w testowaniu klas, gdzie nie musimy martwić się zbyt napuchniętymi zależnościami.

Po więcej informacji odsyłam do wujka googla: bez problemu można znaleźć blogi, artykuły, książki i filmy z opisem SRP oraz pozostałych zasad składających się na SOLID.

Wróćmy do kodu. Postanowiłem główną klasę rozbić na 3:

- główną klasę gry `Panikoton`
- klasę `Player` odpowiedzialną za gracza
- klasę `Stage` odpowiedzialną za aktualny poziom

Klasa `Panikoton` odpowiedzialna jest za wyświetlenie okna, rysowanie sceny (czyli poziomu i gracza) oraz ruch gracza. Klasa `Player` przechowuje parametry gracza takie jak wysokość i szerokość, rozmiar ruchu, pozycję x i y na planszy oraz metody odpowiedzialne za poruszanie graczem. Klasa `Stage` jest bardzo podobna do klasy `Player`.

Dzięki oddzieleniu klasy `Player` od klasy głównej mogłem skrócić nazwy atrybutów i tak z `pos_x` zrobiło się `x` a z `player_w` po prostu `w`. Czytelność jest zachowana, gdyż w kontekście głównej klasy parametry te są dostępne przez `self.player.x` co mówi dużo więcej niż poprzednie `self.pos_x`.

Przy okazji nauczyłem się też czegoś nowego. Do tej pory nie używałem dla metod klas żadnych adnotacji. Jednak bez adnotacji `classmethod` metody klas `Player` i `Stage` za nic nie chciały być dostępne z klasy `Panikoton`. Adnotacja `@classmethod` służy do wystawienia metody na zewnątrz. Pierwszym parametrem nie jest już `self` a `cls` - parametr który przechowuje klasę jako taką a nie jej instancję jak `self`. Szczerze mówiąc jeszcze tego nie rozgryzłem i nie chcę tu napisać jakichś głupot 😉 Na razie zadowolę się tym, że działa oraz podstawowym wytłumaczeniem znalezionym w internetach.

Jeśli ktoś chce się zagłębić bardziej w zmiany zapraszam do porównania sobie tych dwóch commitów: [przed][commit-pre] i [po][commit-post]. Niestety nie pomyślałem i w jednym commit’cie puściłem również usunięcie katalogi z ustawieniami IDE więc jest nieco nieczytelnie, ale z łatwością można znaleźć plik `panikoton.py` i go porównać.

[commit-pre]: https://github.com/zelazowy/panikoton/commit/1ac237190b41e3e0315aac0cb6633a085b0f2f88
[commit-post]: https://github.com/zelazowy/panikoton/commit/d8869da50520b094458e38ab9a24365e8ad94398

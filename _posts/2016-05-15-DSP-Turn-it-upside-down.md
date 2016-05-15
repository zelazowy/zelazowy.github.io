---
layout: post
title:  "DSP: Turn it upside down"
date:   2016-05-15 17:31:00 +0200
categories: daj-sie-poznac
short_desc: "Zacząłem czyścić kod z niepotrzebnych funkcji które nie dowiozą mi poprzednio opisanego MVP. I trochę się rozpędziłem... ;)"
---
Liczba wpisów do końca DPS: 5

Zacząłem czyścić kod z niepotrzebnych funkcji które nie dowiozą mi [poprzednio][poprzedni-wpis] opisanego MVP. I trochę się rozpędziłem... ;)

Uznałem, że tło planszy jakie jest w tej chwili jest bez sensu, bo:
  1. muszę je stworzyć tak duże jak ma być cała plansza, albo
  2. stworzyć je na tyle długie, żeby powtarzanie go co jakiś czas nie wyglądało "nudno"

Dużo bardziej spodobał mi się pomysł generowania tła w czasie rzeczywistym. Tu walniemy chmurkę, tu jakieś drzewko, może jakieś słońce? Może nawet pory dnia? To wszystko byłoby trudno osiągalne przy rysowanym tle (albo musiałbym mieć odpowiednio dużo wersji tegoż).

Także tło wyleciało, z planszy został właściwie tylko grunt pod graczem.

Potem pomyślałem, że w sumie cofanie się gracza nie ma sensu, no bo po co? Nie zamierzam na razie (a może w ogóle?) robić platform po których gracz mógłby skakać. Zresztą jaką miałby motywację bez znajdziek? Wyleciał więc również kod odpowiedzialny za ruch do tyłu. Dalej patrząc - skoro gracz nie może się cofać, to po co użytkownik ma cisnąć cały czas strzałkę w prawo? Zróbmy to za niego.

Kod odpowiedzialny za ruch do przodu - wyleciał. Skoro ten kod wyleciał, to i oznaczanie czy gracz jest wyśrodkowany czy trafił na koniec planszy itp. też stał się zbędny - do piekła z nim.

I tak po porządkach zostało właściwie to:
  * skakanie
  * grunt pod graczem
  * automatyczny ruch gracza do przodu (żeby zobrazować ruch gracza grunt pod nim przesuwa się)

Wygląda to teraz tak:

<img src="/images/panikoton-automove.gif"/>

Co dalej? Losowanie elementów tła :)

[poprzedni-wpis]: http://zelazowy.github.io/daj-sie-poznac/2016/05/08/DSP-MVP-zrewidowane.html

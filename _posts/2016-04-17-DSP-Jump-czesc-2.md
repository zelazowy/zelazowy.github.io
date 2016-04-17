---
layout: post
title:  "DSP: Jump! część 2"
date:   2016-04-17 12:00:00 +0200
categories: daj-sie-poznac
short_desc: "Trochę mi zajęło wymyślenie sposobu na ogranie kilku klawiszy na raz. Potrzebne jest to chociażby do wyświetlenia skoku wraz z ruchem po planszy. Kłopot polegał na tym, że metoda `keyPressEvent` obsługuje tylko wciśnięcia pojedynczych klawiszy..."
---
Patrzcie na to!
<img src="/images/cat-jump.gif"/>

Ale pokolei ;)

---

Trochę mi zajęło wymyślenie sposobu na ogranie kilku klawiszy na raz. Potrzebne jest to chociażby do wyświetlenia skoku wraz z ruchem po planszy. Kłopot polegał na tym, że metoda `keyPressEvent` obsługuje tylko wciśnięcia pojedynczych klawiszy. Gdy miałem wciśnięty klawisz od ruchu w prawo i w tym czasie naciskałem skok, to gracz zatrzymywał się, skakał i mimo dalej wciśniętego klawisza ruchu był już nieruchomy.

Z pomocą przyszedł StackOverflow na którym w końcu postanowiłem poszukać pomocy (pytanie można zobaczyć [tutaj][stackoverflow]). Rozwiązanie okazało się być zaskakująco proste i opiera się o wykorzystanie metody `keyPressEvent` do zbierania wciśniętych klawiszy oraz `keyReleaseEvent` do wyrzucania ich.

Wygląda to mniej więcej tak:  
  * przygotowałem tablicę klawiszy wraz z ich stanem (wciśnięty, nie wciśnięty)  
  * w metodzie `keyPressEvent` ustawiam stan klawisza na wciśnięty  
  * w metodzie `keyReleaseEvent` ustawiam stan klawisza na nieaktywny  

Od teraz metody które wykonywane były natychmiast po wciśnięciu klawisza wykonywane są przez chodzący w aplikacji `Timer` - ten sam który zarządzał samym skokiem. Jego przebieg jest prosty: co określony interwał sprawdzany jest stan każdego z klawiszy i dla wciśniętych wykonywane są przypisane do nich akcje. Dodatkowo zachowane zostało sprawdzanie czy gracz nie jest w trakcie skoku. Takim prostym zabiegiem osiągnąłem wykonywanie kilku akcji jednocześnie.

Gdy już miałem działający skok wraz z ruchem postanowiłem nieco ruszyć na przód stronę estetyczną i zamienić czerwony kwadrat w kota i co więcej zanimowanie go ;) Naturalnym miejscem do wpięcia animacji jest tablica skoku. Przy okazji uprościłem tam logikę i usunąłem kierunek skoku (góra-dół) na rzecz tablicy zawierającej ruch w obu kierunkach.

Przed: `jump_run = [20, 15, 10, 5, 2, 0]`  
Po: `jump_run = [-20, -15, -10, -5, -2, 0, 2, 5, 10, 15, 20]`  

Dzięki temu wystarczyło stworzyć analogiczną tablicę dla grafik i voila! :) Efekt tych działań widać na gifie na samym początku wpisu. Każda klatka animacji nazywa się `cat{0}.png` gdzie `{0}` jest numerem animacji. Dzięki temu wystarczyło dla skoku przypisać numer animacji do korespondującej wartości w tablicy skoku i rysować odpowiedni plik gracza.

Dociekliwych zachęcam do zajrzenia do [kodu klasy][player-code] `Player` gdzie wszystko jest (mam nadzieję) wyraźnie widoczne ;)

[stackoverflow]: http://stackoverflow.com/questions/36581425/how-to-process-short-keypress-in-the-same-time-long-keypress-is-performed
[player-code]: https://github.com/zelazowy/panikoton/blob/master/panikoton.py#L140

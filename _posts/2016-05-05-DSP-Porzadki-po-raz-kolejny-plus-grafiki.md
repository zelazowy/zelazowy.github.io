---
layout: post
title:  "DSP: Porządki (po raz kolejny) + grafiki"
date:   2016-05-05 21:48:00 +0200
categories: daj-sie-poznac
short_desc: "Trochę mnie nie było... W sumie nie wiem czemu, ale chyba ciężar wiszącego na mnie tematu (ogólnie: wykrywanie kolizji) był nieco demotywujący. Doszło do tego trochę poczucie, że osiągnąłem już całkiem sporo - zobaczyłem jak się pisze gry i dało mi to naprawdę sporą dawkę wiedzy...."
---
Trochę mnie nie było... W sumie nie wiem czemu, ale chyba ciężar wiszącego na mnie tematu (ogólnie: wykrywanie kolizji) był nieco demotywujący. Doszło do tego trochę poczucie, że osiągnąłem już całkiem sporo - zobaczyłem jak się pisze gry i dało mi to naprawdę sporą dawkę wiedzy.

No ale w końcu się przemogłem i zasiadłem do działania. Jak zawsze pomogło stare dobre "dziel i zwyciężaj" + użycie techniki pomodoro. Tłumacząc się w jednym zdaniu technika pomodoro to sposób pracy w którym pracujemy nieprzerwanie nad jedną rzeczą przez 25 minut po czym robimy 5 minut przerwy. Zawsze jak zapuszczę "pomidora" moja motywacja wzrasta i problem z ruszeniem nawet dużego tematu znika ;)

Na początek uznałem, że źle nazwałem twór wprowadzony zeszłym razem. Twór ten kończył automatycznie grę, czyli gracz przegrywał. Dlatego też nazwa "obstacle" mi nie pasowała - dużo właściwszym jest nazwanie tego przeciwnikiem. Na razie nieruchomym, ale właśnie zetknięcie z przeciwnikiem powinno kończyć grę. Na szczęście wystarczyło proste Cmd + R i pozmiana wystąpienia słowa "obstacle" na "enemy". Zrobione.

Potem uznałem, że świecenie czerwonym "dywanem" pod graczem jest brzydkie. Podobnie rysowanie przeciwnika jako niebieskiego kloca mogłoby już zostać zastąpione jakąś grafiką. Wpisałem więc w google "8 bit pattern" i dostałem gdzieś w pierwszych wynikach prostą aplikację do tworzenia grafiki pixelowej [https://make8bitart.com][8bitart]. Dosłownie w kilka minut miałem gotowe grafiki dla przeciwnika oraz podłoża planszy.

<img src="/images/enemy.png"/>
<img src="/images/platform-bg.png"/>

Od razu gra zaczęła wyglądać lepiej.

Następnie chciałem zabrać się za ogranie przeszkody. Grafikę również przygotowałem a kod do sprawdzania czy gracz wpadł na przeszkodę właściwie miałem - wystarczy skopiować kod odpowiedzialny za wykrycie kolizji z przeciwnikiem i zmienić zachowanie gry z przegranej na po prostu zatrzymanie gracza (gdy wpadnie horyzontalnie) lub "wkoczenie" gracza na przeszkodę (gdy wpadnie wertykalnie). Ale uznałem, że to dobry materiał na kolejny wpis ;)

Dlatego zachęcam do zajrzenia tu za kilka dni (dam znać na fb) a tymczasem cieszcie oczy nowym wyglądem gry ;)

<img src="/images/game-with-graphics.gif"/>

[8bitart]: https://make8bitart.com

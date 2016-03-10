---
layout: post
title:  "DSP: Zaczynamy!"
date:   2016-03-10 20:29:00 +0100
categories: daj-sie-poznac
short_desc: Na początek muszę się do czegoś przyznać. Otóż w zgłoszeniu popełniłem mały błąd podając, że będę pisał grę w Pythonie + PyQT. Dopiero potem przypomniałem sobie, że...
---
Na początek muszę się do czegoś przyznać. Otóż w zgłoszeniu popełniłem mały błąd podając, że będę pisał grę w Pythonie + PyQT. Dopiero potem przypomniałem sobie, że przecież znalazłem bibliotekę Pygame która zdaje się idealnie pasowała do pisania gry.

Dzisiaj jednak gdy przystąpiłem do instalacji okazało się, że nie będzie tak łatwo. Pygame jest napisana pod Pythona 2.x, ma co prawda wersję alfa pod 3.x ale instalacja nie jest taka prosta. To czego jeszcze się obawiałem to dokumentacja. Skoro biblioteka pisana była pod starszą wersję miałem obawy, że ogarnięcie różnic w pewnych core’owych funkcjach może być nieprzyjemną przeszkodą.

Postanowiłem więc wrócić do „pomyłkowej” wersji i okazuje się, że bez problemu powinienem napisać grę w PyQT 😃 Tak więc pomyłka którą popełniłem przy zgłoszeniu okazała się wcale pomyłką nie być.

Dobra, przyznałem się, możemy lecieć z koksem.

Na sam początek chciałbym napisać prosty „silnik” który narysuje mi jakąś namiastkę gracza oraz pozwoli nim poruszać w obrębie, powiedzmy, kwadratowej planszy. Gracz powinien reagować na strzałki, gdzie pojedyncze przyciśnięcie ma poruszyć gracza o kilka pikseli a przytrzymanie klawisza ma zapętlać ten ruch. Gracz ma się zatrzymać na granicy planszy.

Taki początek powinien nauczyć mnie kilku rzeczy:
* jak ogarnąć ciągłe wciskanie klawiszy i poruszanie graczem
* jak ogarnąć zatrzymanie się gracza na krawędzi planszy

W następnym wpisie mam nadzieję, że pojawi się już jakiś konkretny kod :)

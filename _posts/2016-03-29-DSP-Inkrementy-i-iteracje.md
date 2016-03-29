---
layout: post
title:  "DSP: Inkrementy i iteracje"
date:   2016-03-29 20:35:00 +0200
categories: daj-sie-poznac
short_desc: "Dzisiaj wpis zupełnie nietechniczny, chociaż bardzo przydatny w kontekście samego pisania aplikacji. Zapraszam do krótkiego studium pisania aplikacji inkrementacyjnie i iteracyjnie na przykładzie mojej gry..."
---
Dzisiaj wpis zupełnie nietechniczny, chociaż bardzo przydatny w kontekście samego pisania aplikacji. Zapraszam do krótkiego studium pisania aplikacji inkrementacyjnie i iteracyjnie na przykładzie mojej gry.

Myślałem niedawno o tym, że mój projekt może nie być specjalnie ambitny. Ot, wchodzi gość w nieznane mu tereny, nie przygotował się zbytnio i pewnie nie wie, że można grę napisać dużo szybciej, lepiej i wygodniej. Przez chwilę co prawda myślałem o Unity, ale ostatecznie porzuciłem ten pomysł. Dlaczego?

Sprawa jest prosta - chcę poznać pisanie gier od podszewki. Zacząć jak pionierzy piszący gry 30, 40 lat temu. Mieć wiedzę wystarczającą na powolne rozbudowywanie aplikacji do coraz to bardziej grywalnego tworu.

Takie podejście ma jeszcze jeden plus: bardzo wyraźnie pokazuje siłę iteracyjnego i inkrementacyjnego podejścia do pisania projektów. Co to znaczy?

W skrócie: iteracyjność mówi, że najpierw tworzymy wersję najbardziej podstawową, MVP z MVP. Taką wersję możemy szybko przetestować i zweryfikować podjęte decyzje. W drugiej iteracji korzystamy z doświadczeń których dostarczyła wersja z iteracji pierwszej i tak w kółko, aż dojdziemy do wersji satysfakcjonującej.
Inkrementacyjność (chyba nie ma takiego słowa…) oznacza dopisywanie funkcjonalność jedna po drugiej zamiast pisania wszystkich naraz.

Te techniki idealnie się łączą. Pokażę to na podstawie swojej gry:
* W pierwszej iteracji chciałem mieć tylko wyświetlające się okno gry wraz z kwadratem przedstawiającym gracza. [x]
* Potem inkrementacyjnie dodałem sterowanie graczem w 4 kierunkach [x]
* Przyszła kolej na tło planszy i poruszanie się gracza względem nie tylko okna ale też samej planszy, sterowanie nie było idealne (choć wystarczające) [x]
* Kolejną rzeczą było iteracyjne poprawienie sterowania graczem, usunięcie zbędnych ruchów oraz poprawienie poruszania się po planszy [x]
* W kolejnym inkremencie ma pojawić się prymitywna fizyka gracza [ ]
* itd., itp.

Jak widać zacząłem od bardzo podstawowych wymagań. Jednak dzięki szybkiemu spełnieniu ich mogłem szybko dopisywać nowe funkcjonalności i poprawiać te, które na testach okazywały się zbyt proste lub niepoprawne.

Wyobrażacie sobie co bym teraz miał, gdybym od razu chciał mieć piękne grafiki, muzykę, fizykę, poziomy itp.? Sama mnogość tematów do poruszenia przy pisaniu gry jest przytłaczająca. Na tym etapie DSP miałbym pewnie kilka wpisów planujących cały projekt, jakieś grafiki itp., ale na 99% nie miałbym nawet linijki kodu. I możliwe, że tak by już zostało, bo wielkość projektu po prostu by mnie przytłoczyła.

Na szczęście podejście inkrementów i iteracji idealnie sięu mnie sprawdza i pozwala powoli chociaż niestrudzenie dopisywać kolejne funkcje i ani się obejrzymy będzie gotowa gra 😃

Dajcie znać, czy piszecie ponownie, czy może inny sposób działa dla was dużo lepiej? Zawsze warto dowiedzieć się czegoś nowego 😉

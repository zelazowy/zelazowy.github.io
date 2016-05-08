---
layout: post
title:  "DSP: MVP zrewidowane"
date:   2016-05-08 18:28:00 +0200
categories: daj-sie-poznac
short_desc: "Ostatnio coś mi internet szwankuje w domu. I wiecie co? Dzięki temu wiem, co teraz zrobić z grą 😉 Pewnie wiecie, że gdy nie ma internetu to w przeglądarce chrome pokazuje się odpowiedni komunikat plus obrazek dinozaura nad nim. Ale czy wiecie, że po wciśnięciu spacji zaczyna się minigra w której skaczemy dinozaurem nad przeszkodami?..."
---
Ostatnio coś mi internet szwankuje w domu. I wiecie co? Dzięki temu wiem, co teraz zrobić z grą 😉 Pewnie wiecie, że gdy nie ma internetu to w przeglądarce chrome pokazuje się odpowiedni komunikat plus obrazek dinozaura nad nim. Ale czy wiecie, że po wciśnięciu spacji zaczyna się minigra w której skaczemy dinozaurem nad przeszkodami?

Ta prosta minigra uświadomiła mi jedną rzecz. Podszedłem do pisania Panikotona bardzo ambitnie. Chciałem zrobić klona Super Mario Bros. Z pozoru prosta gra okazuje się mieć tak dużo elementów, że już w tej chwili wiem, że takiego klona nie zrobię. No ale przecież jest multum równie grywalnych gier o dużo prostszej mechanice, jak rzeczona minigra w chromie.

Spojrzałem z lotu ptaka na moje dotychczasowe „dokonania” w pisaniu gry i widzę, że stworzyłem sobie kilka prostych mechanik (jak poruszanie się, skakanie, mega proste wykrywanie kolizji) ale nie jest to gra. Jest to ni mniej ni więcej zbiór różnych mechanik. Chyba można by to nazwać nieco na wyrost frameworkiem czy nawet „silnikiem gry” (w cudzysłowie, nie śmiem inaczej) na podstawie którego można napisać faktyczną grę.

Do końca konkursu zostało niewiele czasu, bo raptem 3 tygodnie. Aby zamknąć grę razem z zamknięciem konkursu (blogowanie będę kontynuował, niekoniecznie na ten sam temat ;)) skupię się teraz na 2 sprawach:

- dokończeniu silnika kolizji z przeszkodami tak, żeby wpadnięcie na nie powodowało zatrzymanie się gracza
- stworzenie jednoplanszowej prostej gdy, w której trzeba będzie skakać nad przeszkodami i omijać wrogów.

Konfrontując to z MVP jakie założyłem sobie na [samym początku][drugi-wpis] nie jest tak źle i aktualny pomysł nie odbiega dramatycznie od założeń. Dla przypomnienia takie MVP chciałem osiągnąć:

*Oczywiście plany na grę są stosunkowo ambitne, aczkolwiek zadowolę się takowym MVP (Minimal Viable Product):*

- *gra będzie posiadała planszę która porusza się razem z graczem*
- *gracz będzie potrafił skakać*
- *jako przeszkody istnieć będą przepaście zabijające gracza*

Nie tracąc już więcej czasu na wymówki zabieram się dalej za kodowanie, a was zapraszam już teraz na kolejny wpis ;)

[drugi-wpis]: http://zelazowy.github.io/daj-sie-poznac/2016/03/04/DSP-Technologie-Inspiracje.html

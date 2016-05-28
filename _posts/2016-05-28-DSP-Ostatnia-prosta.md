---
layout: post
title:  "DSP: Ostatnia prosta"
date:   2016-05-28 19:04:00 +0200
categories: daj-sie-poznac
short_desc: "Trzeba powoli kończyć grę. Po poprzednim wpisie gra wyglądała już całkiem fajnie, ale nie miała sensu - nie dało się ani wygrać ani przegrać. Kwestia wygranej jest właściwie jasna - nie da się ;) Po prostu gra toczy się aż gracz przegra, tyle. Zostaje w takim razie kwestia przegranej..."
---
Liczba wpisów do końca DPS: 1

Trzeba powoli kończyć grę. Po poprzednim wpisie gra wyglądała już całkiem fajnie, ale nie miała sensu - nie dało się ani wygrać ani przegrać. Kwestia wygranej jest właściwie jasna - nie da się ;) Po prostu gra toczy się aż gracz przegra, tyle. Zostaje w takim razie kwestia przegranej.

Tutaj chciałem wykorzystać doświadczenie nabyte przy pierwszej wersji gry czyli przeciwników i prymitywne wykrywanie kolizji. Przeciwników trzeba jakoś wrzucać do gry i tu przydały się te same mechanizmy które zastosowałem przy generowaniu krajobrazu. Stworzyłem więc kolejną klasę tym razem trzymającą typy przeciwników, dodałem ich obsługę przy ruchu krajobrazu i zastosowałem proste wykrywanie kolizji.

Kod odpowiedzialny za całą obsługę przeciwników wygląda następująco:

```python
class Enemy(object):
    shoe = {
        "type": "shoe",
        "w": 40,
        "h": 40,
        "src": "./assets/shoe.png",
        "y": WINDOW_H - 90,
        "x": WINDOW_W,
        "min_v": 20,
        "max_v": 25,
        "v": 0
    }

    @classmethod
    def add_shoe(cls):
        shoe = cls.shoe.copy()
        shoe["v"] = random.randint(shoe["min_v"], shoe["max_v"])

        return shoe

# Stage:
# [...]
@classmethod
    def move(cls):
        # [...]

        # enemies
        for i, enemy in enumerate(cls.enemies):
            enemy["x"] -= enemy["v"]

            if enemy["x"] + enemy["w"] <= 0:
                del cls.enemies[i]

            cls.check_enemy_hit(enemy)

        # randomly create enemy but no more than n are allowed at the time!
        if 1 > len(cls.enemies):
            elif 2 > random.randint(0, 10):
                cls.enemies.append(Enemy.add_shoe())

    @classmethod
    def check_enemy_hit(cls, enemy):
        hit_from_above = cls.player.y + cls.player.h >= enemy["y"]

        hit_from_front = cls.player.x + cls.player.w >= enemy["x"]

        is_behind = cls.player.x > enemy["x"]

        if hit_from_above and hit_from_front and not is_behind:
            cls.game_over = True
```

Te "kilka" linijek kodu pozwoliło całkiem kompleksowo obsłużyć generowanie i zderzanie się z przeciwnikiem. Wystarczyło już tylko dodać metody które wyświetlą komunikat o przegranej i zastopują grę.

Jako ostatni element dodałem jeszcze punkty które lecą w czasie trwania ruchu gracza, nie ma nic lepszego niż rywalizacja ze swoimi własnymi rekordami ;)

Gra w tej chwili jest już "grywalna" więc jej tworzenie uznaję za "skończone". Wiele się nauczyłem w tym czasie i napisałem bardzo prosty silnik gry, który teraz wystarczy wykorzystać, rozwinąć i wydać stworzoną na nim grę dla ludzi :)

<img src="/images/complete-game.gif"/>

Na podsumowanie będzie jeszcze czas w ostatnim wpisie na który już teraz zapraszam. Będzie podsumowanie i pisania gry i samego blogowania, więc będzie ciekawie :)

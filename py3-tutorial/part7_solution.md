## Abschnitt 7: Lösungen
### Aufgabe 1

```python
class Lehrveranstaltung(object):
    def __init__(self):
        self.kapazitaet = int
        self.anzahl_belegte_plaetze = int
        self.anzahl_freie_plaetze = int

    def maximale_kapazitaet(self):
        self.kapazitaet = 30
        print(
            "Die Kapazität der Lehrveranstaltung beträgt "
            + str(self.kapazitaet)
            + "."
        )

    def belegte_plaetze(self):
        print("Bitte geben Sie die Anzahl belegter Plätze an: ")
        self.anzahl_belegte_plaetze = input()
        print("Derzeit sind " + self.anzahl_belegte_plaetze + " Plätze belegt.")

    def freie_plaetze(self):
        self.anzahl_freie_plaetze = \
            self.kapazitaet - int(self.anzahl_belegte_plaetze)
        print(
            "Die Anzahl an freien Plätzen beträgt: "
            + str(self.anzahl_freie_plaetze)
        )


Sozialpsychologie = Lehrveranstaltung()

Sozialpsychologie.maximale_kapazitaet()
Sozialpsychologie.belegte_plaetze()
Sozialpsychologie.freie_plaetze()
```

[Zurück zu Abschnitt 7](part7.md)
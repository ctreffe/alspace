## Abschnitt 7: Lösungen
### Aufgabe 1

**Aufgabenstellung**: Erstellen Sie eine Klasse "Lehrveranstaltung". Definieren Sie innerhalb 
der __init__()-Methode die Datentypen für die Variablen "kapazitaet",
"anzahl_belegte_plaetze" und "anzahl_freie_plaetze". Erstellen Sie drei 
Methoden der Klasse: "maximale_kapazitaet", "belegte_plaetze" und 
"freie_plaetze". In der ersten Methode soll die maximale Kapazität auf 30
festgelegt werden. In der zweiten Methode soll per Eingabe im Terminal die
aktuelle Anzahl an belegten Plätzen erfasst werden. In der dritten Methode
soll die Anzahl an derzeit verfügbaren Plätzen ausgegeben werden.
Demonstrieren Sie die Funktionalitäten der Klasse, indem Sie das konkrete
Objekt "Sozialpsychologie" erstellen.

**Lösung**: Eingangs wird die Klasse `Lehrveranstaltung` erzeugt und innerhalb der 
`__init__()`-Methode werden die Datentypen für die Variablen definiert. Anschließend wird die 
Methode `maximale_kapazitaet()` definiert. Innerhalb dieser Methode wird dem Klassenattribut 
`kapazitaet` der Wert 30 zugewiesen. Daraufhin wird ein `String` mit der in einen `String` 
transformierten `kapazitaet` ausgegeben. Daraufhin wird die Methode `belegte_plaetze()` definiert. 
Innerhalb dieser Methode wird zunächst nach einer Benutzereingabe der Anzahl an belegten Plätzen 
gefragt. Diese Eingabe wird in dem Klassenattribut `anzahl_belegte_plaetze` gespeichert. Im 
Anschluss wird ein `String` ausgegeben. Im nächsten Schritt wird die Methode `freie_plaetze()` 
definiert. Hierbei werden die belegten Plätze von der Kapazität abgezogen. Hierbei ist zu 
beachten, dass die Variable `anzahl_belegte_plaetze` dem Datentyp `str` entspricht, weil sie der 
Benutzereingabe entspricht. Für die Berechnung muss diese Variable mithilfe der `int()`-Funktion 
in den Datentyp `int` umgewandelt werden. Das Ergebnis dieser Berechnung wird in dem 
Klassenattribut `anzahl_freie_plaetze` gespeichert. Abschließend wird das Objekt 
`Sozialpsychologie` der Klasse `Lehrveranstaltung` erzeugt und die drei Methoden werden aufgerufen.

**Code**:
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
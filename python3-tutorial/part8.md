### Lösung zu Abschnitt 7 Aufgabe 1

```python
class Lehrveranstaltung(object):

    def __init__(self):
        self.kapazitaet = int
        self.anzahl_belegte_plaetze = int
        self.anzahl_freie_plaetze = int

    def maximale_kapazitaet(self):
        self.kapazitaet = 30
        print("Die Kapazität der Lehrveranstaltung beträgt " + str(self.kapazitaet) + ".")

    def belegte_plaetze(self):
        print("Bitte geben Sie die Anzahl belegter Plätze an: ")
        self.anzahl_belegte_plaetze = input()
        print("Derzeit sind " + self.anzahl_belegte_plaetze + " Plätze belegt.")

    def freie_plaetze(self):
        self.anzahl_freie_plaetze = self.kapazitaet - int(self.anzahl_belegte_plaetze)
        print("Die Anzahl an freien Plätzen beträgt: " + str(self.anzahl_freie_plaetze))


Sozialpsychologie = Lehrveranstaltung()

Sozialpsychologie.maximale_kapazitaet()
Sozialpsychologie.belegte_plaetze()
Sozialpsychologie.freie_plaetze()
```
## Abschnitt 8: Objektorientiertes Programmieren in Python - Ausblick

### 8.1 Ausblick

Python als Programmiersprache bringt verschiedene Vorteile gegenüber einfacheren Skriptsprachen (z.B. CLEM):

#### Klassen- und Funktionsdefinitionen

* Durch das Definieren eigener Funktionen und Klassen, egal wie einfach oder komplex, erhöht sich die
  Wiederverwendbarkeit von einmal geschriebenem Code enorm.
* Nach dem Baukastenprinzip lassen sich somit schnell Codeblöcke zusammenstellen, die auch anspruchsvolle Aufgaben
  erledigen können
* Besonders häufig durchgeführte Operationen lassen sich leicht auf verschiedene Kontexte übertragen, wenn man
  objektorientiert plant

#### Fehlerbehandlung

* Anstelle unverständlicher Absturzmeldungen lassen sich eigene Fehlernachrichten erzeugen
* Die Ausführung eines Skriptes kann auch im (vorhergesehenen) Fehlerfall mit entsprechenden Maßnahmen fortgesetzt
  werden
* Reaktion auf bestimmte Fehler WÄHREND der Skriptausführung (nicht durch den Ersteller nach oder vor Ausführung)

#### Drittanbietermodule

* Python kann mit einer großen Menge an Modulen erweitert werden
* Drittanbietermodule erfüllen vielfältige Zwecke:
    * Kommunikation mit speziellen Datenbanktypen (CouchDB, MongoDB)
    * Verarbeitung speziellerer Dateiformate
    * Schnittstellen zu anderen Programmen
    * Erweiterte statistische Analysemethoden
    * Bereitstellung grafischer Benutzeroberflächen
* Durch die Vielfalt an Erweiterungspaketen wird Python zu einer sehr mächtigen Scriptingsprache

[**Zurück zur Startseite**](../python3-tutorial)

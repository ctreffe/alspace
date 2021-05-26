---
layout: py3_tutorial
---

## Abschnitt 7

### 7.1 Klassen

Klassen ermöglichen es in Python genau wie in anderen Programmiersprachen, 
Variablen und Funktionen zu einer sinnvollen Einheit zu verbinden. 
Zu einer Klasse zugeordnete Variablen nennen wir Eigenschaften dieser 
Klasse, die zugeordneten Funktionen nennen wir Methoden der Klasse. 
Eine Klassendeklaration erfolgt in Python mit dem Ausdruck **class**:

```python
class Dataset(object):
    Variable1 = "Teststring"

    def __init__(self):
        print("Initialisierung")
        self.Variable2 = 100

    def funktion_1(self):
        print("Funktion 1 wurde ausgeführt")

    def get_variable_1(self):
        return self.Variable1


testset = Dataset()

testset.funktion_1()

print(str(testset.Variable2))

print(testset.get_variable_1())

```

Im oberen Beispiel zur Erstellung einer einfachen Klasse sind mehrere Dinge zu beachten:

* Die Deklaration der Klasse enthält **class**, dann den Namen der 
  Klasse und schließlich den übergeordneten Objekttyp, aus dem sich die 
  Klasse ableitet
* Einfache Klassen leiten sich immer von **object** ab
* Um ein konkretes Objekt aus einer Klasse zu Erstellen, muss die Klasse
  initialisiert werden. Das geschieht, wenn die Klasse im folgenden 
  Skript einem Variablennamen zugeordnet wird 
  (Klassenname gefolgt von runden Klammern)
* Jede Klasse hat eine Methode **__init__()**, die beim Initialisieren 
  der Klasse ausgeführt wird
* Methoden in Klassen erhalten als Parameter mindestens **self**. Das 
  ist eine Referenz auf die Instanz der Klasse, die die Methode 
  aufgerufen hat. Dies ist ein technisches Detail, welches nur bei der 
  Erstellung von Klassen eine Rolle spielt und die Methoden ansonsten 
  nicht beeinflusst
* Klasseneigenschaften werden innerhalb von Methoden mit vorangestelltem
  **self.** erzeugt. Dadurch sind sie in allen
  Methoden der Klasse und auch von außerhalb der Klasse abrufbar

Methoden und Eigenschaften von Klassen bzw. Objekten unterscheiden sich 
ansonsten nicht von herkömmlichen Funktionen und Variablen in Python.


### Aufgabe 1 zu Abschnitt 7

**Erstellen Sie eine Klasse "Lehrveranstaltung". Definieren Sie innerhalb 
der __init__()-Methode die Datentypen für die Variablen "kapazitaet",
"anzahl_belegte_plaetze" und "anzahl_freie_plaetze". Erstellen Sie drei 
Methoden der Klasse: "maximale_kapazitaet", "belegte_plaetze" und 
"freie_plaetze". In der ersten Methode soll die maximale Kapazität auf 30
festgelegt werden. In der zweiten Methode soll per Eingabe im Terminal die
aktuelle Anzahl an belegten Plätzen erfasst werden. In der dritten Methode
soll die Anzahl an derzeit verfügbaren Plätzen ausgegeben werden.
Demonstrieren Sie die Funktionalitäten der Klasse, indem Sie das konkrete
Objekt "Sozialpsychologie" erstellen.**

<div class="d-grid gap-2 d-md-block">
  <a href="part6" class="btn btn-secondary btn-sm" tabindex="1" role="button" aria-disabled="true">Zurück zu Abschnitt 6</a>

  <a href="part7_hints" class="btn btn-secondary btn-sm" tabindex="2" role="button" aria-disabled="true">Hinweise zu den Aufgaben</a>

  <a href="part7_solution" class="btn btn-secondary btn-sm" tabindex="3" role="button" aria-disabled="true">Lösungen zu den Aufgaben</a>

  <a href="part8" class="btn btn-primary btn-sm" tabindex="4" role="button" aria-disabled="true">Weiter zu Abschnitt 8</a>
</div>
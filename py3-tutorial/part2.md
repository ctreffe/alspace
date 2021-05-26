---
layout: py3_tutorial
---

## Abschnitt 2

Im Folgenden werden wir, analog zum Buch **Einstieg in Python**, ein eigenes Spiel entwickeln, 
welches wir Schritt für Schritt um neue Konzepte der Programmiersprache Python erweitern. 
Hierzu können Sie entweder in dem zuvor erstellten oder einem neuen Ordner in PyCharm eine neue 
Python-Datei namens "spiel" anlegen.

### 2.1 Variablen und Operatoren

Wir können verschiedene Werte in Variablen speichern und damit Berechnungen durchführen. 
Die Zuweisung von Werten zu Variablennamen erfolgt mit dem Operator **=**:

```python

a = 3
b = 2

c = a+b
```

Um das Ergebnis unserer Berechnung zu betrachten, benutzen wir den bereits bekannten Befehl **print()**:

```python
a = 3
b = 2

c = a+b

print(c)
```

Die Konsole zeigt uns nun das Ergebnis unserer Berechnung an. Wir können mit dem Operator **+** 
aber nicht nur Zahlen addieren, sondern auch mehrere Zeichenketten oder Zeichenketten 
mit Variablen, die wiederum Zeichenketten enthalten, verbinden. 
Dazu muss das Ergebnis unserer Berechnung, welches in **c** als Ganzzahl vorliegt, 
jedoch umgewandelt werden in eine Zeichenkette (engl. String). 
Hierzu verwenden wir die Funktion **str()**, die verschiedene Arten von Variablen in Strings umwandelt:

```python
a = 3.5
b = 2

c = a+b

print("Ergebnis der Berechnung: " + str(c))
```

Erfolgt keine Umwandlung vor der Verbindung der ganzzahligen Variable **c** mit dem 
gewünschten String, erhalten wir folgende Fehlermeldung:

```
TypeError: can only concatenate str (not "int") to str
```

Neben dem Operator **+** stehen uns für Berechnungen bei Zahlenvariablen 
natürlich auch **\***,**\\** und **-** zur Verfügung. 

Wie wir an der Fehlermeldung sehen, hat eine Zeichenkette als Variable den 
Typ **str** (kurz für String), während eine Ganzzahl den Typ **int** (kurz für Integer) hat. 
Fließkommazahlen wiederum haben den Typ **float**.

Wie wir an **c** sehen, lässt sich anstatt von festen Werten auch das Ergebnis einer Operation 
in eine Variable speichern. Die Variable hat dann als Variablentyp den Typ des Ergebnisses der 
Operation. Den Typ einer beliebigen Variablen können wir mit der Funktion **type()** herausfinden:

```python
a = 3.5
b = 2

c = a + b  # c hat nun den Typ float

print(type(c))

a = "Hello "
b = "World"

c = a + b  # c hat nun den Typ str

print(type(c))
```

Im obigen Beispiel lassen wir das Ergebnis eines Funktionsaufrufs (type()) direkt durch eine 
weitere Funktion (print()) verarbeiten. Solche Verschachtelungen von Funktionen sind in Python 
kein Problem.

Wir können das Ergebnis eines Funktionsaufrufs genau so wie das Ergebnis einer Operation direkt in 
eine Variable speichern:

```python
c = type("Teststring")

print(c)
```

Wir haben also das Ergebnis des Funktionsaufrufs von **type()** in **c** gespeichert, welches sich 
dann einfach mit dem Printbefehl ausgeben lässt. Hierbei ist zu beachten, dass nicht jede Funktion 
einen sinnvoll druckbaren Rückgabewert liefert. Im Falle von **type()** wird uns aber ein Wert 
geliefert, der per **print()** automatisch in einen String umwandeln und gut ausgeben lässt. 
Der Rückgabewert von Type lässt sich übrigens nicht mit anderen Strings durch den Operator **+** 
verbinden!

### Aufgabe 1 zu Abschnitt 2

**Schreiben Sie ein Skript, welches eine von Ihnen eingegebene Zahl zur Ganzzahl 12 addiert. 
Geben Sie das Ergebnis der Addition und den Variablentyp des Ergebnisses mit der Funktion print() 
aus.**

### Aufgabe 2 zu Abschnitt 2

**Schreiben sie ein Skript, welches sie auffordert, zwei beliebige Ganzzahlen zu addieren 
(Sie können die Werte dieser Ganzzahlen selbst festlegen). Fordern Sie zur Eingabe des korrekten 
Ergebnisses auf. Geben Sie sowohl das eingegebene Ergebnis als auch das tatsächlich korrekte 
Ergebnis in die Konsole.**

<div class="d-grid gap-2 d-md-block">
  <a href="part1" class="btn btn-secondary btn-sm" tabindex="1" role="button" aria-disabled="true">Zurück zu Abschnitt 1</a>

  <a href="part2_hints" class="btn btn-secondary btn-sm" tabindex="2" role="button" aria-disabled="true">Hinweise zu den Aufgaben</a>

  <a href="part2_solution" class="btn btn-secondary btn-sm" tabindex="3" role="button" aria-disabled="true">Lösungen zu den Aufgaben</a>

  <a href="part3" class="btn btn-primary btn-sm" tabindex="4" role="button" aria-disabled="true">Weiter zu Abschnitt 3</a>
</div>
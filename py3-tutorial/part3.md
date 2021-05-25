---
layout: py3_tutorial
---

## Abschnitt 3: Basiskonzepte des Programmierens

### 3.1 Zusatzmodule

Die Standarddistribution kommt mit einer Reihe von Modulen, deren Funktionalität wir nutzen können. 
Es gibt z.B. Module zur Bearbeitung von verschiedenen Dateiformaten, Module zur Durchführung 
komplexer mathematischer Berechnungen, oder auch Module zur Interaktion mit dem Betriebssystem. 
Je nach Aufgabe unseres Skripts ist es sinnvoll, einzelne dieser Zusatzmodule zu laden. Hierzu 
verwenden wir **import** Anweisungen zu Beginn unseres Skripts:

```python
import random  # Laden des Zusatzmoduls für Zufallszahlen

a = random.randint(1, 100)
b = random.randint(1, 100)

print(a + b)
```

Im obigen Beispiel laden wir das Zusatzmodul **random**, welches unter anderem Funktionen zur 
Generierung von Zufallszahlen bereitstellt

### 3.2 Vergleichsoperatoren

Bisher waren die von uns erstellten Skripte alle statisch und eindimensional. 
Unabhängig von allen Einflussfaktoren tut jedes unserer bisherigen Skripte immer dasselbe. 
In aller Regel müssen Pythonskripte aber dynamisch auf verschiedene veränderbare Einflussfaktoren 
reagieren, d.h. Benutzereingaben oder vorhandene Daten müssen abgeglichen und bewertet werden.

Zur Durchführung von Abgleichen gibt es in Python die üblichen Vergleichsoperatoren:

* \> größer als
* < kleiner als
* \>= größer gleich
* <= kleiner gleich
* == gleich
* != ungleich

Das Ergebnis einer Vergleichsoperation ist eine boolsche Variable, welche den Wert **True** oder
**False** annehmen kann, je nach Ergebnis des Vergleichs:

```python
a = 4
b = 3

print(a == b)

print(a > b)
```

Das Ergebnis einer Vergleichsoperation können wir ebenfalls wieder in eine Variable speichern:

```python
a = 4
b = 3

c = a == b

print(c)
```

Man beachte im obigen Beispiel das einfache **=** als Zuweisung eines Wertes zu einem 
Variablennamen und das doppelte **==** als Vergleichsoperator. Eine Verwechslung führt in aller 
Regel zu einem Syntaxfehler und somit zum Abbruch der Skriptausführung.

### 3.3 Verzweigungen

Um nun auf das Ergebnis von Vergleichsoperationen reagieren zu können, lassen sich Verzweigungen 
mittels If-Anweisungen in unsere Skripte einbauen. Dabei wird ein bestimmter Codeblock nur dann 
ausgeführt, wenn eine spezifische Vergleichsoperation das erwartete Ergebnis liefert:

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = a + b

if c > 100:
    print("Das Ergebnis ist größer als 100")
else:
    print("Das Ergebnis ist kleiner oder gleich 100")
```

Wenn im obigen Beispiel also **c** größer wird als 100, erfolgt eine andere Ausgabe, als in allen 
anderen Fällen. Die Syntax einer If-Anweisung erfolgt immer nach demselben Muster:

1. if
2. Vergleichsoperation
3. :

Der folgende Codeblock wird um eine Stufe eingerückt. 
Alle folgenden eingerückten Codezeilen werden nur bei Erfüllung der Vergleichsoperation, d.h. wenn 
diese True zurückliefert, ausgeführt. Der Codeblock endet, sobald auch die Einrückung endet.

Wir können auch mehrere Verzweigungen verschachteln. Da Python aber die Einrückungen interpretiert,
muss auf deren Korrektheit besonders geachtet werden:

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = a + b

if c > 100:
    if c > 125:
        print("Das Ergebnis ist größer als 125")
    else:
        print("Das Ergebnis liegt zwischen 101 und 125")
else:
    print("Das Ergebnis ist kleiner oder gleich 100")
```

Neben Verschachtelungen der Anweisungen **if** und **else** lässt sich eine Mehrfachverzweigung 
auch mit **elif** realisieren:

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = a + b

if c > 125:
    print("Das Ergebnis ist größer als 125")
elif c > 100:
    print("Das Ergebnis liegt zwischen 101 und 125")
else:
    print("Das Ergebnis ist kleiner oder gleich 100")
```

### Aufgabe 1 zu Abschnitt 3

**Erstellen Sie ein Skript, welches den:die Benutzer:in auffordert, zwei Zufallszahlen zwischen 1 und 100 
zu addieren, die sie ihm anzeigen. Die Benutzereingabe soll dann mit der korrekten Lösung 
verglichen werden. Melden Sie dem:der Benutzer:in zusammen mit seiner eigenen Eingabe zurück, 
ob seine:ihre eingegebene Lösung korrekt ist oder nicht. Dem:Der Benutzer:in soll die korrekte Lösung ebenfalls 
angezeigt werden.**

<div class="d-grid gap-2 d-md-block">
  <a href="part2" class="btn btn-secondary btn-sm" tabindex="1" role="button" aria-disabled="true">Zurück zu Abschnitt 2</a>

  <a href="part3_hints" class="btn btn-primary btn-lg" tabindex="2" role="button" aria-disabled="true">Hinweise zu den Aufgaben</a>

  <a href="part3_solution" class="btn btn-primary btn-lg" tabindex="3" role="button" aria-disabled="true">Lösungen zu den Aufgaben</a>

  <a href="part4" class="btn btn-secondary btn-sm" tabindex="4" role="button" aria-disabled="true">Weiter zu Abschnitt 4</a>
</div>

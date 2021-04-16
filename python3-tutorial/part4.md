### Lösung zu Abschnitt 3 Aufgabe 1

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = a + b

print("Bitte rechnen Sie die folgende Aufgabe: " + str(a) + " + " + str(b) + ": ")
eingabe = input()

print("Ihre Eingabe: " + str(eingabe))

if int(eingabe) == c:
    print("Ihre eingegebene Lösung ist korrekt!")
else:
    print("Leider ist die eingegebene Lösung nicht korrekt. Die korrekte Lösung lautet: " + str(c))
```

## Abschnitt 4

### Abschnitt 4.1 Verbindung von Vergleichsoperationen

Wir können durch ein paar Erweiterungen auch komplexere Vergleichsoperationen als die bisherigen 
einfachen Vergleiche durchführen:

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = (a + b) / 2

check = 1 <= c < a + b  # Das Ergebnis der Berechnung liegt zwischen zwei Grenzwerten

print(check)

```

Die Variable check im oberen Beispiel ergibt immer **True**. Neben der Verknüpfung mehrerer Vergleichsoperatoren in einem einzigen Vergleich lassen sich auch mehrere Vergleichsoperationen mit den Operatoren **and** und **or** miteinander verbinden:

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = (a + b) / 2

check = 1 <= c and c < a + b  # Das Ergebnis der Berechnung liegt zwischen zwei Grenzwerten

print(check)
```

Das obige Beispiel liefert dasselbe Ergebnis wie das Skript davor, nur dass jetzt die 
komplexe Vergleichsoperation in zwei einfache Vergleichsoperationen aufgeteilt wurde. 
Mit dem Operator **not** lassen sich Vergleiche zusätzlich umkehren:

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = (a + b) / 2

check = not (1 <= c and c < a + b)  # Das Ergebnis der Berechnung liegt zwischen NICHT zwei Grenzwerten

print(check)
```

Nun liefert uns das Skript immer wieder den Wert False. Die Klammern helfen bei der Vereinfachung 
der Vergleichsoperation. Andernfalls müsste **not** vor jeder Vergleichsoperation separat 
gesetzt werden:

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = (a + b) / 2

check = not 1 <= c and not c < a + b  # Das Ergebnis der Berechnung liegt zwischen NICHT zwei Grenzwerten

print(check)
```

### Abschnitt 4.2 Schleifen

Schleifen ermöglichen es uns Codeblöcke wiederholt auszuführen. 
Die Anzahl der Wiederholungen (Iterationen) kann dabei im Vorfeld 
festgelegt sein oder dynamisch bestimmt werden. In Python gibt es 
zwei Arten von Schleifen:

* Die **for** Schleife
* Die **while** Schleife

#### Die **for** Schleife

Mit **for** können wir einen Codeblock wiederholt durchführen, 
wobei wir die Anzahl der Wiederholungen festlegen. In der folgenden 
Schleife verwenden wir die Funktion **range()**, die uns eine 
Zahlenfolge generiert. Die Zahlenfolge beginnt dabei mit 0 und endet 
immer mit der Ganzzahl unter der angegebenen Zahl. Das ist zunächst 
etwas verwirrend, allerdings haben wir so exakt 10 Durchläufe der 
for-Schleife, entsprechend dem in range() angegebenen Wert.

```python
for i in range(10):
    print("Die neue Zahl:")
    print(str(i))
```

Wie wir sehen wird nicht nur der Codeblock in der Schleife wiederholt 
ausgeführt. Die Variable i durchläuft die von **range()** erzeugte 
Zahlenfolge. Wir können auch eigene Zahlenfolgen festlegen. 
Hierzu nutzen wir einen neuen Variablentyp, die Liste:

```python
for i in [1, 2, 3, 4, 7, 8, 9]:
    print("Die neue Zahl:")
    print(str(i))
```

Die Variable **i** durchläuft nun mit jeder Ausführung des Codeblocks in
der Schleife unsere vordefinierte Liste. Listen können auch andere 
Variablentypen und gemischte Variablentypen enthalten. **i** durchläuft 
also die Liste, unabhängig von den enthaltenen Variablen:

```python
for i in ["test", 2, 3, "mitte", 7, 8, "ende"]:
    print("Die neue Zahl:")
    print(str(i))
```

Wir können nun auch Verzweigungen mit Schleifen verbinden. Im folgenden 
Beispiel werden Listenelemente nur in die Konsole geschrieben, wenn es 
sich um Strings handelt. In allen anderen Fällen kommt die Anweisung 
**pass** zum Einsatz, die einfach einen leeren Codeblock darstellt und 
ein Überspringen dieses Codeblocks bewirkt. **pass** kann so z.B. in 
unfertigen Skripten als Platzhalter für spätere Codeblöcke verwendet 
werden:

```python
for i in ["Hello", 2, 3, 9, 7, 8, "World!"]:
    if type(i) == str:
        print(i)
    else:
        pass
```

Normalerweise laufen for-Schleifen so lange, bis die vorgegebene Anzahl 
an Durchläufen erreicht ist. Wir können eine Schleife mithilfe der 
**break** Anweisung auch vorzeitig abbrechen. Die folgende Schleife 
wird abgebrochen, sobald ein Element in der Liste den Variablentyp str 
aufweist:

```python
for i in [1, 2, 3, 9, 7, 8, "Hello", "World!", 10, 11]:
    if type(i) == str:
        break

    print("Zahl: " + str(i))
```

Wie wir sehen wird die Printanweisung nicht mehr ausgeführt, sobald die 
Variable i den Wert "Hello" annimmt. Die Schleife wurde abgebrochen. 
Eine weitere wichtige Anweisung in Schleifen ist **continue**, welche 
dazu führt, dass die aktuelle Ausführung des Schleifen-Codeblocks 
abgebrochen wird, die Schleife aber sofort mit dem nächsten Element von 
vorne beginnt.

Das folgende Beispiel unterscheidet sich vom vorherigen Codeblock nur 
dadurch, dass wir **break** durch **continue** ersetzen:

```python
for i in [1, 2, 3, 9, 7, 8, "Hello", "World!", 10, 11]:
    if type(i) == str:
        continue

    print("Zahl: " + str(i))
```

Wie wir sehen wird die Schleife nun vollständig durchlaufen, da die 
Zahlen 10 und 11 erscheinen. Die Strings in der Liste werden 
aber ausgelassen, da hier die **continue** Anweisung greift.

#### Die **while** Schleife

Während die for-Schleife eine bestimmte Anzahl von Wiederholungen 
durchläuft, z.B. bei der Iteration über eine Liste, kann ein Codeblock 
in einer **while**-Schleife so lange wiederholt werden, bis ein 
bestimmtes Abbruchkriterium eintritt. So können wir z.B. Zahlen so 
lange addieren, bis das Ergebnis einen bestimmten Grenzwert übersteigt:

```python
import random

x = 0

while x < 1000:
    print("Aktuelles Ergebnis: " + str(x))
    y = random.randint(1, 100)
    x = x + y

```

Wenn der obige Codeblock mehrfach ausgeführt wird, sehen wir, dass die 
Anzahl der Wiederholungen unter der Schleife variiert, je nachdem welche
Zufallszahlen gezogen werden. Sobald **x** aber den Wert 1000 
übersteigt, wird die Schleife beendet.

Häufig werden auch Boolvariablen benutzt, um while-Schleifen zu steuern.
Im folgenden Beispiel werden so lange zwei Zufallszahlen gezogen, bis 
zweimal die gleiche Zufallszahl gezogen wurde:

```python
import random

even = False

while not even:
    x = random.randint(1, 10)
    y = random.randint(1, 10)

    print("Wert von x: " + str(x) + " Wert von y: " + str(y))

    if x == y:
        even = True
```

### Aufgabe 1 zu Abschnitt 4

**Erweitern Sie das Skript aus der Aufgabe zu Abschnitt 2.2 um eine 
while-Schleife, sodass der Benutzer seine / die Benutzerin ihre Eingabe 
so lange wiederholen muss, bis er das korrekte Ergebnis eingegeben hat.**

### Aufgabe 2 zu Abschnitt 4

**Erweitern Sie das Skript aus der vorherigen Aufgabe um eine 
for-Schleife, sodass der:die Benutzer:in zunächst angeben 
muss, wie viele Aufgaben er bearbeiten möchte. In der Folge soll der:die 
Benutzer:in dann eine entsprechende Anzahl aufgaben bearbeiten müssen. 
Alle anderen Teile des Skriptes sollen dabei bestehen bleiben.**

[Hinweise zu den Aufgaben](exercise-hints.md)

[**Weiter zu Abschnitt 5**](part5.md)
## Abschnitt 4: Lösungen
### Aufgabe 1

**Aufgabenstellung**: Erweitern Sie das Skript aus der Aufgabe 2 zu Abschnitt 2 um eine 
while-Schleife, sodass der:die Benutzer:in seine:ihre Eingabe so lange wiederholen muss, 
bis er:sie das korrekte Ergebnis eingegeben hat. Die Variablen a und b sollen ganzzahligen 
Zufallszahlen zwischen 1 und 100 entsprechen.

**Lösung**: Damit die `while`-Schleife eingangs ausgeführt wird, wird die Variable `correct` 
zunächst der Wert `False` zugewiesen. Anschließend wird nach der Ausgabe der Aufgabenstellung die 
`while`-Schleife eingefügt. Diese wird mit dem Operator `not` versehen, weil die Schleife solange
ausgeführt werden soll bis die Variable `correct` den Wert `True` hat. Da `correct` nur dann 
`True` sein soll, wenn die korrekte Lösung eingegeben wurde, wird der Variable der Wert `True` 
erst nach Zutreffen der Übereinstimmung von der korrekten Lösung (`c`) und der Benutzereingabe 
(`eingabe`) zugewiesen. Folglich wird die `while`-Schleife nicht mehr ausgeführt, wenn die 
korrekte Lösung eingegeben wurde.

**Code**:
```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = a + b
correct = False

print(
    "Bitte rechnen Sie die folgende Aufgabe: " + str(a) + " + " + str(b) + ": "
)

while not correct:
    eingabe = input()
    print("Ihre Eingabe: " + str(eingabe))

    if int(eingabe) == c:
        print("Ihre eingegebene Lösung ist korrekt!")
        correct = True
    else:
        print(
            "Ihre eingegebene Lösung ist falsch! Bitte versuchen sie es erneut:"
        )
```

### Aufgabe 2

**Aufgabenstellung**: Erweitern Sie das Skript aus der vorherigen Aufgabe um eine 
for-Schleife, sodass der:die Benutzer:in zunächst angeben 
muss, wie viele Aufgaben er:sie bearbeiten möchte. In der Folge soll der:die 
Benutzer:in dann eine entsprechende Aufgabenanzahl bearbeiten müssen. 
Alle anderen Teile des Skriptes sollen dabei bestehen bleiben.

**Lösung**: Um zu erfragen, wie viele Aufgaben der:die Benutzer:in bearbeiten möchte, wird 
zunächst ein `String` mithilfe der `print()`-Funktion ausgegeben. Die Benutzereingabe wird 
anhand der `input()`-Funktion in die Variable `aufgabenanzahl` gespeichert. Anschließend wird die 
`for`-Schleife eingefügt. Hierbei wird die Anzahl an Wiederholungen des nachfolgenden Codeblocks 
mithilfe der `range()`-Funktion bestimmt. Da der Codeblock so oft ausgeführt werden soll, wie 
eingangs von dem:der Benutzer:in angegeben, soll die Wiederholungsanzahl der `aufgabenanzahl` 
entsprechen. Da die `aufgabenanzahl` initial dem Datentyp `str` angehört, muss diese in den 
Datentyp `int` mithilfe der `int()`-Funktion transformiert werden.

**Code**:
```python
import random

print("Wie viele Aufgaben wollen Sie berechnen? Bitte eingeben:")

aufgabenzahl = input()

for i in range(int(aufgabenzahl)):

    a = random.randint(1, 100)
    b = random.randint(1, 100)

    c = a + b
    correct = False

    print(
    "Bitte rechnen Sie die folgende Aufgabe: " + str(a) + " + " + str(b) + ": "
    )

    while not correct:
        eingabe = input()
        print("Ihre Eingabe: " + str(eingabe))

        if int(eingabe) == c:
            print("Ihre eingegebene Lösung ist korrekt!")
            correct = True
        else:
            print(
                "Ihre eingegebene Lösung ist falsch! Bitte versuchen sie es erneut:"
            )
```

[Zurück zu Abschnitt 4](part4.md)
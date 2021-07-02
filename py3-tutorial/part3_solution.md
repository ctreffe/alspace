## Abschnitt 3: Lösungen
### Aufgabe 1

**Aufgabenstellung**: Erstellen Sie ein Skript, welches den:die Benutzer:in auffordert, zwei 
angezeigte Zufallszahlen zwischen 1 und 100 zu addieren. Die Benutzereingabe soll dann 
mit der korrekten Lösung verglichen werden. Melden Sie dem:der Benutzer:in zusammen mit 
seiner:ihrer eigenen Eingabe zurück, ob seine:ihre eingegebene Lösung korrekt ist oder nicht. 
Dem:Der Benutzer:in soll die korrekte Lösung ebenfalls angezeigt werden.

**Lösung**: Zur Lösung dieser Aufgabe muss zunächst das `random`-Modul am Anfang des Skriptes 
importiert werden. Anschließend werden zwei `int`-Zufallszahlen zwischen 1 und 100 mithilfe der 
Funktion `randint()` des Moduls `random` erzeugt und in den Variablen `a` und `b` gespeichert.
Daraufhin wird das Ergebnis der Addition dieser beiden ganzzahligen Zufallszahlen in der Variable 
`c` gespeichert. Damit der:die Benutzer:in weiß, welche Zahlen addiert werden sollen, wird ihm:ihr 
mithilfe der `print()`-Funktion die Aufgabenstellung auf der Console angezeigt. Hierbei ist zu 
beachten, dass die beiden Zufallszahlen vom Datentyp `int` zunächst in den Datentyp `str` 
umgewandelt werden müssen, um sie auszugeben. Abschließend erfolgt mithilfe des 
`if...else`-Statements die Prüfung, ob die eingegebene Lösung korrekt ist. Hierfür wird 
mithilfe des Vergleichsoperators `==` geprüft, ob die anhand der `input()`-Funktion in die 
Variable `eingabe` gespeicherte Benutzereingabe mit dem zuvor berechneten korrekten Lösung (`c`) 
übereinstimmt. Sofern `c` und `eingabe` übereinstimmen, wird 
`Ihre eingegebene Lösung ist korrekt!` ausgegeben. Trifft dies nicht zu, wird 
`Leider ist die eingegebene Lösung nicht korrekt. Die korrekte Lösung lautet:` mit der korrekten 
Lösung ausgegeben. Hierbei ist erneut zu beachten, dass die Variable `c` vom Datentyp `int` für 
die Ausgabe zunächst in den Datentyp `str` umgewandelt werden muss.

**Code**:
```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = a + b

print(
    "Bitte rechnen Sie die folgende Aufgabe: "
    + str(a)
    + " + "
    + str(b)
    + ": "
)
eingabe = input()

print("Ihre Eingabe: " + str(eingabe))

if int(eingabe) == c:
    print("Ihre eingegebene Lösung ist korrekt!")
else:
    print(
        "Leider ist die eingegebene Lösung nicht korrekt. "
        "Die korrekte Lösung lautet: "
        + str(c)
    )
```

[Zurück zu Abschnitt 3](part3.md)
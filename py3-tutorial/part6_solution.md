## Abschnitt 6: Lösungen
### Aufgabe 1

**Aufgabenstellung**: Erstellen Sie eine Funktion, die zwei Zahlenwerte zufällig durch eine 
der vier Grundrechenarten miteinander verknüpft. In einem Skript soll 
ein:e Nutzer:in zunächst zwei Zahlen (mit Kontrolle auf richtige Eingabe) eingeben. 
Diese Zahlen sollen dann die Funktion durchlaufen. Die Funktion soll mittels print() Befehl den 
Typ der Berechnung melden und als Returnwert das Ergebnis der Berechnung 
zurückgeben. Dieses Ergebnis soll dem:der Benutzer:in am Ende angezeigt werden.

**Lösung**: Nach dem Import des Moduls `random` wird die neue, selbstgeschriebene 
Funktion `random_rechner()` definiert. Die Funktion erhält zunächst die beiden undefinierten 
Parameter `zahl1` und `zahl2`. Innerhalb der Funktion wird zunächst mithilfe der Funktion 
`randint()` zufällig eine ganze Zahl zwischen 1 und 4 ausgewählt und in die Variable `selector` 
gespeichert. Anschließend wird jeder der vier möglichen Werte der Variable `selector` innerhalb 
des `if...elif...elif...elif`-Statements berücksichtigt. In Abhängigkeit der Zufallszahl wird ein 
unterschiedlicher `String` mithilfe der `print()`- Funktion ausgegeben, eine der vier 
Grundrechenarten durchgeführt und das Ergebnis anhand von `return` zurückgegeben.
Nach der Funktionsdefinition wird eine leere Liste in der Variable `values` gespeichert, welche 
später zum Einsatz kommt. Anschließend wird mithilfe einer `for`-Schleife zweimal um die Eingabe 
einer Zahl gebeten. Nach jeder Eingabe erfolgt die bereits bekannte Prüfung der Eingabe. 
Allerdings ist hinzugekommen, dass die Eingabe sofern sie ganzzahlig ist, an die zuvor erstellte 
Liste `values` angefügt wird. Abschließend wird die zu Beginn erstellte Funktion mit den beiden in 
der `values`-Liste gespeicherten Zahlen als Parameter aufgerufen. Da `random_rechner()` das 
Ergebnis der Rechnung zurückgibt, wird der Wert dieser Funktion der Variable `ergebnis` zugewiesen. 
Zum Schluss wird ein `String` mit der in einen `str`-Datentyp transformierten Variable `ergebnis` 
ausgegeben.

**Code**:
```python
import random


def random_rechner(zahl1, zahl2):
    selector = random.randint(1, 4)

    if selector == 1:
        print("Eine Addition wird durchgeführt")
        return zahl1 + zahl2

    elif selector == 2:
        print("Eine Subtraktion wird durchgeführt")
        return zahl1 - zahl2

    elif selector == 3:
        print("Eine Multiplikation wird durchgeführt")
        return zahl1 * zahl2

    elif selector == 4:
        print("Eine Division wird durchgeführt")
        return zahl1 / zahl2


values = []

for i in range(2):
    print("Bitte geben sie eine " + str(i + 1) + ". Zahl ein:")

    good_inp = False
    while not good_inp:
        eingabe = input()
        try:
            int(eingabe)
            values.append(eingabe)
            good_inp = True
        except:
            print("Fehleingabe! Bitte geben Sie einen gültigen Wert ein:")

ergebnis = random_rechner(int(values[0]), int(values[1]))

print("Das Ergebnis der Berechnung: " + str(ergebnis))
```

### Aufgabe 2

**Aufgabenstellung**: Verändern Sie das Skript aus Aufgabe zwei des vorangegangenen 
Abschnitts so, dass die Benutzereingabe mit der anschließenden 
Validierung (while-Schleife mit darin verschachteltem try except Block) 
in eine Funktion ausgelagert wird, die nur eine korrekte Benutzereingabe
zurückliefert

**Lösung**: Eingangs wird die selbstgeschriebene Funktion `valid_input()` definiert. Innerhalb der 
Funktion wird der zuvor für die Validierung geschriebene Code eingefügt. Im Falle von validen 
Input wird dieser (in der Variable `eingabe` gespeichert) zurückgegeben. Die Funktion 
`valid_input()` wird innerhalb der `while`-Schleife aufgerufen.

**Code**:
```python
import random


def valid_input():
    good_inp = False

    while not good_inp:
        eingabe = input()
        try:
            int(eingabe)
            good_inp = True
        except:
            print("Fehleingabe! Bitte geben Sie einen gültigen Wert ein:")

    return eingabe


a = random.randint(1, 100)
b = random.randint(1, 100)
c = random.randint(1, 100)
d = random.randint(1, 100)
e = random.randint(1, 100)
f = random.randint(1, 100)

liste = [(a, b), (c, d), (e, f)]

for i in liste:

    correct = False

    print(
        "Bitte rechnen Sie die folgende Aufgabe: "
        + str(i[0])
        + " + "
        + str(i[1])
        + ": "
    )

    while not correct:

        eingabe = valid_input()

        print("Ihre Eingabe: " + str(eingabe))

        if int(eingabe) == i[0] + i[1]:
            print("Ihre eingegebene Lösung ist korrekt!")
            correct = True
        else:
            print(
                "Ihre eingegebene Lösung ist falsch! "
                "Bitte versuchen Sie es erneut:"
            )
```

[Zurück zu Abschnitt 6](part6.md)

## Abschnitt 6: Lösungen
### Aufgabe 1

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

    print("Bitte rechnen Sie die folgende Aufgabe: " + str(i[0]) + " + " + str(i[1]) + ": ")

    while not correct:

        eingabe = input()

        print("Ihre Eingabe: " + str(eingabe))

        if int(eingabe) == i[0] + i[1]:
            print("Ihre eingegebene Lösung ist korrekt!")
            correct = True
        else:
            print("Ihre eingegebene Lösung ist falsch! Bitte versuchen Sie es erneut:")
```

[Zurück zu Abschnitt 6](part6.md)

[**Weiter zu Abschnitt 7**](part7.md)

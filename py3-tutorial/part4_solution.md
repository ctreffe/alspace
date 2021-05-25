## Abschnitt 4: Lösungen
### Aufgabe 1

```python
import random

a = random.randint(1, 100)
b = random.randint(1, 100)

c = a + b
correct = False

print("Bitte rechnen Sie die folgende Aufgabe: " + str(a) + " + " + str(b) + ": ")

while not correct:
    eingabe = input()
    print("Ihre Eingabe: " + str(eingabe))

    if int(eingabe) == c:
        print("Ihre eingegebene Lösung ist korrekt!")
        correct = True
    else:
        print("Ihre eingegebene Lösung ist falsch! Bitte versuchen sie es erneut:")
```

### Aufgabe 2

```python
import random

print("Wie viele Aufgaben wollen Sie berechnen? Bitte eingeben:")

aufgabenzahl = input()

for i in range(int(aufgabenzahl)):

    a = random.randint(1, 100)
    b = random.randint(1, 100)

    c = a + b
    correct = False

    print("Bitte rechnen Sie die folgende Aufgabe: " + str(a) + " + " + str(b) + ": ")

    while not correct:
        eingabe = input()
        print("Ihre Eingabe: " + str(eingabe))

        if int(eingabe) == c:
            print("Ihre eingegebene Lösung ist korrekt!")
            correct = True
        else:
            print("Ihre eingegebene Lösung ist falsch! Bitte versuchen sie es erneut:")
```

[Zurück zu Abschnitt 4](part4.md)
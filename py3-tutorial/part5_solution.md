## Abschnitt 5: Lösungen
### Aufgabe 1

```python
import random

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
        eingabe = input()
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

### Aufgabe 2

```python
import random

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

        good_inp = False
        while not good_inp:
            eingabe = input()
            try:
                int(eingabe)
                good_inp = True
            except:
                print("Fehleingabe! Bitte geben Sie einen gültigen Wert ein:")

        print("Ihre Eingabe: " + str(eingabe))

        if int(eingabe) == i[0] + i[1]:
            print("Ihre eingegebene Lösung ist korrekt!")
            correct = True
        else:
            print(
                "Ihre eingegebene Lösung ist falsch!  "
                "Bitte versuchen Sie es erneut:"
            )
```

[Zurück zu Abschnitt 5](part5.md)
## Abschnitt 3: Lösungen
### Aufgabe 1

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
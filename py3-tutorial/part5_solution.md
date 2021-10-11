## Abschnitt 5: Lösungen
### Aufgabe 1

**Aufgabenstellung**: Bauen Sie das Skript aus Aufgabe 1 zum letzten Abschnitt so um, dass 
der:die Benutzer:in nun 3 Aufgaben bearbeiten muss. 
Sie können hierfür eine for-Schleife verwenden. Lassen Sie allerdings 
die zu addierenden Zahlen nicht wie zuvor innerhalb der for-Schleife 
erzeugen. Erzeugen Sie stattdessen eine verschachtelte Liste oder eine 
Liste von Tupeln, die jeweils zwei Werte enthalten und iterieren Sie 
dann über diese Liste.

**Lösung**: Um 3 Additionsaufgaben mit jeweils zwei Zufallszahlen zu erzeugen, müssen eingangs 
sechs Zufallszahlen mithilfe der `randint()`-Funktion des importierten `random`-Moduls erzeugt 
werden. Anschließend wird eine Liste von Tupeln erstellt und in der Variable `liste` gespeichert.
Ein Tupel umfasst innerhalb der `liste` immer zwei der zu Beginn erzeugten Zufallszahlen.
Anschließend wird mithilfe einer `for`-Schleife festgelegt, dass der nachfolgende Codeblock so oft 
ausgeführt werden soll, wie die `liste` Elemente beinhaltet (insgesamt drei Tupel, also drei mal). 
Explizit bedeutet `for i in liste:` hierbei für jeden Tupel in der Liste. Die Variable `i` kann 
hierbei beliebig gewählt werden. Beispielsweise würde auch `for tupel in liste:` funktionieren.
Anschließend wird der bereits bekannte Code eingefügt. Hierbei ist zu beachten, dass auf die 
einzelnen Zufallszahlen auf eine spezifische Art und Weise zugegriffen werden muss. Beispielsweise 
kann auf die erste Zahl des Tupels in dieser Form zugegriffen werden: `i[0]`. Auf die zweite Zahl, 
die sich im Tupel befindet, kann in dieser Form zugegriffen werden: `i[1]`. Die Variable `i` wird 
über die `for`-Schleife hinweg iteriert, sodass sie bei der ersten Durchführung dem Wert 0 hat, bei 
der zweiten Durchführung den Wert 1 hat und bei der dritten Durchführung den Wert 2 hat. Folglich 
wird beim ersten Durchlauf auf den ersten Tupel, beim zweiten Durchlauf auf den zweiten Tupel und 
beim dritten Durchlauf auf den dritten Tupel der `liste` zugegriffen. Konkret bedeutet dies z.B. 
unter Annahme der `liste = [(1, 10), (20, 5), (18, 99)]`, dass bei dem ersten Durchlauf der 
for-Schleife auf die Elemente `0[0]` und `0[1]` zugegriffen wird. Diese entsprächen `1` und `10`. 
Da das korrekte Ergebnis nicht wie zuvor in einer eigenen Variable gespeichert wurde, wird es 
innerhalb des `if`-Statements berechnet. Wie bei den vorherigen Aufgaben ist zu beachten, dass die 
Zufallszahlen vom Datentyp `int` in den Datentyp `str` transformiert werden müssen, um sie 
auszugeben.

**Code**:
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

### Aufgabe 2

**Aufgabenstellung**: Erweitern Sie das Skript aus der ersten Aufgabe in diesem Abschnitt 
um einen try except Block, der die Eingabe auf Gültigkeit überprüft. 
Sollte der:die Benutzer:in keine gültige Eingabe gemacht 
haben, soll er:sie eine erneute Eingabe vornehmen müssen und eine 
entsprechende Fehlermeldung angezeigt bekommen.

**Lösung**: Zur Lösung dieser Aufgabe wird innerhalb der ersten `while`-Schleife eine weitere 
Variable (`good_input`) und eine zweite `while`-Schleife hinzugefügt. Der Variable `good_input` 
wird zunächst der Wert `False` zugewiesen. Solange die Variable `good_input` nicht den Wert `True` 
hat, wird der auf die zweite `while`-Schleife folgende Codeblock ausgeführt. Mithilfe des 
`try...except`-Blocks wird anhand der Funktion `int()` geprüft, ob es sich bei der Benutzereingabe 
um eine ganzzahlige Eingabe vom Datentyp `int` handelt. Sofern dies zutrifft, wird der Variable 
`good_input` der Wert `True` zugewiesen. Andernfalls wird `Fehleingabe! Bitte geben Sie einen 
gültigen Wert ein:` ausgegeben.

**Code:**
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

    print("Bitte rechnen Sie die folgende Aufgabe: " + str(i[0]) + " + " + str(i[1]) + ": ")

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
            print("Ihre eingegebene Lösung ist falsch! Bitte versuchen Sie es erneut:")
```

[Zurück zu Abschnitt 5](part5.md)
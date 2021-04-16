### Lösung zu Abschnitt 4 Aufgabe 1

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

### Lösung zu Abschnitt 4 Aufgabe 2

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

## Abschnitt 5

### Abschnitt 5.1 Mehr zu Listen, Tupeln und Dictionaries

Bislang haben wir Listen nur im Zusammenhang mit der **for-Schleife** 
kennengelernt. Häufig wollen wir aber nicht auf alle Elemente einer 
Liste nacheinander zugreifen, sondern nur auf bestimmte Elemente. 
Zu diesem Zwecke lassen sich Indizes benutzen, die an das Ende einer 
Liste oder einer Listenvariable angehängt werden:

```python
liste = [5, 6, 7, 8, 9]

print(liste[0])  # gibt den ersten Listeneintrag zurück

print(liste[4])  # gibt den fünften Listeneintrag zurück

print(liste[0:2])  # gibt die ersten zwei Listeneinträge zurück

print(liste[3:])  # gibt ab dem vierten Eintrag alle Listeneinträge zurück
```

An den obigen Beispielen lassen sich zwei Besonderheiten erkennen, 
die Python von einigen anderen Programmiersprachen (z.B. R) 
unterscheidet und für viele Benutzer:innen verwirrend wirken können:

1. Die Zählung der Listeneinträge beginnt bei 0. Alle folgenden 
   Listeneinträge bekommen also einen Index, der sich um 1
   von der tatsächlichen Position in der Liste unterscheidet
2. Wenn ein Bereich angegeben wird, ist die Zahl links vom **:** im 
   Ergebnis enthalten, die Zahl rechts davon jedoch
   nicht

Mithilfe der Indizierung lassen sich nun einzelne Einträge in Listen 
nicht nur abrufen, sondern auch gezielt verändern:

```python
liste = [5, 6, 7, 8, 9]

liste[0] = "Hallo"

print(liste)
```

Eine andere Art von Liste ist der **Tupel**, welcher nicht mit eckigen, 
sondern runden Klammern erzeigt wird. Im Unterschied zu Listen kann man 
die einzelnen Elemente in Tupeln nach ihrer Erstellung nicht mehr 
bearbeiten:

```python
liste = (5, 6, 7, 8, 9)

liste[0] = "Hallo"

print(liste)
```

Der obige Codeblock gibt eine Fehlermeldung zurück, da wir versuchen 
einen Tupel zu bearbeiten.

Ein dritter und in Pythonskripten sehr häufig genutzter Variablentyp 
ist das sogenannte **Dictionary**. Dictionaries sind ungeordnete Listen, 
deren einzelne Elemente nicht über ihre Position, sondern einen eigenen 
**Key** referenziert werden. Dies bedeutet, dass man auf Einträge von 
Dictionaries über ihren jeweiligen Key zugreifen kann 
(wie in der Windows Registry). Dictionaries werden durch geschwungene 
Klammern erzeugt. Die Keys müssen immer Stringvariablen sein, während 
die zugeordneten Elemente beliebige Datenformate aufweisen können:

```python
dict_1 = {"Key1": 150, "Key2": "Hello World", "Key3": True, "testkey": 20}

print(dict_1["testkey"])
```

Über die Einträge in einem Dictionary kann man genau so eine 
**for-Schleife** laufen lassen, wie über Tupel oder Listen. 
Beachten muss man dabei aber, dass nicht die zugeordneten Werte, 
sondern die Keys iteriert werden:

```python
liste = [5, 6, 7, 8, 9]

tupel = (5, 6, 7, 8, 9)

dict_1 = {"Key1": 150, "Key2": "Hello World", "Key3": True, "testkey": 20}

for i in liste:
    print(i)

for i in tupel:
    print(i)

for i in dict_1:  # Ausgabe der Keys
    print(i)

for i in dict_1:  # Ausgabe der zugeordneten Werte
    print(dict_1[i])
```

### Abschnitt 5.2 Exception Handling in Python

Python bietet uns die Möglichkeit Fehler, die eigentlich zu einem 
Abbruch der Skriptausführung führen würden, gezielt abzufangen und eine 
angemessene Reaktion zu zeigen, die aber kein Skriptabbruch ist. Zu 
diesem Zwecke können wir einen **try except** Codeblock verwenden, der 
ähnlich funktioniert wie eine **if else** Verzweigung:

```python
print("Bitte geben sie eine Zahl ein:")

eingabe = input()

try:
    int(eingabe)
except:
    print("Fehler: Sie haben keine Zahl eingegeben")

print("Ihre Eingabe: " + str(eingabe))
```

Der try except Block bietet uns also die Möglichkeit, im Falle eines 
Fehlers eine eigene Reaktion zu programmieren, anstatt das Skript 
abstürzen zu lassen. Im obigen Beispiel wird das Skript an sich 
fehlerfrei ausgeführt, auch wenn eine falsche Eingabe erfolgt ist.

### Aufgabe 1 zu Abschnitt 5

**Bauen Sie das Skript aus Aufgabe 1 zum letzten Abschnitt so um, dass 
der:die Benutzer:in nun 3 Aufgaben bearbeiten muss. 
Sie können hierfür eine for-Schleife verwenden. Lassen Sie allerdings 
die zu addierenden Zahlen nicht wie zuvor innerhalb der for-Schleife 
erzeugen. Erzeugen Sie stattdessen eine verschachtelte Liste oder eine 
Liste von Tupeln, die jeweils zwei Werte enthalten und iterieren Sie 
dann über diese Liste**

### Aufgabe 2 zu Abschnitt 5

**Erweitern Sie das Skript aus der ersten Aufgabe in diesem Abschnitt 
um einen try except Block, der die Eingabe auf Gültigkeit überprüft. 
Sollte der:die Benutzer:in keine gültige Eingabe gemacht 
haben, soll er eine erneute Eingabe vornehmen müssen und eine 
entsprechende Fehlermeldung angezeigt bekommen.**

[Hinweise zu den Aufgaben](exercise-hints.md)

[**Weiter zu Abschnitt 6**](part6.md)
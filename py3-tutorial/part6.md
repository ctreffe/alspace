---
layout: py3_tutorial
---

## Abschnitt 6

### 6.1 Funktionen

Wir haben bislang eine ganze Reihe existierender Python-Funktionen genutzt.
Dazu gehören z.B. **str()**, **input()**, **random.randint()** oder auch
**print()**. Neben vorgefertigten Funktionen können wir natürlich in 
Python auch eigene Funktionen deklarieren, die spezifische Aufgaben 
erfüllen sollen. Im folgenden Beispiel erstellen wir eine Funktion, die 
uns immer den jeweils ersten und letzten Eintrag einer Liste als neue 
Liste zurückliefert:

```python
def list_parser(liste):
    new_list = []
    new_list.append(liste[0])
    new_list.append(liste[len(liste) - 1])

    return new_list


print(list_parser([1, 2, 3, 4]))
```

Im obigen Beispiel nutzen wir zwei neue Funktionen. Zum einen gibt 
uns **len()** die Länge z.B. einer Liste zurück. **append()** ist die 
spezifische Funktion des Variablentyps **list** (also einer Liste), mit 
der neue Elemente an das Ende einer Liste angehängt werden können. In 
unserer Funktion erzeugen wir also eine neue Liste, die wir mit dem 
ersten und dem letzten Element 
(len(liste)-1 ist dafür der passende Ausdruck) der übergebenen Liste 
füllen. Am Ende geben wir mit der Anweisung **return** unsere neue 
Liste zurück.

Wichtig bei der Definition von Funktionen ist zum einen der Operator 
**def**, welcher Python zeigt, dass in der Folge eine neue Funktion 
definiert wird, sowie die Parameter (auch Argumente genannt), die hinter
dem Namen der neuen Funktion in runden Klammern angegeben werden. 
Im obigen Beispiel ist der Parameter zunächst undefiniert, wir geben 
also nur einen Namen an. Wir können genau so auch einen Standardwert 
setzen, der beim Aufruf der Funktion genutzt wird, sofern keine Liste 
als Parameter übergeben wird:

```python
def list_parser(liste=[1, 2, 3, 4]):  # jetzt mit Standardwert

    new_list = []
    new_list.append(liste[0])
    new_list.append(liste[len(liste) - 1])

    return new_list


print(list_parser())  # Funktionsaufruf ohne Parameter

print(list_parser(liste=[4, 5, 6, 7]))  # Funktionsaufruf mit Parameter

print(list_parser([4, 5, 6, 7]))  # Funktionsaufruf mit unnamed Parameter
```

Im letzten Funktionsaufruf wird als Parameter zwar eine Liste übergeben, 
aber ohne den Parameternamen anzugeben. Diese Art des Funktionsaufrufs 
ohne Parameternamen ist üblich, es sei aber darauf verwiesen, dass auch 
bei Python ein Mischen der unnamed und named Parameter nicht 
unproblematisch ist und nur in eine Richtung funktioniert:

```python
def addition(a=10, b=5):
    return a + b


print(addition(b=2))  # Man kann für einzelne Parameter Werte übergeben

print(addition(6, b=4))  # Unnamed vor den Named Parametern ist erlaubt

print(addition(a=5, b))  # Named vor Unnamed ist nicht erlaubt!
```

Natürlich sind auch Funktionen ohne Rückgabewert und ohne Parameter möglich:

```python
def trenner():
    print("**********")


trenner()

print("Dies hier steht zwischen zwei Trennern")

trenner()
```


### Aufgabe 1 zu Abschnitt 6

**Erstellen Sie eine Funktion, die zwei Zahlenwerte zufällig durch eine 
der vier Grundrechenarten miteinander verknüpft. In einem Skript soll 
ein:e Nutzer:in zunächst zwei Zahlen (mit Kontrolle auf richtige Eingabe) eingeben. 
Diese Zahlen sollen dann die Funktion durchlaufen. Die Funktion soll mittels print() Befehl den 
Typ der Berechnung melden und als Returnwert das Ergebnis der Berechnung 
zurückgeben. Dieses Ergebnis soll dem:der Benutzer:in am Ende angezeigt werden.**

### Aufgabe 2 zu Abschnitt 6

**Verändern Sie das Skript aus Aufgabe zwei des vorangegangenen 
Abschnitts so, dass die Benutzereingabe mit der anschließenden 
Validierung (while-Schleife mit darin verschachteltem try except Block) 
in eine Funktion ausgelagert wird, die nur eine korrekte Benutzereingabe
zurückliefert**

<div class="d-grid gap-2 d-md-block">
  <a href="part6_hints" class="btn btn-secondary btn-sm" tabindex="2" role="button" aria-disabled="true">Hinweise zu den Aufgaben</a>

  <a href="part6_solution" class="btn btn-secondary btn-sm" tabindex="3" role="button" aria-disabled="true">Lösungen zu den Aufgaben</a>
</div>

<br><br><br>

<div class="d-grid gap-2 d-md-flex justify-content-md-between">
  <a href="part5" class="btn btn-outline-primary btn-sm" tabindex="1" role="button" aria-disabled="true">Zurück zu Abschnitt 5</a>

  <a href="part7" class="btn btn-primary btn-sm" tabindex="4" role="button" aria-disabled="true">Weiter zu Abschnitt 7</a>
</div>
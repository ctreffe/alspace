## Abschnitt 2: Lösungen

### Aufgabe 1

**Aufgabenstellung**: Schreiben Sie ein Skript, welches eine von Ihnen eingegebene Zahl 
zur Ganzzahl 12 addiert. Geben Sie das Ergebnis der Addition und den Variablentyp des 
Ergebnisses mit der Funktion print() aus.

**Lösung**: Um User-Input zu generieren, wird die `input()`-Funktion verwendet. Durch 
Aufruf der `input()`-Funktion wird der Programmlauf solange gestoppt, bis der:die 
Benutzer:in eine Eingabe über die Tastatur tätigt und auf Enter klickt. Diese 
Benutzereingabe wird in der Variable `eingabe` gespeichert. Damit User 
wissen, dass Sie eine Eingabe tätigen müssen, wird zuvor durch die `print()`-Funktion 
der `String` "Bitte eine Zahl eingeben: " ausgegeben.
Da die Benutzereingabe standardmäßig als `String` gespeichert wird und Python nur mit 
numerischen Variablen rechnen kann, muss bei der Berechnung des Ergebnisses die 
`float()`-Funktion angewendet werden. Die `float()`-Funktion wandelt die `eingabe` 
(=`String`) in einen `float` (= Fließkomma-Zahl) um. Das Ergebnis der Addition von der 
eingegebenen Zahl und 12 wird in der Variable `ergebnis` gespeichert.
Abschließend wird das Ergebnis und ein erklärender `String` mithilfe der 
`print()`-Funktion ausgegeben. Hierfür muss die Variable `ergebnis` vom Variablentyp 
`float` mithilfe der `str()`-Funktion zu einem `String` konvertiert werden. 
Abschließend wird der Variablentyp der Variable `ergebnis` mithilfe der 
`type()`-Funktion ausgegeben, um zu demonstrieren, dass der Variablentyp dieser 
Variable `float` ist.

**Code**:
```python
# Eingabe

print("Bitte Zahl eingeben: ")
eingabe = input()

# Verarbeitung

ergebnis = 12 + float(eingabe)

# Ausgabe

print("Das Ergebnis der Addition lautet: " + str(ergebnis))
print(type(ergebnis))
```

### Aufgabe 2

**Aufgabenstellung**: Schreiben sie ein Skript, welches sie auffordert, zwei beliebige Ganzzahlen zu addieren 
(Sie können die Werte dieser Ganzzahlen selbst festlegen). Fordern Sie zur Eingabe des korrekten 
Ergebnisses auf. Geben Sie sowohl das eingegebene Ergebnis als auch das tatsächlich korrekte 
Ergebnis in die Konsole.

**Lösung**: Eingangs werden zwei beliebige Ganzzahlen in den Variablen `a` und `b` 
gespeichert. Um später abzugleichen, ob das korrekte Ergebnis von dem:der Benutzer:in 
berechnet wurde, wird das korrekte Ergebnis der Addition von `a` und `b` in der 
Variable `c` gespeichert. Anschließend wird die Aufforderung zur Berechnung der Aufgabe 
mithilfe der `print()`-Funktion ausgegeben. Daraufhin wird auf die Eingabe des:der 
Benutzer:in mithilfe der `input()`-Funktion gewartet und die Benutzereingabe in der 
Variable `eingabe` gespeichert. Im Anschluss wird ein erklärender `String` und die 
`eingabe`-Variable vom gleichen Variablentypen (`String`) mithilfe der `print()`-Funktion 
ausgegeben. Abschließend wird ein erklärender `String` und das am Anfang berechnete 
korrekte Ergebnis der Addition mithilfe der `print()`-Funktion ausgegeben. Da das am 
Anfang berechnete Ergebnis in der Variable `c` vom Variablentyp `int` gespeichert wird, 
muss die Variable mithilfe der `str()`-Funktion in einen `String` konvertiert werden.

**Code**:
```python
a = 5
b = 4

c = a + b

print("Bitte rechnen sie folgende Aufgabe: 5 + 4:")
eingabe = input()

print("Ihre Eingabe: " + eingabe)
print("Das korrekte Ergebnis: " + str(c))
```

[Zurück zu Abschnitt 2](part2.md)
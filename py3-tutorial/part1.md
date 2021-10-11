---
layout: py3_tutorial
---

## Abschnitt 1

Im Folgenden werden wir in wenigen einfachen Schritten die Standarddistribution von Python 
installieren und anschließend eine geeignete Entwicklungsumgebung zum Erstellen einfacher 
Pythonskripte hinzufügen.

### 1.1 Installieren der Python Standard-Distribution

Die Python Installationsdatei für **Windows** kann unter folgendem Link heruntergeladen werden:<br>
https://www.python.org/ftp/python/3.10.0/python-3.10.0-amd64.exe

Die Python Installationsdatei für **macOS** kann unter folgendem Link heruntergeladen werden:<br>
https://www.python.org/ftp/python/3.10.0/python-3.10.0-macos11.pkg

Im Rahmen der Installation können zwei Optionen ausgewählt werden:
1. Die Installation kann entweder für alle Benutzer:innen eines Rechners oder nur für den angemeldeten 
   Benutzer oder die angemeldete Benutzerin durchgeführt werden. 
   Wenn Python für **alle Benutzer:innen** installiert werden soll, muss die Option 
   "Install launcher für all users" ausgewählt werden. 
2. Damit unsere Python Installation später problemlos von anderen Programmen 
   (z.B. unserer bevorzugten Entwicklungsumgebung) erkannt und genutzt werden kann, 
   müssen wir noch die Option **"Add Python 3.10 to PATH"** auswählen.

Danach kann Python per Klick auf "Install Now" in das Standardverzeichnis (C:\Python310) 
installiert werden.

### 1.2 Installieren der passenden Entwicklungsumgebung (PyCharm)

Mit der Python Standarddistribution wird eine Entwicklungsumgebung namens *IDLE* installiert. 
Da diesem Editor jedoch wichtige Kernfeatures (z.B. die Möglichkeit zu horizontalem Scrollen in 
Skripten) fehlen, raten wir davon ab, mit IDLE zu arbeiten. Als Entwicklungsumgebung für 
einfache Python Skripte eignet sich stattdessen das beliebte Open Source Tool **PyCharm**, 
welches unter folgendem Link heruntergeladen werden kann: 

Für **Windows**:<br>
https://www.jetbrains.com/de-de/pycharm/download/download-thanks.html?platform=windows&code=PCC

Für **macOS**:<br>
https://www.jetbrains.com/de-de/pycharm/download/download-thanks.html?platform=mac&code=PCC

### 1.3 Einrichten von PyCharm
Nach der Installation muss PyCharm zunächst eingerichtet werden.
Beim Einrichten von PyCharm kann angegeben werden, dass PyCharm noch nicht zuvor verwendet 
wurde und das "UI Theme" (z.B. Dracula) kann ausgewählt werden. 
Ein Script wird zunächst nicht benötigt, daher wird kein "Launcher Script" erstellt. 
Die folgenden Plug-ins sind optional. <br>
Im Anschluss kann die Option "New Project" ausgewählt werden. 
Danach wird der:die Benutzende aufgefordert, eine "Location", also einen Speicherort und einen 
Dateinamen festzulegen. Außerdem muss der Interpreter ausgewählt werden. Hierfür wird bei 
"Existing interpreter" "Python 3.10" verwendet. 
Weiterhin besteht die Möglichkeit, eine "main.py" zu erstellen. Diese Option wird nicht ausgewählt. 
Nachdem auf "Weiter" geklickt wurde, wird die Benutzeroberfläche von PyCharm dargestellt. 
Oben links wird nun der neu erstellte Ordner abgebildet. 

### 1.4 Ein einfaches Testskript (Hello World)
Um nun eine Python-Datei zu erstellen, welche sich in dem zuvor erstellten Ordner befindet, 
wird ein Rechtsklick auf diesen Ordner ausgeführt, "New" ausgewählt und dann auf "Python File" 
geklickt. 
Diese neue Datei wird als "script" benannt. Wir sehen, dass Pythondateien die Dateiendung .py erhalten. 
Im nächsten Schritt wird in diese neue "script.py", 
welche sich automatisch nach der Erstellung öffnet, zunächst ein **einzeiliger Kommentar** eingefügt.
Einzeilige Kommentare werden zu Beginn oder innerhalb einer Zeile mit **#** gekennzeichnet: <br>

````python
# Dies ist ein einzeiliger Kommentar
````

Neben den einzeiligen Kommentaren können auch mehrzeilige Kommentare verfasst werden.
Mehrzeilige Kommentare können in der Form von Docstrings wie folgt gekennzeichnet werden:<br>

```python
"""
Dies ist ein sogenannter Docstring, welcher
über mehrere Zeilen verlaufen kann und wie
ein Kommentar behandelt wird.
"""
```

Kommentare beeinflussen die Ausführung des Codes nicht. Beispielsweise wird auskommentierter Code
nicht ausgeführt.

Wir wollen nun unter den einführenden Kommentar unser erstes kleines Programm schreiben:

```python
print("Hello world!")
```

### 1.5 Ausführen von Skriptdateien aus PyCharm

Nachdem wir unser erstes Skript erstellt haben, können wir in der Menüleiste 
(im oberen Bildschirmbereich) auf "File" klicken und dann "Save all" auswählen.
Nun wird der aktuelle Stand des Ordners, welcher unsere script.py beinhaltet,
an dem ursprünglich ausgewählten Speicherort (=Location) gesichert.

In PyCharm wird uns sowohl der zuvor erstellte Ordner als auch die sich darin befindende 
"script.py" unter dem "Project-Reiter" (links) angezeigt. Durch einen **Rechtsklick** auf die 
"script.py" und das Auswählen der Option `Run 'script.py'` kann die script.py ausgeführt 
werden.
Als Resultat wird uns in der Konsole (im unteren Bildschirmbereich) die Zeichenfolge **Hello world!** 
angezeigt, die mit der Funktion **print()** ausgegeben wurde. 
Zeichenketten werden immer von einfachen Anführungszeichen **'** oder doppelten 
Anführungszeichen **"** umschlossen
```
Hello world!
```
Dieses ursprüngliche Skript lässt sich leicht erweitern. Beispielsweise könnte zunächst eine 
Namensabfrage erfolgen und anschließend eine personalisierte Begrüßung ausgegeben werden.
Hierfür wird das bestehende Programm um eine weitere print()-Funktion und die Funktion **input()**, 
durch die eine Benutzereingabe in der Konsole erwartet wird, erweitert. Diese Benutzereingabe wird 
in der Variable "name" gespeichert.
```python
print("Bitte geben Sie Ihren Namen ein: ")
name = input()
print("Hello " + name + "!")
```
Da die Ausführung des Skriptes erst nach einer beliebigen Benutzereingabe und Bestätigung dieser 
durch **Enter** fortgesetzt wird, kann die Funktion **input()** unter anderem Skripte an 
beliebiger Stelle unterbrechen und erst nach manueller Bestätigung fortsetzen.
Sobald der:die Benutzer:in Enter drückt, wird die Ausführung des Skriptes fortgesetzt und die 
personalisierte Begrüßung ausgegeben.

<div class="d-grid gap-2 d-md-flex justify-content-md-between">
  <a href="../py3-tutorial" class="btn btn-outline-primary btn-sm" tabindex="1" role="button" aria-disabled="true">Zurück zur Startseite</a>

  <a href="part2" class="btn btn-primary btn-sm" tabindex="2" role="button" aria-disabled="true">Weiter zu Abschnitt 2</a>
</div>

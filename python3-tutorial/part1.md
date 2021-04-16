## Abschnitt 1: Vorbereitung

Im Folgenden werden wir in wenigen einfachen Schritten die Standarddistribution von Python installieren und anschließend eine geeignete Entwicklungsumgebung zum Erstellen einfacher Pythonskripte hinzufügen.

### 1.1 Installieren der Python Standard-Distribution

Die Python Installationsdatei für **Windows** kann unter folgendem Link heruntergeladen werden:<br>
https://www.python.org/ftp/python/3.9.4/python-3.9.4-amd64.exe

Die Python Installationsdatei für **macOS** kann unter folgendem Link heruntergeladen werden:<br>
https://www.python.org/ftp/python/3.9.4/python-3.9.4-macos11.pkg

Im Rahmen der Installation können zwei Optionen ausgewählt werden:
1. Die Installation kann entweder für alle Benutzer:innen eines Rechners oder nur für den angemeldeten 
   Benutzer oder die angemeldete Benutzerin durchgeführt werden. 
   Wenn Python für **alle Benutzer:innen** installiert werden soll, muss die Option 
   "Install launcher für all users" ausgewählt werden. 
2. Damit unsere Python Installation später problemlos von anderen Programmen 
   (z.B. unserer bevorzugten Entwicklungsumgebung) erkannt und genutzt werden kann, 
   müssen wir noch die Option **"Add Python 3.9 to PATH"** auswählen.

Danach kann Python per Klick auf "Install Now" in das Standardverzeichnis (C:\Python39) 
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
Nach der Installation von PyCharm muss PyCharm zunächst eingerichtet werden.
Beim Einrichten von PyCharm kann zunächst angegeben werden, dass PyCharm noch nicht zuvor verwendet 
wurde und das "UI Theme" (z.B. Dracula) kann ausgewählt werden. 
Ein Script wird zunächst nicht benötigt, daher wird kein "Launcher Script" erstellt. 
Die folgenden Plug-ins sind optional. <br>
Im Anschluss kann die Option "New Project" ausgewählt werden. 
Danach wird der:die Benutzende aufgefordert, eine "Location", also einen Speicherort und einen 
Dateinamen festzulegen. Außerdem muss der Interpreter ausgewählt werden. Hierfür wird bei 
"Existing interpreter" "Python 3.9" verwendet. 
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
'''
Dies ist ein sogenannter Docstring, welcher
über mehrere Zeilen verlaufen kann und wie
ein Kommentar behandelt wird.
'''

```

Kommentare beeinflussen die Ausführung des Codes nicht. Beispielsweise wird auskommentierter Code
nicht ausgeführt.

Wir wollen nun unter den einführenden Kommentar unser erstes kleines Programm schreiben:
```python
print("Hello world!")
```
Abschließend klicken wir mit einem Rechtsklick auf unsere "scrip.py"
und wählen Run'script' aus. Nun wird unser Skript ausgeführt und als Resultat wird uns im Terminal 
(im unteren Bildschirmbereich) als Ausgabe einfach die Zeichenfolge **Hello world!** angezeigt, 
die wir mit der Funktion **print()** ausgegeben wurde. 
Zeichenketten werden immer von einfachen Anführungszeichen **'** oder doppelten 
Anführungszeichen **"** umschlossen
```
Hello world!
```

### 1.5 Ausführen von Skriptdateien aus dem Windows Explorer

Nachdem wir unser erstes Skript erstellt haben, können wir in der Menüleiste 
(im oberen Bildschirmbereich) auf "File" klicken und dann "Save all" auswählen.
Nun wird der aktuelle Stand des Ordners, welcher unsere script.py beinhaltet,
an dem ursprünglich ausgewählten Speicherort (=Location) gesichert.

Wenn wir nun diesen erstellten Ordner öffnen, sehen wir, dass sich unsere "script.py" in diesem 
befindet.  Die Datei können wir per Doppelklick nun direkt ausführen. 
Allerdings passiert bei der Ausführung nicht viel, außer dass sich eine Python-Konsole sehr schnell 
öffnet und wieder schließt. 
Dies liegt daran, dass nach der Ausführung eines Pythonskriptes aus dem Windows Explorer heraus, 
egal ob erfolgreich oder nicht, die Konsole sofort wieder geschlossen wird.

Um dies zu verändern, erweitern wir unser bestehendes Programm um eine zusätzliche Zeile, 
durch die eine Benutzereingabe in der Konsole erwartet wird:

```python
print("Hello World")
input()
```

Bei erneuter Ausführung des Skriptes aus dem Windows Explorer bleibt die Konsole nun geöffnet und 
erwartet eine beliebige Benutzereingabe, die durch **Enter** bestätigt werden kann. 
Sobald der:die Benutzer:in Enter drückt, wird das Skript beendet und die Konsole 
schließt sich.

Die Funktion **input()** kann also unter anderem Skripte an beliebiger Stelle unterbrechen und 
erst nach manueller Bestätigung fortsetzen.

[**Weiter zu Abschnitt 2**](part2.md)

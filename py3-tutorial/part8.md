---
layout: py3_tutorial
---

## Abschnitt 8 - !Under Construction!

### 8.1 Dekoratoren

In Python dienen Dekoratoren in der Regel dazu, Funktionen oder Klassen
zu erweitern, ohne ihren Code selbst zu verändern. Das kann z.B. relevant
sein, wenn die gewünschte Erweiterung in bestimmten Fällen ausgeführt
werden soll, in anderen aber die unveränderte bzw. nicht erweiterte
Originalfunktion gewünscht ist. Hier ein einfaches Beispiel für die
Nutzung eines selbstdefinierten Decorators:

```python
def decorator(fun):
    def decorate():
        print("Ich erweitere bzw. dekoriere die Originalfunktion")
        fun()
  
    return decorate

@decorator
def original():
    print("Ich bin die Originalfunktion")

outer()
```

https://codecitrus.com/python-decorator/


<!--

Grundsätzlich ist ein **Decorator** eine Funktion, die eine andere Funktion als Argument entgegennimmt, 
irgendeine Form von Funktionalität hinzufügt und dann eine andere Funktion zurückgibt, ohne dass 
der Sourcecode der originalen Funktion (die entgegengenommen wurde) verändert wird.

Dies wird an dem folgenden Beispiel deutlich. Die "decorator_function" nimmt die 
"original_function" als Argument entgegen. In der decorator_function befindet sich eine 
weitere Funktion, die wrapper_function, welche bei Ausführung "Start" ausgibt, die original_function
ausführt und "Stop" ausgibt. Diese wrapper_function wird durch "return wrapper_function" ausgegeben.
(Und *nicht* ausgeführt!) Abschließend wird die orig_func, also eine weitere Funktion, welche lediglich
"Continue" ausgibt, definiert. Wenn nun erwünscht ist, dass anstelle der bislang nicht definierten
"original_function", die "orig_func" von der "decorator_function" entgegengenommen und innerhalb 
der wrapper_function ausgeführt wird, kann dies über zwei Wege erfolgen:
1. Umständlich per zwei Codezeilen: 
   ```python 
   x = decorator_function(orig_func)
   x ()
   ```
2. Oder per **Decorator** (@decorator_function). Dieser Decorator ersetzt die Codezeile 
   `x = decorator_function(orig_func)`, sodass direkt `orig_func()` ausgeführt werden kann.


```python
def decorator_function(original_function):
    def wrapper_function():
        print("Start")
        original_function()
        print("Stop")

    return wrapper_function


@decorator_function
def orig_func():
    print("Continue")


orig_func()
```
-->



<div class="d-grid gap-2 d-md-flex justify-content-md-between">
  <a href="part7" class="btn btn-outline-primary btn-sm" tabindex="1" role="button" aria-disabled="true">Zurück zu Abschnitt 7</a>

  <a href="../py3-tutorial" class="btn btn-primary btn-sm" tabindex="2" role="button" aria-disabled="true">Zur Startseite</a>
</div>


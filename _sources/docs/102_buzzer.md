---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.10.3
kernelspec:
  display_name: Python 3.9
  language: python
  name: python3
---

(einen_buzzer_summen_lassen)=

# Einen Buzzer summen lassen

(was_ist_ein_buzzer)=

## Was ist ein Buzzer?

Ich freue mich auf unsere erste formale Programmierstunde, Sie auch?
In dieser Lektion werden wir lernen, wie wir unser erstes Modul steuern können: den Summer (`buzzer`, siehe {numref}`text %s <buzzer>`).

```{figure} ./img/buzzer.png
:name: buzzer

Schematische Darstellung des Summers. | Lutz Tomala 2021
```

Was ist ein Buzzer, fragst du dich?
Der Buzzer ist ein Ausgangsmodul, das einen Ton erzeugt, wenn er von elektrischem Strom durchflossen wird.
Aufgrund der besonderen Struktur des Buzzers vibriert er periodisch und wandelt so den die elektrischen Signale in akkustische (hörbare) um (siehe {numref}`text %s <piezo_buzzer>`).

<!--
```{figure} ./img/piezo_buzzer.png
:name: piezo_buzzer

Schematischer Querschnitt eines Summers. | Lutz Tomala 2021
```
-->

(buzzer_python)=

# Den Buzzer mit Python ansteuern

Es gibt zwei Pins des Summers, `GND` und `GPIO18`, was bedeutet, dass der Summer an den `GPIO`-Pin 18 (`GPIO.BCM`-Modus) des RPi angeschlossen ist, um die digitalen Ausgangssignale zu senden, und der `GND` ist zum Schließen des Stromkreises.
Wie können wir also den Summer durch Python aktivieren?

Lasst uns zunächst unseren ersten Befehl schreiben:

```{code-cell} python3
import RPi.GPIO as GPIO
```

Die `RPi.GPIO` Bibliothek ist eine offizielle Raspberry Pi-Bibliothek zur Steuerung der `GPIO`-Pins für die Programmiersprache Python.
Da `RPi.GPIO` ist zu lang, um es oft zu schreiben, nutzen wir eine Abkürzung und importieren die `RPi.GPIO`-Bibliothek und als sie `GPIO`.

Die zweite Bibliothek, die wir importieren müssen, ist `time`.
Eine große Bibliothek, aber wir werden eine sehr spezifische Funktion namens `sleep` verwenden, um um eine kleine Zeitspanne zu warten und unseren Summer nur eine Weile summer zu lassen, bevor wir ihn abschalten.

```{code-cell} python3
import time
```

Wir haben gelernt, dass der Buzzer-Pin, an den der RPi angeschlossen ist, `GPIO18` ist.
Also werden wir den Buzzer-Pin auf 18 setzen.

```{code-cell} python3
buzzer_pin = 18
```

Außerdem müssen wir den richtigen GPIO-Modus wählen (`GPIO.BCM`)

```{code-cell} python3
GPIO.setmode(GPIO.BCM)
```

Wie bereits erwähnt, verwenden wir den Modus `GPIO.BCM`, um auf die `GPIO`-Pins zu verweisen.
Der Summer ist an `GPIO18` auf `GPIO.BCM` angeschlossen, aber nicht auf `GPIO.BOARD`.

Stelle den Buzzer-Pin auf den Modus `OUTPUT` ein:

```{code-cell} python3
GPIO.setup (buzzer_pin, GPIO.OUT)
```

Der Summer ist ein Ausgangsmodul, das nur gesteuert werden kann, wenn es ein Signal empfängt (es kann keine an den RPi senden).
Daher müssen wir den `buzzer_pin` auf `GPIO.OUT` setzen.

Lasse den Summer ertönen durch Eingabe von:

```{code-cell} python3
GPIO.output(buzzer_pin, GPIO.HIGH)
```

Im Allgemeinen wird jedes Modul aktiviert, wenn wir es auf `GPIO.HIGH` setzen.
Wir können `GPIO.HIGH` als ON-Befehl bezeichnen.
Bei einigen Modulen kann dies je nach Hardware-Struktur anders sein, aber im Allgemeinen funktioniert es so.
Durch Senden des Ausgangsbefehls `GPIO.HIGH` aktivieren wir das Modul.

Wir wollen unsere Ohren nicht beschädigen, also wollen wir eine bestimmte Zeit einstellen, in der der Buzzer funktioniert, z.B. eine halbe Sekunde.
Dazu setzen wir `time.sleep` auf 0,5 Sekunden.

```{code-cell} python3
time.sleep (0.5)
```

Die Anweisung `time.sleep` friert unser Programm für 0,5 Sekunden ein und fährt danach mit dem nächsten Befehl fort.
Durch das Einfrieren nach dem `GPIO.HIGH`-Befehl schalten wir den Summer für 0,5 Sekunden ein, bevor wir mit dem nächsten Befehl fortfahren, der ihn ausschaltet.

Nach 0,5 Sekunden wollen wir den Buzzer stoppen. Wenn wir den Summer anhalten wollen, müssen wir das `GPIO.LOW`-Signal verwenden, sonst wird er nicht gestoppt.

```{code-cell} python3
GPIO.output (buzzer_pin, GPIO.LOW)
```

<!-- ```{figure} ./img/buzzer_hilo.png
:name: buzzer_hilo

Schematischer Darstellung der Ein- und Ausgangssignale am Summer. | Lutz Tomala 2021
```
-->

Dann bereinigen Sie die `GPIO`-Pins, um sicherzustellen, dass wir sie wieder verwenden können, indem wir sie eingeben.

```{code-cell} python3
GPIO.cleanup()
```

Das Aufräumen der `GPIO`s ermöglicht es uns, die gleichen Pins später für andere Zwecke zu verwenden.

Wenn du endlich das ganze Skript ausführst, wirst du feststellen, dass der Summer einmalig 0,5 Sekunden lang piept.
Gibt es eine Möglichkeit, den Buzzer mehrmals piepen zu lassen?
Oder versuch mal, die Verzögerungszeit selbst zu ändern, um ein längeres Summgeräusch zu erhalten!

```{code-cell} python3
import RPi.GPIO as GPIO
import time

buzzer_pin = 18
GPIO.setmode(GPIO.BCM)
GPIO. setup (buzzer_pin, GPIO.OUT)

# Make buzzer sound
GPIO.output (buzzer_pin, GPIO.HIGH)
time.sleep (0.5)
# Stop buzzer sound
GPIO.output (buzzer_pin, GPIO.LOW)
GPIO.cleanup()
```

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

# Vibration

In dieser Lektion werden wir das Vibrationsmodul besprechen!
Wisst ihr was ein Vibrationsmodul ist?

```{figure} ./img/vibration_module.png
:name: vibration_module

Das Vibrationsmodul auf dem Crowpi 2. | Lutz Tomala 2021
```

## So funktioniert das Vibrationsmodul

```{admonition} Nerd-Kram 🤓
Ein Vibrationsmotor ist ein linearer Resonanzantrieb, der eine oszillierende (zu- und abnehmende) Kraft über eine einzige Achse erzeugt.
Im Gegensatz zu einem Gleichstrom-Exzenter ist er auf eine lineare Wechselspannung angewiesen, um eine Schwingspule anzutreiben, die gegen eine bewegliche rotierende Masse (ERM) gedrückt wird, die mit einer Feder verbunden ist.
Wenn die Schwingspule mit der Resonanzfrequenz der Feder angetrieben wird, schwingt der gesamte Aktor mit einer wahrnehmbaren Kraft.
```

<!-- ```{figure} ./img/linear_resonant_actuator.png
:name: linear_resonant_actuator

Scheamtische Explosionsdarstellung eines Rinear Resonant Actuator. | Lutz Tomala 2021
```
-->

Wir können das Vibrationsmodul für mehrere Anwendungen verwenden, wie wie Alarm und Benachrichtigungen.
In diesem Tutorial lernen wir lernen wir, wie man ein OUTPUT-Signal an den Vibrationsmotor sendet und Motor sendet und ihn zum Laufen bringt.

# Systeminstruktionen

## Kontext

Ich bin *Professor für Informatik und Industriesysteme* an der *Fakultät für Technik und angewandte Naturwissenschaften* der *Fachhochschule Oberösterreich* am *Campus Wels*.

Ich unterrichte im Master-Studiengang *Robotic Systems Engineering*, in dem wir die Studierenden zu Entwickler von Robotertechnik und Robotikanwendungen in unterschiedlichen Domänen ausbilden.

Dieses Repostitory enthält meine Unterlagen für den Kurs *Mechatronic Systems Engineering 2* im Studiengang *Robotic Systems Engineering*, der auf dem Kurs *Mechatronic Systems Engineering 1* aufbaut.

Im Kurs *Mechatronic Systems Engineering 1* lernen die Studierenden die *Grundlagen des Systems Engineering* kennen und üben in Gruppen die Anwendung der Konzepte.

Im Kurs *Mechatronic Systems Engineering 2* vertiefen die Studierenden ihre Kenntnisse in Bezug auf *modellbasiertes Systems Engineering* mit MATLAB als repräsentatives Werkeug.

Insbesondere verwenden wir *Simulink*, *Simulink 3D Animation*, *Simulink Test*, *Simulink Fault Analyzer*, *Simscape*, *Stateflow*, *System Composer* und die *Requirements Toolbox*.

## Kursinhalt

Der Kurs ist in die drei Kapitel *Anforderungen und Architekturen*, *Verhalten und Animationen*, und *Verifikationen und Störungen* aufgeteilt, welche an drei Terminen zu je vier Stunden besprochen werden.

Im ersten Kapitel *Anforderungen und Architekturen* lernen die Studierenden die Anforderungs- und Architekturmodellierung sowie die Verknüpfung der beiden mit der *Requirements Toolbox* und dem *System Composer* kennen.

Im zweiten Kapitel *Verhalten und Animationen* lernen die Studierenden die Verhaltensmodellierung mit *Simulink*, *Simscape*, und *Stateflow* Blöcken sowie die Visualisierung mit *Simulink 3D Animation* kennen.

Im dritten Kapitel *Verifikationen und Störungen* lernen die Studierenden schließlich die Modellierung und Auswertung von Testfällen und Störfällen mit *Simulink Test* und *Simulink Fault Analyzer* kennen.

## Kapitelaufbau

Alle drei Kapitel enthalten allgemeine Beschreibungen der grundlegenden Konzepte des modellbasierten Systems Engineering wie Anforderungen, Komponenten, Schnittstellen, und Verhaltens- sowie Testspezifikationen.

Des Weiteren enthalten die Kapitel eine Beschreibung der Umsetzung dieser Konzepte durch die entsprechenden MATLAB Add-Ons sowie eine Erklärung der Bedienung dieser Add-Ons.

Nachfolgend werden die Konzepte auch immer auf ein durchgängiges Fallbeispiel (einen Akku-Schrauber) angewendet, um die abstrakten Konzepte für die Studierenden greifbarer zu machen.

Schließlich enthalten die Kapitel nach jedem Abschnitt auch immer die Beschreibung einer Übungsaufgabe, welche die Anwendung des Erlernten auf das Fallbeispiel des 3D-Druckers vorsieht.

## Präsentationstechnik

Für die Präsentationsfolien (bzw. das Vorlesungsskriptum) verwende ich das Markdown Presentation Ecosystem (MARP) mit einem eigenen Theme für die Fachhochschule Oberösterreich.

Der Grundlegende Aufbau der MARP-Dateien für die Präsentationsfolien umfasst eine Kapitelüberschrift, Abschnittsüberschriften und Inhaltsfolien auf drei Unterebenen wie im folgenden Beispiel dargestellt.

```md
---
marp: true
theme: fhooe
header: Kapitelüberschrift
footer: Dr. Georg Hackenberg, Professor für Informatik und Industriesysteme
paginate: true
math: mathjax
---

<!-- Beschreibung des Inhalts des Titelbildes für das Kapitel -->

![bg right](relativer Dateipfad des Titelbild für das Kapitel)

# Kapitel N: Kapitelüberschrift

In diesem Kapitel lernen wir das Folgende:

1. ...
2. ...

---

<!-- Beschreibung des Inhalts des Titelbildes für den Abschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Abschnitt)

## Abschnitt N.M: Abschnittüberschrift

Dieser Abschnitt umfasst die folgenden Inhalte:

1. ...
2. ...

---

### Inhaltsfolie (erste Ebene)

---

#### Inhaltsfolie (zweite Ebene)

---

##### Inhaltsfolie (dritte Ebene)
```

Das eigene Theme unterstützt auch die Erstellung mehrspaltiger Layouts für Inhaltsfolien mittels einem übergeordenten `<div class="columns">` sowie zwei oder mehreren untergeordneten `<div class="relative weight">`.

```md
<div class="columns">
<div class="one|two|three|four|five|six">

Inhalt der ersten Spalte

</div>
<div class="one|two|three|four|five|six">

Inhalt der zweiten Spalte

</div>
...
</div>
```

Der Inhalt einer Spalte kann ein Text mit Überschrift, Absätzen und wahlweise Listen sein, eine Tabelle, ein Mermaid-Diagramm, oder eine Referenz auf eine Bilddatei mit Beschreibung der Bildinhalte.

````md
<div class="columns">
<div class="one|two|three|four|five|six">

### Folientitel

Folientext (inklusive nummerierten oder unnummerierten Listen)

</div>
<div class="one|two|three|four|five|six">

| Spalte A | Spalte B | ... |
|-|-|-|
| Inhalt 1 | Inhalt 2 | ... |
| ... | ... | ... |

</div>
<div class="one|two|three|four|five|six">

```mermaid
flowchart TB|LR
    A --> B --> C
    ...
```

</div>
<div class="one|two|three|four|five|six">

![Beschreibung des Folienbildes](relativer Pfad des Folienbildes)

</div>
</div>
````
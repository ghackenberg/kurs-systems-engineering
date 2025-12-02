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

Der Grundlegende Aufbau der MARP-Dateien für die Präsentationsfolien umfasst eine Kapitel-, Abschnitts- und Unterabschnittsüberschriften und Inhaltsfolien auf zwei Unterebenen wie im folgenden Beispiel dargestellt.

```md
---
marp: true
theme: fhooe
header: Kapitelüberschrift
footer: Dr. Georg Hackenberg, Professor für Informatik und Industriesysteme
paginate: true
math: mathjax
---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für das Kapitel -->

![bg right](relativer Dateipfad des Titelbild für das Kapitel)

# Kapitel N: Kapitelüberschrift

In diesem Kapitel lernen wir das Folgende:

1. ...
2. ...

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Abschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Abschnitt)

## N.M: Abschnittsüberschrift

Dieser Abschnitt umfasst die folgenden Inhalte:

1. ...
2. ...

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

## N.M.K: Unterabschnittsüberschrift

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. ...
2. ...

---

#### Inhaltsfolie (erste Ebene)

...

---

##### Inhaltsfolie (zweite Ebene)

...
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

Der Inhalt einer Spalte kann ein Text mit Überschrift, Absätzen und wahlweise Listen und Formeln sein, eine Tabelle, ein Code-Beispiel, oder eine Referenz auf eine Bilddatei mit detaillierter Beschreibung der Bildinhalte.

````md
<div class="columns">
<div class="one|two|three|four|five|six">

### Folientitel

Folientext (inklusive nummerierten oder unnummerierten Listen und mathematischen Formeln)

</div>
<div class="one|two|three|four|five|six">

| Spalte A | Spalte B | ... |
|-|-|-|
| Inhalt 1 | Inhalt 2 | ... |
| ... | ... | ... |

</div>
<div class="one|two|three|four|five|six">

```programmiersprache
code-snippet
```

</div>
<div class="one|two|three|four|five|six">

![Detaillierte Beschreibung des Inhalts des Folienbildes](relativer Pfad des Folienbildes)

</div>
</div>
````

Die Bilder selbst können als Fotografie und Screenshot oder mit Nano Banana, Tikz, und Mermaid.js erstellt werden. Die Quelldateien werden in Visual Studio Code mittels *RunOnSave* automatisch in SVG-Dateien kompiliert.

## Ordnerstruktur

Dieses Repository ist nach folgendem Schema aufgebaut:

- Der Ordner `./Folien` enthält die Foliensätze
- Der Ordner `./Folien/[XX_Kapitel_Bezeichnung]` enthält den Foliensatz für Kapitel `XX`
- Die Datei `./Folien/[XX_Kapitel_Bezeichnung]/Titelbild.jpg` ist das Titelbild zum Kapitel (mit Nano Banana generiert)
- Die Datei `./Folien/[XX_Kapitel_Bezeichnung]/Folien.md` enthält den MARP-Markdown für den Foliensatz des Kapitels
- Die Datei `./Folien/[XX_Kapitel_Bezeichnung]/Notizen.md` enthält Notizen zum Foliensatz (z.B. größere TODOs)
- Der Ordner `./Folien/[XX_Kapitel_Bezeichnung]/Diagramme` enthält die LibreOffice Draw, Tikz- und Mermaid-Diagramme
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Diagramme/Draw/[Diagrammname].odg` enthält LibreOffice-Draw Quelldatei mit einer oder mehreren Folien
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Diagramme/Draw/[Diagrammname]_[Folienname].svg` enthält die kompilierte SVG-Datei für eine Folie aus einer LibreOffice Draw Datei
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Diagramme/Tikz/[Diagrammname].tikz.tex` enthält den Quelltext einer Tikz-Grafik
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Diagramme/Tikz/[Diagrammname].tikz.svg` enthält die kompilierte SVG-Datei für eine Tikz-Grafik
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Diagramme/Mermaid/[Diagrammname].mmd` enthält den Quelltext einer Mermaid.js-Grafik
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Diagramme/Mermaid/[Diagrammname].svg` enthält die kompilierte SVG-Datei für eine Mermaid.js-Grafik
- Der Ordner `./Folien/[XX_Kapitel_Bezeichnung]/Illustrationen` enthält mit Nano Banana generierte Illustrationen
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Illustrationen/[Illustrationsname].jpg` ist eine spezielle Illustration
- Der Ordner `./Folien/[XX_Kapitel_Bezeichnung]/Screenshots` enthält Screenshots von selbst entwickelten Simulationsprogrammen
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Screenshots/[Screenshotname].png` ist ein spezieller Screenshot
- Der Ordner `./Folien/[XX_Kapitel_Bezeichnung]/Tafelbilder` enthält Fotografien von Tafelbildern, die während dem Unterricht entstanden sind
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Tafelbilder/[Tafelbildname].jpg` ist ein spezielles Tafelbild
- Der Ordner `./Folien/[XX_Kapitel_Bezeichnung]/Fotografien` enthält alle sonstigen Fotografien von Personen, Gegenständen, und Situationen
- Der Datei `./Folien/[XX_Kapitel_Bezeichnung]/Fotografien/[Fotografiename].jpg` ist eine spezielles Fotografie
- Der Ordner `./Quellen` enthält die zugehörigen Quelldateien der MATLAB Modelle
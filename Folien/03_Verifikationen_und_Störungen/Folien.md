---
marp: true
theme: fhooe
header: MSE - Kapitel 3: Verifikationen und Störungen
footer: Dr. Georg Hackenberg, Professor für Informatik und Industriesysteme
paginate: true
math: mathjax
---

<!-- Eine abstrakte Darstellung von Verifikation und Störungen. Ein komplexes, leuchtendes Netzwerk aus verbundenen Knoten symbolisiert Systemtests, wobei einige Knoten rot aufblitzen, um Fehler anzuzeigen. Das Ganze schwebt vor einer dunklen Galaxie, die die Weite und Komplexität des zu analysierenden Systems darstellt. -->

![bg right](./Titelbild.jpg)

# Kapitel 3: Verifikationen und Störungen

In diesem Kapitel lernen wir das Folgende:

1. Verifikation von Modellen mit Simulink Test
2. Analyse von Störfällen mit Simulink Fault Analyzer

---

<!-- Eine abstrakte Illustration der Verifikation. Eine Reihe von grünen Häkchen und perfekt ineinandergreifenden Puzzleteilen schweben vor einem wirbelnden kosmischen Nebel. Dies visualisiert den Prozess der erfolgreichen Überprüfung und Modellvalidierung. -->

![bg right](./Illustrationen/Abschnitt_1.jpg)

## 3.1: Verifikation mit Simulink Test

Dieser Abschnitt umfasst die folgenden Inhalte:

1. Grundlagen der Verifikation
2. Test-Manager in Simulink Test
3. Testsequenzen und -bewertungen
4. Test-Harness
5. Fallbeispiel: Akku-Schrauber
6. Übungsaufgabe: 3D-Drucker

---

<!-- Eine abstrakte Darstellung der Grundlagen der Verifikation. Eine grundlegende geometrische Form, wie ein leuchtender Würfel, wird von Linien und Pfeilen umgeben, die auf seine Oberflächen zeigen. Dies symbolisiert die Kernprinzipien der Verifikation vor einem ruhigen, dunklen Sternenhimmel. -->

![bg right](./Illustrationen/Abschnitt_1_1.jpg)

### 3.1.1: Grundlagen der Verifikation

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Definition und Zweck der Verifikation
2. Testgetriebene Entwicklung
3. Verifikationsstufen (MIL, SIL, PIL, HIL)

---

#### Was ist Verifikation?

Die Verifikation ist der Prozess, bei dem überprüft wird, ob ein System oder eine Komponente die spezifizierten Anforderungen erfüllt. Es wird die Frage beantwortet: "Bauen wir das System richtig?"

---

##### Testgetriebene Entwicklung

Bei der testgetriebenen Entwicklung (Test-Driven Development, TDD) werden die Tests vor der eigentlichen Implementierung geschrieben. Dies hilft, die Anforderungen klar zu definieren und stellt sicher, dass die Implementierung testbar ist.

---

#### Verifikationsstufen

- **Model-in-the-Loop (MIL):** Testen des Modells in einer reinen Simulationsumgebung.
- **Software-in-the-Loop (SIL):** Testen des aus dem Modell generierten Codes auf dem Entwicklungsrechner.
- **Processor-in-the-Loop (PIL):** Testen des generierten Codes auf der Zielhardware.
- **Hardware-in-the-Loop (HIL):** Testen der Zielhardware mit dem darauf laufenden Code gegen eine Simulation der Systemumgebung.

---

<!-- Eine abstrakte Darstellung des Test-Managers. Eine zentrale, leuchtende Kugel orchestriert kleinere, umkreisende Lichtpunkte. Dies symbolisiert, wie der Test-Manager verschiedene Testfälle und -suiten innerhalb eines dichten Sternhaufens in einer Galaxie organisiert. -->

![bg right](./Illustrationen/Abschnitt_1_2.jpg)

### 3.1.2: Test-Manager in Simulink Test

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Übersicht und UI des Test-Managers
2. Hierarchie: Test-Datei, Test-Suite, Test-Case
3. Konfiguration eines Test-Cases

---

#### Übersicht des Test-Managers

Der Test-Manager ist die zentrale Anlaufstelle für die Verwaltung, Ausführung und Auswertung von Tests in Simulink.

---

##### Test-Hierarchie

- **Test-Datei:** Enthält eine oder mehrere Test-Suiten.
- **Test-Suite:** Gruppiert zusammengehörige Test-Cases.
- **Test-Case:** Definiert einen einzelnen Test mit System-Under-Test, Eingangsdaten und Bewertungskriterien.

---

<!-- Eine abstrakte Darstellung von Testsequenzen. Eine leuchtende Zeitachse aus pulsierenden Lichtern bewegt sich von links nach rechts, wobei Kontrollpunkte aufleuchten, wenn die Sequenz sie passiert. Dies repräsentiert den Ablauf von Testsequenzen und Bewertungen vor dem Hintergrund des tiefen Weltraums. -->

![bg right](./Illustrationen/Abschnitt_1_3.jpg)

### 3.1.3: Testsequenzen und -bewertungen

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Verwendung des Test Sequence Blocks
2. When-Dekomposition zur Strukturierung
3. Assertions und logische Bewertungen

---

#### Test Sequence Block

Der Test Sequence Block ermöglicht die Erstellung komplexer Testabläufe mit zeitlicher Abfolge von Aktionen und Überprüfungen direkt im Modell.

---

##### When-Dekomposition

Innerhalb des Test Sequence Blocks können `when`-Bedingungen verwendet werden, um den Test in logische Schritte zu unterteilen, die unter bestimmten Bedingungen oder zu bestimmten Zeiten aktiv werden.

---

<!-- Eine abstrakte Darstellung eines Test-Harness. Eine schützende, transparente Sphäre umschließt eine komplexe, leuchtende Struktur (das zu testende System) und isoliert sie von der umgebenden kosmischen Umgebung. Dies illustriert das Konzept einer kontrollierten Testumgebung. -->

![bg right](./Illustrationen/Abschnitt_1_4.jpg)

### 3.1.4: Test-Harness

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Konzept des Test-Harness
2. Erstellung und Management

---

#### Was ist ein Test-Harness?

Ein Test-Harness ist ein separates Modell, das eine Komponente (das "System under Test") isoliert und eine kontrollierte Umgebung für das Testen bereitstellt.

---

<!-- Eine abstrakte Darstellung des Fallbeispiels Akku-Schrauber. Glühende blaue und weiße Konstellationen formen die Silhouette eines Akku-Schraubers, dessen interne Mechanik als separate, hellere Sternenkarte hervorgehoben wird. Das Ganze ist vor einer dunklen Galaxie dargestellt. -->

![bg right](./Illustrationen/Abschnitt_1_5.jpg)

### 3.1.5: Fallbeispiel: Akku-Schrauber

Dieser Unterabschnitt wendet die Konzepte auf das Fallbeispiel an.

---

#### Testen des Antriebsmodells

Anwendung der Testmethoden auf das Antriebsmodell des Akku-Schraubers zur Überprüfung der funktionalen Anforderungen.

---

<!-- Eine abstrakte Darstellung der Übungsaufgabe 3D-Drucker. Ein stilisierter, leuchtender Drahtgitter-Extruderkopf eines 3D-Druckers zieht eine leuchtende Bahn in der Leere des Weltraums, vor dem Hintergrund einer fernen Galaxie. -->

![bg right](./Illustrationen/Abschnitt_1_6.jpg)

### 3.1.6: Übungsaufgabe: 3D-Drucker

Dieser Unterabschnitt beschreibt die Übungsaufgabe.

---

#### Aufgabe: Verifikation des Heizbetts

Erstellen Sie Test-Cases mit dem Test-Manager, um die Anforderungen an das Heizbett des 3D-Druckers zu verifizieren.

---

<!-- Eine abstrakte Darstellung der Störungsanalyse. Eine zerbrochene, leuchtende geometrische Form mit Rissen aus roter Energie, die sich durch sie ziehen, symbolisiert einen Systemfehler. Die Szene ist vor einem turbulenten, stürmischen Nebel angesiedelt. -->

![bg right](./Illustrationen/Abschnitt_2.jpg)

## 3.2: Störungsanalyse mit Simulink Fault Analyzer

Dieser Abschnitt umfasst die folgenden Inhalte:

1. Grundlagen der Störungsanalyse
2. Fault Analyzer App
3. Störungsmodellierung und -injektion
4. Sicherheitsanalyse (FMEA)
5. Fallbeispiel: Akku-Schrauber
6. Übungsaufgabe: 3D-Drucker

---

<!-- Eine abstrakte Darstellung der Grundlagen der Störungsanalyse. Zwei gegensätzliche abstrakte Formen schweben vor einem Doppelsternsystem: Eine stabile, stetig blau leuchtende Form (Fail-Safe) und eine andere, die Anzeichen von Beschädigung zeigt, aber ihre Kernstruktur mit einem widerstandsfähigen goldenen Licht beibehält (Fail-Operational). -->

![bg right](./Illustrationen/Abschnitt_2_1.jpg)

### 3.2.1: Grundlagen der Störungsanalyse

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Definition und Arten von Störungen
2. Sicherheitskonzepte (Fail-Safe, Fail-Operational)

---

#### Was ist eine Störung?

Eine Störung (Fault) ist eine anormale Bedingung oder ein Defekt auf Komponentenebene, der zu einem Ausfall (Failure) des Systems führen kann.

---

##### Sicherheitskonzepte

- **Fail-Safe:** Das System geht im Fehlerfall in einen sicheren Zustand über.
- **Fail-Operational:** Das System kann seine Funktion auch im Fehlerfall (ggf. eingeschränkt) aufrechterhalten.

---

<!-- Eine abstrakte Darstellung der Fault Analyzer App. Ein digitales Dashboard mit leuchtenden Diagrammen und Graphen schwebt im Weltraum und zeigt Fehlerdaten und Analyseergebnisse vor dem Hintergrund einer Spiralgalaxie. -->

![bg right](./Illustrationen/Abschnitt_2_2.jpg)

### 3.2.2: Fault Analyzer App

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Übersicht der App und des Workflows
2. Verwaltung von Störungen im Katalog

---

#### Übersicht der Fault Analyzer App

Die App bietet eine grafische Oberfläche zur Definition, Verwaltung und Analyse von Störungen und deren Auswirkungen auf das Systemverhalten.

---

<!-- Eine abstrakte Darstellung der Störungsmodellierung und -injektion. Ein Strom roter, störungsartiger Partikel wird in ein stabiles, blaues Energienetz injiziert, was zu lokalen Unterbrechungen führt. Die Szene spielt sich vor einem dunklen Nebel ab. -->

![bg right](./Illustrationen/Abschnitt_2_3.jpg)

### 3.2.3: Störungsmodellierung und -injektion

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Hinzufügen von Störungen zu Modellen
2. Bedingte und zeitgesteuerte Störungsinjektion

---

#### Hinzufügen von Störungen

Störungen werden über spezielle Blöcke (z.B. Fault Inport/Outport) in das Simulink-Modell eingefügt, um deren Verhalten zu simulieren.

---

<!-- Eine abstrakte Darstellung der Sicherheitsanalyse (FMEA). Ein komplexes, vernetztes Netz von Knoten wird gezeigt, bei dem einige Pfade rot hervorgehoben sind, um die Ausbreitung eines Fehlers zu verfolgen. Die Darstellung ähnelt einer Himmelskarte, die Flugbahnen von Asteroiden zeigt. -->

![bg right](./Illustrationen/Abschnitt_2_4.jpg)

### 3.2.4: Sicherheitsanalyse (FMEA)

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Durchführung einer FMEA
2. Analyse der Simulationsergebnisse

---

#### Durchführung einer FMEA

Systematische Analyse von potenziellen Fehlermodi und deren Auswirkungen (Failure Mode and Effects Analysis) mit Unterstützung des Fault Analyzers.

---

<!-- Eine abstrakte Darstellung des Fallbeispiels Akku-Schrauber. Eine stilisierte Darstellung eines Akku-Schraubers, ähnlich der vorherigen, aber diesmal mit einem leuchtenden roten Fehlersymbol, das auf seiner Motorkomponente erscheint, vor einem galaktischen Hintergrund. -->

![bg right](./Illustrationen/Abschnitt_2_5.jpg)

### 3.2.5: Fallbeispiel: Akku-Schrauber

Dieser Unterabschnitt wendet die Konzepte auf das Fallbeispiel an.

---

#### Analyse von Motorstörungen

Simulation von Störfällen wie einem Kurzschluss im Motor des Akku-Schraubers und Analyse der Auswirkungen.

---

<!-- Eine abstrakte Darstellung der Übungsaufgabe 3D-Drucker. Ein Drahtgittermodell eines 3D-Drucker-Extruders, bei dem ein leuchtendes rotes 'X' oder ein Blockadesymbol an der Düse erscheint. Das Ganze ist vor dem Hintergrund einer fernen, schwach leuchtenden Galaxie dargestellt. -->

![bg right](./Illustrationen/Abschnitt_2_6.jpg)

### 3.2.6: Übungsaufgabe: 3D-Drucker

Dieser Unterabschnitt beschreibt die Übungsaufgabe.

---

#### Aufgabe: Störungsanalyse des Extruders

Modellieren und analysieren Sie mögliche Störungen am Extruder des 3D-Druckers, wie z.B. eine verstopfte Düse.

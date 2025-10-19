---
marp: true
theme: fhooe
header: MSE - Kapitel 3: Verifikationen und Störungen
footer: Dr. Georg Hackenberg, Professor für Informatik und Industriesysteme
paginate: true
math: mathjax
---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für das Kapitel -->

![bg right](relativer Dateipfad des Titelbild für das Kapitel)

# Kapitel 3: Verifikationen und Störungen

In diesem Kapitel lernen wir das Folgende:

1. Verifikation von Modellen mit Simulink Test
2. Analyse von Störfällen mit Simulink Fault Analyzer

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Abschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Abschnitt)

## 3.1: Verifikation mit Simulink Test

Dieser Abschnitt umfasst die folgenden Inhalte:

1. Grundlagen der Verifikation
2. Test-Manager in Simulink Test
3. Testsequenzen und -bewertungen
4. Test-Harness
5. Fallbeispiel: Akku-Schrauber
6. Übungsaufgabe: 3D-Drucker

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

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

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

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

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

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

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

### 3.1.4: Test-Harness

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Konzept des Test-Harness
2. Erstellung und Management

---

#### Was ist ein Test-Harness?

Ein Test-Harness ist ein separates Modell, das eine Komponente (das "System under Test") isoliert und eine kontrollierte Umgebung für das Testen bereitstellt.

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

### 3.1.5: Fallbeispiel: Akku-Schrauber

Dieser Unterabschnitt wendet die Konzepte auf das Fallbeispiel an.

---

#### Testen des Antriebsmodells

Anwendung der Testmethoden auf das Antriebsmodell des Akku-Schraubers zur Überprüfung der funktionalen Anforderungen.

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

### 3.1.6: Übungsaufgabe: 3D-Drucker

Dieser Unterabschnitt beschreibt die Übungsaufgabe.

---

#### Aufgabe: Verifikation des Heizbetts

Erstellen Sie Test-Cases mit dem Test-Manager, um die Anforderungen an das Heizbett des 3D-Druckers zu verifizieren.

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Abschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Abschnitt)

## 3.2: Störungsanalyse mit Simulink Fault Analyzer

Dieser Abschnitt umfasst die folgenden Inhalte:

1. Grundlagen der Störungsanalyse
2. Fault Analyzer App
3. Störungsmodellierung und -injektion
4. Sicherheitsanalyse (FMEA)
5. Fallbeispiel: Akku-Schrauber
6. Übungsaufgabe: 3D-Drucker

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

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

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

### 3.2.2: Fault Analyzer App

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Übersicht der App und des Workflows
2. Verwaltung von Störungen im Katalog

---

#### Übersicht der Fault Analyzer App

Die App bietet eine grafische Oberfläche zur Definition, Verwaltung und Analyse von Störungen und deren Auswirkungen auf das Systemverhalten.

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

### 3.2.3: Störungsmodellierung und -injektion

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Hinzufügen von Störungen zu Modellen
2. Bedingte und zeitgesteuerte Störungsinjektion

---

#### Hinzufügen von Störungen

Störungen werden über spezielle Blöcke (z.B. Fault Inport/Outport) in das Simulink-Modell eingefügt, um deren Verhalten zu simulieren.

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

### 3.2.4: Sicherheitsanalyse (FMEA)

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1. Durchführung einer FMEA
2. Analyse der Simulationsergebnisse

---

#### Durchführung einer FMEA

Systematische Analyse von potenziellen Fehlermodi und deren Auswirkungen (Failure Mode and Effects Analysis) mit Unterstützung des Fault Analyzers.

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

### 3.2.5: Fallbeispiel: Akku-Schrauber

Dieser Unterabschnitt wendet die Konzepte auf das Fallbeispiel an.

---

#### Analyse von Motorstörungen

Simulation von Störfällen wie einem Kurzschluss im Motor des Akku-Schraubers und Analyse der Auswirkungen.

---

<!-- Detaillierte Beschreibung des Inhalts des Titelbildes für den Unterabschnitt -->

![bg right](relativer Dateipfad des Titelbild für den Unterabschnitt)

### 3.2.6: Übungsaufgabe: 3D-Drucker

Dieser Unterabschnitt beschreibt die Übungsaufgabe.

---

#### Aufgabe: Störungsanalyse des Extruders

Modellieren und analysieren Sie mögliche Störungen am Extruder des 3D-Druckers, wie z.B. eine verstopfte Düse.

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

1.  Definition und Zweck der Verifikation
2.  Verifikation vs. Validierung
3.  Testgetriebene Entwicklung (TDD)
4.  Verifikationsstufen im V-Modell (MIL, SIL, PIL, HIL)

---

### Verifikation & Validierung

**Verifikation** ist der Prozess, der sicherstellt, dass ein System oder eine Komponente seine spezifizierten Anforderungen erfüllt.
- Konformität mit der Spezifikation
- Interne Sicht auf die Korrektheit
- Frage: "Bauen wir das System richtig?"

**Validierung** ist der Prozess, der sicherstellt, dass das System die Bedürfnisse der Stakeholder und den beabsichtigten Verwendungszweck erfüllt.
- Erfüllung des Nutzerbedarfs
- Externe Sicht auf die Nützlichkeit
- Frage: "Bauen wir das richtige System?"

---

<div class="columns">
<div>

**Verifikation**

![w:1000](./Illustrationen/Verifikation.jpg)

</div>
<div>

**Validierung**

![w:1000](./Illustrationen/Validierung.jpg)

</div>
</div>

---

#### Testgetriebene Entwicklung (TDD)

Bei der testgetriebenen Entwicklung (Test-Driven Development, TDD) wird der Entwicklungszyklus durch das Schreiben von Tests gesteuert.

Dieser Ansatz zwingt zur Auseinandersetzung mit den Anforderungen, bevor Code oder Modelle erstellt werden, und führt zu modularen und testbaren Architekturen.

**Red-Green-Refactor-Zyklus:**

![](./Diagramme/Mermaid/TDD_Red_Green_Refactor.svg)

---

#### **Red-Green-Refactor**-Zyklus

<div class="columns top">
<div class="three">

##### 1. Red

Schreibe einen automatisierten Test, der eine neue Anforderung oder Funktion validiert.

Dieser Test muss zunächst fehlschlagen, da die Funktionalität noch nicht implementiert ist.

</div>
<div class="three">

##### 2. Green

Implementiere exakt die Funktionalität, die notwendig ist, damit der zuvor geschriebene Test erfolgreich durchläuft.

Ziel ist es nicht, perfekten Code zu schreiben, sondern nur den Test zu bestehen.

</div>
<div class="three">

##### 3. Refactor

Räume den Code oder das Modell auf (Refactoring), um die interne Struktur zu verbessern, ohne das extern beobachtbare Verhalten zu ändern.

Alle Tests müssen weiterhin erfolgreich sein.

</div>
</div>

---

<div class="columns">
<div>

#### Verifikationsstufen im V-Modell

Das V-Modell stellt den Zusammenhang zwischen Entwicklungs- und **Testphasen** dar. Jede Spezifikationsebene auf der linken Seite wird durch eine entsprechen-de **Testebene** auf der rechten Seite verifiziert:
- Komponententest (MIL/SIL/PIL)
- Integrationstest
- Systemtest (HIL)
- Abnahmetest

</div>
<div>

![Diagramm des V-Modells. Links absteigend: Systemanforderungen, Systemarchitektur, Komponenten-Design, Implementierung. Rechts aufsteigend: Komponententest (MIL/SIL/PIL), Integrationstest, Systemtest (HIL), Abnahmetest. Pfeile verbinden die korrespondierenden Ebenen. w:1000](./Diagramme/Draw/V-Modell.svg)

</div>
</div>

---

#### **Testebenen** im V-Modell

- **Komponententest (Unit Testing):** Überprüfung der korrekten Implementierung der Komponente gemäß Spezifikation. Finden von Fehlern auf der untersten Ebene.
- **Integrationstest:** Aufdeckung von Fehlern, die bei der Interaktion zwischen Komponenten auftreten (z.B. falsche Datenübergabe, Timing-Probleme).
- **Systemtest:** Überprüfung, ob das System die in den Systemanforderungen definierten funktionalen und nicht-funktionalen Anforderungen (z.B. Performance, Zuverlässigkeit, Sicherheit) erfüllt.
- **Abnahmetest (Acceptance Testing):** Bestätigung, dass das System die Erwartungen und vertraglichen Anforderungen erfüllt und für den Einsatz bereit ist.

---

#### **Testverfahren** im V-Modell (1 / 2)

Das folgende Diagramm veranschaulicht die verschiedenen Verifikationsstufen innerhalb des V-Modells, angefangen von der frühen Modellprüfung bis hin zum Testen mit realer Hardware. Es zeigt den Übergang von rein simulationsbasierten Tests (MIL) zu Hardware-nahen Tests (HIL).

![](./Diagramme/Mermaid/MIL_SIL_PIL_HIL.svg)

---

#### **Testverfahren** im V-Modell (2 / 2)


- **Model-in-the-Loop (MIL):** Testen des Modells in einer reinen Simulationsumgebung zur frühzeitigen Überprüfung von Algorithmen und Logik.
- **Software-in-the-Loop (SIL):** Testen des aus dem Modell automatisch generierten Quellcodes auf dem Entwicklungsrechner. Stellt die Korrektheit der Codegenerierung sicher.
- **Processor-in-the-Loop (PIL):** Testen des kompilierten Codes auf der Zielhardware (Prozessor). Verifiziert, dass der Code auf der Zielarchitektur korrekt ausgeführt wird.
- **Hardware-in-the-Loop (HIL):** Testen der finalen Steuerungshardware mit dem darauf laufenden Code gegen eine Echtzeitsimulation der physikalischen Systemumgebung (Strecke).

---

<!-- Eine abstrakte Darstellung des Test-Managers. Eine zentrale, leuchtende Kugel orchestriert kleinere, umkreisende Lichtpunkte. Dies symbolisiert, wie der Test-Manager verschiedene Testfälle und -suiten innerhalb eines dichten Sternhaufens in einer Galaxie organisiert. -->

![bg right](./Illustrationen/Abschnitt_1_2.jpg)

### 3.1.2: Test-Manager in Simulink Test

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1.  Übersicht und UI des Test-Managers
2.  Hierarchie: Test-Datei, Test-Suite, Test-Case
3.  Konfiguration eines Test-Cases (SUT, Inputs, Assessments)
4.  Optionen und Callbacks

---

#### Das Test-Manager User-Interface

Der Test-Manager ist die zentrale IDE für alle verifikationsbezogenen Aktivitäten in Simulink.

Er bietet Werkzeuge zum Erstellen, Verwalten, Ausführen und Analysieren von Tests.

![Screenshot des Simulink Test Managers. Links ist der "Test Browser" mit einer Baumstruktur aus Test-Dateien, -Suiten und -Cases markiert. In der Mitte ist der "Test Case Editor" mit Abschnitten wie "System Under Test", "Inputs" und "Assessments" hervorgehoben. Rechts ist das "Results and Artifacts" Panel sichtbar. bg contain right](./Screenshots/Simulink_Test_Manager.png)

---

<div class="columns">
<div class="five">

#### Test-Hierarchie: Strukturierung von Tests

Simulink Test organisiert Tests in einer dreistufigen Hierarchie, um Skalierbarkeit und Wiederverwendbarkeit über Projekte hinweg zu gewährleisten.

-   **Test-Datei (`.mldatx`):** Der Top-Level-Container. Er speichert allgemeine Einstellungen sowie die Test-Suites und Test-Cases.
-   **Test-Suite:** Gruppiert zusammengehörige Test-Cases. Suiten können verschachtelt werden, um eine Struktur abzubilden.
-   **Test-Case:** Die kleinste ausführbare Testeinheit. Definiert ein einzelnes zu testendes Szenario mit Eingaben / Ausgaben.

</div>
<div>

![](./Diagramme/Mermaid/Simulink_Test_Hierarchie.svg)

</div>
</div>

---

<div class="columns">
<div class="five">

#### Test-Datei (`.mldatx`)

Auf der obersten Ebene werden globale Konfigurationen gemacht:

-   **Tags:** Schlüsselwörter zur Filterung und Gruppierung von Tests (z.B. `functional`, `regression`).
-   **Description/Requirements:** Dokumentation des Testziels und Verknüpfung zu Anforderungsdokumenten.
-   **Callbacks:** MATLAB-Skripte, die vor oder nach dem Ausführen aller Tests in der Datei laufen (z.B. für Setup/Teardown).
-   **Coverage Settings:** Konfiguration der Metriken für die Modellabdeckung (z.B. Condition, Decision, MCDC).
-   **Test File Options:** Verwaltung von externen Testdaten.

</div>
<div>

![](./Diagramme/Mermaid/Simulink_Test_Hierarchie_File.svg)

</div>
</div>

---

![](./Screenshots/Simulink_Test_File.png)

---

#### Strategien zur Aufteilung von Test-Dateien

<div class="columns top">
<div>

##### 1. Komponente

Jede Hauptkomponente oder jedes Subsystem im Modell erhält eine eigene Test-Datei.

**Vorteile:**
- Sehr modular.
- Klar definierte Verantwortlichkeiten.
- Gut für große Teams.

</div>
<div>

##### 2. Test-Ebene

Tests werden nach ihrer Ebene im V-Modell gruppiert.

**Vorteile:**
- Passt gut zu formalen Prozessen.
- Trennt Unit- von Integrations- oder Systemtests.

</div>
<div>

##### 3. Anforderungssatz

Tests werden basierend auf High-Level-Features oder Anforderungs-dokumenten gruppiert.

**Vorteile:**
- Sehr gute Nachverfolgbarkeit.
- Erleichtert die Verifikation.

</div>
</div>

---

<div class="columns">
<div class="five">

#### Test-Suite

Auf Suite-Ebene können viele Einstellungen der Test-Datei überschrieben oder verfeinert werden:

-   **Tags / Requirements:** Eigene Tags und Anforderungs-Links nur für diese Suite.
-   **Callbacks:** Skripte, die vor/nach jedem Test-Case *in dieser Suite* ausgeführt werden.
-   **Coverage Settings:** Spezifische Abdeckungseinstellungen für eine Gruppe von Tests.

</div>
<div>

![](./Diagramme/Mermaid/Simulink_Test_Hierarchie_Suite.svg)

</div>
</div>

---

![](./Screenshots/Simulink_Test_Suite.png)

---

#### Typische Suite-Strukturen

Die folgende Suite-Struktur mit zugeordneten Testfällen würde sich z.B. für ein Antriebssystem eignen:

-   **Funktionale Tests:** Überprüfen das korrekte Verhalten gemäß der Spezifikation (z.B. `Test_Anlaufverhalten` und `Test_Lastwechsel`).
-   **Robustheitstests:** Testen das Verhalten bei ungültigen Eingaben oder an den Grenzen des Betriebsbereichs (z.B. `Test_Ueberspannung` oder `Test_Negative_Sollvorgabe`).
-   **Regressionstests:** Stellen sicher, dass frühere Funktionalität nicht durch Änderungen beeinträchtigt wurde.
-   **Sicherheitstests:** Überprüfen die Reaktion auf simulierte Störfälle (z.B. `Test_Motor_Blockiert`).

---

<div class="columns">
<div class="five">

#### Test-Case

Ein Test-Case besteht aus mehreren Abschnitten, die das "Was, Wie, Womit und Was-sollte-sein" eines Tests beschreiben:
-   **Tags / Description / Requirements:** Was wird getestet und warum? Verlinkung zur Anforderung.
-   **System Under Test:** Welches Modell oder welche Komponente wird getestet?
-   **Inputs:** Womit wird das SUT stimuliert? (Eingangssignale)
-   **Assessments:** Was ist das erwartete Ergebnis? (Bewertungskriterien)

</div>
<div>

![](./Diagramme/Mermaid/Simulink_Test_Hierarchie_Case.svg)

</div>
</div>

---

![](./Screenshots/Simulink_Test_Case.png)

---

#### Typische Test-Cases

<div class="columns top">
<div>

##### Anforderungstest

Der häufigste Fall: Ein Test-Case wird erstellt, um eine einzelne Anforder-ung zu verifizieren.

**Beispiel:** "Verifiziere REQ-MOTOR-05: Das maximale Überschwingen der Drehzahl darf 10% nicht überschreiten."

</div>
<div>

##### Grenzwertetest

Dieser Test prüft das Verhalten des Systems an den Rändern seines spezifizierten Betriebsbereichs.

**Beispiel:** "Was passiert bei maximaler Eingangsspan-nung und maximaler Last?"

</div>
<div>

##### Robustheitstest

Hier wird das System gezielt mit ungültigen oder unerwarteten Eingaben konfrontiert, um seine Robustheit zu prüfen.

**Beispiel:** "Wie reagiert das System auf eine Sollwert-Vorgabe von -100 U/min?"

</div>
</div>

---

#### Test-Case - **System Under Test (SUT)**

In diesem Abschnitt wird festgelegt, welche Komponente getestet wird und in welchem Kontext.

-   **Model:** Der Pfad zum Simulink-Modell (`.slx`).
-   **Test Harness:** Wenn ein Subsystem das SUT ist, wird hier das zu verwendende Test-Harness ausgewählt.
-   **Simulation Mode:** Legt fest, wie das Modell ausgeführt wird (z.B. `Normal`, `Accelerator`, `Software-in-the-Loop (SIL)`).
-   **Parameter Overrides:** Erlaubt das Überschreiben von Workspace-Variablen oder Block-Parametern für diesen spezifischen Test-Case.

---

![](./Screenshots/Simulink_Test_Case_SUT.png)

---

<div class="columns">
<div class="three">

#### Wahl des richtigen Simulationsmodus (1 / 2)

##### Normal / Accelerator

-   **Normal:** Das Modell wird interpretiert. Gut für Debugging.
-   **Accelerator:** Das Modell wird vor der Ausführung zu C-Code kompiliert. Deutlich schneller, ideal für rechenintensive Simulationen und große Testkampagnen.
-   Beide Modi werden für die grundlegende Verifikation der Algorithmen und Logik im Modell verwendet (**Model-in-the-Loop, MIL**).

</div>
<div>

![](./Diagramme/Mermaid/MIL_SIL_PIL_1.svg)

</div>
</div>

---

<div class="columns">
<div class="three">

#### Wahl des richtigen Simulationsmodus (2 / 2)

##### Software- / Processor-in-the-Loop (SIL/PIL)

-   **SIL:** Der aus dem SUT generierte Code wird auf dem Host-PC kompiliert und gegen das Test-Harness ausgeführt. Verifiziert die Korrektheit der Codegenerierung.
-   **PIL:** Der generierte Code wird auf dem Zielprozessor (z.B. einem embedded Mikrocontroller) ausgeführt. Verifiziert die Korrektheit auf der Zielhardware.
-   Diese Modi sind essenziell, um die Konformität zwischen Modell und finaler Implementierung sicherzustellen.

</div>
<div>

![](./Diagramme/Mermaid/MIL_SIL_PIL_2.svg)

</div>
</div>

---

#### Test-Case - **Inputs**

Dieser Abschnitt definiert die Stimuli, also die Eingangssignale, mit denen das SUT während des Tests angeregt wird. Es gibt verschiedene Quellen für diese Signale:

-   **Signal Editor Block:** Der Standard. Ermöglicht die grafische Definition von Signalverläufen (konstant, Rampe, Sinus, etc.) für mehrere Signale.
-   **MAT-Datei:** Importiert Signal-Daten aus einer `.mat`-Datei. Ideal, um aufgezeichnete reale Messdaten oder komplexe, vorgenerierte Signale zu verwenden.
-   **Test Sequence Block:** Die Eingänge können auch direkt aus einem `Test Sequence` Block kommen. Das ist nützlich, wenn die Stimuli von komplexen Zuständen im Testablauf abhängen.
-   **From Workspace:** Lädt die Eingangsdaten aus MATLAB Workspace-Variablen.

---

![](./Screenshots/Simulink_Test_Case_Inputs.png)

---

#### Strategien für Test-Eingangssignale

Die Wahl der richtigen Eingangssignale ist entscheidend für die Aussagekraft eines Tests. Hier sind drei mögliche Strategien:

<div class="columns top">
<div>

##### Synthetische Signale

Für die meisten funk-tionalen Tests werden einfache, synthetische Signale (Sprung, Rampe, Sinus) verwendet, um Reaktionen des Systems zu provozieren.

</div>
<div>

##### Aufgezeichnete Daten

Um das Verhalten unter realen Bedingungen zu prüfen, werden oft Daten aus Messfahrten oder Feldversuchen verwendet.

</div>
<div>

##### Zufällige Daten

Für Robustheitstests oder zur statistischen Absicherung werden oft zufällige oder pseudo-zufällige Eingangssignale verwendet (z.B. mit dem `Random Number` Block).

</div>
</div>

---

#### Test-Case - **Simulation Outputs**

In diesem Abschnitt wird festgelegt, welche Signale aus dem Modell während der Simulation aufgezeichnet (geloggt) werden sollen.

Die hier ausgewählten Signale stehen später für die Bewertung (Assessments) zur Verfügung. Es ist wichtig, alle Signale zu loggen, die zur Überprüfung der Anforderungen notwendig sind.

-   **Ausgangssignale:** Die Ports am Ausgang des SUT werden standardmäßig geloggt.
-   **Interne Signale:** Es können aber auch beliebige interne Signale innerhalb des SUT markiert und für die Aufzeichnung ausgewählt werden. Dies ist extrem nützlich für das Debugging und die Analyse von internen Zuständen des Reglers oder der Strecke.

---

![](./Screenshots/Simulink_Test_Case_Simulation_Outputs.png)

---

#### Typische zu loggende Signale

Was sollte man loggen? So viel wie nötig, so wenig wie möglich.

<div class="columns top">
<div>

##### Ausgänge

Alle Ausgangssignale des SUT sind fast immer relevant.
- `ist_drehzahl`
- `ist_temperatur`
- `status_led`

</div>
<div>

##### Interne Zustände

Signale, die für die Verifikation von Anforderungen oder das Debugging gebraucht werden.
- `regler_interner_zustand`
- `motor_strom`
- `fehler_flag`

</div>
<div>

##### Berechnete Werte

Abgeleitete Größen, die im Test ausgewertet werden sollen.
- `regel_abweichung` (soll - ist)
- `leistung` (spannung * strom)

</div>
</div>

---

#### Test-Case - **Sequence Diagram Assessment**

Unter `Assessments` wird die eigentliche Testlogik definiert. Eine mächtige Option hierfür ist der `Test Sequence` Block. Im Gegensatz zur reinen Stimuli-Generierung im `Inputs`-Bereich, kann ein `Test Sequence` Block hier sowohl das SUT anregen als auch dessen Reaktionen überwachen und bewerten.

-   **Struktur:** Der Block verwendet eine an Stateflow angelehnte Syntax mit Schritten (`Steps`) und Übergängen.
-   **Aktionen:** In jedem Schritt können Aktionen ausgeführt werden (z.B. Sollwerte ändern).
-   **Bewertung:** Die `verify` Anweisung prüft, ob eine Bedingung zu einem bestimmten Zeitpunkt wahr ist. Schlägt eine `verify` Bedingung fehl, schlägt der gesamte Test-Case fehl.

---

![](./Screenshots/Simulink_Test_Case_Sequence_Diagram_Assessment.png)

---

<div class="columns">
<div>

#### Typische Anwendung

Test Sequences eignen sich hervorragend für die Prüfung von **kausalen und temporalen Anforderungen**, bei denen eine bestimmte Abfolge von Aktionen und Reaktionen verifiziert werden muss.

**Anforderung:**
> "Wenn der Start-Knopf gedrückt wird, soll die Power-LED innerhalb von 50ms auf 'Grün' wechseln. Erst danach darf der Motor anlaufen."

</div>
<div>

```
// Step 1: Initial State
when (time > 1.0) {
  start_button = true;
  // Press button
  transition to Step 2;
}

// Step 2: Check LED
verify(led_status == GREEN);
// Check must pass immediately
verify(elapsed(50, msec));
// Check that it happened within 50ms
transition to Step 3;

// Step 3: Check Motor
verify(motor_speed > 0);
// Motor should only start now
```

</div>

---

#### Test-Case - **Baseline Criteria**

Ein Baseline-Test vergleicht das Verhalten des SUT mit einem zuvor aufgezeichneten "guten" Ergebnis.

-   **Ablauf:**
    1.  Man führt die Simulation einmal aus und überprüft manuell, ob die aufgezeichneten Signale (z.B. die `ist_drehzahl`) den Erwartungen entsprechen.
    2.  Dieses Ergebnis wird als "Baseline" gespeichert.
    3.  Für alle nachfolgenden Testläufe vergleicht Simulink Test das aktuelle Ergebnis automatisch mit der Baseline.
-   **Toleranzen:** Es können absolute, relative oder zeitliche Toleranzen definiert werden, innerhalb derer das Signal von der Baseline abweichen darf.

---

![](./Screenshots/Simulink_Test_Case_Baseline_Criteria.png)

---

#### Wann verwendet man Baseline-Tests?

Baseline-Tests sind besonders nützlich in zwei Hauptszenarien:

<div class="columns top">
<div>

##### 1. Regressionstests

Wenn eine Komponente geändert oder überarbeitet wird, will man sicherstellen, dass das bestehende, korrekte Verhalten nicht unbeabsichtigt verändert wurde ("Regression").

</div>
<div>

##### 2. Komplexe, nicht-lineare Systeme

Manchmal ist das erwartete Verhalten eines Systems zu komplex, um es mit einfachen `verify` Anweisungen zu beschreiben (z.B. das Schwingungsverhalten einer mechanischen Struktur).

</div>
</div>

---

#### Test-Case - **Logical and Temporal Assessments**

Dies ist die flexibelste und mächtigste Form der Bewertung. Sie ermöglicht die Definition von beliebigen, komplexen Testlogiken in einer eigenen Test-Beschreibungssprache, die an Stateflow erinnert.

-   **Operatoren:** Eine reichhaltige Bibliothek an logischen (`&&`, `||`, `!`) und temporalen Operatoren (`after`, `before`, `elapsed`, `count`) steht zur Verfügung.
-   **`verify` Anweisung:** Das Kernstück. `verify(condition)` prüft, ob eine Bedingung erfüllt ist.
-   **Struktur:** Die Logik kann durch `when`-Dekomposition und Zustände strukturiert werden, um auch sehr komplexe Szenarien abzubilden.

---

![](./Screenshots/Simulink_Test_Logical_And_Temporal_Assessment.png)

---

<div class="columns">
<div>

#### Typische Anwendung

Diese Art der Bewertung wird verwendet, um explizite, textuelle Anforderungen direkt in ausführbaren Testcode umzusetzen.

**Anforderung REQ-HB-02 (Überschwingen):**
> "Beim Erreichen der Solltemperatur von 60°C darf die gemessene Temperatur das Ziel um nicht mehr als 3°C überschreiten."

</div>
<div>

```
// Definiere Soll- und Maximaltemperatur
define soll_temp = 60;
define max_temp = soll_temp + 3;

// Überwache die Temperatur während
// der gesamten Simulation.
// Die verify-Anweisung wird in jedem
// Zeitschritt ausgewertet.
verify(ist_temperatur <= max_temp);
```

*Diese eine Zeile genügt, um die Anforderung für den gesamten Simulationslauf zu überwachen.*

</div>
</div>

---

#### Test-Case - **Custom Criteria**

Wenn die eingebauten Assessment-Möglichkeiten nicht ausreichen, können Sie mit `Custom Criteria` beliebigen MATLAB-Code zur Bewertung heranziehen.

-   **Funktionsweise:** Es wird eine MATLAB-Funktion geschrieben, die am Ende der Simulation aufgerufen wird.
-   **Übergabeparameter:** Diese Funktion erhält Zugriff auf alle geloggten Signale und Zeitdaten der Simulation.
-   **Rückgabewert:** Die Funktion muss einen booleschen Wert zurückgeben (`true` für bestanden, `false` für fehlgeschlagen) und kann zusätzlich eine Fehlermeldung generieren.

---

![](./Screenshots/Simulink_Test_Case_Custom_Criteria.png)

---

#### Typische Anwendung für Custom Criteria

<div class="columns">
<div>

##### Frequenzanalyse

**Anforderung:** "Die Resonanzfrequenz im Ausgangssignal darf nicht unter 50 Hz liegen."

**Umsetzung:**
Eine MATLAB-Funktion, die das Ausgangssignal mittels `fft()` (Fast Fourier Transform) analysiert, die dominante Frequenz findet und prüft, ob diese über dem Grenzwert liegt.

</div>
<div>

##### Statistische Auswertung

**Anforderung:** "Die Standardabweichung der Regelabweichung im stationären Zustand muss kleiner als 0.1 sein."

**Umsetzung:**
Eine MATLAB-Funktion, die den letzten Teil des Signals für die Regelabweichung extrahiert, mittels `std()` die Standardabweichung berechnet und mit dem Grenzwert vergleicht.

</div>
</div>

---

<!-- Eine abstrakte Darstellung von Testsequenzen. Eine leuchtende Zeitachse aus pulsierenden Lichtern bewegt sich von links nach rechts, wobei Kontrollpunkte aufleuchten, wenn die Sequenz sie passiert. Dies repräsentiert den Ablauf von Testsequenzen und Bewertungen vor dem Hintergrund des tiefen Weltraums. -->

![bg right](./Illustrationen/Abschnitt_1_3.jpg)

### 3.1.3: Testsequenzen und -bewertungen

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1.  Der Test Sequence Block
2.  Strukturierung mit `when`-Dekomposition
3.  Logische und temporale `verify` Operatoren
4.  Definition von Test-Szenarien

---

#### Der Test Sequence Block

Der `Test Sequence` Block ist ein mächtiges Werkzeug, um komplexe, zustandsbasierte Testabläufe und Bewertungen zu modellieren. Er nutzt eine an Stateflow angelehnte Syntax und Semantik.

<div class="columns">
<div class="three">

##### Hauptmerkmale:

-   **Schrittbasierte Ausführung:** Der Block durchläuft eine definierte Sequenz von Schritten (`Step`).
-   **Aktionen & Übergänge:** In jedem Schritt können Aktionen definiert und Bedingungen für den Übergang zum nächsten Schritt festgelegt werden.
-   **Stimuli-Generierung:** Kann Ausgangssignale erzeugen, um das SUT anzuregen.
-   **Bewertung:** Kann Eingangssignale vom SUT empfangen und mit `verify` Operatoren bewerten.

</div>
<div class="three">

![Screenshot eines einfachen Test Sequence Blocks. Im Editor sind zwei Schritte ('Step 1: Initialize', 'Step 2: Ramp Up') mit einem Pfeil dazwischen zu sehen. Im Code-Fenster steht `output = 0;` in Step 1 und `output = output + 1;` in Step 2.](placeholder.jpg)

</div>
</div>

---

#### Strukturierung mit `when`-Dekomposition

Die `when`-Dekomposition ist ein Mechanismus zur Strukturierung von parallelen oder zustandsabhängigen Testsequenzen innerhalb eines einzigen Test Sequence Blocks.

<div class="columns">
<div class="four">

Anstatt einer einzelnen, langen Sequenz von Schritten, ermöglicht `when` die Aufteilung in nebenläufige "Prozesse", die auf bestimmte Ereignisse oder Bedingungen reagieren.

**Beispiel:** Ein Prozess generiert Stimuli, während ein anderer parallel dazu die Systemantwort überwacht.

```
% Test Sequence Code
when (condition_A)
  % Sequenz für Fall A
  verify(data > 100);
when (condition_B)
  % Sequenz für Fall B
  verify(response_time < 2.0);
```

</div>
<div class="two">

![Screenshot des Test Sequence Editors mit When-Dekomposition. Links im Strukturbaum sind zwei 'when' Bedingungen ('when: high_load', 'when: low_load') unterhalb der Hauptsequenz zu sehen, was die parallele Struktur verdeutlicht.](placeholder.jpg)

</div>
</div>

---

#### Logische und Temporale `verify` Operatoren

Das Herzstück der Bewertung in Testsequenzen sind die `verify` Operatoren. Sie ermöglichen die formale Spezifikation von Anforderungen als überprüfbare Assertions.

| Operator         | Beschreibung                                                                       | Beispiel                               |
| ---------------- | ---------------------------------------------------------------------------------- | -------------------------------------- |
| `verify(cond)`   | Prüft, ob die boolesche Bedingung `cond` wahr ist.                                 | `verify(temperature <= 120)`           |
| `verify(A == B)` | Prüft auf Gleichheit. Auch `~=`, `<`, `>`, `<=`, `>=` sind möglich.                | `verify(target_speed == actual_speed)` |
| `verify(t, E)`   | (Temporal) Prüft, ob das Ereignis `E` zum Zeitpunkt `t` eintritt.                  | `verify(after(5, sec), motor_off == 1)` |
| `verify(in(E))`  | (Temporal) Prüft, ob das Ereignis `E` während des aktuellen Zeitschritts eintritt. | `verify(in(overheat_warning))`         |

Die Kombination mit temporalen Operatoren wie `after`, `before`, `elapsed` und `count` ermöglicht die Prüfung komplexer Echtzeitanforderungen.

---

#### Beispiel: Temporale `verify` Anweisung

**Anforderung:** "Nachdem der `start` Befehl gegeben wurde, muss das Signal `status` innerhalb von 200 Millisekunden den Wert 4 erreichen und dort für mindestens 1 Sekunde bleiben."

**Umsetzung in Test Sequence:**

```
when (in(start_command)) {
  // Check for response within 200 ms
  verify(after(200, msec), status == 4);

  // Check if status remains 4 for 1 sec
  when (status == 4) {
    verify(elapsed(1, sec));
  }
}
```

Diese deklarative Art der Testspezifikation ist präzise, lesbar und direkt mit den textuellen Anforderungen verknüpfbar.

---

<!-- Eine abstrakte Darstellung eines Test-Harness. Eine schützende, transparente Sphäre umschließt eine komplexe, leuchtende Struktur (das zu testende System) und isoliert sie von der umgebenden kosmischen Umgebung. Dies illustriert das Konzept einer kontrollierten Testumgebung. -->

![bg right](./Illustrationen/Abschnitt_1_4.jpg)

### 3.1.4: Test-Harness

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1.  Zweck und Vorteile eines Test-Harness
2.  Erstellung und Konfiguration
3.  Management von Test-Harnesses
4.  Synchronisation mit dem Hauptmodell

---

#### Zweck und Vorteile eines Test-Harness

Ein Test-Harness ist ein separates, eigenständiges Simulink-Modell, das eine Komponente (das SUT) für Testzwecke kapselt.

<div class="columns">
<div class="two">

##### Hauptvorteile:

-   **Isolation:** Das SUT wird von der Komplexität des Gesamtmodells entkoppelt. Dies vereinfacht das Testen und die Analyse erheblich.
-   **Kontrollierte Umgebung:** Das Harness stellt alle notwendigen Eingaben, Ausgaben und Konfigurationen bereit, um das SUT in einer kontrollierten und reproduzierbaren Umgebung zu betreiben.
-   **Wiederverwendbarkeit:** Ein Harness kann für viele verschiedene Test-Cases verwendet werden.
-   **Reduzierte Komplexität:** Da nur das SUT und die Testumgebung geladen und kompiliert werden, sind Simulationen oft schneller.
-   **Saubere Trennung:** Hält das produktive Modell frei von Test-Logik und -Artefakten.

</div>
<div class="four">

![Diagramm, das das Konzept eines Test-Harness zeigt. In der Mitte ist ein Block "System Under Test". Pfeile von einem "Inputs / Stimuli" Block (z.B. Signal Builder) zeigen auf das SUT. Pfeile vom SUT zeigen auf einen "Outputs / Sinks / Assessments" Block (z.B. Scope, Test Sequence). Das Ganze ist von einem Rahmen mit der Beschriftung "Test Harness Model" umgeben.](placeholder.jpg)

</div>
</div>

---

#### Erstellung und Konfiguration eines Test-Harness

Simulink bietet einen automatisierten Prozess zur Erstellung von Test-Harnesses.

1.  **Rechtsklick auf das Subsystem:** Wählen Sie im Kontextmenü `Test Harness` -> `Create for [subsystem_name]`.
2.  **Konfigurationsdialog:**
    -   **Name:** Geben Sie dem Harness einen aussagekräftigen Namen.
    -   **Sources & Sinks:** Legen Sie fest, wie die Ein- und Ausgänge des SUT im Harness dargestellt werden sollen (z.B. `Inport`/`Outport` Blöcke, `Signal Builder`, `Scope`).
    -   **Synchronisation:** Konfigurieren Sie, ob Änderungen am SUT automatisch in das Harness übernommen werden sollen.
    -   **Post-Create Callback:** Führen Sie ein Skript aus, nachdem das Harness erstellt wurde (z.B. um Test-Parameter zu laden).

![Screenshot des 'Create Test Harness' Dialogs in Simulink. Die Felder für Name, Sources und Sinks sind sichtbar. Unter 'Source' ist die Option 'Signal Builder' ausgewählt, unter 'Sinks' die Option 'Scope'.](placeholder.jpg)

---

#### Management von Test-Harnesses

Ein einzelnes Subsystem kann mehrere Test-Harnesses besitzen, z.B. für verschiedene Testkategorien wie funktionales Testen, Äquivalenztests oder Robustheitstests.

<div class="columns">
<div class="two">

-   **Öffnen:** Über das Subsystem-Kontextmenü oder direkt im Test-Manager.
-   **Aktivieren:** Man kann zwischen den verschiedenen Harnesses für ein SUT wechseln.
-   **Löschen:** Nicht mehr benötigte Harnesses können entfernt werden.
-   **Exportieren:** Ein Harness kann in ein eigenständiges Modell exportiert werden.

Die Harnesses werden zusammen mit dem Hauptmodell gespeichert, aber als separate Artefakte verwaltet.

</div>
<div class="four">

![Screenshot, der das Badge-Symbol an einem Simulink-Subsystem zeigt, welches anzeigt, dass Test-Harnesses vorhanden sind. Ein Klick auf das Symbol öffnet ein Menü mit einer Liste der verfügbaren Harnesses ('Functional_Tests', 'Fault_Tests') und der Option 'Manage Harnesses'.](placeholder.jpg)

</div>
</div>

---

#### Synchronisation mit dem Hauptmodell

Eine kritische Funktion ist die Synchronisation zwischen der Komponente im Hauptmodell und der Kopie im Test-Harness.

-   **Push:** Änderungen am SUT im Test-Harness können in das Hauptmodell zurückgespielt werden. Dies ist nützlich, wenn während des Testens ein Fehler im SUT gefunden und behoben wird.
-   **Pull (Rebuild):** Änderungen am SUT im Hauptmodell werden in das Test-Harness übernommen. Dies ist der Standardfall, um sicherzustellen, dass immer die aktuelle Version der Komponente getestet wird.

Simulink warnt den Benutzer, wenn die Komponente im Harness nicht mehr mit der im Hauptmodell synchron ist. Eine konsistente Strategie für die Synchronisation ist entscheidend für die Verlässlichkeit der Testergebnisse.

---

<!-- Eine abstrakte Darstellung des Fallbeispiels Akku-Schrauber. Glühende blaue und weiße Konstellationen formen die Silhouette eines Akku-Schraubers, dessen interne Mechanik als separate, hellere Sternenkarte hervorgehoben wird. Das Ganze ist vor einer dunklen Galaxie dargestellt. -->

![bg right](./Illustrationen/Abschnitt_1_5.jpg)

### 3.1.5: Fallbeispiel: Akku-Schrauber

Dieser Unterabschnitt wendet die Konzepte auf das Fallbeispiel an und verifiziert eine Anforderung an das Antriebsmodell.

1.  Anforderung definieren
2.  Test-Case im Test-Manager anlegen
3.  Eingangssignal (Stimulus) erstellen
4.  Bewertung mittels Baseline-Test

---

#### Anforderung: Einschwingverhalten des Motors

Eine funktionale Anforderung an den Antrieb des Akku-Schraubers könnte lauten:

**REQ-MOTOR-01: Schnelles Anlaufverhalten**
> "Bei einem Drehzahlsollwertsprung von 0 auf 500 U/min bei Nennlast soll die Motordrehzahl innerhalb von **1.5 Sekunden** einen Bereich von **+/- 5%** um den Sollwert erreichen und darin verbleiben."

Diese Anforderung spezifiziert sowohl die **Anstiegszeit** als auch das **stationäre Verhalten** und eignet sich ideal für einen Baseline-Test.

---

<div class="columns">
<div class="two">

#### Anlegen des Test-Cases

1.  **Test-Datei erstellen:** `Antriebs-Tests.mldatx`
2.  **Test-Suite anlegen:** `Funktionale Tests`
3.  **Test-Case anlegen:** `Test_Anlaufverhalten_REQ_MOTOR_01`
4.  **SUT festlegen:** Das Subsystem, das den Motor und seine Regelung enthält, wird als `System Under Test` ausgewählt.
5.  **Test-Harness erstellen:** Für das Motor-Subsystem wird ein neues Harness mit einem `Signal Builder` als Eingang und einem `Scope` als Ausgang generiert.

</div>
<div class="four">

![Screenshot des Test-Managers. Links ist die Hierarchie mit 'Antriebs-Tests', 'Funktionale Tests' und 'Test_Anlaufverhalten_REQ_MOTOR_01' zu sehen. Im Editor ist das Motor-Subsystem als SUT eingetragen.](placeholder.jpg)

</div>
</div>

---

#### Erstellen des Eingangssignals (Stimulus)

Im `Signal Builder` Block innerhalb des Test-Harness wird das Eingangssignal für den Drehzahlsollwert definiert:

1.  Ein Signal `soll_drehzahl` wird erstellt.
2.  Zum Zeitpunkt `t = 0.5s` wird ein Sprung von `0` auf `500` U/min definiert.
3.  Ein zweites Signal `lastmoment` wird konstant auf Nennlast (z.B. `0.2 Nm`) gesetzt.

![Screenshot des Signal Builder Fensters. Zwei Signale sind sichtbar: 'soll_drehzahl' zeigt einen Sprung von 0 auf 500 bei t=0.5. Das zweite Signal 'lastmoment' ist eine konstante Linie bei 0.2.](placeholder.jpg)

---

#### Durchführung und Bewertung als Baseline-Test

1.  **Baseline erstellen:** Der Test wird einmal ausgeführt. Das Ergebnis (der Zeitverlauf der `ist_drehzahl`) wird im `Results & Artifacts` Bereich inspiziert. Wenn das Verhalten den Erwartungen entspricht, wird es per Rechtsklick als Baseline gespeichert.
2.  **Baseline-Kriterium hinzufügen:** Im Abschnitt `Assessments` des Test-Cases wird ein `Baseline` Kriterium hinzugefügt und mit der gespeicherten Baseline verknüpft. Toleranzen werden gesetzt (z.B. `Absolute Tolerance = 25` U/min, entsprechend 5% von 500).
3.  **Test erneut ausführen:** Der Test wird erneut ausgeführt. Simulink Test vergleicht nun automatisch das aktuelle Simulationsergebnis mit der Baseline.
4.  **Ergebnis analysieren:** Das Ergebnis wird als `Passed` oder `Failed` angezeigt. Bei `Failed` zeigt ein Plot exakt die Abweichung zwischen dem aktuellen Signal und der Baseline an.

---

<!-- Eine abstrakte Darstellung der Übungsaufgabe 3D-Drucker. Ein stilisierter, leuchtender Drahtgitter-Extruderkopf eines 3D-Druckers zieht eine leuchtende Bahn in der Leere des Weltraums, vor dem Hintergrund einer fernen Galaxie. -->

![bg right](./Illustrationen/Abschnitt_1_6.jpg)

### 3.1.6: Übungsaufgabe: 3D-Drucker

Dieser Unterabschnitt beschreibt die Übungsaufgabe zur Verifikation des Heizbett-Reglers.

1.  Anforderungen spezifizieren
2.  Test-Harness für Heizbett-Regler erstellen
3.  Test-Cases implementieren (Baseline & Temporal)
4.  Tests ausführen und dokumentieren

---

#### Aufgabe 1: Anforderungen an das Heizbett formulieren

Definieren Sie mindestens zwei verifizierbare Anforderungen für den Temperaturregler des Heizbetts in der Anforderungsspezifikation (`.slreqx` Datei). Versehen Sie diese mit eindeutigen IDs.

**Beispiel-Anforderungen:**

-   **REQ-HB-01: Aufheizzeit:** "Das Heizbett muss eine Solltemperatur von 60°C (ausgehend von 20°C) in weniger als 180 Sekunden erreichen."
-   **REQ-HB-02: Überschwingen:** "Beim Erreichen der Solltemperatur darf die gemessene Temperatur das Ziel um nicht mehr als 3°C überschreiten (Überschwingen < 5%)."
-   **REQ-HB-03: Stationäre Genauigkeit:** "Im stationären Zustand muss die Temperatur im Bereich von +/- 1°C um den Sollwert gehalten werden."

---

#### Aufgabe 2: Test-Harness und Test-Cases anlegen

1.  Erstellen Sie ein Test-Harness für die Komponente, die den Heizbett-Regler enthält. Konfigurieren Sie es mit einem `Signal Builder` für den Temperatursollwert und `Scopes` zur Beobachtung von Soll- und Ist-Temperatur.
2.  Erstellen Sie eine Test-Datei `Heizbett_Tests.mldatx`.
3.  Legen Sie für jede Anforderung aus Aufgabe 1 einen eigenen Test-Case an und verlinken Sie diesen mit der jeweiligen Anforderung in der `.slreqx` Datei.

![Screenshot, der den 'Requirements' Bereich eines Test-Cases im Test-Manager zeigt. Eine Anforderung mit der ID 'REQ-HB-01' und der Beschreibung 'Aufheizzeit' ist mit dem Test-Case verlinkt.](placeholder.jpg)

---

#### Aufgabe 3: Test-Logik implementieren

Implementieren Sie die Bewertungskriterien für Ihre Test-Cases.

-   **Für REQ-HB-01 (Aufheizzeit):**
    -   Verwenden Sie einen `Test Sequence` Block.
    -   Definieren Sie einen Sollwertsprung von 20°C auf 60°C.
    -   Nutzen Sie eine `verify` Anweisung, die prüft, ob `ist_temp >= 60` innerhalb von 180 Sekunden eintritt. `verify(after(180, sec), ist_temp >= 60)`

-   **Für REQ-HB-02 & REQ-HB-03 (Überschwingen & Genauigkeit):**
    -   Verwenden Sie einen `Baseline` Test. Führen Sie eine Simulation mit einem gut abgestimmten Regler durch und speichern Sie das Ergebnis als Baseline.
    -   Definieren Sie passende Toleranzen, die das erlaubte Überschwingen und die stationäre Abweichung abdecken.

---

#### Aufgabe 4: Testausführung und Dokumentation

1.  Führen Sie alle Test-Cases im Test-Manager aus.
2.  Sollten Tests fehlschlagen, analysieren Sie die Ergebnisse mit den von Simulink Test bereitgestellten Plots und passen Sie ggf. die Reglerparameter im Modell an.
3.  Sobald alle Tests erfolgreich sind, generieren Sie einen Test-Report im PDF-Format über die `Report` Funktion im Test-Manager.
4.  Dieser Report dient als Nachweis (Traceability) dafür, dass die Anforderungen durch Tests abgedeckt und erfüllt sind.

![Screenshot der 'Generate Report' Vorschau im Simulink Test Manager. Es zeigt ein Deckblatt mit Metadaten und eine Zusammenfassung der Testergebnisse (z.B. '3 Passed, 0 Failed').](placeholder.jpg)

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

1.  Terminologie: Störung, Fehler, Ausfall
2.  Arten von Störungen
3.  Sicherheitskonzepte (Fail-Safe, Fail-Operational, Fail-Tolerant)

---

#### Terminologie: Störung, Fehler, Ausfall (Fault, Error, Failure)

In der System- und Sicherheitsanalyse ist eine präzise Terminologie entscheidend.

-   **Störung (Fault):**
    -   Die vermutete oder tatsächliche **Ursache** eines Problems.
    -   Eine anormale physikalische Bedingung oder ein Defekt (z.B. ein durchgebrannter Widerstand, ein Software-Bug, ein Sensor-Kurzschluss).
    -   Eine Störung ist statisch und muss nicht zwangsläufig zu einem Problem führen.

-   **Fehler (Error):**
    -   Ein **Zustand** im System, der von der korrekten oder erwarteten Systemoperation abweicht.
    -   Ein Fehler ist die Manifestation einer Störung. (z.B. ein falscher Wert wird von einem Sensor gelesen, eine Variable im Speicher wird korrumpiert).

-   **Ausfall (Failure):**
    -   Das extern beobachtbare **Ereignis**, bei dem ein System seine spezifizierte Funktion nicht mehr erbringt.
    -   Ein Ausfall tritt auf, wenn ein Fehler an die Systemgrenze propagiert.

**Kausalkette:** Eine **Störung** kann einen **Fehler** verursachen, der wiederum zu einem **Ausfall** führen kann.

---

#### Arten von Störungen

Störungen können nach verschiedenen Kriterien klassifiziert werden.

<div class="columns">
<div class="three">

##### Nach Dauer:

-   **Permanent:** Die Störung bleibt bestehen (z.B. Kabelbruch).
-   **Transien/Temporär:** Die Störung tritt nur für eine kurze Zeit auf (z.B. durch elektromagnetische Interferenz).
-   **Intermittierend:** Die Störung tritt sporadisch auf und verschwindet wieder (z.B. Wackelkontakt).

</div>
<div class="three">

##### Nach Natur:

-   **Hardware-Störungen:** Physikalische Defekte (Alterung, Fertigungsfehler).
-   **Software-Störungen:** Fehler im Code (logische Fehler, Speicherlecks).
-   **Systematische Störungen:** Fehler im Entwicklungsprozess (Anforderungsfehler, Designfehler).

</div>
<div class="three">

##### Nach Verhalten (Beispiele):

-   **Stuck-at-Zero/One:** Signal ist permanent auf 0 oder 1 fixiert.
-   **Offset:** Dem korrekten Wert wird ein konstanter Fehler addiert.
-   **Gain-Fehler:** Das Signal wird mit einem falschen Faktor skaliert.
-   **Verzögerung:** Das Signal wird verspätet geliefert.

</div>
</div>

---

#### Sicherheitskonzepte

Sicherheitskonzepte beschreiben, wie ein System auf das Auftreten von Störungen reagieren soll, um Schaden abzuwenden.

-   **Fail-Safe:**
    -   Das System geht im Fehlerfall in einen vordefinierten, sicheren Zustand über. Dieser Zustand ist typischerweise ein Zustand ohne Energie oder Bewegung.
    -   **Beispiel:** Eine Ampelanlage schaltet bei einer Störung auf gelbes Blinklicht oder komplett ab. Ein Zugbremssystem wird bei Druckverlust automatisch aktiviert.

-   **Fail-Operational:**
    -   Das System kann seine Funktion auch nach dem Eintreten einer (oder mehrerer) Störungen aufrechterhalten, möglicherweise mit reduzierter Leistung.
    -   Dies wird üblicherweise durch Redundanz erreicht.
    -   **Beispiel:** Ein Flugzeug mit mehreren redundanten Flugsteuerungssystemen (`Fly-by-Wire`).

-   **Fail-Tolerant:**
    -   Ein allgemeinerer Begriff, der die Fähigkeit eines Systems beschreibt, trotz Störungen weiterhin korrekt zu funktionieren. `Fail-Operational` ist eine spezifische Form der Fehlertoleranz.

---

<!-- Eine abstrakte Darstellung der Fault Analyzer App. Ein digitales Dashboard mit leuchtenden Diagrammen und Graphen schwebt im Weltraum und zeigt Fehlerdaten und Analyseergebnisse vor dem Hintergrund einer Spiralgalaxie. -->

![bg right](./Illustrationen/Abschnitt_2_2.jpg)

### 3.2.2: Fault Analyzer App

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1.  Workflow der Störungsanalyse
2.  Die Fault Analyzer UI
3.  Verwaltung von Störungen und Störungssätzen

---

#### Workflow der Störungsanalyse

Der typische Workflow mit dem Fault Analyzer folgt einem strukturierten Prozess, um die Auswirkungen von Störungen systematisch zu untersuchen.

1.  **Störungen definieren:** Identifizieren und definieren Sie potenzielle Störungen im System (z.B. Sensor fällt aus, Aktor klemmt).
2.  **Störungen modellieren:** Fügen Sie diese Störungen an den entsprechenden Stellen im Simulink-Modell hinzu.
3.  **Störungen aktivieren:** Legen Sie Bedingungen fest, wann eine Störung während der Simulation injiziert werden soll (z.B. zu einem bestimmten Zeitpunkt, bei Eintreten eines Ereignisses).
4.  **Simulationen ausführen:** Führen Sie Simulationen für jedes Fehlerszenario sowie eine nominale Simulation (ohne Fehler) als Referenz durch.
5.  **Ergebnisse analysieren:** Vergleichen Sie das Verhalten des Systems mit und ohne Störung, um die Auswirkungen zu verstehen.
6.  **Dokumentieren:** Erstellen Sie Berichte, z.B. für eine FMEA (Failure Mode and Effects Analysis).

---

#### Die Fault Analyzer UI

Die App bietet eine integrierte Umgebung für diesen Workflow.

![Screenshot der Fault Analyzer App. Markiert sind drei Hauptbereiche: 1. (links) Der "Fault Table", eine Tabelle mit allen definierten Störungen, ihren Namen, Speicherorten und Aktivierungsbedingungen. 2. (Mitte) Die "Model"-Ansicht, die die Hierarchie des Simulink-Modells zeigt. 3. (rechts) Der "Simulation"-Bereich mit Buttons zum Ausführen der nominalen Simulation und der "Fault Simulation Campaign".](placeholder.jpg)

---

#### Verwaltung von Störungen und Störungssätzen

-   **Störung (Fault):**
    -   Wird im Fault Analyzer erstellt und einem Modellelement (Block oder Signal) zugeordnet.
    -   Jede Störung hat einen Namen, eine Beschreibung und ein definiertes Verhalten (z.B. "force to value 0").

-   **Bedingung (Condition):**
    -   Eine logische Bedingung, die definiert, wann eine Störung aktiv wird.
    -   Kann zeitbasiert (`time > 10`) oder zustandsbasiert (`temperature > 90`) sein.
    -   Eine Störung, die keiner Bedingung zugeordnet ist, kann manuell aktiviert werden.

-   **Störungssatz (Fault Set):**
    -   Eine benannte Sammlung von einer oder mehreren Störungen, die für eine Simulationskampagne gleichzeitig aktiviert werden.
    -   **Beispiel:** Ein Satz "Sensor-Fehler" könnte die Störungen "Kurzschluss Temperatursensor" und "Ausfall Drehzahlsensor" enthalten. Die Kampagne würde dann eine Simulation pro Störung in diesem Satz durchführen.

---

<!-- Eine abstrakte Darstellung der Störungsmodellierung und -injektion. Ein Strom roter, störungsartiger Partikel wird in ein stabiles, blaues Energienetz injiziert, was zu lokalen Unterbrechungen führt. Die Szene spielt sich vor einem dunklen Nebel ab. -->

![bg right](./Illustrationen/Abschnitt_2_3.jpg)

### 3.2.3: Störungsmodellierung und -injektion

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1.  Hinzufügen von Störungen zu Modellelementen
2.  Verwendung des `Fault Inport/Outport` Blocks
3.  Bedingte und zeitgesteuerte Störungsinjektion

---

#### Hinzufügen von Störungen zu Modellelementen

Der Fault Analyzer ermöglicht es, Störungen direkt zu vielen Standard-Simulink-Blöcken hinzuzufügen, ohne das Modelllayout zu verändern.

1.  **Rechtsklick auf einen Block:** Wählen Sie `Fault Analyzer` -> `Add Fault`.
2.  **Konfiguration:** Im Fault Analyzer wird eine neue Störung erstellt, die mit diesem Block assoziiert ist.
3.  **Fehlerverhalten definieren:** Sie können festlegen, wie sich der Block im Fehlerfall verhalten soll, z.B. einen Ausgangsport auf einen bestimmten Wert zwingen (`Force to value`).

<div class="columns">
<div class="two">

**Beispiel: Gain-Block**
Einem `Gain` Block kann eine Störung hinzugefügt werden, die seinen Gain-Parameter auf 0 setzt und so das Signal unterbricht.

**Beispiel: Relational Operator**
Einem Vergleichsoperator (`>`) kann eine Störung hinzugefügt werden, die sein Ergebnis invertiert.

</div>
<div class="four">

![Screenshot, der das Kontextmenü eines 'Gain'-Blocks in Simulink zeigt. Der Mauszeiger ist auf dem Menüpunkt 'Fault Analyzer' -> 'Add Fault' positioniert. Im Hintergrund ist die Fault Analyzer App zu sehen, in der eine neue, noch unbenannte Störung in der Tabelle erscheint.](placeholder.jpg)

</div>
</div>

---

#### Verwendung des `Fault Inport/Outport` Blocks

Für komplexere Störungsmodelle oder wenn eine Störung an einer Signalleitung statt an einem Block eingefügt werden soll, werden `Fault Inport` und `Fault Outport` Blöcke verwendet.

-   **`Fault Inport`:** Ersetzt das nominale Signal durch ein Fehlersignal, wenn die Störung aktiv ist. Das Fehlersignal wird an einem separaten Eingang des Blocks definiert.
-   **`Fault Outport`:** Leitet das nominale Signal an einen zusätzlichen Ausgang weiter, wenn die Störung aktiv ist. Dies kann zur Modellierung von Mitigationspfaden genutzt werden.

Diese Blöcke werden oft in einem `Subsystem` gekapselt, das als `Faulty_Sensor` oder `Faulty_Actuator` bezeichnet wird, um das Modell übersichtlich zu halten.

---

#### Bedingte und zeitgesteuerte Störungsinjektion

Die Aktivierung einer Störung wird über logische Bedingungen gesteuert. Dies ist entscheidend, um realistische Szenarien zu simulieren.

1.  **Störung auswählen:** Wählen Sie die zu konfigurierende Störung in der Fault Analyzer Tabelle aus.
2.  **Bedingung hinzufügen:** Klicken Sie auf `Add Condition`.
3.  **Bedingung definieren:** Geben Sie im `Condition` Feld eine MATLAB- oder Simulink-kompatible logische Expression ein.
    -   **Zeitgesteuert:** `time >= 5.2`
    -   **Zustandsabhängig:** `ist_drehzahl > 1000 && moment < 0.1`
    -   **Kombiniert:** `(time > 10) && (status == 2)`

Wenn die Bedingung während der Simulation `true` wird, wird die Störung injiziert und bleibt für den Rest der Simulation aktiv (es sei denn, sie wird anders modelliert).

![Screenshot des "Trigger" oder "Condition" Bereichs für eine Störung in der Fault Analyzer App. Ein Textfeld ist mit der Bedingung `time > 3.5` gefüllt. Ein Dropdown-Menü bietet Optionen wie 'On time', 'On event', 'Always on'.](placeholder.jpg)

---

<!-- Eine abstrakte Darstellung der Sicherheitsanalyse (FMEA). Ein komplexes, vernetztes Netz von Knoten wird gezeigt, bei dem einige Pfade rot hervorgehoben sind, um die Ausbreitung eines Fehlers zu verfolgen. Die Darstellung ähnelt einer Himmelskarte, die Flugbahnen von Asteroiden zeigt. -->

![bg right](./Illustrationen/Abschnitt_2_4.jpg)

### 3.2.4: Sicherheitsanalyse (FMEA)

Dieser Unterabschnitt umfasst die folgenden Inhalte:

1.  Konzept der FMEA
2.  Durchführung einer Simulationskampagne
3.  Analyse der Ergebnisse im Vergleich

---

#### Konzept der FMEA (Failure Mode and Effects Analysis)

Die FMEA ist eine systematische, induktive Methode zur Analyse der Sicherheit und Zuverlässigkeit eines Systems.

-   **Failure Mode:** Die Art und Weise, wie eine Komponente ausfallen kann (z.B. Kurzschluss, Bruch, falscher Software-Zustand).
-   **Effects Analysis:** Die Untersuchung der Konsequenzen jedes Fehlermodus für das lokale System, die nächsthöhere Systemebene und das Gesamtsystem (Endbenutzer).
-   **Ziel:** Potenzielle Ausfälle frühzeitig identifizieren, ihre Auswirkungen bewerten und Maßnahmen zur Risikominderung definieren.

Der Fault Analyzer ist ein Werkzeug zur **Validierung der "Effects Analysis"** durch Simulation.

---

#### Durchführung einer Simulationskampagne

Sobald Störungen und Störungssätze definiert sind, kann der Fault Analyzer eine "Simulation Campaign" durchführen.

1.  **Störungssatz auswählen:** Wählen Sie den Satz von Störungen aus, die Sie analysieren möchten.
2.  **Kampagne starten:** Klicken Sie auf `Run Fault Simulation(s)`.
3.  **Ablauf:** Der Fault Analyzer führt nun automatisch mehrere Simulationen durch:
    -   Eine **nominale Simulation** (Referenzlauf) ohne aktive Störungen.
    -   Für **jede Störung** im ausgewählten Störungssatz eine separate Simulation, in der nur diese eine Störung gemäß ihrer Bedingung injiziert wird.
4.  **Ergebnisspeicherung:** Alle Simulationsläufe werden aufgezeichnet und für den Vergleich gespeichert.

---

#### Analyse der Ergebnisse im Simulation Data Inspector

Nach der Kampagne können die Ergebnisse aller Läufe im `Simulation Data Inspector` verglichen werden.

<div class="columns">
<div class="two">

Der Vergleich der Zeitverläufe kritischer Signale zwischen dem nominalen und den fehlerhaften Läufen macht die **Auswirkungen (Effects)** der Störung direkt sichtbar.

##### Analysefragen:
-   Wird der sichere Zustand erreicht?
-   Wie schnell propagiert der Fehler durch das System?
-   Werden Sicherheitsgrenzen überschritten?
-   Funktionieren die implementierten Sicherheitsmechanismen wie erwartet?

</div>
<div class="four">

![Screenshot des Simulation Data Inspectors. Im Anzeigebereich werden mehrere Graphen übereinandergelegt. Eine schwarze Linie zeigt das 'nominale' Verhalten eines Signals 'temperatur'. Eine rote Linie, beschriftet mit 'Fault: sensor_stuck_at_80', weicht deutlich davon ab und bleibt konstant. Eine blaue Linie ('Fault: sensor_offset') verläuft parallel zur nominalen.](placeholder.jpg)

</div>
</div>

---

<!-- Eine abstrakte Darstellung des Fallbeispiels Akku-Schrauber. Eine stilisierte Darstellung eines Akku-Schraubers, ähnlich der vorherigen, aber diesmal mit einem leuchtenden roten Fehlersymbol, das auf seiner Motorkomponente erscheint, vor einem galaktischen Hintergrund. -->

![bg right](./Illustrationen/Abschnitt_2_5.jpg)

### 3.2.5: Fallbeispiel: Akku-Schrauber

Dieser Unterabschnitt wendet die Störungsanalyse auf das Fallbeispiel an.

1.  Fehlermodus definieren: Blockierter Motor
2.  Störung im Modell implementieren
3.  Simulation und Analyse der Auswirkung

---

#### Fehlermodus: Blockierter Motor

**Szenario:** Während des Betriebs blockiert der Antrieb des Akku-Schraubers mechanisch (z.B. die Schraube verkeilt sich).
**Erwartetes Verhalten:** Der Motorregler sollte den hohen Strom erkennen und den Motor abschalten, um eine Überhitzung oder Beschädigung zu verhindern (Sicherheitsfunktion).
**Fehlermodus:** Die Motordrehzahl fällt abrupt auf Null, obwohl der Regler weiterhin eine Spannung anlegt.
**Auswirkung:** Der Motorstrom (`I_motor`) steigt rapide an (Stall Current).

---

<div class="columns">
<div class="two">

#### Implementierung der Störung

1.  **Störung erstellen:** Im Fault Analyzer wird eine Störung mit dem Namen `Motor_Blocked` erstellt.
2.  **Störung zuordnen:** Die Störung wird der mechanischen Rotationsgeschwindigkeit im Simscape-Modell des Motors zugeordnet.
3.  **Verhalten definieren:** Das Verhalten wird so eingestellt, dass die Geschwindigkeit auf den Wert `0` gezwungen wird (`Force to value`).
4.  **Bedingung festlegen:** Die Störung wird zum Zeitpunkt `t = 2s` injiziert, nachdem der Motor normal angelaufen ist. `time >= 2.0`

</div>
<div class="four">

![Screenshot, der das Simscape-Modell des Motors zeigt. Eine Störung ist mit dem "Rotational Velocity" Port des Motorblocks verbunden. In der Fault Analyzer App ist die Störung 'Motor_Blocked' mit der Bedingung 'time >= 2.0' konfiguriert.](placeholder.jpg)

</div>
</div>

---

#### Simulation und Analyse der Auswirkung

Eine Simulationskampagne wird mit der `Motor_Blocked` Störung ausgeführt.

![Screenshot des Simulation Data Inspectors, der zwei Signale vergleicht: 'ist_drehzahl' und 'ist_strom'. Die nominalen Läufe (schwarz) zeigen normales Verhalten. Die fehlerhaften Läufe (rot, 'Fault: Motor_Blocked') zeigen, wie die Drehzahl bei t=2s auf Null fällt, während der Strom gleichzeitig auf einen sehr hohen Wert ansteigt und dort verbleibt, was auf eine fehlende oder fehlerhafte Schutzschaltung hindeutet.](placeholder.jpg)

**Analyse:** Der Plot zeigt deutlich den gefährlichen Anstieg des Motorstroms. Dies validiert die Notwendigkeit einer Überstrom-Schutzschaltung. In einem nächsten Schritt könnte eine solche Schutzschaltung modelliert und die Analyse wiederholt werden, um zu verifizieren, dass sie den Motor im Fehlerfall korrekt abschaltet.

---

<!-- Eine abstrakte Darstellung der Übungsaufgabe 3D-Drucker. Ein Drahtgittermodell eines 3D-Drucker-Extruders, bei dem ein leuchtendes rotes 'X' oder ein Blockadesymbol an der Düse erscheint. Das Ganze ist vor dem Hintergrund einer fernen, schwach leuchtenden Galaxie dargestellt. -->

![bg right](./Illustrationen/Abschnitt_2_6.jpg)

### 3.2.6: Übungsaufgabe: 3D-Drucker

Dieser Unterabschnitt beschreibt die Übungsaufgabe zur Störungsanalyse am Extruder des 3D-Druckers.

1.  Fehlermodi für den Extruder identifizieren
2.  Störungen modellieren und injizieren
3.  Auswirkungen analysieren (FMEA)
4.  (Optional) Sicherheitsmechanismus implementieren

---

#### Aufgabe 1: Fehlermodi identifizieren und modellieren

Identifizieren und modellieren Sie mindestens zwei realistische Störungen für den Extruder-Mechanismus des 3D-Druckers.

**Beispiel-Störungen:**

-   **`Nozzle_Clog` (Düse verstopft):**
    -   **Modellierung:** Fügen Sie dem Extruder-Antriebsmodell eine Störung hinzu, die ein extrem hohes Lastmoment simuliert oder die Geschwindigkeit des Vorschubmotors auf Null setzt.
    -   **Auswirkungshypothese:** Der Filamentvorschub stoppt, der Antriebsmotor könnte überlasten.

-   **`Heater_Sensor_Fail` (Temperatursensor defekt):**
    -   **Modellierung:** Fügen Sie dem Temperatursignal, das vom Sensor zum Regler geht, eine Störung hinzu. Modellieren Sie zwei Fälle: `Stuck-at-20` (Sensor liefert konstant Raumtemperatur) und `Stuck-at-250` (Sensor liefert Maximaltemperatur).
    -   **Auswirkungshypothese (`Stuck-at-20`):** Der Regler wird versuchen, ununterbrochen zu heizen, was zu einer gefährlichen Überhitzung führt (`Thermal Runaway`).

---

#### Aufgabe 2: Simulationskampagne durchführen

1.  Erstellen Sie im Fault Analyzer für jede Störung aus Aufgabe 1 ein entsprechendes `Fault` Objekt.
2.  Legen Sie sinnvolle Injektionsbedingungen fest (z.B. nach Erreichen der Solltemperatur).
3.  Fassen Sie die Störungen in einem Störungssatz `Extruder_Faults` zusammen.
4.  Führen Sie eine Simulationskampagne für diesen Störungssatz durch.

---

#### Aufgabe 3: FMEA-Analyse der Ergebnisse

Analysieren Sie die Simulationsergebnisse im `Simulation Data Inspector` und füllen Sie eine FMEA-Tabelle aus (z.B. in Excel oder als Markdown-Tabelle).

| Fehlermodus              | Mögliche Ursache        | Auswirkung (Lokal, System)                               | S (Severity) | Detektion                      | O (Occurrence) | D (Detection) | RPN |
| ------------------------ | ----------------------- | -------------------------------------------------------- | ------------ | ------------------------------ | -------------- | ------------- | --- |
| `Nozzle_Clog`            | Verunreinigtes Filament | Motor blockiert, Druckauftrag scheitert.                 | 6            | Hoher Motorstrom               | 4              | 3             | 72  |
| `Heater_Sensor_Stuck-20` | Kabelbruch              | **Unkontrolliertes Aufheizen**, Brandgefahr, Druck scheitert | **10**       | Plausibilitäts-Check (Software) | 2              | 5             | 100 |
| ...                      | ...                     | ...                                                      | ...          | ...                            | ...            | ...           | ... |

**Diskutieren Sie:** Welche Störung stellt das größte Risiko dar und warum?

---

#### Aufgabe 4 (Optional): Sicherheitsmechanismus implementieren

Wählen Sie die kritischste Störung (`Heater_Sensor_Stuck-at-20`) und implementieren Sie einen Sicherheitsmechanismus im Modell.

**Idee:** Ein einfacher `Stateflow` Chart oder MATLAB Function Block als "Watchdog".

**Logik:**
> "Wenn der Regler für mehr als 60 Sekunden eine Heizleistung von >95% ausgibt, die gemessene Temperatur sich aber um weniger als 1°C ändert, dann liegt eine Störung vor. Schalte in diesem Fall das Heizrelais ab und setze einen permanenten `Error` Status."

Verifizieren Sie anschließend durch eine erneute Störungssimulation, dass Ihr Sicherheitsmechanismus die gefährliche Überhitzung wirksam verhindert.

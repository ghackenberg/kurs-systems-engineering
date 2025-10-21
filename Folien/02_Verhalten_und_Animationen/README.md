---
marp: true
theme: fhooe
header: MSE - Kapitel 2: Verhalten und Animationen
footer: Dr. Georg Hackenberg, Professor für Informatik und Industriesysteme
paginate: true
math: mathjax
---

![bg right](./Titelbild.jpg)

# Kapitel 2: Verhalten und Animationen

Dieses Kapitel umfasst die folgenden vier Abschnitte:

1. **Simulink Signalmodelle**
2. **Simscape Physikmodelle**
3. **Stateflow Logikmodelle**
4. **Simulink 3D Animation**

---

#### Das richtige Werkzeug für jede Aufgabe

Mechatronische Systeme sind oft *hybride* Systeme, die unterschiedliche Arten von Verhalten kombinieren. MATLAB & Simulink bieten spezialisierte Werkzeuge für jede dieser Aufgaben, die oft im selben Modell kombiniert werden.

<div class="columns top">
<div>

##### Simulink: Signalfluss

Kausale Modellierung

*(Blöcke berechnen Ausgangsignale aus Eingangssignalen)*

`y(t) = f(t, u)`

</div>
<div>

##### Simscape: Physik

Akausale Modellierung

*(Blöcke definieren ein Gleichungssystem, das gelöst werden muss)*

`F(t, u, y) = 0`

</div>
<div>

##### Stateflow: Logik

Zustandsautomaten

*(Diskerete Zustände und Zustandsübergänge zu definierten Ereignissen)*

`On <-[Guard]-> Off`

</div>
</div>

---

![bg right](./Simulink.jpg)

## 2.1 Simulink **Signalmodelle**

In diesem ersten Abschnitt lernen wir die folgenden Dinge:

1. Grundlagen von Signalen (Zeitverlauf, Stetigkeit, Differenzierbarkeit)
2. Wichtige Simulink-Blöcke (zustandslos, mit Zuständen, Bibliothek)
3. TODO Solver

---

<div class="columns">
<div class="three">

### Was ist Simulink?

Simulink ist eine grafische Programmierumgebung für die Modellierung, Simulation und Analyse von dynamischen Systemen.

Es basiert auf dem Prinzip des **signalbasierten Designs**, bei dem Blöcke durch Linien verbunden werden, die den Signalfluss repräsentieren. Jede Linie transportiert ein Signal, z.B. einen Messwert oder einen Sollwert, von einem Block zum nächsten.

Simulink-Modelle werden über die Zeit simuliert, um das Verhalten eines Systems zu verstehen.

</div>
<div>


![](https://upload.wikimedia.org/wikipedia/commons/3/36/Simulink_Logo_%28non-wordmark%29.png)

</div>
</div>

---

![bg contain right](./Simulink_Signale.jpg)

### 2.1.1. Signale

Signale und deren mathematische Eigenschaften:

- Signale als Zeitverlaufs-funktionen
- Stetigkeit und Nicht-Stetigkeit von Signalen
- Differenzierbarkeit von Signalen
- Abschnittsweise Differenzierbarkeit von Signalen
- Eingangs- und Ausgangssignale

---

<div class="columns">
<div class="two">

#### Was ist ein Signal?

Ein **Signal** ist eine Funktion, die eine physikalische Größe über die Zeit beschreibt. Es repräsentiert den zeitlichen Verlauf von Informationen in einem System.

Mathematisch wird ein Signal als Funktion $s(t)$ ausgedrückt, wobei $t$ die Zeit ist. Der Wert des Signals zu einem Zeitpunkt $t$ kann sein:

- **Skalar:** Ein einzelner Wert (z.B. Temperatur).
- **Vektor:** Mehrere Werte (z.B. 3D-Position).
- **Matrix:** Eine Tabelle von Werten (z.B. Bilddaten).

</div>
<div>

![width:1000px](./Diagramme/Signal.svg)

</div>
</div>

---

<div class="columns">
<div class="two">

#### **Stetigkeit** von Signalen

Eine erste wichtige mathematische Eigenschaften der Signalfunktionen ist deren **Stetigkeit**:

- **Stetige Signale:** Ein Signal ist stetig, wenn sein Verlauf keine Sprünge aufweist. Viele physika-lische Größen wie die Geschwindigkeit und Position eines Körpers werden so modelliert.

- **Nicht-stetige Signale:** Diese Signale weisen Sprungstellen auf, wie z.B. das Signal eines `Step`-Blocks. Sie sind entscheidend für die Model-lierung von Schaltvorgängen und Ereignissen.

</div>
<div>

![width:1000px](./Diagramme/Signal_Stetigkeit.svg)

</div>
</div>

---

<div class="columns">
<div class="two">

#### **Differenzierbarkeit** von Signalen

Eine zweite wichtige mathematische Eigenschaft ist deren **Differenzierbarkeit:**

- **Differenzierbare Signale:** Sind "glatt" und stetig, d.h. sie besitzen an jedem Punkt eine eindeutige Ableitung. Dies ist ideal für die Modellierung von Systemen durch Differentialgleichungen.

- **Nicht-differenzierbare Signale:** Haben "Knick"-Stellen oder Sprünge, an denen keine eindeutige Ableitung existiert. Beispiele sind Rechtecksignale oder Signale mit abrupten Änderungen.

</div>
<div>

![width:1000px](./Diagramme/Signal_Differenzierbarkeit.svg)

</div>
</div>

---

<div class="columns">
<div class="two">

#### ***Abschnittsweise* Differenzierbarkeit** von Signalen

- Viele technische Signale sind nicht über ihren gesamten Verlauf differenzierbar, aber in einzelnen Abschnitten ("stückweise") schon.

- An den Übergangsstellen zwischen diesen Abschnitten (z.B. bei Sprüngen oder Knicken) ist das Signal nicht differenzierbar.

- Simulink-Solver sind darauf ausgelegt, solche abschnittsweise differenzierbaren Signale zu verarbeiten, indem sie die Integrationsschritte an den Unstetigkeitsstellen anpassen.

</div>
<div>

![width:1000px](./Diagramme/Signal_Abschnittsweise_Differenzierbarkeit.svg)

</div>
</div>

---

<div class="columns">
<div class="two">

#### Eingangs- und Ausgangssignale

Simulink-Blöcke verarbeiten Signale. Dabei wird zwischen Ein- und Ausgangssignalen unterschieden:

- **Eingangssignale (Inputs):** Signale, die in einen Block hineinfließen. Sie sind die "Ursache" oder die Information, die der Block zur Druchführung seiner Berechnung benötigt.

- **Ausgangssignale (Outputs):** Signale, die von einem Block erzeugt und ausgegeben werden. Sie sind die "Wirkung" oder das Ergebnis der blockinternen Berechnung.

</div>
<div>

![width:1000px](./Diagramme/Signal_IO.svg)

</div>
</div>

---

![bg contain right](./Simulink_Blöcke.jpg)

### 2.1.2. Blöcke

Blockarten und -funktionsweisen und die Simulink-Bibliothek:

1. Einfache zustandslose Blöcke
2. Allgemeine zustandslose Blöcke
3. Blöcke mit kontinuierlichen Zuständen
4. Blöcke mit diskreten Zuständen
5. Blöcke mit hybriden Zuständen
6. Die Simulink-Bibliothek

---

<div class="columns">
<div class="four">

#### ***Einfache* zustandslose** Blöcke

Im einfachsten Fall ist das Ausgabesignal $y$ zum Zeitpunkt $t$ ausschließlich abhängig vom Eingabessignal $u$ zum Zeitpunkt $t$.

Allgemein ergibt sich daraus folgender **mathematischer Zusammenhang** zwischen den beiden Signalfunktionen:

$y(t) = f(u(t))$

Das Beispiel auf der rechten Seite zeigt eine konkrete Formulierung für die Funktion $f$ für einen `Gain`-Block.

</div>
<div>

![](./Diagramme/Block_Gain.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

![width:1000px](./Diagramme/Signal_Gain.svg)

</div>
<div>

![](./Diagramme/Block_Gain.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

#### ***Allgemeine* zustandslose** Blöcke

Im etwas allgemeineren Fall ist das Ausgabesignal $y$ weiterhin ausschließlich abhängig von Eingangssignal $u$.

Jedoch kann der Zusammenhang hier z.B. auch **zeitversetzt** sein, woraus sich folgende Formulierung ergibt:

$y(t) = f(t, u)$

Das Beispiel auf der rechten Seite zeigt wieder eine konkrete Formulierung der Funktion $f$ für einen `Delay`-Block.

</div>
<div>

![](./Diagramme/Block_Delay.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

![width:1000px](./Diagramme/Signal_Delay.svg)

</div>
<div>

![](./Diagramme/Block_Delay.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

#### Blöcke mit ***kontinuierlichen* Zuständen**

**Zustandsfunktion** beschreibt den Zustand des Blocks über die Zeit kontinuierlich und lückenlos

$x_c(t) = \int\dot{x}_c(t)dt$

**Ableitungsfunktion** beschreibt die Änderung des Zustands über die Zeit ebenfalls kontinierlich und lückenlos

$\dot{x}_c(t) = f_d(t, x_c, u)$

**Ausgabefunktion** beschreibt die Ausgabesignale des Systems unter Berücksichtigung der Eingabesignale und des Zustands

$y(t) = f_o(t, x_c, u)$

</div>
<div>

![](./Diagramme/Block_Integrator.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

![width:1000px](./Diagramme/Signal_Integrator.svg)

</div>
<div>

![](./Diagramme/Block_Integrator.svg)

</div>
</div>

----

<div class="columns">
<div class="four">

#### Blöcke mit ***diskreten* Zuständen**

**Zustandssequenz** repräsentiert den Zustands des Blocks ausschließlich zu bestimmten *Zeitpunkten*

$x_d = x_{d_0}, x_{d_1}, x_{d_2}, ...$ mit Zeitpunkten $t_0,t_1,t_2,...$

**Aktualisierungsfunktion** beschreibt die Berechnung der jeweiligen *Folgezustände* aus den *Vorgängerzuständen*

$x_{d_{k+1}} = f_u(t_{k+1}, x_c, x_{d_k}, u)$

**Ausgabefunktion** (mit $t_k \leq t < t_{k+1}$) beschreibt die Ausgabe *abschnittsweise* zwischen den Zustanssprüngen

$y(t) = f_o(t, x_{d_k}, u)$

</div>
<div>

![](./Diagramme/Block_Discrete_Time_Integrator.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

![width:1000px](./Diagramme/Signal_Discrete_Time_Integrator.svg)

</div>
<div>

![](./Diagramme/Block_Discrete_Time_Integrator.svg)

</div>
</div>

---

<div class="columns">
<div class="three">

#### Blöcke mit ***hybriden* Zuständen**

**Zustandsfunktion** und **-sequenz** kombiniert in einem Tupel

$x = (x_c,x_d)$

**Aktualisierungsfunktion** für diskrete Zustandssprünge

$x_{d_{k+1}} = f_u(t_{k+1},x_c,x_{d_k},u)$

**Ableitungfunktion** (mit $t_k \leq t < t_{k+1}$) nun abschnittsweise

$\dot{x}_c(t) = f_d(t,x_c,x_{d_k},u)$

**Ausgabefunktion** (mit $t_k \leq t < t_{k+1}$) auch abschnittsweise

$y(t) = f_o(t,x_c,x_{d_k},u)$

</div>
<div>

![](./Diagramme/Block_Hybrid.svg)

</div>
</div>

---

<div class="columns">
<div class="three">

![width:1000px](./Diagramme/Signal_Hybrid.svg)

</div>
<div>

![](./Diagramme/Block_Hybrid.svg)

</div>
</div>

---

![bg contain right](./Simulink_Bibliothek.png)

#### Die Simulink-Bibliothek

- **Sources:** Erzeugen Signale (z.B. `Constant`, `Step`, `Sine Wave`).
- **Sinks:** Visualisieren Signale (z.B. `Scope`, `Display`).
- **Math Operations:** Einfache Berechnungen  (z.B. `Add`, `Gain`).
- **Continuous:** Kontinuierliche Zeit-funktionen (z.B. `Integrator`).
- **Discrete:** Diskrete Zeitfunktionen (z.B. `DiscreteIntegrator`)

---

##### Wichtige Blöcke: **Sources**

Quellen sind der Ausgangspunkt für Signale in einem Simulink-Modell.

<div class="columns top">
<div>

![height:175px](./Simulink_Block_Constant.png)

*Erzeugt einen konstanten Wert.*

</div>
<div>

![height:175px](./Simulink_Block_Step.png)

*Erzeugt eine Sprungfunk-tion zu einer bestimmten Zeit.*

</div>
<div>

![height:175px](./Simulink_Block_Sine_Wave.png)

*Erzeugt ein sinusförmiges Signal mit einstellbarer Amplitude, Frequenz und Phase.*

</div>
</div>

---

##### Wichtige Blöcke: **Sinks**

Senken dienen zur Analyse und Anzeige von Signalen während und nach der Simulation.

<div class="columns top">
<div>

![height:175px](./Simulink_Block_Display.png)

*Zeigt den numerischen Wert eines Signals am Ende der Simulation an.*

</div>
<div>

![height:175px](./Simulink_Block_Scope.png)

*Zeigt Signale in einem Oszilloskop-ähnlichen Diagramm an.*

</div>
<div>

![height:175px](./Simulink_Block_To_File.png)

*Schreibt Signaldaten in eine MAT-Datei zur späteren Analyse.*

</div>
</div>

---

##### Wichtige Blöcke: **Math Operations**

Diese Blöcke führen grundlegende mathematische Operationen mit Signalen durch.

<div class="columns top">
<div>

![height:175px](./Simulink_Block_Gain.png)

*Multipliziert ein Signal mit einem konstanten Faktor (Verstärkung).*

</div>
<div>

![height:175px](./Simulink_Block_Add.png)

*Addiert oder subtrahiert zwei oder mehr Signale elementweise.*

</div>
<div>

![height:175px](./Simulink_Block_Polynomial.png)

*Berechnet einen Polynomwert für das Eingangssignal.*

</div>
</div>

---

##### Wichtige Blöcke: **Continuous**

Diese Blöcke sind das Herzstück für die Modellierung von physikalischen Systemen, die durch Differentialgleichungen beschrieben werden.

<div class="columns">
<div>

![height:175px](./Simulink_Block_Transport_Delay.png)

*Verzögert das Eingangssignal um eine bestimmte Zeit.*

</div>
<div>

![height:175px](./Simulink_Block_Integrator.png)

*Führt eine kontinuierliche Integration des Eingangssignals durch.*

</div>
<div>

![height:175px](./Simulink_Block_Integrator_Second_Order.png)

*Führt eine doppelte kontinuierliche Integration des Eingangssignals durch.*

</div>
</div>

---

##### Wichtige Blöcke: **Discrete**

Diese Blöcke modellieren diskrete Systeme oder diskrete Anteile in hybriden Systemen.

<div class="columns top">
<div>

![height:175px](./Simulink_Block_Memory.png)

*Speichert den Wert des Eingangssignals vom vorherigen Zeitschritt.*

</div>
<div>

![height:175px](./Simulink_Block_Discrete_Time_Integrator.png)

*Führt eine diskrete Integration des Eingangssignals durch.*

</div>
<div>

![height:175px](./Simulink_Block_Discrete_Derivative.png)

*Berechnet die diskrete Ableitung des Eingangssignals.*

</div>
</div>

---

![bg contain right](./Simulink_Solver.jpg)

### 2.1.3. Solver

TODO

---

<div class="columns">
<div class="two">

### TODO Folie - Simulationsphasen

</div>
<div>

![](https://de.mathworks.com/help/simulink/ug/simulationphasesloop.png)

</div>
</div>

---

### TODO Folie - Abtastzeiten

---

#### TODO Folie - **Diskrete** Abtastzeiten

---

#### TODO Folie - **Mehrratige** diskrete Abtastzeiten

---

#### TODO Folie - **Kontinuierliche** Abtastzeiten

---

#### TODO Folie - Kontinuierliche Abtastzeiten **mit festgelegten Unterschritten**

---

#### TODO Folie - **Variable** kontinuierliche Abtastzeiten

---

#### TODO Folie - **Asynchrone** Abtastzeiten

---

### TODO Folie - Solverarten

---

#### TODO Folie - Kontinuierliche und diskrete Solver

---

#### TODO Folie - Explizite und implizite kontinuierliche Solver

---

#### TODO Folie - Kontinuierliche Ein-Schritt und Mehr-Schritt-Solver

---

#### TODO Folie - Kontinuierliche Solver erster und variabler Ordnung

---

![bg contain right:40%](../01_Anforderungen_und_Architekturen/Case_Study.jpg)

### 2.1.4. Fallbeispiel: Akku-Schrauber

Wir modellieren das vereinfachte Verhalten des Motors. Annahme: Die Drehzahl des Motors ist direkt proportional zur angelegten Spannung, abzüglich eines Lastmoments.

---

#### TODO Folienüberschrift

TODO kurzer Text

- Ein `Constant`-Block repräsentiert die Spannung vom Akku.
- Ein `Gain`-Block modelliert den Motor (wandelt Spannung in Drehzahl um).
- Ein `Subtract`-Block reduziert die Drehzahl durch ein Lastmoment.
- Ein `Scope` zeigt die resultierende Motordrehzahl an.

---

![bg right](../Übungsaufgabe.jpg)

### 2.1.5. Übungsaufgabe

Modellieren Sie mit Simulink das Verhalten des Extruders eines 3D-Druckers.

Vereinfachte Annahme: Die Menge des extrudierten Filaments pro Sekunde ist direkt proportional zur Geschwindigkeit des Vorschubmotors.

Stellen Sie die Vorschubgeschwindigkeit mit einem `Step`-Block dar und visualisieren Sie die Gesamtlänge des extrudierten Filaments über die Zeit mit einem `Scope`.

---

![bg right](./Simscape.jpg)

## 2.2 Simscape **Physikmodelle**

In diesem zweiten Abschnitt lernen wir die folgenden Dinge:

1. **Grundlagen der physikalischen Modellierung**<br/>(Akausale Modellierung)
2. **Wichtige Blöcke in Simscape**<br/>(Elektrisch, Mechanisch)
3. **Einfache physikalische Modelle erstellen**<br/>(Ein einfacher RC-Kreis)

---

### 2.2.1. Was ist Simscape?

Simscape ist eine Erweiterung von Simulink für die Modellierung von **physikalischen Systemen**.

Im Gegensatz zu Simulink (Signalfluss) verwendet Simscape ein **akausales, physikalisches Netzwerk-Konzept**. Man verbindet Komponenten so, wie sie in der Realität verbunden wären (z.B. elektrische Bauteile). Die Gleichungen werden vom Solver automatisch aufgestellt.

Verbindungen repräsentieren den Austausch von Energie. Jede Domäne (z.B. elektrisch, mechanisch) hat ihre eigenen Verbindungsarten.

---

<div class="columns">
<div>

#### Domänen und Referenzen

Simscape-Modelle benötigen für jede physikalische Domäne einen `Solver Configuration`-Block und einen Referenzblock.

- **Solver Configuration:** Konfiguriert den spezialisierten Solver für die physikalischen Gleichungen.
- **Referenzblock:** Definiert den Bezugspunkt für die physikalischen Größen (z.B. elektrische Masse `GND` oder ein mechanisches Gehäuse).

</div>
<div>

![Beschreibung: Simscape-Modell mit Solver Configuration und Electrical Reference](./Simscape_Solver.png)

</div>
</div>

---

#### Wichtige Blöcke: Elektrisch

Die `Foundation Library` enthält grundlegende Blöcke für verschiedene Domänen.

<div class="columns">
<div class="one">

**DC Voltage Source**
Eine ideale Gleichspannungsquelle.

**Resistor**
Ein ohmscher Widerstand.

**Capacitor**
Ein Kondensator.

</div>
<div class="two">

**Electrical Reference**
Der Massepunkt (0V) für elektrische Schaltkreise.

**Sensor/Actuator**
Blöcke wie `Current Sensor` oder `Voltage Sensor` messen physikalische Größen und geben sie als Simulink-Signal aus.

</div>
</div>

---

<div class="columns">
<div>

#### Einfaches Beispiel: RC-Kreis

Wir modellieren einen einfachen RC-Tiefpass. Eine Spannungsquelle lädt einen Kondensator über einen Widerstand.

- Die Blöcke werden wie in einem Schaltplan verbunden.
- Ein `Voltage Sensor` misst die Spannung am Kondensator.
- Das Ergebnis wird mit einem `Scope` angezeigt. Die Spannung am Kondensator folgt einer e-Funktion.

</div>
<div>

![Beschreibung: Simscape-Modell eines RC-Kreises](./Simscape_Beispiel_RC.png)

</div>
</div>

---

![bg contain right:40%](../01_Anforderungen_und_Architekturen/Case_Study.jpg)

### 2.2.2. Fallbeispiel: Akku-Schrauber

Wir modellieren den Gleichstrommotor des Akku-Schraubers als physikalisches System.

- **Elektrischer Teil:** Eine `DC Voltage Source` (der Akku) wird an einen `Resistor` (der Wicklungswiderstand) angeschlossen.
- **Mechanischer Teil:** Der `DC Motor`-Block wandelt die elektrische Energie in eine mechanische Rotation um. Ein `Inertia`-Block repräsentiert die Trägheit des Rotors.
- Ein `Rotational Motion Sensor` misst die Drehzahl und gibt sie als Simulink-Signal aus.

---

![bg right](../Übungsaufgabe.jpg)

### 2.2.3. Übungsaufgabe

Modellieren Sie mit Simscape das Heizbett des 3D-Druckers.

- Verwenden Sie die thermische Domäne von Simscape.
- Modellieren Sie das Heizbett als `Thermal Mass`.
- Fügen Sie eine `Controlled Heat Flow Rate Source` hinzu, um die Heizleistung zu steuern.
- Messen Sie die Temperatur mit einem `Temperature Sensor` und zeigen Sie den Verlauf in einem `Scope` an.
- Fügen Sie einen `Convective Heat Transfer`-Block hinzu, um den Wärmeverlust an die Umgebung zu modellieren.

---

![bg right](./Stateflow.jpg)

## 2.3 Stateflow **Logikmodelle**

In diesem dritten Abschnitt lernen wir die folgenden Dinge:

1. **Grundlagen der logischen Modellierung**<br/>(Zustandsautomaten)
2. **Wichtige Elemente in Stateflow**<br/>(Zustände, Transitionen, Aktionen)
3. **Einfache Logikmodelle erstellen**<br/>(Ein einfacher Lichtschalter)

---

### 2.3.1. Was ist Stateflow?

Stateflow ist eine Umgebung zur Modellierung von **ereignisgesteuerter Logik** basierend auf **Zustandsautomaten** und **Flussdiagrammen**.

Es eignet sich hervorragend, um komplexe Entscheidungslogik, Betriebsmodi oder Ablaufsteuerungen zu modellieren, die in reiner Signalverarbeitung mit Simulink nur schwer darstellbar wären.

Ein Stateflow-Diagramm (Chart) wird als Block in ein Simulink-Modell eingefügt und interagiert mit diesem über Ein- und Ausgangssignale.

---

<div class="columns">
<div>

#### Elemente eines Stateflow-Charts

- **Zustände (States):** Repräsentieren einen bestimmten Modus des Systems. Ein System kann sich immer nur in einem Zustand befinden.
- **Transitionen (Transitions):** Pfeile, die den Übergang von einem Zustand in einen anderen definieren.
- **Bedingungen (Conditions):** Logische Ausdrücke an Transitionen, die wahr sein müssen, damit der Übergang stattfindet (z.B. `input > 5`).
- **Aktionen (Actions):** Befehle, die beim Eintreten, Verlassen oder während eines Zustands ausgeführt werden (`entry`, `exit`, `during`).

</div>
<div>

![Beschreibung: Ein einfacher Stateflow-Chart mit zwei Zuständen und Transitionen](./Stateflow_Elemente.png)

</div>
</div>

---

<div class="columns">
<div>

#### Einfaches Beispiel: Lichtschalter

Wir modellieren einen einfachen Schalter mit zwei Zuständen: `On` und `Off`.

- Ein Eingangssignal `switch_pos` steuert den Zustand.
- **Transition `Off` -> `On`:** Wird ausgelöst, wenn `switch_pos == 1`.
- **Transition `On` -> `Off`:** Wird ausgelöst, wenn `switch_pos == 0`.
- In jedem Zustand wird ein Ausgang `light_status` auf `1` (On) oder `0` (Off) gesetzt.

</div>
<div>

![Beschreibung: Stateflow-Chart für einen Lichtschalter](./Stateflow_Beispiel_Schalter.png)

</div>
</div>

---

![bg contain right:40%](../01_Anforderungen_und_Architekturen/Case_Study.jpg)

### 2.3.2. Fallbeispiel: Akku-Schrauber

Wir modellieren die Steuerungslogik des Akku-Schraubers.

- **Zustände:** `Off`, `Forward`, `Reverse`.
- **Eingänge:** `trigger_pressed` (boolean), `direction_switch` (enum).
- **Logik:**
    - Von `Off` nach `Forward`, wenn `trigger_pressed` wahr ist und `direction_switch` auf "vorwärts" steht.
    - Von `Off` nach `Reverse`, wenn `trigger_pressed` wahr ist und `direction_switch` auf "rückwärts" steht.
    - Von `Forward` oder `Reverse` zurück nach `Off`, wenn `trigger_pressed` losgelassen wird.
- **Ausgänge:** Ein Signal `motor_voltage`, das im Zustand `Off` 0 ist und sonst der Akkuspannung entspricht.

---

![bg right](../Übungsaufgabe.jpg)

### 2.3.3. Übungsaufgabe

Modellieren Sie mit Stateflow die Betriebslogik des 3D-Druckers.

Erstellen Sie einen Zustandsautomaten mit den folgenden Zuständen:
- `Idle` (Leerlauf)
- `Heating` (Aufheizen von Druckbett und Düse)
- `Printing` (Druckvorgang)
- `Finished` (Druck beendet)

Definieren Sie die Eingänge (z.B. `start_print_button`, `target_temp_reached`) und die Transitionen zwischen den Zuständen.

---

![bg right](./Simulink3D.jpg)

## 2.4 Simulink 3D Animation

In diesem vierten Abschnitt lernen wir die folgenden Dinge:

1. **Grundlagen der 3D-Visualisierung**<br/>(VRML/X3D-Welten)
2. **Verbindung von Modell und Animation**<br/>(Der VR Sink Block)
3. **Einfache Animationen erstellen**<br/>(Bewegung eines Würfels)

---

### 2.4.1. Was ist Simulink 3D Animation?

Simulink 3D Animation ermöglicht die Visualisierung von Simulink- und Simscape-Simulationen in einer **virtuellen 3D-Umgebung**.

Es verbindet das dynamische Modell mit einer 3D-Welt, die im **VRML**- oder **X3D**-Format beschrieben ist. Dadurch kann man die Bewegungen und das Verhalten von mechanischen Systemen, Fahrzeugen oder Robotern realistisch darstellen.

Die Verbindung wird durch spezielle Simulink-Blöcke hergestellt, die Simulationsdaten an die Objekte in der 3D-Welt senden.

---

<div class="columns">
<div>

#### Der VR Sink Block

Der `VR Sink`-Block ist die Brücke zwischen Simulink und der virtuellen Welt.

- Er nimmt Simulink-Signale als Eingang.
- Diese Signale werden verwendet, um Eigenschaften (Felder) von Objekten (Nodes) in der 3D-Welt zu manipulieren.
- Typische Eigenschaften sind `translation` (Position), `rotation` (Drehung) oder `color`.

Man wählt im Block das Zielobjekt und die zu steuernde Eigenschaft aus.

</div>
<div>

![Beschreibung: Der VR Sink Block mit seinen Parametern](./VR_Sink.png)

</div>
</div>

---

<div class="columns">
<div>

#### Einfaches Beispiel: Würfel bewegen

Wir animieren einen einfachen Würfel in einer vordefinierten 3D-Welt.

- Ein `Sine Wave`-Block in Simulink erzeugt ein sinusförmiges Signal.
- Dieses Signal wird auf den Eingang des `VR Sink`-Blocks gegeben.
- Der `VR Sink` ist so konfiguriert, dass er die `translation` (Position) des Würfels auf der X-Achse steuert.
- Ergebnis: Der Würfel bewegt sich in der 3D-Ansicht harmonisch hin und her.

</div>
<div>

![Beschreibung: Simulink-Modell zur Steuerung eines Würfels in 3D](./Simulink_3D_Beispiel.png)

</div>
</div>

---

![bg contain right:40%](../01_Anforderungen_und_Architekturen/Case_Study.jpg)

### 2.4.2. Fallbeispiel: Akku-Schrauber

Wir visualisieren die Rotation des Bohrfutters (Chuck) unseres Akku-Schrauber-Modells.

- Das Simscape-Modell des Motors berechnet die Winkelgeschwindigkeit.
- Ein `Integrator`-Block berechnet daraus den Rotationswinkel über die Zeit.
- Dieses Winkelsignal wird an einen `VR Sink`-Block übergeben.
- Der `VR Sink` steuert das `rotation`-Feld des Bohrfutter-Objekts in der 3D-Welt des Akku-Schraubers.
- Ergebnis: Das Bohrfutter dreht sich in der 3D-Ansicht entsprechend der simulierten Motordrehzahl.

---

![bg right](../Übungsaufgabe.jpg)

### 2.4.3. Übungsaufgabe

Animieren Sie die Bewegung des Druckkopfes Ihres 3D-Drucker-Modells.

- Erstellen Sie ein einfaches Simulink-Modell, das die X- und Y-Position des Druckkopfes über die Zeit generiert (z.B. mit `Ramp`-Blöcken).
- Verwenden Sie einen `VR Sink`-Block, um die `translation`-Eigenschaft des Druckkopf-Objekts in einer bereitgestellten 3D-Welt zu steuern.
- Stellen Sie sicher, dass sich der Druckkopf auf der XY-Ebene bewegt.

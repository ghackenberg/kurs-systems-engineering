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

![bg right](./Illustrationen/Simulink.jpg)

## 2.1 Simulink **Signalmodelle**

In diesem ersten Abschnitt lernen wir die folgenden Dinge:

1. **Signale** (Zeitverläufe)
2. **Blöcke** (Funktionsvorschriften)
3. **Kompositionen** (Verknüpfungen)
4. **Abtastzeiten** (Diskretisierungen)
5. **Solver** (Berechnungen)

---

![bg contain right:35%](./Screenshots/Simulink_Component_Create.png)

### Simulink-Verhalten erstellen

Für jede atomare Komponente im System Composer kann ein  Verhalten in Simulink modelliert werden.

1.  **Rechtsklick** auf die Komponente.
2.  Wählen Sie im Kontextmenü `Create Behavior > Simulink Behavior`.
3.  System Composer erstellt ein neues, verknüpf-tes Simulink-Modell (`.slx`-Datei) und öffnet es.
4.  Die Ports der Komponente werden automatisch als In- und Out-Ports im Simulink-Modell angelegt.

---

![bg contain right:35%](./Screenshots/Simulink_Component_Link.png)

### Bestehendes Verhalten verknüpfen

Bestehende Simulink-Modelle können wiederver-wendet werden, indem sie mit einer Komponente verknüpft werden.

1.  **Rechtsklick** auf die Komponente.
2.  Wählen Sie im Kontextmenü `Link to > Model`.
3.  Navigieren Sie zur gewünschten `.slx`-Datei und wählen Sie sie aus.

Dies ist ideal für die Wiederverwendung von Bibliothekskomponenten oder  existierenden Verhaltensmodellen.

---

![bg contain right:35%](./Screenshots/Simulink_Component_Finished.png)

### Vorschau des Verhaltens

Sobald einer Komponente ein Simulink-Verhalten zugewiesen ist, zeigt System Composer eine Miniatur-Vorschau des Simulink-Modells direkt im Komponentenblock an.

-   **Visuelle Referenz:** Gibt einen schnellen Überblick über die interne Logik.
-   **Navigation:** Ein **Doppelklick** auf die Komponente öffnet das verknüpfte Simulink-Modell zur Bearbeitung des Verhaltens.

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

![bg contain right](./Illustrationen/Simulink_Signale.jpg)

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

![width:1000px](./Diagramme/Draw/Signal.svg)

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

![width:1000px](./Diagramme/Draw/Signal_Stetigkeit.svg)

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

![width:1000px](./Diagramme/Draw/Signal_Differenzierbarkeit.svg)

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

![width:1000px](./Diagramme/Draw/Signal_Abschnittsweise_Differenzierbarkeit.svg)

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

![width:1000px](./Diagramme/Draw/Signal_IO.svg)

</div>
</div>

---

![bg contain right](./Illustrationen/Simulink_Blöcke.jpg)

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
<div>

### Was ist ein Block?

Ein **Block** ist das grundlegende Element eines Simulink-Modells.

Er repräsentiert eine mathematische Funktion oder ein logisches Konstrukt, das **Eingangssignale** verarbeitet, um **Ausgangssignale** zu erzeugen.

Neben den Signalen umfassen Blöcke noch **Zustände** (eine Art *Gedächtnis*) und **Parameter** zur Konfiguration des Block-verhaltens.

</div>
<div>

![](./Diagramme/Mermaid/Block.svg)

</div>
</div>

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

![](./Diagramme/Mermaid/Block_Gain.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

![width:1000px](./Diagramme/Draw/Signal_Gain.svg)

</div>
<div>

![](./Diagramme/Mermaid/Block_Gain.svg)

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

![](./Diagramme/Mermaid/Block_Delay.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

![width:1000px](./Diagramme/Draw/Signal_Delay.svg)

</div>
<div>

![](./Diagramme/Mermaid/Block_Delay.svg)

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

![](./Diagramme/Mermaid/Block_Integrator.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

![width:1000px](./Diagramme/Draw/Signal_Integrator.svg)

</div>
<div>

![](./Diagramme/Mermaid/Block_Integrator.svg)

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

![](./Diagramme/Mermaid/Block_Discrete_Time_Integrator.svg)

</div>
</div>

---

<div class="columns">
<div class="four">

![width:1000px](./Diagramme/Draw/Signal_Discrete_Time_Integrator.svg)

</div>
<div>

![](./Diagramme/Mermaid/Block_Discrete_Time_Integrator.svg)

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

![](./Diagramme/Mermaid/Block_Hybrid.svg)

</div>
</div>

---

<div class="columns">
<div class="three">

![width:1000px](./Diagramme/Draw/Signal_Hybrid.svg)

</div>
<div>

![](./Diagramme/Mermaid/Block_Hybrid.svg)

</div>
</div>

---

![bg contain right](./Screenshots/Simulink_Bibliothek.png)

#### Die Simulink-Bibliothek

Die Simulink-Bibliothek biete eine Vielzahl von vordefinierten Blöcken:

- **Sources + Sinks:** Signale erzeugen und visualisieren
- **Math Operations:** Einfache mathematische Operationen
- **Continuous + Discrete:** Glatte und sprunghafte Funktionen
- **Ports & Subsystems:** Kapselung und Wiederverwendung

---

##### Wichtige Blöcke: **Sources**

Quellen sind der Ausgangspunkt für Signale in einem Simulink-Modell.

<div class="columns top">
<div>

![height:175px](./Screenshots/Simulink_Block_Constant.png)

*Erzeugt einen konstanten Wert.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Step.png)

*Erzeugt eine Sprungfunk-tion zu einer bestimmten Zeit.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Sine_Wave.png)

*Erzeugt ein sinusförmiges Signal mit einstellbarer Amplitude, Frequenz und Phase.*

</div>
</div>

---

##### Wichtige Blöcke: **Sinks**

Senken dienen zur Analyse und Anzeige von Signalen während und nach der Simulation.

<div class="columns top">
<div>

![height:175px](./Screenshots/Simulink_Block_Display.png)

*Zeigt den numerischen Wert eines Signals am Ende der Simulation an.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Scope.png)

*Zeigt Signale in einem Oszilloskop-ähnlichen Diagramm an.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_To_File.png)

*Schreibt Signaldaten in eine MAT-Datei zur späteren Analyse.*

</div>
</div>

---

##### Wichtige Blöcke: **Math Operations**

Diese Blöcke führen grundlegende mathematische Operationen mit Signalen durch.

<div class="columns top">
<div>

![height:175px](./Screenshots/Simulink_Block_Gain.png)

*Multipliziert ein Signal mit einem konstanten Faktor (Verstärkung).*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Add.png)

*Addiert oder subtrahiert zwei oder mehr Signale elementweise.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Polynomial.png)

*Berechnet einen Polynomwert für das Eingangssignal.*

</div>
</div>

---

##### Wichtige Blöcke: **Continuous**

Diese Blöcke sind das Herzstück für die Modellierung von physikalischen Systemen, die durch Differentialgleichungen beschrieben werden.

<div class="columns">
<div>

![height:175px](./Screenshots/Simulink_Block_Transport_Delay.png)

*Verzögert das Eingangssignal um eine bestimmte Zeit.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Integrator.png)

*Führt eine kontinuierliche Integration des Eingangssignals durch.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Integrator_Second_Order.png)

*Führt eine doppelte kontinuierliche Integration des Eingangssignals durch.*

</div>
</div>

---

##### Wichtige Blöcke: **Discrete**

Diese Blöcke modellieren diskrete Systeme oder diskrete Anteile in hybriden Systemen.

<div class="columns top">
<div>

![height:175px](./Screenshots/Simulink_Block_Memory.png)

*Speichert den Wert des Eingangssignals vom vorherigen Zeitschritt.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Discrete_Time_Integrator.png)

*Führt eine diskrete Integration des Eingangssignals durch.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Discrete_Derivative.png)

*Berechnet die diskrete Ableitung des Eingangssignals.*

</div>
</div>

---

##### Wichtige Blöcke: **Ports & Subsystems**

Diese Blöcke sind essenziell für die hierarchische Gliederung und Wiederverwendung von Modellen.

<div class="columns top">
<div>

![height:175px](./Screenshots/Simulink_Block_InputPort.png)

*Definiert einen Eingang für ein Subsystem oder Modell.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_OutputPort.png)

*Definiert einen Ausgang für ein Subsystem oder Modell.*

</div>
<div>

![height:175px](./Screenshots/Simulink_Block_Subsystem.png)

*Gruppiert Blöcke, um ein hierarchisches Subsystem zu erstellen.*

</div>
</div>

---

![bg contain right:40%](./Screenshots/Simulink_Component_Created.png)

### Port-Zuordnung

Die Ports einer System Composer Komponente werden direkt auf die `Inport`- und `Outport`-Blöcke im Simulink-Modell abgebildet.

-   **Eindeutige Namen:** Der Name eines Ports im Architekturmodell muss mit dem Namen des entsprechenden Port-Blocks im Simulink-Modell übereinstimmen.
-   **Konsistente Schnittstellen:** Die auf den Ports definierten Schnittstellen (Datentyp, Dimension, etc.) müssen mit den Simulink-Signaleigenschaften kompatibel sein.

---

### Komponente vs. Subsystem

Obwohl beide zur Gliederung von Modellen dienen, haben sie unterschiedliche Zwecke.

<div class="columns top">
<div>

#### System Composer **Komponente**

-   **Was?** Ein Baustein der Systemarchitektur.
-   **Wo?** Wird in `.slx`-Dateien für Architekturmodelle verwendet.
-   **Zweck:** Definiert die Struktur und die Schnittstellen eines Systems (`Wer?`).
-   **Ports:** Formale Ports, die auf Schnittstellen basieren.

</div>
<div>

#### Simulink **Subsystem**

-   **Was?** Eine Gruppierung von Blöcken.
-   **Wo?** Wird in `.slx`-Dateien für Verhaltensmodelle verwendet.
-   **Zweck:** Kapselt eine detaillierte Funktion oder Logik innerhalb eines Verhaltensmodells (`Wie?`).
-   **Ports:** Einfache In- und Outports ohne formale Definition.

</div>
</div>

---

![bg contain right](./Illustrationen/Simulink_Linien.jpg)

### 2.1.3. Kompositionen

Themen in diesem Unterabschnitt:

1. **Gewöhnliche Differential-gleichungen** (Zeitliche Veränderung des Zustands)
2. **Steife gewöhnliche Differen-tialgelichungen** (schnelle und langsame Änderungen)
3. **Differential-algebraische Gleichungen** (algeraische Randbedingungen)

---

#### Was sind Kompositionen?

Der Begriff **Komposition** beschreibt die Zusammensetzung und Verschaltung von einzelnen Simulink-Blöcken zu einem größeren Ganzen:

- Ausgangssignale von Blöcken werden weitergeleitet an Eingangssignale von anderen Blöcken
- Ein Ausgangssignal kann dabei nur an ein, oder aber mehrere Eingangssignale weitergeleitet werden
- Ein Ausgangssignal eines Blocks kann auch direkt als Eingangssignal desselben Blocks verwendet werden
- Die Weiterleitung von Signalen erfolgt in Simulink mithilfe von sogenannten *Linien* (d.h. scharze Linien)

---

![bg contain right:40%](./Screenshots/Simulink_Linie.png)

#### Linie in Simulink erstellen (Ausgangssignal auf Eingangssignal weiterleiten)

In Simulink können Weiterleitungen zwischen Ausgangs- und Eingangssignalen einfach per Drag & Drop erstellt werden.

- Die Signale selbst erste als Ports auf den zugehörigen Blöcken dargestellt
- Die Drag & Drop Operation kann beim Ausgangssignal starten
- Alternativ kann die Operation auch beim Eingangssignal starten

---

![bg contain right:40%](./Screenshots/Simulink_Linie_Fork.png)

#### Ein Ausgangssignal auf **mehere** Eingangs-signale weiterleiten

Ein Ausgangssignal kann auch an mehrere Eingangssignale von unterschiedlichen Blöcken weitergeleitet werden.

- Ein Eingangssignal kann jedeoch nur mit einem Ausgangssignal verknüpft werden, sonst wäre es nicht Eindeutig
- Die Drag & Drop Operaton startet dieses mal beim Eingangsignal und endet auf einer bestehenden Linie

---

#### Mathematische Beschreibung einer Komposition

Gegeben seien zwei Blöcke $f_1,f_2$ mit den Eingängen $u_1,u_2$ und Ausgänge $y_1,y_2$:

$y_1(t) = f_1(t, u_1)$ und $y_2(t) = f_2(t, u_2)$

Durch die Komposition erwingen wir die Gleichheit von $y_1$ und $u_2$:

$u_1 = y_2 \Rightarrow f_2(t, u_2) = f_2(t, y_1)$

Grafische Darstellung der Komposition:

![](./Diagramme/Mermaid/Komposition.svg)

---

#### Komposition mit **Schleifen**

Eine Schleife entsteht, wenn wir zusätzlich Gleichheit von $y_2$ und $u_1$ erzwingen:

$u_2 = y_1 \Rightarrow f_1(t, u_1) = f_1(t, y_2)$

Grafische Darstellung der erweiterten Komposition:

![](./Diagramme/Mermaid/Komposition_Schleife.svg)

Ist kein Problem, solange $f_1$ oder $f_2$ Zusstände haben oder zeitverzögert reagieren.

---

#### Komposition mit **algebraischen** Schleifen

Ein Sonderfall entsteht, wenn die Blöcke $f_1,f_2$ Signale direkt durchleiten:

$y_1(t) = f_1(u_1(t))$ und $y_2(t) = f_2(u_2(t)) \Rightarrow f_1(f_2(u_2(t))) = f_2(u_2(t))$

Grafische Drastellung dieses Sonderfalls mit direkter Signaldurchleitung:

![](./Diagramme/Komposition_Schleife_Algebraisch.svg)

Dieser Fall muss bei der Simulationsrechnung gesondert berücksichtigt werden.

---

#### Mathematische Eigenschaften einer Komposition

Eine Komposition ohne algebraische Schleife ergibt eine gewöhnliche Differential-gleichung, andernfalls erhält man eine differential-algebraische Gleichung:

<div class="columns">
<div>

##### **Gewöhnliche** Differentialgleichung

*Reine Zeitintegration (z.B. vertikaler Wurf eines Balls)*

![width:200px](./Illustrationen/ODE.jpg)

</div>
<div>

##### Differential-**algebraische** Gleichung

*Zeitintegration mit Randbedingungen (z.B. Pendelbewegung)*

![width:200px](./Illustrationen/DAE.jpg)

</div>
</div>

---

#### Gewöhnliche Differentialgleichungen (ODEs)

Viele physikalische Systeme werden durch **gewöhnliche Differentialgleichungen (ODEs)** beschrieben. Eine ODE ist eine mathematische Gleichung, die die zeitliche Änderung eines Systemzustands beschreibt.

Die allgemeine Form einer ODE erster Ordnung lautet:

$\dot{x} = f(t, x)$

- $x$ ist der **Zustandsvektor** des Systems (z.B. Position und Geschwindigkeit).
- $\dot{x}$ ist die erste Ableitung von $x$ nach der Zeit $t$.
- $f$ ist eine Funktion, die die Dynamik des Systems beschreibt.

Simulink-Solver sind darauf ausgelegt, solche Gleichungssysteme numerisch zu lösen, um den Verlauf von $x(t)$ zu finden.

---

#### Beispiel: Vertikaler Wurf eines Balls

Wir betrachten den vertikalen Wurf eines Balls in einem Gravitationsfeld ohne Berücksichtigung des Luftwiderstands. Die Bewegung des Balls kann durch eine gewöhnliche Differentialgleichung beschrieben werden.

Die Beschleunigung in y-Richtung ist:

$\ddot{y} = -g$ (wobei $g$ die Erdbeschleunigung ist)

Um dies in ein System von ODEs erster Ordnung umzuwandeln, definieren wir die Zustandsgrößen als Position ($y$) und Geschwindigkeit ($v$):

$\dot{y} = v$
$\dot{v} = -g$

---

![bg contain right](./Screenshots/Simulink_ODE.png)

#### Umsetzung als Simulink-Modell

Im Simulink-Modell würde man:
1.  Drei `Constant`-Blöcke verwenden, um $-g$, $v_0$ und $y_0$ zu definieren.
2.  Zwei `Integrator`-Blöcke verwenden, um $-g$ zu $v$ und $v$ zu $y$ zu integrieren.
3.  Zwei `Scope`-Blöcke verwenden, um $v$ und $y$ zu visualisieren.

---

#### Steifigkeit von ODEs ("Stiff" Systems)

Ein Differentialgleichungssystem wird als **steif** bezeichnet, wenn es Zeitkonstanten enthält, die sich über mehrere Größenordnungen erstrecken.

Das bedeutet, das System hat Komponenten, die sich **sehr schnell** ändern, und andere, die sich **sehr langsam** ändern.

**Problem:** Explizite (nicht-steife) Solver wie `ode45` müssen extrem kleine Zeitschritte verwenden, um die schnellen Änderungen stabil zu erfassen. Dies macht die Simulation ineffizient, besonders wenn die schnelle Dynamik bereits abgeklungen ist.

**Lösung:** Implizite (steife) Solver wie `ode15s` sind für solche Probleme konzipiert. Sie sind pro Schritt rechenintensiver, können aber deutlich größere Zeitschritte stabil bewältigen, was die Gesamtsimulationszeit drastisch reduziert.

---
### Beispiel : RC-Schaltung mit unterschiedlich schnellen Gliedern

Ein klassisches Beispiel für ein steifes System ist eine elektrische Schaltung, die Komponenten mit sehr unterschiedlichen Zeitkonstanten enthält. Betrachten wir zwei RC-Glieder in Reihe:

- **Schnelles RC-Glied:** Hat eine sehr kleine Zeitkonstante ($\tau_1 = R_1 C_1$). Es reagiert sehr schnell auf Änderungen der Eingangsspannung.
- **Langsames RC-Glied:** Hat eine große Zeitkonstante ($\tau_2 = R_2 C_2$). Es reagiert langsam auf Änderungen.

Wenn $\tau_1 \ll \tau_2$ ist, ist das System steif. Ein expliziter Solver müsste die gesamte Simulation über sehr kleine Zeitschritte verwenden, um die schnelle Dynamik des ersten RC-Glieds korrekt zu erfassen, selbst wenn diese Dynamik längst abgeklungen ist.

---

<div class="columns">
<div class="two">

#### Mathematisches Modell der RC-Schaltung

**Differentialgleichungen:**

$\dot{V}_1 = \frac{1}{R_1 C_1}(V_{in} - V_1)$
$\dot{V}_2 = \frac{1}{R_2 C_2}(V_1 - V_2)$

**Verhalten:**
Bei einer Sprungfunktion als $V_{in}$ steigt $V_1$ sehr schnell an und erreicht fast sofort den Endwert. $V_2$ folgt $V_1$ jedoch viel langsamer.

Ein steifer Solver kann die schnelle Anfangsphase mit kleinen Schritten und die langsame Folgephase mit großen Schritten effizient simulieren.

</div>
<div>

![width:1000px](./Diagramme/Draw/RC-Schaltung.svg)

</div>
</div>

---

![bg contain right:40%](./Screenshots/Simulink_Steif.png)

#### Umsetzung des Modells in Simulink

1.  **Sources:** Ein `Step`-Block liefert die Eingangsspannung $V_{in}$, `Constant`-Blöcke definieren die  Wiederstände $(R_1, R_2)$ und Kapazitäten $(C_1, C_2)$.
3.  **Math Operations:** `Subtract`-, `Product`- und `Divide`-Blöcke werden verwendet, um die Terme $\frac{1}{R_1 C_1}(V_{in} - V_1)$ und $\frac{1}{R_2 C_2}(V_1 - V_2)$ zu bilden.
2.  **Continuous:** Für jede Spannung ($V_1, V_2$) wird ein `Integrator`-Block verwendet.

---

#### Differential-Algebraische Gleichungen (DAEs)

**Differential-Algebraische Gleichungen (DAEs)** sind Systeme von Gleichungen, die sowohl Differentialgleichungen als auch algebraische Gleichungen enthalten. Im Gegensatz zu gewöhnlichen Differentialgleichungen (ODEs) können DAEs nicht immer in eine explizite Form $\dot{x} = f(t, x)$ umgewandelt werden.

Die allgemeine Form einer DAE ist:
$F(t, x, \dot{x}) = 0$

- $x$ ist der Vektor der abhängigen Variablen.
- $\dot{x}$ ist der Vektor der Ableitungen.
- $F$ ist eine Funktion, die sowohl Differential- als auch algebraische Beziehungen ausdrückt.

---

#### Beispiel: Integration zweier Variablen mit Randbedingung

Betrachten wir ein einfaches System, das sowohl eine Differentialgleichung als auch eine algebraische Gleichung enthält:

**Gleichungssystem:**
$\dot{x} = -x + y$
$0 = x - y^2$

Hier ist $x$ eine Differentialvariable, deren Ableitung $\dot{x}$ in der ersten Gleichung vorkommt. $y$ ist eine algebraische Variable, die durch die zweite Gleichung an $x$ gekoppelt ist.

Dieses System kann nicht direkt in die Form $\dot{z} = f(t, z)$ gebracht werden, ohne die algebraische Gleichung explizit nach $y$ aufzulösen (was hier $y = \pm\sqrt{x}$ wäre).

---

![bg contain right:40%](./Screenshots/Simulink_DAE.png)


#### Umsetzung des einfachen DAE in Simulink

1. **Differentialgleichung:** Ein `Integrator`-Block wird für $x$ verwendet. Sein Eingang ist $-x + y$. Dies erfordert einen `Difference`-Block mit Eingängen $y$ und $x$.
2. **Algebraische Gleichung:** Man kann einen `Algebraic Constraint`-Block verwenden, der die Gleichung $x - y^2 = 0$ löst, um $y$ zu finden. Der Eingang des Blocks ist $x-y^2$ und der Ausgang ist $y$.

---

![bg contain right](./Illustrationen/Simulink_Abtastzeiten.jpg)

### 2.1.4. Abtastzeiten

In diesem Unterabschnitt betrachten wir die folgenden Arten von Abtast-zeiten für Simulink-Blöcke:

1. **Konstante Abtastzeiten**
2. **Variable Abtastzeiten**
3. **Diskrete Abtastzeiten**
4. **Mehrratige Abtastzeiten**
5. **Kontinuierliche Abtastzeiten**
6. **Vererbte Abtastzeiten**

---

### Was sind Abtastzeiten?

Die **Abtastzeit** (`Sample Time`) eines Blocks legt fest, zu welchen Zeitpunkten er ausge-führt wird, d.h. wann seine Ausgänge und sein interner Zustand aktualisiert werden.

- **Effizienz:** Eine korrekte Konfiguration der Abtastzeiten ist entscheidend für die Geschwindigkeit der Simulation.
- **Genauigkeit**: Die Konfiguration hat außerdem eine Auswirkung auf die Genaugkeit der Simualtionsergebnisse.
- **Definition:** Die Abtastzeit wird typischerweise als zweidimensionaler Vektor `[Periode, Offset]` definiert.
- **Typen**: Konstant, variabel, diskret, mehrratig, kontinuierlich, kontinuierlich mit festem kleinen Zeitschritt, und vererbt

---

<div class="columns">
<div class="three">

#### **Konstante** Abtastzeiten `[inf, 0]`

Blöcke mit konstanter Abtastzeit werden nur **einmal zu Beginn** der Simulation (`t=0`) ausgewertet.

- Ihr Ausgangswert bleibt während der gesamten Simulationsdauer unverändert.
- Dies ist nützlich für Parameter oder Sollwerte, die sich nicht ändern.

**Beispiel:** Ein `Constant`-Block, der den Wert der Erdbeschleunigung (`9.81`) für eine Simulation bereitstellt.

</div>
<div class="two">

![width:1000px](./Diagramme/Draw/Abtastzeit_Konstant.svg)

</div>
</div>

---

<div class="columns">
<div class="three">

#### **Variable** Abtastzeiten `[-2, Tvo]`

Blöcke mit **variabler Abtastzeiten** werden zu beliebigen diskreten Zeiten abgetastet. Simulink unterstützt zwei Mechanismen, um variable Abtastzeiten zu realisieren:

- **Manuelle Bestimmung** der Abtastzeiten mittels `NextTimeHit`-Eigenschaft (z.B. `Pulse Generator` Block).
- **Atomatische Bestimmung** der Abtastzeiten mittels `ZeroCrossing`-Vektor (z.B. `Crossing Hit` Block).

</div>
<div class="two">

![width:1000px](./Diagramme/Draw/Abtastzeit_Variabel.svg)

</div>
</div>

---

<div class="columns">
<div class="three">

#### **Nulldurchgänge** (Zero Crossings)

Die **automatische Bestimmung** mittels Nulldurchgängen wird verwendet, um den exakten Zeitpunkt von Ereignissen zu bestimmen (z.B. Kollision zweier Körper).

- Die exakte Bestimmung des Zeitpunktes ist oft wichtig für die Genauigkeit der Simulationsrechnung
- Blöcke können kontinuierliche Signale für die automatische Bestimmung von Nulldurchgängen übergeben

</div>
<div class="two">

![width:1000px](./Diagramme/Draw/Abtastzeit_Variabel_ZeroCrossing.svg)

</div>
</div>

---

<div class="columns">
<div class="three">

#### **Diskrete** Abtastzeiten `[Ts, To]`

Der Block wird in regelmäßigen Intervallen ausgeführt (z.B. digitale Signalverarbeitung).

- **`Ts` (Sample Time):** Der zeitliche Abstand zwischen zwei Ausführungen.
- **`To` (Offset):** Eine anfängliche Zeitverzögerung.
- Die Ausführungszeitpunkte sind also `To, To + Ts, To + 2*Ts, ...`.

**Beispiel:** Ein `Discrete-Time Integrator`-Block mit `[0.1, 0]` wird alle 0,1 Sekunden ausgeführt.

</div>
<div class="two">

![width:1000px](./Diagramme/Draw/Abtastzeit_Diskret.svg)

</div>
</div>

---

<div class="columns">
<div class="three">

#### **Mehrratige** Abtastzeiten

Ein Modell ist mehrratig, wenn es Blöcke mit **unterschiedlichen Abtastzeiten** enthält.

-  Erfordert Synchronisation zwischen den verschiedenen "Zeitdomänen", um Daten-verlust oder Inkonsistenzen zu vermeiden.

**Beispiel:** Ein *schneller* digitaler Regler (`Ts = 0.01s`) interagiert mit einem *langsameren* physikalischen Streckenmodell (`Ts = 0.1s`). Zwischen den beiden Teilen ist ein `Rate Transition`-Block notwendig.

</div>
<div class="two">

![width:1000px](./Diagramme/Draw/Abtastzeit_Mehrratig.svg)

</div>
</div>

---

#### **Kontinuierliche** Abtastzeiten `[0, 0]`

Blöcke mit dieser Abtastzeit werden in jedem Simulationszeitschritt ausgeführt.

- **Anwendung:** Wird für Blöcke verwendet, die kontinuierliche Zustände haben (z.B. `Integrator`) und deren Verhalten durch Differentialgleichungen beschrieben wird.
- **Festlegung:** Erfordert einen Solver für kontinuierliche Systeme (z.B. `ode45`), der die Schrittweite dynamisch anpasst, um die Genauigkeit zu gewährleisten.
- **Aufteilung:** Solver arbeiten mit *großen* Zeitschritten zur Signalaufzeichnung sowie mit *kleinen* Zeitschritten, um die Genauigkeit zu verbessern.

**Beispiel:** Ein `Integrator`-Block, der die *Geschwindigkeit* eines Fahrzeugs integriert, um dessen *Position* zu berechnen. Da die Bewegung ein kontinuierlicher physikalischer Prozess ist, muss der Block kontinuierlich arbeiten, um eine Positionskurve zu erhalten.

---

#### Kontinuierliche Abtastzeiten **mit festem kleinen Zeitschritt** `[0, 1]`

Diese spezielle Einstellung signalisiert, dass der Block zwar kontinuierlich ist, aber der Solver einen festen, sehr kleinen Zeitschritt verwenden soll, um das Verhalten anzunähern.

- Wird seltener verwendet und ist für spezielle Anwendungsfälle gedacht, bei denen eine Annäherung an ein kontinuierliches Verhalten mit fester Schrittweite erforderlich ist.

**Beispiel:** In einem Modell, das für die *Echtzeit-Hardware-in-the-Loop (HIL)-Simulation* vorgesehen ist, muss der Solver mit einer festen Schrittweite laufen, die der Abtastrate der Hardware entspricht. Ein kontinuierlicher Block in diesem Modell könnte `[0, 1]` verwenden, um anzuzeigen, dass er sich an diese feste Schrittweite anpasst.

---

#### **Vererbte** Abtastzeiten `[-1, 0]`

Dies ist die Standardeinstellung für viele Blöcke. Der Block **erbt** seine Abtastzeit von dem Block, der mit seinem Eingang verbunden ist.

- **Vorteil:** Sorgt für Konsistenz der Abtastzeiten entlang des Signalflusses und reduziert den Konfigurationsaufwand.
- **Konsistenz:** Ausgangssignale werden mit exakt derselben Abtastzeit neu berechnet wie Eingangssignale eines Blocks.

**Beispiel:** Ein `Gain`-Block, der mit dem Ausgang eines `Sine Wave`-Blocks verbunden ist, der mit einer Abtastzeit von 0.01s konfiguriert ist. Der `Gain`-Block erbt automatisch die Abtastzeit von 0.01s und wird somit mit der gleichen Frequenz wie die Sinuswelle aktualisiert.

---

![bg contain right:40%](./Screenshots/Simulink_Timing_Properties.png)

### Abtastzeit **konfigurieren**

Die Abtastzeit eines Blocks kann in dessen **Blockparametern** eingestellt werden.

- **Doppelklick** auf einen Block öffnet den Parameterdialog.
- Unter dem Reiter `Main` (oder `Block Properties`) findet sich oft das Feld `Sample time`.
- Hier kann der gewünschte Wert (z.B. `0.1` für eine diskrete Abtastzeit von 100ms oder `-1` für vererbt) eingetragen werden.

---

![bg contain right:40%](./Screenshots/Simulink_Timing_Legend.png)

### Abtastzeiten **visualisieren**

Simulink kann die verschiedenen Abtastzeiten im Modell farblich hervorheben, um die Analyse zu erleichtern.

- Gehen Sie im Menü auf `Debug > Information Overlays > Sample Time > Colors`.
- Jeder Abtastzeit wird eine eindeutige Farbe zugewiesen.
- Die **Sample Time Legend** (erreichbar über dasselbe Menü) zeigt die Zuordnung von Farben zu Abtastzeiten an.

---

![bg contain right](./Illustrationen/Simulink_Solver.jpg)

### 2.1.5. Solver

In diesem Abschnitt betrachten wir die folgenden Themen:

- **Simulationsphasen** (die große Klammer um die jeweilige Simulationsrechnung)
- **Solver-Arten** (die Logik zur Bestimmung der Zeitschritte und Berechnung von Werten)
- **Nulldurchgangserkennung** (eine wichtige Methode für eine hohe Genauigkeit)

---

#### Was sind Solver?

Solver sind für die Berechnung der Zustände und Signalverläufe während eines Simulationsdurchlaufs zuständig.

- Dabei muss entschieden werden, zu welchen Zeitpunkten die Ableitungen, Zustände und Signale des Modells berechnet werden
- Die Zeitpunkte hängen grundsätzlich von den konfigurierten Abtastzeiten der Blöcke und den Solver-Einstellungen ab.
- Eine wichtige Aufgabe der Solver ist die Bestimmung der Abtastzeiten von kontinuierlichen Singalverläufen.
- Für diskrete Signalverläufe ist die Bestimmung der Abtastzeiten einfacher, da sie exakt vorgegebn sind.

---

<div class="columns">
<div class="three">

#### Simulationsphasen

Eine Simulink-Simulation durchläuft typischerweise zwei Hauptphasen:

1.  **Initialisierungsphase:** Simulink wertet Blockparameter aus, berechnet Anfangszustände und bestimmt die Abtastzeiten.
2.  **Simulationsschleife (Ausführungsphase):** Der Solver bestimmt die größe der Zeitschritte und berechnet die Ausgänge, Zustände und Ableitungen des Modells. Diese Phase wiederholt sich, bis die Simulationszeit endet oder ein Abbruchkriterium erfüllt ist.

</div>
<div>

![](./Diagramme/Mermaid/Simulationsphasen.svg)

</div>
</div>

---

<div class="columns">
<div>

#### Solver-Auswahl

Die Grafik auf der rechten Seite zeigt den Entscheidungsbaum für die Auswahl:

- Zunächst ist zu klären, ob mit einem **festen Schritt** (*diskret* oder *Echtzeit-anforderung*) oder mit **variablen Schritten** gerechnet werden soll.
- Danach hängt die Entscheidung noch davon ab, ob das Modell **kontinuierliche Zustände** beinhaltet oder nicht.

</div>
<div>

![](https://de.mathworks.com/help/simulink/ug/library_of_solvers.png)

</div>
</div>

---

<div class="columns">
<div>

#### **Automatische** Solver-Auswahl

Simulink bietet auch die Möglichkeit, den Solver automatisch auszuwählen:

- Die Auswahl hängt zudem noch davon ab, ob das Modell eine **gewöhnliche Differentialgleichung** oder eine **differential-algebraische Gleichung** ist.
- Zudem hängt die Auswahl bei ge-wöhnlichen Differentialgleichungen von deren **Steifigkeit** ab.

</div>
<div>

![](https://de.mathworks.com/help/simulink/ug/autosolver_heuristics.png)

</div>
</div>

---

#### Fixed-Step Discrete Solver

**Fixed-Step Discrete Solver** führen die Simulation in festen, vordefinierten Zeitschritten durch. Die Ausführungspunkte sind gleichmäßig über die Simulationszeit verteilt.

**Anwendungsbereiche:**
-   **Echtzeitsysteme:** Da die Ausführungszeitpunkte fest sind, eignen sie sich hervorragend für die Codegenerierung und den Einsatz in Echtzeitumgebungen (z.B. Hardware-in-the-Loop-Simulationen).
-   **Diskrete Systeme:** Für Modelle, die ausschließlich diskrete Blöcke enthalten.

**Vorteile:**
-   Vorhersehbares Verhalten und Ausführungszeit.
-   Einfache Implementierung in eingebetteten Systemen.

---

#### Fixed-Step Discrete Solver **Funktionsweise**

Zu jedem festen Zeitschritt (`step_size`) werden die Ausgänge der diskreten Blöcke berechnet und deren interne Zustände aktualisiert. Die Berechnung basiert auf den aktuellen Eingängen und den Zuständen des vorherigen Zeitschritts.

**Pseudocode:**
```
// Initialisiere die Zeit
t = t_start
while t < t_end:
  // Berechne Ausgänge basierend auf aktuellen Eingängen und Zuständen
  outputs = calculate_outputs(t, states, inputs)
  // Aktualisiere Zustände für den nächsten Zeitschritt
  states = update_states(t, states, inputs, step_size)
  // Aktualliesere die Zeit
  t = t + step_size
```


---

#### Variable-Step Discrete Solver

**Variable-Step Discrete Solver** passen ihre Schrittweite an die Ereignisse im Modell an. Sie springen von einem Ereignis zum nächsten, anstatt feste Zeitschritte zu verwenden.

**Anwendungsbereiche:**
-   **Ereignisgesteuerte Systeme:** Effizient für Modelle mit unregelmäßigen diskreten Ereignissen oder wenn die genaue Zeitsteuerung von Ereignissen wichtig ist.
-   **Hybride Systeme:** Kann in Kombination mit kontinuierlichen Solvern verwendet werden, um diskrete Anteile in hybriden Systemen zu lösen.

**Vorteile:**
-   Effizienter für Modelle mit wenigen, aber unregelmäßigen diskreten Ereignissen.
-   Genauere Erfassung von Ereigniszeitpunkten.

---

#### Variable-Step Discrete Solver **Funktionsweise**

Der Solver identifiziert den Zeitpunkt des nächsten diskreten Ereignisses (z.B. die nächste Abtastzeit eines Blocks, ein Trigger-Ereignis) und springt direkt zu diesem Zeitpunkt. Die Zustände werden nur an diesen Ereignispunkten aktualisiert.

**Pseudocode:**
```
t = t_start
while t < t_end:
  // Finde den Zeitpunkt des nächsten diskreten Ereignisses
  next_event_time = find_next_event(t, states, inputs)
  step_size = next_event_time - t
  // Berechne Ausgänge und aktualisiere Zustände am Ereigniszeitpunkt
  outputs = calculate_outputs(t, states, inputs)
  states = update_states(t, states, inputs, step_size)
  t = next_event_time
```

---

#### Fixed-Step Continuous Solver

**Fixed-Step Continuous Solver** verwenden eine konstante Schrittweite, um die kontinuierlichen Zustände eines Systems zu integrieren.

**Anwendungsbereiche:**
-   **Echtzeitsysteme:** Ideal für die Codegenerierung und den Einsatz in Echtzeitumgebungen, da die Rechenlast pro Zeitschritt konstant ist.
-   **Systeme mit bekannter Dynamik:** Wenn die Dynamik des Systems gut verstanden wird und eine feste Schrittweite ausreicht, um die Genauigkeit zu gewährleisten.

**Vorteile:**
-   Vorhersehbares Verhalten und Rechenzeit.
-   Einfache Implementierung.

---

#### Fixed-Step Continuous Solver **Funktionsweise**

Zu jedem festen Zeitschritt (`step_size`) berechnet der Solver die Ableitungen der kontinuierlichen Zustände. Anschließend wird eine numerische Integrationsmethode (z.B. Euler, Runge-Kutta 4. Ordnung) angewendet, um die Zustände am Ende des Zeitschritts zu schätzen.

**Pseudocode (allgemein):**
```
t = t_start
while t < t_end:
  // Berechne Ableitungen der Zustände
  derivatives = calculate_derivatives(t, states, inputs)
  // Integriere Zustände zum nächsten Zeitschritt
  states = integrate(states, derivatives, step_size)
  t = t + step_size
```

---

#### Variable-Step Continuous Solver

**Variable-Step Continuous Solver** passen ihre Schrittweite dynamisch während der Simulation an, um eine vorgegebene Fehlertoleranz einzuhalten.

**Anwendungsbereiche:**
-   **Allgemeine Simulationen:** Die Standardwahl für die meisten kontinuierlichen Systeme, da sie eine gute Balance zwischen Genauigkeit und Rechenzeit bieten.
-   **Systeme mit variabler Dynamik:** Zum Beispiel anwendbar für Systeme mit schnellen Einschwingvorgänge gefolgt von langsamen Driftphasen.

**Vorteile:**
-   Optimale Balance zwischen Genauigkeit und Simulationsgeschwindigkeit.
-   Effiziente Handhabung von Systemen mit unterschiedlichen Zeitkonstanten.

---

#### Variable-Step Continuous Solver **Funktionsweise**

Der Solver schätzt bei jedem Zeitschritt den lokalen Fehler der Integration. Ist der Fehler zu groß, wird die Schrittweite reduziert und der Schritt wiederholt. Ist der Fehler klein, wird die Schrittweite für den nächsten Schritt erhöht, um die Effizienz zu steigern.

**Pseudocode (allgemein):**
```
t = t_start
while t < t_end:
  // Bestimme optimale Schrittweite basierend auf Fehlertoleranz
  step_size = determine_optimal_step_size(t, states, inputs, error_tolerance)
  // Berechne Ableitungen der Zustände
  derivatives = calculate_derivatives(t, states, inputs)
  // Integriere Zustände zum nächsten Zeitschritt
  states = integrate(states, derivatives, step_size)
  t = t + step_size
```

---

#### **Algebraische Schleifen** in Solvern

**Beschreibung:**
Eine **algebraische Schleife** entsteht, wenn der Ausgang eines Blocks direkt oder indirekt als einer seiner Eingänge verwendet wird, ohne dass ein Zustand oder eine Zeitverzögerung dazwischenliegt. Dies führt zu einer zirkulären Abhängigkeit, die nicht durch einfache Vorwärtsberechnung gelöst werden kann.

**Problemstellung:**
Simulink kann die Ausgänge der Blöcke in einer algebraischen Schleife nicht direkt berechnen, da die Werte voneinander abhängen. Dies erfordert eine spezielle Behandlung durch den Solver.

---

#### Lösen von **algebraischen Schleifen** in Simulink

**Verfahren:**
1.  **Erkennung:** Simulink erkennt algebraische Schleifen während der Kompilierung des Modells.
2.  **Iterative Lösung:** Für kontinuierliche algebraische Schleifen verwendet Simulink bei jedem Zeitschritt einen iterativen numerischen Ansatz (z.B. Newton-Raphson-Verfahren), um die Werte zu finden, die die algebraische Gleichung erfüllen.

**Auswirkungen:**
-   Die iterative Lösung von algebraischen Schleifen kann die Simulations-geschwindigkeit erheblich reduzieren.
-   Die Genauigkeit der Lösung hängt von der Konvergenz des Verfahrens ab.

---

#### Newton-Raphson-Verfahren

Das **Newton-Raphson-Verfahren** ist ein effizientes iteratives Verfahren zur numerischen Bestimmung von Nullstellen einer reellwertigen Funktion $f(x)$. In Simulink wird es häufig zur Lösung von algebraischen Schleifen eingesetzt, indem es iterativ die Werte findet, die die algebraischen Gleichungen erfüllen.

**Mathematische Formulierung:**
Die Iterationsvorschrift lautet:
$x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$

- $x_n$: Die aktuelle Näherung der Nullstelle.
- $f(x_n)$: Der Funktionswert an der Stelle $x_n$.
- $f'(x_n)$: Die erste Ableitung der Funktion an der Stelle $x_n$.

---

<div class="columns">
<div>

#### **Funktionsweise** des Newton-Raphson-Verfahrens

- Man beginnt mit einem Startwert $x_0$.
- In jedem Schritt wird eine Tangente an die Funktion $f(x)$ im Punkt $(x_n, f(x_n))$ gelegt.
- Der Schnittpunkt dieser Tangente mit der x-Achse liefert die nächste, verbesserte Näherung $x_{n+1}$.
- Iteration endet, wenn Fehlerschwelle unterschritten wurde.

</div>
<div>

![Newton-Raphson-Verfahren](https://upload.wikimedia.org/wikipedia/commons/e/e0/NewtonIteration_Ani.gif)

</div>
</div>

---

#### **Pseudocode** für das Newton-Raphson-Verfahren

Und so könnte eine Implementierung des Verfahren in MATLAB (oder eine anderen Programmiersprache) aussehen:

```
function newton_raphson(f, f_prime, x0, tolerance, max_iterations):
  x = x0
  for i from 1 to max_iterations:
    fx = f(x)
    if abs(fx) < tolerance:
      return x
    f_prime_x = f_prime(x)
    if f_prime_x == 0:
      error "Division by zero"
    x = x - fx / f_prime_x
  return x // Konvergenz nicht erreicht
```


---

#### **Zero Crossings** in Solvern

**Beschreibung:**
Ein **Zero Crossing** (Nulldurchgang) ist ein Ereignis, bei dem ein kontinuierliches Signal einen Schwellenwert (oft Null) überschreitet. Solche Ereignisse können diskrete Änderungen im Systemverhalten auslösen, z.B. das Umschalten eines Schalters, das Erreichen einer Begrenzung oder das Auslösen eines Triggers.

**Problemstellung:**
Kontinuierliche Solver könnten solche Ereignisse überspringen, wenn ihre Schrittweite zu groß ist, was zu ungenauen Ergebnissen oder verpassten Zustandsänderungen führen würde.

---

#### *Verfahren* zur Bestimmung von Nulldurchgängen in Simulink

1. **Erkennung:** Simulink-Solver (insbesondere *Variable-Step Continuous Solver*) verfügen über integrierte Mechanismen zur Erkennung von Zero Crossings.
2. **Ereignis-Lokalisierung:** Wenn ein potenzieller Nulldurchgang erkannt wird, reduziert der Solver seine Schrittweite, um den genauen Zeitpunkt des Ereignisses präzise zu lokalisieren.
3. **Zustandsanpassung:** Am exakten Zeitpunkt des Nulldurchgangs wird die Integration angehalten, die diskreten Zustände des Modells werden aktualisiert (falls das Ereignis eine diskrete Änderung auslöst), und die Integration wird von diesem neuen Punkt aus fortgesetzt.

---

<div class="columns">
<div class="four">

#### **Funktionsweise** der Lokalisierung von Nulldurchgängen

1.  **Intervall-Identifikation:** Der Solver identifiziert ein Zeitintervall $[t_a, t_b]$, in dem ein Signal sein Vorzeichen wechselt (d.h., $sign(f(t_a)) \neq sign(f(t_b))$).
2.  **Intervall-Halbierung:** Das Intervall wird dann in der Mitte geteilt ($t_m = (t_a + t_b) / 2$).
3.  **Vorzeichenprüfung:** Das Vorzeichen von $f(t_m)$ wird überprüft. Das neue Intervall wird auf die Hälfte reduziert, in der der Vorzeichenwechsel weiterhin stattfindet.
4.  **Iteration:** Dieser Prozess wird wiederholt, bis die Länge des Intervalls eine vorgegebene Toleranz unterschreitet.

</div>
<div>

![Bisektionsverfahren](https://upload.wikimedia.org/wikipedia/commons/8/8c/Bisection_method.svg)

</div>
</div>

---

#### **Pseudocode** für die Lokalisierung von Nulldurchgängen

Und so könnte die Implementierung des Verfahren in MATLAB aussehen:

```
function bisection(f, a, b, tolerance, max_iterations):
  if sign(f(a)) == sign(f(b)):
    error "No sign change in interval"

  for i from 1 to max_iterations:
    m = (a + b) / 2
    fm = f(m)
    if abs(fm) < tolerance:
      return m
    if sign(fm) == sign(f(a)):
      a = m
    else:
      b = m
  return m // Konvergenz nicht erreicht
```

---

#### Bedeutung und Beispiele

**Bedeutung:**
Die präzise Handhabung von Zero Crossings ist entscheidend für die Genauigkeit und Stabilität von Simulationen, insbesondere in hybriden Systemen, die sowohl kontinuierliche als auch diskrete Dynamiken aufweisen.

**Beispiele für Blöcke, die Zero Crossings erzeugen:**
-   `Switch`-Block: Schaltet, wenn das Steuersignal einen Schwellenwert überschreitet.
-   `Relay`-Block: Schaltet bei bestimmten Ein- und Ausschaltpunkten.
-   `Saturation`-Block: Erreicht eine obere oder untere Begrenzung.
-   `Hit Crossing`-Block: Erkennt, wenn ein Signal einen bestimmten Wert erreicht.

---

### 2.1.6. Fallbeispiel: Akku-Schrauber

Im Rahmen dieses Kapitels wenden wir die gelernten Konzepte der Simulink Signalmodelle auf das durchgängige Fallbeispiel eines Akku-Schraubers an. Ziel ist es, das vereinfachte Verhalten des Motors zu modellieren.

**Annahmen für das Signalmodell:**
-   Die Drehzahl des Motors ist direkt proportional zur angelegten Spannung.
-   Ein Lastmoment reduziert die effektive Drehzahl.

Dieses Modell wird uns helfen, die Dynamik des Antriebsstrangs zu verstehen und die Auswirkungen verschiedener Eingangsspannungen und Lasten zu analysieren.

---

### Simulink-Modell der **Energieversorgung**

**Akku-Modellierung:**
-   Ein `Constant`-Block kann die Nennspannung des Akkus repräsentieren.
-   Für eine detailliertere Modellierung könnte eine `Lookup Table` verwendet werden, um die Spannungsabnahme in Abhängigkeit vom Ladezustand oder der Stromabgabe abzubilden.

**Ladegerät-Modellierung:**
-   Ein `Step`-Block kann den Zeitpunkt des Anschließens des Ladegeräts simulieren.
-   Ein `Constant`-Block oder ein `Pulse Generator` kann die Ladespannung oder den Ladestrom darstellen.

---

### Simulink-Modell des **Antriebssystems**

**Motor-Modellierung:**
-   Ein `Gain`-Block kann die Umwandlung der angelegten Spannung in eine proportionale Motordrehzahl darstellen (z.B. U/min pro Volt).
-   Ein `Subtract`-Block kann das Lastmoment simulieren, das die Drehzahl reduziert. Das Lastmoment könnte von einem anderen Block (z.B. `Constant` oder `Step`) kommen.

**Getriebe-Modellierung:**
-   Ein weiterer `Gain`-Block kann das Getriebe repräsentieren, das die Motordrehzahl in die Abtriebsdrehzahl des Bohrfutters übersetzt (z.B. ein Untersetzungsverhältnis).

---

![bg right](../Übungsaufgabe.jpg)

### 2.1.7. Übungsaufgabe

Modellieren Sie das Verhalten der atomaren physikalischen Kompo-nenten des 3D-Druckers (z.B. Antriebe) mithilfe von Simulink Signalmodellen.

*Das Verhalten von Software-Komponenten werden wir hingegen später mithilfe von Stateflow Logikmodelle beschreiben.*

---

![bg right](./Illustrationen/Simscape.jpg)

## 2.2 Simscape **Physikmodelle**

In diesem zweiten Abschnitt lernen wir die folgenden Dinge:

1. TODO Kurze Übersicht über die Inhalte des Abschnitts

---

TODO Kurze Einführung in SimScape. Keine detaillierte Beschreibung, wie für Simulink oder Stateflow.

---

![bg right](./Illustrationen/Stateflow.jpg)

## 2.3 Stateflow **Logikmodelle**

In diesem dritten Abschnitt lernen wir die folgenden Dinge:

1. TODO Kurze Übersicht über die Inhalte des Abschnitts


---

TODO Detaillierte Einführung in Stateflow. Ähnlicher Tiefgang wie bei der Einführung von Simulink.

---

![bg right](./Illustrationen/Simulink3D.jpg)

## 2.4 Simulink **3D Animation**

In diesem vierten Abschnitt lernen wir die folgenden Dinge:

1. TODO Kurze Übersicht über die Inhalte des Abschnitts

---

TODO Detaillierte Einführung in Simulink 3D Animation. Ähnlicher Tiefgang wie bei der Einführung von Simulink selbst.
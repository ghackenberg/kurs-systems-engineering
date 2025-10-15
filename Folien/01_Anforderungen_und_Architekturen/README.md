---
marp: true
theme: fhooe
header: MSE - Kapitel 1: Anforderungen und Architekturen
footer: Dr. Georg Hackenberg, Professor für Informatik und Industriesysteme
paginate: true
math: mathjax
---

![bg right](./Titelbild.jpg)

# Kapitel 1: Anforderungen und Architekturen

Dieses Kapitel umfasst die folgenden drei Abschnitte:

1. Anforderungen sammeln
1. Architekturen festlegen
1. Profile anwenden

---

![bg right](./Anforderungen.jpg)

## 1. Anforderungen sammeln

In diesem ersten Abschnitt lernen wir die folgenden Dinge:

1. **Architekturmodelle erstellen**<br/>(System Composer)
1. **Requirement Sets erstellen**<br/>(Requirement Manager)
1. **Requirements erstellen**<br/>(3 Requirement-Typen)
1. **Requirements verknüpfen**<br/>(6 Link-Typen)

---

<div class="columns">
<div>

### Der Start-Bildschirm

Zuerst starten wir Simulink und erstellen eine neues Architekturmodell für den System Composer.

Der System Composer stellt als Vorlage ein Architekturmodell, ein Software-Architekturmodell, und ein Aktivitäts-diagramm bereit.

*Wir erwenden das einfache Architektur-modell an dieser Stelle!*

</div>
<div>

![](./Architektur_Modell_Neu.png)

</div>
</div>

---

<div class="columns">
<div>

### Die Architektur-Ansicht

Nachdem das neue Architekturmodell erstellt wurde, wechselt MATLAB in die Modellierungsansicht.

In der Modellierungsansicht können die Komponenten der Architektur definiert und miteinander verknüpft werden.

*Im initialen Zustand ist die Architektur leer, das heißt die Architektur beinhaltet keine Komponenten.*

</div>
<div>

![](./Architektur_Modell_Leer.png)

</div>
</div>

---

<div class="columns">
<div>

### Der Apps-Reiter

Komponenten modellieren wir auch erst später; jetzt laden wir zunächst Mal die Requirements Manager Ansicht.

Denn im ersten Schritt wollen wir die Anforderungen an das System beschreiben.

*Um die Umsetzung der Anforderungen und die Verifikation der Umsetzung kümmern wir uns später!*

</div>
<div>

![](./Architektur_Modell_Apps.png)

</div>
</div>

---

<div class="columns">
<div>

### Requirement Set hinzufügen

In der Requirements Manager Ansicht definieren wir zunächst ein sogenanntes Requirement Set.

In einem Requirement Set können wir mehrere Anforderungen sammeln und gemeinsam verwalten.

*Requirement Sets werden in einer eigenen Datei gespeichert und können auch wiederverwendet werden!*

</div>
<div>

![](./Architektur_Modell_RequirementsSet_Neu.png)

</div>
</div>

---

<div class="columns">
<div>

### Requirement hinzufügen

Im nächsten Schritt fügen wir einzelne Requirements dem zuvor erstellten Requirement Set hinzu.

Die Requirements repräsentieren die Anforderungen an das System und können hierarchisch strukturiert werden.

*Identifikation und Sammlung von Anforderungen erfolgt durch unterstützende Kreativtechniken!*

</div>
<div>

![](./Architektur_Modell_Requirement_Neu.png)

</div>
</div>

---

<div class="columns">
<div>

### Der Property Inspector

Die Eigenschaften der einzelnen Requirements können in der Property Inspector Ansicht verwaltet werden.

Die Eigenschaften umfassen einen Typ, eine Zusammenfassung, und eine detaillierte Beschreibung.

*Die Requirements Toolbox erzwingt keine spezielle Art der Beschreibung (z.B. definierte Satzmuster)!*

</div>
<div>

![](./Architektur_Modell_Requirement_Beispiel.png)

</div>
</div>

---

<div class="columns">
<div>

### Die Requirement-Typen

Wir unterscheiden diese Typen:

- **Container** - Gruppierung von Anforderungen (z.B. nach Ingenieursdisziplin)
- **Functional** - Klassische Funktionale Anforderungen (z.B. Wandlung von Energie)
- **Informational** - Klassische nicht-funktionale Anforderungen (z.B. Performance oder Sicherheit)

</div>
<div>

![](./Architektur_Modell_Requirement_Edit.png)

</div>
</div>

---

![bg contain right:20%](./Requirement_Typen_Container.jpg)

#### Requirement-Typ **Container**

**Zweck:** Diese dienen primär der Strukturierung und Hierarchisierung der Anforderungen. Sie fungieren als Ordner oder Überschriften, um logische Gruppen zu bilden.

**Beispiel:** Eine Anforderung mit dem Typ Container könnte "System-Sicherheit" oder "Benutzerverwaltung" lauten und darunter eine Reihe spezifischer Funktionaler Anforderungen enthalten.

**Status:** Container-Anforderungen selbst tragen nicht zum Implementierungs- oder Verifizierungsstatus bei. Der Status wird jedoch durch die funktionalen Anforderungen innerhalb des Containers bestimmt und auf der Containerebene aggregiert.

---

![bg contain right:20%](./Requirement_Typen_Functional.jpg)

#### Requirement-Typ **Functional**

**Zweck:** Diese Anforderungen sind das Kernstück der Spezifikation. Sie beschreiben direkt die erforderlichen Fähigkeiten und das Verhalten des zu entwickelnden Systems oder Produkts.

**Beispiel:** "Das System muss die Eingabedaten innerhalb von 50 Millisekunden verarbeiten." oder "Die Benutzeroberfläche muss einen 'Speichern'-Button enthalten."

**Status:** Die Toolbox berechnet den Implementierungs- und Verifizierungsstatus basierend auf den Links zu Designelementen (Implementierung) und Tests (Verifizierung). Sie tragen direkt zum Fortschritt bei.

---

![bg contain right:20%](./Requirement_Typen_Informational.jpg)

#### Requirement-Typ **Informational**

**Zweck:** Dient der Erfassung von Anforderungen oder Informationen, die kein direktes funktionales Verhalten darstellen oder die das System nicht direkt implementieren muss, wie nicht-funktionale Anforderungen und zusätzliche Erklärungen.

**Beispiel:** "Die Verwendung der Bibliothek X ist aus Gründen der Kompatibilität erforderlich." oder "Alle Passwörter müssen eine Mindestlänge von 8 Zeichen haben (Sicherheitsanforderung)."

**Status:** Informational-Anforderungen tragen nicht zum Implementierungs- oder Verifizierungsstatus bei. Sie dienen rein dokumentarischen oder ergänzenden Zwecken im Kontext der Anforderungssammlung.

---

<div class="columns">
<div>

### Der Requirements Editor

Neben dem Requirements Manager bietet die Requirements Toolbox auch den sogenannten Requirements Editor.

Der Requirements Editor kann über den Reiter **Requirements** im oberen Menü-band geöffnet werden.

*Der Requirements Editor kann insbesondere für die Verknüpfung von Anforderungen verwenden wertden!*

</div>
<div>

![](./Architektur_Modell_Requirement_Editor.png)

</div>
</div>

---

<div class="columns">
<div>

### Die Tabellen-Ansicht

Der Requirements Editor bietet zunächst die gewohnte tabellarische Ansicht der Anforderungen.

Die Details der einzelnen Anforderungen wiederum auch im Property Inspector dargestellt.

*Neben der tabellarischen Darstellung bietet der Requirements Editor auch eine Dokumentendarstellung.*

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Tabelle.png)

</div>
</div>

---

<div class="columns">
<div>

### Die Dokumenten-Ansicht

Die Dokumentendarstellung zeigt neben der Zusammenfassung auch die Beschrei-bung der einzelnen Anforderungen.

Diese Darstellung beim Durchlesen der Anforderungsspezifikation aufgrund des höheren Detaillierungsgrades.

*Eine Bearbeitung der Inhalte ist in der Dokumentenansicht direkt jedoch nicht möglich!*

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Dokument.png)

</div>
</div>

---

<div class="columns">
<div>

### Link erstellen (1 / 2)

Ein mächtiges Werkzeug in der System-entwicklung ist die Nachverfolgung von Anforderungen (*Tracing*).

Vor die Nachverfolgung bietet die Requirements Toolbox die Möglichkeit, sogenannte **Links** einzufügen.

*Im Requirements Editor kann dazu zunächst die zu vernüpfende Anforder-ung ausgewählt werden!*

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_Select.png)

</div>
</div>

---

<div class="columns">
<div>

### Link erstellen (2 / 2)

Danach muss eine weitere Anforderung ausgewählt werden, die mit der vorigen verknüpft werden soll.

Schließlich kann die Erstellung des Links bestätigt werden und so ein neue Ver-küpfung geschaffen werden.

*Beachte, das Anforderungen auch mit Komponenten und anderen Modell-elementen verknüpft werden können!*

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_Create.png)

</div>
</div>

---

<div class="columns">
<div>

### Der Link-Abschnitt

Nach Erstellen einer neuer Verknüpfung ist der Link im Property Inspector rechts unten zu sehen.

Die Ansicht zeigt für die gewählte Anforderung alle damit verknüpften Modellelemente.

*Somit kann bei Änderung der Anforderung schnell untersucht werden, welche Folgen die Änderung hat!*

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_View.png)

</div>
</div>

---

<div class="columns">
<div>

### Die Links-Ansicht

Zudem gibt es eine eigene Links-Ansicht, welche eine Übersicht über alle Verknüpfungen im Modell gibt.

Die Ansicht zeigt auch Vernüpfungen zu anderen Modellen (d.h. anderen Modell-dateien).

*In dieser Ansicht können einzelne Links ausgewählt und deren Eigenschaften im Property Inspector bearbeitet werden!*

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_Show.png)

</div>
</div>

---

<div class="columns">
<div>

### Die Link-Typen

Schließlich unterscheidet die MATLAB Requirements Toolbox standardmäßig sechs Link-Typen:

**Confirmed by**, **Derives**, **Implements**, **Refines**, **Related to**, und **Verifies**.

*Im Folgenden betrachten wir die einzelnen Typen, deren Bedeutung, und typische Anwendungsfälle.*

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_Edit.png)

</div>
</div>

---

![bg contain right:40%](./Link_Typen_Confirmed.jpg)

#### Link-Typ **Confirmed by** (*Bestätigt durch*)

*Dieser Link-Typ wird verwendet, um eine Anforderung mit einem Testfall oder Testergebnis zu verknüpfen.*

**Bedeutung:** Das verknüpfte Element (z. B. ein Test) zeigt, dass die Anforderung erfüllt ist und ordnungsgemäß funktioniert.

**Beispiel:** Eine Anforderung "Das System muss Daten in weniger als 500 ms laden" wird durch einen Leistungstest bestätigt.

---

![bg contain right:30%](./Link_Typen_Derives.jpg)

#### Link-Typ **Derives** (*Leitet ab*)

*Dieser Typ stellt eine Hierarchie oder einen Abstammungsverlauf zwischen Anforderungen her.*

**Bedeutung:** Eine Anforderung wird aus einer höherstufigen oder Eltern-Anforderung abgeleitet. Die abgeleitete Anforderung ist eine spezifischere Ausformulierung der übergeordneten.

**Beispiel:** Die hochstufige Anforderung "Das Benutzerkonto muss sicher sein" leitet die spezifischere Anforderung ab: "Das Passwort muss mindestens 8 Zeichen lang sein."

---

![bg contain right:35%](./Link_Typen_Implements.jpg)

#### Link-Typ **Implements** (*Implementiert*)

*Dieser Link-Typ verbindet eine Anforderung mit dem Code oder Design-Modell, das sie erfüllt.*

**Bedeutung:** Das verknüpfte Element (Code-Funktion, Simulink-Block usw.) setzt die Anforderung technisch um. Dies ist ein kritischer Link für die Rückverfolgbarkeit von der Anforderung zur Implementierung.

**Beispiel:** Die Anforderung "Berechne den Steigungswinkel der Achse" implementiert eine spezifische MATLAB-Funktion (calculate_slope.m).

---

![bg contain right:25%](./Link_Typen_Refines.jpg)

#### Link-Typ **Refines** (*Verfeinert*)

*Dieser Typ wird ähnlich wie "Derives" zur Spezifizierung verwendet, liegt aber oft auf derselben Ebene oder dient dazu, eine Anforderung detaillierter oder präziser zu machen, ohne eine strenge Eltern-Kind-Beziehung zu implizieren.*

**Bedeutung:** Die eine Anforderung fügt Details hinzu oder stellt klar, was eine andere Anforderung bedeutet. Es ist eine Verfeinerung des Umfangs oder der Spezifikation.

**Beispiel:** Eine Anforderung "Die Benutzeroberfläche muss intuitiv sein" wird verfeinert durch "Die Navigationsleiste muss stets sichtbar sein."

---

![bg contain right:25%](./Link_Typen_Related.jpg)

#### Link-Typ **Related to** (*Bezogen auf*)

*Dies ist der generischste Link-Typ und wird für alle Verbindungen verwendet, die nicht in die spezifischeren Kategorien fallen.*

**Bedeutung:** Die verknüpften Elemente haben eine relevante Verbindung oder gegenseitige Abhängigkeit, aber keine formelle Beziehung (wie Implementierung oder Ableitung).

**Beispiel:** Die Anforderung "Das System muss unter Linux laufen" ist bezogen auf die Anforderung "Das System muss eine bestimmte Datenbank verwenden," da beide die Umgebung betreffen.

---

![bg contain right:35%](./Link_Typen_Verifies.jpg)

#### Link-Typ **Verifies** (*Überprüft*)

*Dieser Link-Typ stellt eine Verbindung zwischen einem Test und der Anforderung her, die er validieren soll. Es ist oft die umgekehrte Richtung von "Confirmed by".*

**Bedeutung:** Das verknüpfte Element (in der Regel ein Test oder ein Test-Artefakt) dient dazu, zu beweisen, dass die Anforderung erfüllt ist. Es zeigt die Testabdeckung der Anforderung.

**Beispiel:** Ein Unittest überprüft die Anforderung "Die Bremsfunktion muss bei <10 km/h aktiviert werden."

---

![bg right](../Übungsaufgabe.jpg)

### Übungsaufgabe

Sammle Anforderungen an den 3D-Drucker und dokumentiere die Anforderungen mithilfe der MATLAB Requirements Toolbox.

*Achte auf sinnvolle Container-Hierarchien, Zusammenfassungen, Beschreibungen, und Begründungen!*

---

![bg right](./Architekturen.jpg)

## 2. Architekturen festlegen

In diesem zweiten Abschnitt lernen wir die folgenden Dinge:

1. **Komponenten erstellen**<br/>(Reference, Variant, Adapter)
1. **Ports erstellen / verknüpfen**<br/>(Input, Output, Physical)
1. **Interfaces erstellen / zuweisen**<br/>(Value, Composite  Data, Physical)
1. **Anforderungen verknüpfen**<br/>(Tracability Matrix)

---

![bg right](../Übungsaufgabe.jpg)

### Übungsaufgabe

TODO

---

![bg right](./Stereotypen.jpg)

## 3. Profile anwenden

In diesem dritten Abschnitt lernen wir die folgenden Dinge:

1. **Profil erstellen / anwenden**<br/>(Stereotype, Property)
1. **Views erstellen / nutzen**<br/>(Component Filter, Port Filter)

---

![bg right](../Übungsaufgabe.jpg)

### Übungsaufgabe

TODO
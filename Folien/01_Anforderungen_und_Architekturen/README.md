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

In diesem Kapitel nutzen wir die folgenden Add-Ons:

1. System Composer
1. Requirements Toolbox

---

<div class="columns">
<div>

## Der Start-Bildschirm

TODO

</div>
<div>

![](./Architektur_Modell_Neu.png)

</div>
</div>

---

<div class="columns">
<div>

## Die Architektur-Ansicht

TODO

</div>
<div>

![](./Architektur_Modell_Leer.png)

</div>
</div>

---

<div class="columns">
<div>

## Der Apps-Reiter

TODO

</div>
<div>

![](./Architektur_Modell_Apps.png)

</div>
</div>

---

<div class="columns">
<div>

## Requirement Set hinzufügen

TODO

</div>
<div>

![](./Architektur_Modell_RequirementsSet_Neu.png)

</div>
</div>

---

<div class="columns">
<div>

## Requirement hinzufügen

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Neu.png)

</div>
</div>

---

<div class="columns">
<div>

## Der Property Inspector

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Beispiel.png)

</div>
</div>

---

<div class="columns">
<div>

## Die Requirement-Typen

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

### Requirement-Typ **Container**

**Zweck:** Diese dienen primär der Strukturierung und Hierarchisierung der Anforderungen. Sie fungieren als Ordner oder Überschriften, um logische Gruppen zu bilden.

**Beispiel:** Eine Anforderung mit dem Typ Container könnte "System-Sicherheit" oder "Benutzerverwaltung" lauten und darunter eine Reihe spezifischer Funktionaler Anforderungen enthalten.

**Status:** Container-Anforderungen selbst tragen nicht zum Implementierungs- oder Verifizierungsstatus bei. Der Status wird jedoch durch die funktionalen Anforderungen innerhalb des Containers bestimmt und auf der Containerebene aggregiert.

---

![bg contain right:20%](./Requirement_Typen_Functional.jpg)

### Requirement-Typ **Functional**

**Zweck:** Diese Anforderungen sind das Kernstück der Spezifikation. Sie beschreiben direkt die erforderlichen Fähigkeiten und das Verhalten des zu entwickelnden Systems oder Produkts.

**Beispiel:** "Das System muss die Eingabedaten innerhalb von 50 Millisekunden verarbeiten." oder "Die Benutzeroberfläche muss einen 'Speichern'-Button enthalten."

**Status:** Die Toolbox berechnet den Implementierungs- und Verifizierungsstatus basierend auf den Links zu Designelementen (Implementierung) und Tests (Verifizierung). Sie tragen direkt zum Fortschritt bei.

---

![bg contain right:20%](./Requirement_Typen_Informational.jpg)

### Requirement-Typ **Informational**

**Zweck:** Dient der Erfassung von Anforderungen oder Informationen, die kein direktes funktionales Verhalten darstellen oder die das System nicht direkt implementieren muss, wie nicht-funktionale Anforderungen und zusätzliche Erklärungen.

**Beispiel:** "Die Verwendung der Bibliothek X ist aus Gründen der Kompatibilität erforderlich." oder "Alle Passwörter müssen eine Mindestlänge von 8 Zeichen haben (Sicherheitsanforderung)."

**Status:** Informational-Anforderungen tragen nicht zum Implementierungs- oder Verifizierungsstatus bei. Sie dienen rein dokumentarischen oder ergänzenden Zwecken im Kontext der Anforderungssammlung.

---

<div class="columns">
<div>

## Der Requirements Editor

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Editor.png)

</div>
</div>

---

<div class="columns">
<div>

## Die Tabellen-Ansicht

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Tabelle.png)

</div>
</div>

---

<div class="columns">
<div>

## Die Dokumenten-Ansicht

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Dokument.png)

</div>
</div>

---

<div class="columns">
<div>

## Link erstellen (1 / 2)

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_Select.png)

</div>
</div>

---

<div class="columns">
<div>

## Link erstellen (2 / 2)

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_Create.png)

</div>
</div>

---

<div class="columns">
<div>

## Der Link-Abschnitt

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_View.png)

</div>
</div>

---

<div class="columns">
<div>

## Die Links-Ansicht

TODO

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_Show.png)

</div>
</div>

---

<div class="columns">
<div>

## Die Link-Typen

TODO

**Confirmed by**, **Derives**, **Implements**, **Refines**, **Related to**, **Verifies**

</div>
<div>

![](./Architektur_Modell_Requirement_Editor_Link_Edit.png)

</div>
</div>

---

![bg contain right:40%](./Link_Typen_Confirmed.jpg)

### Link-Typ **Confirmed by** (*Bestätigt durch*)

*Dieser Link-Typ wird verwendet, um eine Anforderung mit einem Testfall oder Testergebnis zu verknüpfen.*

**Bedeutung:** Das verknüpfte Element (z. B. ein Test) zeigt, dass die Anforderung erfüllt ist und ordnungsgemäß funktioniert.

**Beispiel:** Eine Anforderung "Das System muss Daten in weniger als 500 ms laden" wird durch einen Leistungstest bestätigt.

---

![bg contain right:30%](./Link_Typen_Derives.jpg)

### Link-Typ **Derives** (*Leitet ab*)

*Dieser Typ stellt eine Hierarchie oder einen Abstammungsverlauf zwischen Anforderungen her.*

**Bedeutung:** Eine Anforderung wird aus einer höherstufigen oder Eltern-Anforderung abgeleitet. Die abgeleitete Anforderung ist eine spezifischere Ausformulierung der übergeordneten.

**Beispiel:** Die hochstufige Anforderung "Das Benutzerkonto muss sicher sein" leitet die spezifischere Anforderung ab: "Das Passwort muss mindestens 8 Zeichen lang sein."

---

![bg contain right:35%](./Link_Typen_Implements.jpg)

### Link-Typ **Implements** (*Implementiert*)

*Dieser Link-Typ verbindet eine Anforderung mit dem Code oder Design-Modell, das sie erfüllt.*

**Bedeutung:** Das verknüpfte Element (Code-Funktion, Simulink-Block usw.) setzt die Anforderung technisch um. Dies ist ein kritischer Link für die Rückverfolgbarkeit von der Anforderung zur Implementierung.

**Beispiel:** Die Anforderung "Berechne den Steigungswinkel der Achse" implementiert eine spezifische MATLAB-Funktion (calculate_slope.m).

---

![bg contain right:25%](./Link_Typen_Refines.jpg)

### Link-Typ **Refines** (*Verfeinert*)

*Dieser Typ wird ähnlich wie "Derives" zur Spezifizierung verwendet, liegt aber oft auf derselben Ebene oder dient dazu, eine Anforderung detaillierter oder präziser zu machen, ohne eine strenge Eltern-Kind-Beziehung zu implizieren.*

**Bedeutung:** Die eine Anforderung fügt Details hinzu oder stellt klar, was eine andere Anforderung bedeutet. Es ist eine Verfeinerung des Umfangs oder der Spezifikation.

**Beispiel:** Eine Anforderung "Die Benutzeroberfläche muss intuitiv sein" wird verfeinert durch "Die Navigationsleiste muss stets sichtbar sein."

---

![bg contain right:25%](./Link_Typen_Related.jpg)

### Link-Typ **Related to** (*Bezogen auf*)

*Dies ist der generischste Link-Typ und wird für alle Verbindungen verwendet, die nicht in die spezifischeren Kategorien fallen.*

**Bedeutung:** Die verknüpften Elemente haben eine relevante Verbindung oder gegenseitige Abhängigkeit, aber keine formelle Beziehung (wie Implementierung oder Ableitung).

**Beispiel:** Die Anforderung "Das System muss unter Linux laufen" ist bezogen auf die Anforderung "Das System muss eine bestimmte Datenbank verwenden," da beide die Umgebung betreffen.

---

![bg contain right:35%](./Link_Typen_Verifies.jpg)

### Link-Typ **Verifies** (*Überprüft*)

*Dieser Link-Typ stellt eine Verbindung zwischen einem Test und der Anforderung her, die er validieren soll. Es ist oft die umgekehrte Richtung von "Confirmed by".*

**Bedeutung:** Das verknüpfte Element (in der Regel ein Test oder ein Test-Artefakt) dient dazu, zu beweisen, dass die Anforderung erfüllt ist. Es zeigt die Testabdeckung der Anforderung.

**Beispiel:** Ein Unittest überprüft die Anforderung "Die Bremsfunktion muss bei <10 km/h aktiviert werden."
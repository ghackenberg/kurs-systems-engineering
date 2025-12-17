---
marp: true
theme: fhooe
header: MSE - Epilog
footer: Dr. Georg Hackenberg, Professor für Informatik und Industriesysteme
paginate: true
math: mathjax
---

![bg right](./Titelbild.jpg)

# Epilog: Zusammenfassung und Ausblick

In diesem Kapitel fassen wir die wichtigsten Erkenntnisse des Kurses zusammen und werfen einen Blick auf das große Ganze des modellbasierten Systems Engineering.

---

## Was haben wir gelernt?

Der Kurs ruht auf drei Säulen, die den Kern des modellbasierten Entwicklungsprozesses abbilden:

1.  **Anforderungen & Architekturen**
    *(Wie man Systeme formal beschreibt und strukturiert)*

2.  **Verhalten & Animationen**
    *(Wie man die Dynamik dieser Systeme modelliert)*

3.  **Verifikationen & Störungen**
    *(Wie man sicherstellt, dass die Systeme korrekt und sicher sind)*

---

### Kapitel 1: Anforderungen & Architekturen

-   **Requirements Toolbox:** Anforderungen werden systematisch erfasst, strukturiert (Container) und typisiert (Functional, Informational).
-   **Traceability:** Durch die Verknüpfung von Anforderungen untereinander (`Derives`, `Refines`) und mit Architekturelementen (`Implements`) schaffen wir eine lückenlose Nachverfolgbarkeit.
-   **System Composer:** Wir bauen komplexe Systemarchitekturen aus Komponenten, Ports und klar definierten Schnittstellen.
-   **Metadaten & Sichten:** Mit Profilen und Stereotypen reichern wir unser Modell um wertvolle Metadaten (z.B. Kosten, Gewicht) an. Views helfen uns, die Komplexität zu beherrschen, indem wir uns auf spezifische Aspekte (z.B. nur mechanische Bauteile) konzentrieren.

---

### Kapitel 2: Verhalten & Animationen

-   **Drei Paradigmen für hybride Systeme:**
    -   **Simulink:** Kausale, signalbasierte Modellierung für Steuerungs- und Regelungsalgorithmen. *(Was ist die Wirkung einer Ursache?)*
    -   **Simscape:** Akausale, physikalische Netzwerkmodellierung für multidisziplinäre Systeme (Mechanik, Elektrik, etc.). *(Wie verhält sich das Gesamtsystem?)*
    -   **Stateflow:** Zustandsbasierte Modellierung für Logik, Abläufe und komplexe Entscheidungen. *(In welchem Zustand befindet sich das System?)*
-   **3D Animation:** Die Visualisierung der Simulationsergebnisse in einer 3D-Umgebung macht das Verhalten des Systems greifbar und verständlich.

---

### Kapitel 3: Verifikationen & Störungen

-   **Methodische Grundlage:** Wir nutzen etablierte Konzepte wie die testgetriebene Entwicklung (TDD) und das V-Modell (MIL, SIL, PIL, HIL), um die Qualität unserer Entwicklung sicherzustellen.
-   **Simulink Test:** Wir automatisieren die anforderungsbasierte Verifikation unserer Modelle. Mit dem Test Manager verwalten wir Testfälle, die in isolierten Test-Harnesses ausgeführt und formal bewertet werden (Baseline, `verify`).
-   **Testabdeckung (Coverage):** Wir messen objektiv die Gründlichkeit unserer Tests (z.B. Decision, Condition, MCDC), um ungetestete Logikpfade aufzudecken.
-   **Simulink Fault Analyzer:** Wir analysieren die Systemsicherheit durch gezielte Injektion von Störungen und validieren so die Wirksamkeit unserer Sicherheitsmechanismen (FMEA).

---

## Das große Ganze: MBSE in der Praxis

Modellbasiertes Systems Engineering ist kein Werkzeug, sondern ein **durchgängiger, iterativer Prozess**, der alle Phasen der Entwicklung verbindet.

Der wahre Mehrwert liegt in der **digitalen Durchgängigkeit**: Anforderungen, Architektur, Verhalten, und Tests sind nicht länger isolierte Dokumente, sondern ein integriertes, lebendiges Gesamtmodell.

Diese **Traceability** ist der Schlüssel zur Beherrschung von Komplexität, zur schnellen Auswirkungsanalyse bei Änderungen und zur effizienten Zertifizierung sicherer und zuverlässiger mechatronischer Systeme.

---

# Fragen?

Vielen Dank für Ihre Aufmerksamkeit!

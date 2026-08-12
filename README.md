# Dr. Scale

Skalierungsrechner von Patientenportalen. Szenarienbasierte Entscheidungsunterstützung für
Krankenhäuser.

**→ [erencanersoy.github.io/dr-scale](https://erencanersoy.github.io/dr-scale/)**

## Was das Werkzeug leistet

Dr. Scale beantwortet zwei Entscheidungsfragen, beide mit einer Zahl in Terminen je Jahr.

| Entscheidungsfrage | Ergebnisgröße |
|---|---|
| Soll eine weitere Klinik an das Portal angebunden werden? | Mindestgröße einer Klinik |
| Trägt sich die Gesamtinvestition? | Break-even des Portals |

Weil beide Antworten in Terminen je Jahr stehen, lassen sie sich unmittelbar an der eigenen
Terminliste prüfen. Szenarien zeigen, wie stark die Antwort vom künftigen digitalen
Buchungsanteil abhängt. Eine Sensitivitätsanalyse zeigt, welche Rechengröße die Schwelle am
stärksten verschiebt und wo sich genauere Daten am ehesten lohnen.

## Rechenkern

Bewertet wird nach der Kapitalwertmethode, die die Ausführungsvorschrift zu § 7 der
Landeshaushaltsordnung vorschreibt. Alle Zahlungen werden in zwei Gruppen geteilt. Was mit dem
angebundenen Terminvolumen wächst, steht in `N`. Was unabhängig davon anfällt, steht im
Fixblock `F`.

```
KW(V) = V × N − F
```

Der Nutzen je umgestelltem Termin ergibt sich aus dem vermiedenen Terminausfall, der
eingesparten Verwaltungszeit und den variablen Kosten je Onlinebuchung.

```
n   = (r_off − r_on) / 100 × b  +  t / 60 × c  −  k
d_j = d_0 + (d_H − d_0) × j / H
N   = Σ n × d_j / (1 + i)^j
F   = I₀ + Σ K / (1 + i)^j − Σ A_j / (1 + i)^j
```

Beide Ergebnisgrößen sind Ablesungen an derselben Geraden.

```
m = a / N        Mindestgröße einer Klinik in Terminen je Jahr
B = F / N        Break-even des Portals in Terminen je Jahr
```

Der vermiedene Vergütungsabschlag `A_j` folgt aus der Digitalisierungsabschlagsvereinbarung
nach § 5 Abs. 3h KHEntgG. Dem digitalen Terminmanagement ist genau eine von 19 gleich
gewichteten Muss-Anforderungen des Fördertatbestands 2 zuzuordnen.

## Aufbau

Das Modell trennt streng zwischen dem allgemeinen Teil und den Werten des betrachteten Hauses.
Der allgemeine Teil stammt aus Rechtsgrundlage und Literatur und gilt für jedes Krankenhaus in
Deutschland. Sechs Herkunftsarten werden unterschieden und durchgehend farblich gekennzeichnet:
Literatur, Rechtsgrundlage, Sekundärdaten, Annahme, Festlegung und im Modell Berechnetes.

Voreingestellt ist ein Musterkrankenhaus mit frei gewählten, gerundeten Werten ohne empirischen
Anspruch. Alle als *Zu erheben* gekennzeichneten Größen muss jedes Haus selbst ermitteln.

Jede Gleichung wird zusätzlich beschreibend erläutert, jeder Wert nennt Herkunft und Beleg.
Zitiert wird nach APA 7.

## Anwendungsbeispiel

Die Werte eines Anwendungsbeispiels sind mit AES-256-GCM verschlüsselt hinterlegt. Der Schlüssel
wird über PBKDF2-HMAC-SHA256 mit 250.000 Runden aus einem Passwort abgeleitet, die
Entschlüsselung erfolgt ausschließlich im Browser über die Web-Crypto-Schnittstelle. Ohne
Passwort sind diese Werte auch im Quelltext nicht lesbar. Das allgemeine Modell ist ohne
Passwort vollständig zugänglich.

## Ausgabe

Fünf Abbildungen in wissenschaftlicher Darstellung lassen sich als Vektorgrafik speichern, bei
Bedarf als PNG. Linienarten sind so gewählt, dass die Abbildungen auch im Schwarzweißdruck
unterscheidbar bleiben. Jeder Reiter lässt sich zusätzlich als Markdown speichern oder über den
Druckdialog als PDF ausgeben.

## Technisches

Eine einzelne, in sich geschlossene HTML-Datei ohne externe Abhängigkeiten. Keine Bibliothek,
keine Schriftart und kein Bild wird nachgeladen. Diagramme werden als SVG erzeugt.

## Hinweis

Modellhafte Beispielrechnung unter offengelegten Annahmen. Sie dient der Vorbereitung einer
Entscheidung und ersetzt keine Wirtschaftlichkeitsberechnung nach haushaltsrechtlichen Vorgaben.
Drei Rechengrößen sind Annahmen ohne Quelle. Der Zusammenhang zwischen Onlinebuchung und
geringerem Terminausfall ist gemessen, ein ursächlicher Zusammenhang ist nicht belegt.

---

Erencan Ersoy · Masterarbeit an der Freien Universität Berlin

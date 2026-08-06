# Dr. Scale

Planungsrechner zur Einführung und Skalierung von Terminmanagementportalen im Krankenhaus.

**→ [erencanersoy.github.io/dr-scale](https://erencanersoy.github.io/dr-scale/)** (passwortgeschützt)

## Was das Werkzeug leistet

Dr. Scale unterstützt Krankenhäuser evidenzbasiert dabei, die Wirtschaftlichkeit digitaler
Terminmanagementportale nachvollziehbar und transparent zu bewerten. Es verbindet Rechengrößen
aus Literatur, Sekundärdaten und Annahmen mit den Daten des jeweiligen Krankenhauses. Daraus
werden Nettonutzen und Break-even berechnet. Alle Eingangsgrößen und Szenarien sind anpassbar.

Die Bewertung erfolgt über Szenarien, weil die Wirtschaftlichkeit von den zugrunde gelegten
Annahmen und späteren Entwicklungen abhängt, die zum Zeitpunkt der Bewertung noch nicht sicher
absehbar sind. Unterschieden werden ein Referenzszenario ohne Bereitstellung und drei
literaturbasierte Skalierungsstrategien.

## Rechenkern

Der jährliche Nettonutzen ergibt sich als

```
N = N_A + N_B − K + K_C
```

mit den vermiedenen Terminausfällen `N_A = (r(0) − r(d)) · T · b`, der Prozessentlastung
`N_B = d · T · τ · c`, den laufenden Kosten `K` und dem vermiedenen Vergütungsabschlag
`K_C = a · E`. Die Versäumnisquote folgt aus `r(d) = d · r_online + (1 − d) · r_offline`,
die Amortisationsdauer aus `t = I₀ / N`.

Herleitung, Quellen der Annahmen und Grenzen der Aussagekraft sind in der Anwendung selbst
unter „Über Dr. Scale" dokumentiert.

## Technisches

Eine einzelne, in sich geschlossene HTML-Datei ohne externe Abhängigkeiten. Keine Bibliothek,
keine Schriftart und kein Bild wird nachgeladen. Diagramme werden als SVG erzeugt und lassen
sich als PNG oder SVG für die Weiterverwendung speichern.

Der Inhalt ist mit AES-256-GCM verschlüsselt, der Schlüssel wird über PBKDF2-HMAC-SHA256 mit
250.000 Runden aus dem Passwort abgeleitet. Die Entschlüsselung erfolgt ausschließlich im
Browser über die Web-Crypto-Schnittstelle. Ohne Passwort ist der Inhalt auch im Quelltext
nicht lesbar.

## Hinweis

Modellhafte Beispielrechnung unter offengelegten Annahmen. Sie dient der Vorbereitung einer
Entscheidung und ersetzt keine Wirtschaftlichkeitsberechnung nach haushaltsrechtlichen Vorgaben.

---

Erencan Ersoy · Masterarbeit an der Freien Universität Berlin

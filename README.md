# BaroWatch — Website

Statische Webseite für die App **BaroWatch** (App Store): Datenschutzerklärung, Support-Kontakt, Impressum.

Gehostet via **GitHub Pages**: <https://alfhellmund.github.io/BaroWatch/>

## Seiten

- `index.html` — Landing-Page
- `privacy.html` — Sprachauswahl der Datenschutzerklärung (ohne Erklärungstext; erzeugt, nicht von Hand)
- `privacy-de.html` — Datenschutzerklärung Deutsch (maßgeblich, von Hand gepflegt)
- `privacy-<code>.html` — Datenschutzerklärung je weitere Sprache, beginnend mit `privacy-en.html` (erzeugt)
- `support.html` — Support-Kontakt + FAQ
- `impressum.html` — Anbieterkennzeichnung (§ 5 DDG / § 18 MStV)
- `style.css` — Gestaltung, dazu die Klasse `.pruefen` für Entwurfsmarker

## Änderungen an der Datenschutzerklärung

Ändert die App Berechtigungen, Speicherung oder Datenwege, wird `privacy-de.html` gegen den Code nachgezogen und Fassung und Stand im Kopf
der Seite und in der Fassungszeile erhöht.

Ablauf bei einer neuen Fassung (Werkzeug `Tools/privacy_l10n.py` im Repository der Starpath-App):

1. `privacy-de.html` ändern, Fassung und Stand erhöhen.
2. `python3 Tools/privacy_l10n.py pruefen <Pfad zu diesem Ordner>` meldet je Sprache die veralteten Einheiten (`data-quelle` weicht vom aktuellen deutschen Text ab).
3. Veraltete Einheiten nachübersetzen, die Seite mit `bauen` neu erzeugen, bis `pruefen` Exit 0 liefert und 0 veraltet meldet.
4. Marker-Suche (unten) leer, dann Push.

Regeln:

- Die Dateinamen `privacy-<code>.html` werden nicht umbenannt (App Store Connect, Privacy Policy URL nicht editierbar). `<code>` ist die Sprachkennung der App in Kleinbuchstaben (`pt-br`, `zh-hans`).
- `privacy.html` entsteht nur über `python3 Tools/privacy_l10n.py bauen <Pfad zu diesem Ordner> --nur-auswahl`.

Offene Punkte in einem Entwurf werden mit `<span class="pruefen">…</span>` markiert. Vor jedem Push
muss diese Suche leer sein:

```sh
grep -n 'class="pruefen"' *.html
```

## Lokal testen

```sh
cd BaroWatch
python3 -m http.server 8000
open http://localhost:8000
```

# BaroWatch — Website

Statische Webseite für die App **BaroWatch** (App Store): Startseite, Datenschutzerklärung, Support-Kontakt, Impressum.

Gehostet via **GitHub Pages**: <https://alfhellmund.github.io/BaroWatch/>

## Seiten

Jeder Seitentyp hat eine deutsche Quelle (von Hand gepflegt), Sprachfassungen (erzeugt) und eine Sprachauswahl (erzeugt, nicht von Hand):

| Typ | Quelle | Sprachfassungen | Sprachauswahl |
|---|---|---|---|
| Startseite | `index-de.html` | `index-<code>.html`, beginnend mit `index-en.html` | `index.html` |
| Support | `support-de.html` | `support-<code>.html`, beginnend mit `support-en.html` | `support.html` (mit Kontaktadresse) |
| Datenschutzerklärung | `privacy-de.html` | `privacy-<code>.html`, beginnend mit `privacy-en.html` | `privacy.html` |
| Impressum | `impressum.html` (maßgeblich) | `impressum-en.html` (Übersetzung) | keine |

- `style.css` — Gestaltung, dazu die Klasse `.pruefen` für Entwurfsmarker; erzeugt aus `Tools/website_style.css` im Repository der Starpath-App (nicht von Hand ändern)

## Änderungen an den Seiten

**Gestaltung:** Die eine Quelle von `style.css` ist `Tools/website_style.css` im Repository der Starpath-App, gemeinsam mit der Website von Starpath. Geändert wird nur die Quelle; jedes `bauen` (auch `--nur-auswahl`) schreibt `style.css` daraus, und `pruefen` meldet jede Abweichung (Prüfpunkt r).

**Datenschutzerklärung:** Ändert die App Berechtigungen, Speicherung oder Datenwege, wird `privacy-de.html` gegen den Code nachgezogen und Fassung und Stand im Kopf
der Seite und in der Fassungszeile erhöht.

Ablauf bei einer neuen Fassung einer deutschen Quelle (Werkzeug `Tools/website_l10n.py` im Repository der Starpath-App):

1. Die deutsche Quelle ändern (bei `privacy-de.html` zusätzlich Fassung und Stand erhöhen).
2. `python3 Tools/website_l10n.py pruefen <Pfad zu diesem Ordner>` meldet je Datei und Typ die veralteten Einheiten (`data-quelle` weicht vom aktuellen deutschen Text ab).
3. Veraltete Einheiten nachübersetzen, die Seiten mit `bauen` neu erzeugen (`bauen` baut alle Typen einer Sprache und schreibt die Auswahlen neu), bis `pruefen` Exit 0 liefert und 0 veraltet meldet.
4. Marker-Suche (unten) leer, dann Push.

Regeln:

- Die Dateinamen `index-<code>.html`, `support-<code>.html` und `privacy-<code>.html` werden nicht umbenannt (App Store Connect: Privacy Policy URL und Support URL sind nicht editierbar). `<code>` ist die Sprachkennung der App in Kleinbuchstaben (`pt-br`, `zh-hans`). Dasselbe gilt für `index.html`, `support.html`, `privacy.html`, `impressum.html` und `impressum-en.html`.
- Die Sprachauswahlen (`index.html`, `support.html`, `privacy.html`) entstehen nur über `python3 Tools/website_l10n.py bauen <Pfad zu diesem Ordner> --nur-auswahl`.
- Das Impressum gibt es deutsch (`impressum.html`, maßgeblich) und englisch (`impressum-en.html`); die Fußzeilen der übrigen Sprachen verweisen auf die englische Fassung mit dem Zusatz „(English)“.

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

# Rettet die Umwelt 🦦

Ein Browser-Spiel von Josephine: Schwimm mit Carl dem Otter durchs Meer und
fange alle Öl-Kleckse mit dem Kescher.

## Spielen

`Spiel/index.html` im Browser öffnen. Das Spiel funktioniert auch per Doppelklick
ohne Server. Am Computer: Pfeiltasten oder WASD zum Schwimmen, Leertaste zum Fangen.
Am Tablet: Richtungsknöpfe gedrückt halten und mit dem anderen Finger „Fangen“ antippen.
Hoch- und Querformat werden unterstützt.

Zum Ausprobieren auf einem Tablet im selben WLAN im Hauptordner starten:

```sh
python3 -m http.server 8000
```

Dann am Tablet `http://<IP-des-Computers>:8000/` öffnen.

## Bereitstellen

Die Website besteht aus statischen Dateien; es gibt keinen Build und keine
Paketinstallation. Für GitHub Pages ist `main` als Quelle vorgesehen, Ordner `/`
(Repository-Wurzel). Die Änderungen werden nach dem Zusammenführen in `main`
über den bestehenden Pages-Deploy veröffentlicht.

Für andere statische Webserver diese Dateien und Ordner zusammen bereitstellen:

- `index.html` und `Spiel/`
- `favicon.svg`, `favicon.ico` und `apple-touch-icon.png`
- `site.webmanifest` und `icons/`

Alle Installationspfade sind relativ und funktionieren auch unter einem Unterpfad
wie `/rettet-die-umwelt/`. Die weiteren Ordner enthalten Entwürfe und Prototypen.

## Auf dem Tablet zum Home-Bildschirm hinzufügen

Die bereitgestellte HTTPS-Seite öffnen. Auf dem iPad in Safari „Teilen“ →
„Zum Home-Bildschirm“ wählen; auf Android die entsprechende Option im Browsermenü.
Das Otter-Symbol wird als App-Symbol verwendet. Zum erneuten Laden der installierten
Website wird weiterhin eine Internetverbindung benötigt.

Die Symbolvorlage ist `favicon.svg`; PNG-Dateien gibt es in 180, 192 und 512 Pixeln,
das ICO enthält 16, 32 und 48 Pixel. Das SVG ist zusätzlich in den beiden
Einstiegsseiten eingebettet, damit das Tab-Symbol auch in der einzelnen Spieldatei
verfügbar bleibt. Änderungen an der Vorlage auch in diese Kopien und Exporte übernehmen.

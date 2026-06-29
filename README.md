# ESP32‑S3 N16R8 — Interaktiver Board‑Guide 🔬

> Der vollständige Guide zum **ESP32‑S3 N16R8** (16 MB Flash · 8 MB **Octal**‑PSRAM · WiFi + BLE 5 · 2× USB‑C) — mit **echten Messwerten**, interaktivem Pinout, Forensik (echt oder Klon?) und Firmware‑Benchmarks. Alle Werte real am Board erhoben, keine Datenblatt‑Abschriften.

<p align="left">
  <img alt="HTML5" src="https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white">
  <img alt="JavaScript" src="https://img.shields.io/badge/Vanilla_JS-F7DF1E?logo=javascript&logoColor=black">
  <img alt="Zero Dependencies" src="https://img.shields.io/badge/Dependencies-0-success">
  <img alt="Hardware" src="https://img.shields.io/badge/Hardware-ESP32--S3_N16R8-FF5B4A">
  <img alt="Sprache" src="https://img.shields.io/badge/Sprache-Deutsch-blue">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-green">
</p>

**🔗 Live‑Demo:** <https://esp32-s3.mculab.workers.dev/>

---

## 📖 Worum geht es?

Dieses Repository enthält eine **statische, interaktive Single‑Page‑Website**, die ein ESP32‑S3‑Entwicklungsboard der Variante **N16R8** komplett dokumentiert — vom Pinout bis zur forensischen Echtheitsprüfung. Das konkret untersuchte Board ist ein **DevKitC‑1‑v1.0‑Klon** (häufig als *YD‑ESP32‑S3* gehandelt) mit echtem Espressif‑Silizium, zwei USB‑C‑Buchsen und einer **CH343**‑UART‑Brücke statt des originalen CP2102N.

Der Clou: **Sämtliche Angaben sind real am Chip gemessen** — per `esptool`, MicroPython und eigenen ESP‑IDF‑Firmwares — und nicht aus Datenblättern übernommen.

## ✨ Features

- 📊 **Interaktives Pinout** — alle GPIOs nach Funktion filterbar (frei · tabu · Strapping · Spezial · ADC · Touch), dynamisch aus JS‑Daten gerendert
- 🔬 **Forensik & Tiefenprüfung (T1–T9)** — Beweise, dass PSRAM (8 MB Octal) und Flash (16 MB) *wirklich* verbaut sind: MAC‑OUI, Voll‑Aliasing‑Test, JEDEC‑ID u. v. m.
- ⚡ **Live‑Benchmarks** — direkter Drei‑Wege‑Vergleich **MicroPython** vs. **ESP‑IDF** vs. **idf‑max** (Maximal‑Firmware) für USB, GPIO, Flash, WLAN, BLE, Dual‑Core
- 🐍 **Kopierfertige Code‑Rezepte** — getestete MicroPython‑Snippets (RGB‑LED, WiFi, PSRAM‑Test, ADC, Touch, Deep‑Sleep …) mit Copy‑Button
- 🧰 **Werkzeuge & Methoden** — jedes verwendete Tool (esptool, mpremote, pyserial, bleak, ESP‑IDF …) mit Installations‑ und Praxis‑Hinweisen, auch für Einsteiger
- 🩹 **Troubleshooting & Silizium‑Errata** — die typischen Stolperfallen (nur ~300 KB RAM, ttyACM statt ttyUSB, GPIO‑33–37‑Crash) inklusive Lösung
- 🌙 **Dark/Light‑Mode** mit `localStorage`‑Persistenz, kein Flash beim Laden
- 📱 **Responsive** mit mobiler Navigation und Reveal‑Animationen via `IntersectionObserver`
- 🌐 **Zweisprachig angelegt** (DE primär, EN über `index-en.html`) mit `hreflang`‑Verlinkung

## 🧱 Tech‑Stack

| Bereich        | Umsetzung                                                        |
| -------------- | --------------------------------------------------------------- |
| Markup         | Einzelne `index.html` (HTML5, semantisch)                       |
| Styling        | Inline‑CSS mit Custom Properties (Theme‑Tokens, Grid, Gradients)|
| Interaktivität | **Vanilla JavaScript** — keine Frameworks, keine Build‑Tools    |
| Schriften      | Google Fonts (Inter, JetBrains Mono) mit `preconnect`           |
| Hosting        | Cloudflare Workers (alternativ GitHub Pages / Netlify)          |

> **Keine Abhängigkeiten, kein Build‑Schritt.** Die Seite ist reines statisches HTML/CSS/JS und läuft auf jedem beliebigen Webserver.

## 📂 Projektstruktur

```text
.
├── index.html              # Deutsche Hauptseite  ✅ enthalten
├── index-en.html           # Englische Version    ⬅ noch ergänzen (verlinkt)
├── og-image.png            # Social-Vorschau 1200×630 px  ⬅ noch ergänzen
├── firmware/
│   └── idf-max-merged.bin  # Fertiges Flash-Image (Download)  ⬅ noch ergänzen
├── README.md
└── LICENSE
```

<details>
<summary>Optionale Quellcode‑Ordner (falls du die Firmware/Skripte mitveröffentlichst)</summary>

```text
├── idf-max/          # Quellcode der Maximal-Firmware (USB/WiFi/BLE/Selftest/Soak)
├── idf-throughput/   # Durchsatz-Messfirmware (ESP-IDF)
├── idf-ble/          # BLE-Notify-Messfirmware (NimBLE)
└── Tiefenpruefung/   # Forensik-Skripte zur Test-Serie T1–T9
```
</details>

> ⚠️ **Hinweis:** In der `index.html` werden `index-en.html`, `og-image.png` und `firmware/idf-max-merged.bin` referenziert. Lade diese Dateien mit ins Repo, sonst zeigen die Sprachumschaltung, die Link‑Vorschau in Foren/Messengern und der Firmware‑Download ins Leere.

## 🚀 Lokal ansehen

Da es sich um statisches HTML handelt, genügt ein simpler lokaler Webserver:

```bash
# Python (überall vorinstalliert)
python3 -m http.server 8000
# danach im Browser öffnen: http://localhost:8000

# Alternativen
npx serve .
php -S localhost:8000
```

Ein einfacher Doppelklick auf `index.html` funktioniert ebenfalls — über `http://` werden Google Fonts und relative Pfade aber zuverlässiger geladen.

## 🌍 Deployment

**Cloudflare Workers / Pages** (wie in der Live‑Demo)
- Repository mit Cloudflare verbinden, Build‑Command leer lassen, Output‑Verzeichnis auf den Repo‑Root setzen.

**GitHub Pages**
1. Repo → **Settings → Pages**
2. *Source:* „Deploy from a branch", Branch `main`, Ordner `/ (root)`
3. Speichern — die Seite ist nach kurzer Zeit unter `https://<user>.github.io/<repo>/` erreichbar.

> Bei GitHub Pages im Unterpfad ggf. die absoluten `canonical`/`og:url`‑URLs in der `index.html` an die neue Domain anpassen.

## 🔍 SEO & Auffindbarkeit

Die Seite ist von Grund auf für Suchmaschinen und Link‑Vorschauen ausgelegt:

- Strukturierte Daten als JSON‑LD (`TechArticle` + `FAQPage`)
- Open‑Graph‑ und Twitter‑Card‑Meta‑Tags
- `canonical` + `hreflang` (de / en / x‑default)
- Verifizierungs‑Tags für Google Search Console und Bing Webmaster Tools

> Diese Verifizierungs‑Meta‑Tags (`google-site-verification`, `msvalidate.01`) sind kontogebunden. Ersetze sie durch deine eigenen, falls du die Property neu anlegst — oder belasse sie, wenn die Property bereits bestätigt ist.

## 🔌 Über das Board (Kurzfassung)

| Merkmal        | Wert                                                       |
| -------------- | ---------------------------------------------------------- |
| SoC            | ESP32‑S3 (QFN56), 2× Xtensa LX7 + LP‑Core, bis 240 MHz     |
| Flash          | 16 MB (Quad)                                               |
| PSRAM          | **8 MB Octal (OPI)** — benötigt die `SPIRAM_OCT`‑Firmware  |
| Funk           | WiFi 802.11 b/g/n (2,4 GHz) · Bluetooth 5 LE               |
| USB            | 2× USB‑C: „COM" (CH343 → UART) + nativer USB des SoC       |
| Gerätename     | `/dev/ttyACM0` (CH343 nutzt `cdc_acm`, **nicht** ttyUSB!)  |
| Layout         | DevKitC‑1 **v1.0**‑Klon (RGB‑LED auf GPIO48)               |

**Die drei häufigsten Stolperfallen** (ausführlich auf der Seite):
1. Nur ~300 KB RAM? → Es wurde die Nicht‑Octal‑Firmware geflasht. Die **`SPIRAM_OCT`‑Variante** verwenden.
2. Kein `/dev/ttyUSB0`? → Richtig so, das Board meldet sich als **`/dev/ttyACM0`**.
3. Absturz bei **GPIO 33–37**? → Diese Pins gehören fest der Octal‑PSRAM. Stattdessen 1–18, 21, 38–42, 47 nutzen.

## 🤝 Mitwirken

Korrekturen, ergänzende Messwerte oder eine Übersetzung sind willkommen — gerne als Issue oder Pull Request. Da alle Angaben am realen Board verifiziert wurden, bitte neue Messwerte mit der jeweiligen Methode/Firmware dokumentieren.

## ☕ Support

In diesem Guide steckt viel Mess‑ und Detailarbeit. Wenn er dir geholfen hat, freut sich der Autor über einen Kaffee — ganz ohne Druck.

## 📄 Lizenz

Dieses Projekt ist **dual lizenziert**:

- **Code** (HTML, CSS, JavaScript) — [MIT‑Lizenz](LICENSE)
- **Inhalte** (Texte, Mess‑Ergebnisse, Tabellen, Grafiken) — [CC BY 4.0](LICENSE-CONTENT)

Du darfst die Inhalte teilen und weiterverarbeiten, auch kommerziell, solange du den Urheber nennst und auf die Lizenz verlinkst. Vorgeschlagene Namensnennung:

> „ESP32‑S3 N16R8 Board Guide" von Chris, lizenziert unter CC BY 4.0. Quelle: <https://esp32-s3.mculab.workers.dev/>

## 👤 Autor

**Chris** · Board‑Guide & sämtliche Messungen

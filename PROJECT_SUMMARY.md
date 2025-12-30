# Projekt-Zusammenfassung – ESP32-C6 TFT 1.91" mit ESPHome

Diese Notiz fasst die wichtigsten Schritte, Entscheidungen und Stolpersteine
für ein ESPHome-Projekt mit einem ESP32-C6 und 1.91" ST7789 TFT zusammen.
Gedacht als **Gedächtnisstütze für Folgeprojekte**.

---

## Ziel
- ESP32-C6 mit 1.91" TFT (170×320, ST7789)
- ESPHome **über Python/venv** (ohne Home-Assistant-Add-on)
- USB-Flash + OTA
- Veröffentlichung auf GitHub inkl. Screenshot & Release

---

## Entwicklungsumgebung
- OS: Windows 11
- Python mit virtual environment (`venv`)
- ESPHome via `pip`
- Editor: VS Code
- Flash per USB (COM-Port)

### Setup
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install esphome
```

---

## ESPHome Grundkonfiguration
- **Framework:** ESP-IDF (zwingend für ESP32-C6)
- **Board:** `esp32-c6-devkitc-1`
  - Fallback bei Problemen: `esp32-c6-devkitm-1`

---

## TFT / SPI Pinout (bewährt)

| Funktion | GPIO |
|--------|------|
| CS     | GPIO7 |
| DC     | GPIO6 |
| RST    | GPIO14 |
| SCLK   | GPIO5 |
| MOSI   | GPIO4 |
| Backlight | GPIO15 |

- Display-Treiber: `st7789v`
- Auflösung: `170 x 320`
- Rotation: `90`

---

## Projektdateien

```
├─ esp32c6-tft191.yaml
├─ secrets.yaml          (lokal, niemals committen)
├─ secrets.yaml.example
├─ .gitignore
├─ README.md
└─ images/
   └─ display.jpg
```

---

## Flash & Test
```powershell
esphome run esp32c6-tft191.yaml --device COMx
```

Falls Flash nicht startet:
- **BOOT gedrückt halten**
- **RESET kurz drücken**
- BOOT loslassen, sobald Flash beginnt

---

## GitHub Workflow
- `.gitignore` früh anlegen
- Secrets niemals committen
- Screenshot im README einbinden
- Release mit Tag `v1.0.0`

---

## Lessons Learned
- ESP32-C6 → **immer ESP-IDF**
- Secret-Namen müssen exakt übereinstimmen
- Erst Backlight testen, dann Display

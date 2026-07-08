# PAL/NTSC Region Support

Sodium64 unterstützt jetzt die Umschaltung zwischen PAL- und NTSC-Video-Systemen über das Menü.

## Verwendung

1. Drücke **START** während ein Spiel läuft, um das Einstellungsmenü zu öffnen
2. Navigiere zu **REGION** (mit Pfeiltasten nach oben/unten)
3. Wähle zwischen:
   - **NTSC** (60 Hz, 262 Zeilen) - Standard für Nordamerika/Japan
   - **PAL** (50 Hz, 312 Zeilen) - Standard für Europa/Australien

## Technische Details

### NTSC (National Television System Committee)
- **Bildfrequenz**: 60 Hz
- **Zeilen pro Frame**: 262
- **Auflösung**: 256×224 Pixel (aktiv)

### PAL (Phase Alternating Line)
- **Bildfrequenz**: 50 Hz
- **Zeilen pro Frame**: 312
- **Auflösung**: 256×239 Pixel (aktiv)

## VI-Register (Video Interface)

Die folgenden N64-VI-Register werden basierend auf der Region konfiguriert:

| Register | NTSC | PAL |
|----------|------|-----|
| VI_V_SYNC | 0x20D | 0x271 |
| VI_H_SYNC | 0xC15 | 0xC48 |
| VI_V_VIDEO | 0x2501FF | 0x2402OF |

## Implementierung

- **menu.S**: Menü-Option "REGION" mit NTSC/PAL-Auswahl
- **main.S**: Dynamische VI-Konfiguration beim Start basierend auf `vi_region`
- **Speicherung**: Die Einstellung wird in `vi_region` gespeichert und bleibt bis zur Änderung bestehen

## Kompatibilität

- PAL-ROMs sollten mit PAL-Einstellung laufen
- NTSC-ROMs sollten mit NTSC-Einstellung laufen
- Manche Spiele funktionieren möglicherweise mit beiden Einstellungen


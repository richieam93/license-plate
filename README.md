# PlateVision Add-on for Home Assistant

A powerful, AI-powered license plate and vehicle recognition system built for Home Assistant.

## Features
- ✅ Real-time license plate detection using YOLOv8 + EasyOCR
- ✅ REST API for HA integration (`/api/latest/plate`, `/api/stream/feed`, etc.)
- ✅ Live MJPEG stream (`/api/stream/feed`)
- ✅ Web UI with dashboard, history, settings, RTSP config
- ✅ Persistent storage via `/data/`
- ✅ Configurable via HA UI (RTSP URL, language, intervals, etc.)
- ✅ Fully compatible with Raspberry Pi, Intel, AMD

## Installation
1. In HA: **Einstellungen → System → Add-on Store → ⋮ → „Neuer Add-on-Store“**
2. Füge hinzu: `https://github.com/yourusername/platevision-addon`
3. Suche nach „PlateVision“ → Installieren → Konfigurieren → Starten
4. Öffne unter: `http://[HA_IP]:5000`

## Configuration
| Option | Description |
|--------|-------------|
| `rtsp_url` | RTSP stream URL (e.g., `rtsp://user:pass@ip:554/stream`) |
| `language` | OCR language (`deu`, `eng`, etc.) |
| `detection_interval` | Detection frequency in seconds |
| `enable_stream` | Enable live MJPEG stream |
| `upload_images` | Save detected plates |
| `upload_vehicles` | Save detected vehicles |

## Home Assistant Integration

### Sensors (REST)
```yaml
sensor:
  - platform: rest
    name: "Letztes Kennzeichen"
    resource: http://[HA_IP]:5000/api/latest/plate
    value_template: "{{ value_json.plate_text }}"
    scan_interval: 10
    json_attributes:
      - confidence
      - vehicle_type
      - vehicle_color
      - timestamp
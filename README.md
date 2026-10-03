# esphome-media-page

A ready-made media player page for ESPHome + LVGL (480x320 landscape):
cover art, title/artist, progress, prev/play/next, volume slider.

## Requirements
- ESPHome >= 2025.9, ESP-IDF, PSRAM
- `lvgl` configured in your project, display 480x320 (e.g. rotated 320x480 panel)
- Home Assistant API with "Allow the device to perform Home Assistant actions" enabled

## Usage

```yaml
substitutions:
  mp_entity: media_player.your_player          # your entity
  mp_ha_url: "http://homeassistant.local:8123"

packages:
  media_page:
    url: https://github.com/YOUR_USER/esphome-media-page
    ref: v0.1.0
    files: [packages/media_page.yaml]
    refresh: 1d
```

Open the page from your own UI:

```yaml
on_click:
  - lvgl.page.show: media_page
```

## Substitutions
| Name | Default | Description |
|---|---|---|
| `mp_entity` | `media_player.example` | Media player entity |
| `mp_ha_url` | `http://homeassistant.local:8123` | HA base URL (no trailing slash), used for cover art |
| `mp_page_id` | `media_page` | Page id |
| `mp_back_page` | `main_page` | Page to open with the back button |
| `mp_art_format` | `JPEG` | `JPEG` or `PNG` |
| `mp_text_idle` | `Nothing playing` | Idle title |
| `mp_icon_font_file` | MDI from GitHub | Path/URL to materialdesignicons-webfont.ttf |
| `mp_accent`, `mp_bg`, `mp_card`, ... | see file | Colors |

## Notes
- Package pages can end up first in `lvgl.pages`; add `lvgl.page.show: main_page` in `esphome.on_boot`.
- All labels set their own font, so a global LVGL label theme will not break the page.
- Cover art uses ESPHome `online_image`: progressive JPEG is not supported, and format must match the source.

## License
MIT

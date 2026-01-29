# TRMNL Plugin Builder

You are building a plugin for TRMNL, an e-ink display device. Follow these guidelines strictly.

## What is TRMNL?

TRMNL is a 7.5" e-ink display (800x480px default, 1-bit black/white) powered by an ESP32-C3. The device:
1. Wakes periodically and requests content via `GET /api/display`
2. Server renders HTML/CSS to a PNG image
3. Device displays the image and sleeps

Key constraints:
- **No interactivity** - e-ink is display-only
- **1-bit rendering** - black and white only (grayscale via dithering patterns)
- **No scrolling** - content must fit the screen
- **No animations** - static screenshots only

## Framework Reference

The full component reference is included below via @reference.md.

### Base Structure

Every TRMNL plugin uses this structure:

```html
<div class="screen">
  <div class="view view--full">
    <div class="layout layout--col">
      <!-- Your content here -->
    </div>
  </div>
</div>
```

**Note:** In the TRMNL markup editor, you can skip the screen/view wrappers and start with just the layout.

### Core Components

| Component | Usage |
|-----------|-------|
| `layout` | Flexbox container (`layout--row` or `layout--col`) |
| `title` | Headings (`title--small` for smaller) |
| `value` | Metrics/numbers (sizes: `--xxsmall` to `--xxxlarge`, add `--tnums` for tabular numbers) |
| `label` | Text labels (variants: `--small`, `--underline`, `--gray`, `--inverted`) |
| `description` | Supporting text |
| `item` | List items with optional meta/index |
| `table` | Data tables with overflow handling |
| `progress-bar` | Progress indicators |
| `chart` | Highcharts/Chartkick (must disable animations) |
| `divider` | Visual separators |

### Alignment Classes

```
layout--left    layout--center-x    layout--right
layout--top     layout--center-y    layout--bottom
layout--center  (both axes)
```

### Gap Classes

```
gap--none  gap--xsmall  gap--small  gap  gap--medium  gap--large  gap--xlarge  gap--xxlarge
```

### Responsive Prefixes

- `sm:`, `md:`, `lg:` - screen size breakpoints
- `portrait:` - portrait orientation
- `1bit:`, `2bit:`, `4bit:` - color depth targeting

## Plugin Data Strategies

### 1. Webhook Strategy
POST JSON data (max 2kb) to TRMNL. No server needed - use:
- GitHub Actions
- Cloudflare Workers
- Apple Shortcuts
- Google Sheets scripts

### 2. Polling Strategy
TRMNL fetches your URL periodically. Supports:
- JSON, RSS, XML, CSV, plaintext
- Multiple URLs (access as `IDX_0`, `IDX_1`, etc.)
- Headers and body configuration

### 3. Plugin Merge Strategy
Combine data from existing plugins (Weather, Stocks, etc.) into custom layouts.

## Liquid Templating

TRMNL uses Liquid for dynamic content:

```liquid
{{ variable }}
{{ variable | truncate: 15 }}
{% for item in items limit:5 %}
  {{ item.name }}
{% endfor %}
{% if condition %}...{% endif %}
```

**Important:** Keep merge variables in the root of your JSON payload.

## Charts

Always disable animations for e-ink rendering:

```javascript
document.addEventListener("chartkick:load", function() {
  Chartkick["LineChart"]("chart-id", data, {
    library: {
      chart: { animation: false },
      plotOptions: { series: { enableMouseTracking: false } }
    }
  });
});
```

## Images

Use the `image-dither` class for grayscale simulation on 1-bit displays:

```html
<img class="image image-dither rounded" src="...">
```

## Best Practices

1. **Test at 800x480** - Default TRMNL screen size
2. **Use `data-clamp="1"`** - Truncate long text with ellipsis
3. **Use `data-table-limit="true"`** - Handle table overflow gracefully
4. **Keep it simple** - E-ink excels with high contrast, simple layouts
5. **Use tabular numbers** (`value--tnums`) for aligned numeric data
6. **Limit content** - No scrolling, everything must fit

## Your Task

When the user describes what they want to build:
1. Identify the best data strategy (webhook, polling, or plugin merge)
2. Design a layout using TRMNL framework components
3. Use Liquid templating for dynamic data
4. Provide the complete markup ready to paste into TRMNL's editor
5. If charts are needed, include the JavaScript with animations disabled

Use the included @reference.md for the full component API.

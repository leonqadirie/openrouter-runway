# TRMNL Framework Reference

Complete component and utility reference for building TRMNL plugins.

## How TRMNL Works

TRMNL is an e-ink display device (ESP32-C3 with 7.5" EPD screen, 800x480px):
1. Device wakes periodically and requests content via `GET /api/display`
2. Server renders HTML/CSS to a PNG image
3. Device displays the image and sleeps

## Screen (Root Container)

```html
<div class="screen">
  <div class="view view--full">
    <div class="layout">
      <!-- Content -->
    </div>
  </div>
</div>
```

### Modifiers

| Class | Description |
|-------|-------------|
| `screen--portrait` | Portrait orientation (480x800) |
| `screen--og` | Original TRMNL device |
| `screen--v2` | TRMNL V2 device |
| `screen--1bit` | 1-bit color depth |
| `screen--4bit` | 4-bit color depth |
| `screen--no-bleed` | Remove padding, edge-to-edge |
| `screen--dark-mode` | Inverted colors |
| `screen--backdrop` | Patterned/gray background |

### CSS Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `--screen-w` | 800px | Screen width |
| `--screen-h` | 480px | Screen height |
| `--full-w` | calc(--screen-w - --gap × 2) | Usable width |
| `--full-h` | calc(--screen-h - --gap × 2) | Usable height |
| `--ui-scale` | 1 | UI scaling factor |
| `--color-depth` | 1 | Display bit depth |

## View (Container Sizes)

```html
<div class="view view--full">...</div>
<div class="view view--half_horizontal">...</div>
<div class="view view--half_vertical">...</div>
<div class="view view--quadrant">...</div>
```

Note: When building in the markup editor, Layout alone is sufficient without View wrapper.

## Layout (Flexbox Container)

### Row Layout (Horizontal)
```html
<div class="layout layout--row">
  <div>Item 1</div>
  <div>Item 2</div>
</div>
```

### Column Layout (Vertical)
```html
<div class="layout layout--col">
  <div>Item 1</div>
  <div>Item 2</div>
</div>
```

### Alignment Modifiers

**Horizontal:**
- `layout--left` - Align left
- `layout--center-x` - Center horizontally
- `layout--right` - Align right

**Vertical:**
- `layout--top` - Align top
- `layout--center-y` - Center vertically
- `layout--bottom` - Align bottom

**Both:**
- `layout--center` - Center on both axes

### Stretch Modifiers

**Container:**
- `layout--stretch` - Stretch children both ways
- `layout--stretch-x` - Horizontal only
- `layout--stretch-y` - Vertical only

**Child elements:**
- `stretch-x` - Stretch this element horizontally
- `stretch-y` - Stretch this element vertically

## Columns

```html
<div class="columns">
  <div class="column">Column 1</div>
  <div class="column">Column 2</div>
  <div class="column">Column 3</div>
</div>
```

Flexible - add as many columns as needed.

## Title Bar

```html
<div class="title_bar">
  <img class="image" src="/images/plugins/icon.svg" alt="Icon">
  <span class="title">Plugin Title</span>
  <span class="instance">Subtitle</span>
</div>
```

## Typography

### Title

```html
<span class="title">Base Title</span>
<span class="title title--small">Small Title</span>

<!-- Responsive -->
<span class="title title--small lg:title--base">Adaptive</span>
```

### Value (Metrics/Numbers)

```html
<span class="value value--xxsmall">XXSmall</span>
<span class="value value--xsmall">XSmall</span>
<span class="value value--small">Small</span>
<span class="value">Base</span>
<span class="value value--large">Large</span>
<span class="value value--xlarge">XLarge</span>
<span class="value value--xxlarge">XXLarge</span>
<span class="value value--xxxlarge">XXXLarge</span>

<!-- Tabular numbers (fixed-width digits) -->
<span class="value value--large value--tnums">48,206.62</span>

<!-- Responsive -->
<span class="value value--small md:value--large lg:value--xlarge">Adaptive</span>

<!-- Orientation -->
<span class="value value--large portrait:value--small">Portrait-aware</span>
```

### Label

```html
<span class="label">Base Label</span>
<span class="label label--small">Small Label</span>
<span class="label label--underline">Underlined</span>
<span class="label label--small label--underline">Small Underlined</span>
```

### Description

```html
<span class="description">Supporting descriptive text</span>
```

### Divider

```html
<div class="divider"></div>
```

## Item Component

### Simple Item
```html
<div class="item">
  <div class="content">
    <span class="title title--small">Item Title</span>
    <span class="description">Description text</span>
    <div class="flex gap--small">
      <span class="label label--small label--underline">Tag 1</span>
      <span class="label label--small label--underline">Tag 2</span>
    </div>
  </div>
</div>
```

### Item with Index
```html
<div class="item">
  <div class="meta">
    <span class="index">1</span>
  </div>
  <div class="content">
    <span class="title title--small">Item Title</span>
    <span class="description">Description</span>
  </div>
</div>
```

### Item with Meta (no index)
```html
<div class="item">
  <div class="meta"></div>
  <div class="content">
    <span class="title title--small">Title</span>
  </div>
</div>
```

### Emphasis Levels
```html
<div class="item item--emphasis-1">...</div>  <!-- Default -->
<div class="item item--emphasis-2">...</div>  <!-- Medium -->
<div class="item item--emphasis-3">...</div>  <!-- High -->
```

## Table

```html
<table class="table" data-table-limit="true">
  <thead>
    <tr>
      <th><span class="title">Header 1</span></th>
      <th><span class="title">Header 2</span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><span class="label">Cell 1</span></td>
      <td><span class="value value--small value--tnums">123</span></td>
    </tr>
  </tbody>
</table>
```

### Size Variants

| Class | Description |
|-------|-------------|
| `table` / `table--base` | Standard spacing |
| `table--large` | Increased row height |
| `table--small` / `table--condensed` | Compact |
| `table--xsmall` | Most condensed |

### Indexed Table
```html
<table class="table table--indexed">
  <tbody>
    <tr>
      <td><span class="meta"><span class="index">1</span></span></td>
      <td><span class="label">Content</span></td>
    </tr>
  </tbody>
</table>
```

### Data Attributes
- `data-table-limit="true"` - Enable overflow handling ("and X more")
- `data-clamp="1"` - Single-line truncation with ellipsis

## Progress Components

### Progress Bar
```html
<div class="progress-bar progress-bar--large">
  <div class="content">
    <span class="label">Progress Label</span>
    <span class="value value--xxsmall">75%</span>
  </div>
  <div class="track">
    <div class="fill" style="width: 75%"></div>
  </div>
</div>
```

**Sizes:** `progress-bar--small`, `progress-bar--base`, `progress-bar--large`

**Emphasis:** `progress-bar--emphasis-2`, `progress-bar--emphasis-3`

### Progress Dots
```html
<div class="progress-dots progress-dots--large">
  <div class="track">
    <div class="dot dot--filled"></div>  <!-- Completed -->
    <div class="dot dot--filled"></div>
    <div class="dot dot--current"></div>  <!-- Active -->
    <div class="dot"></div>               <!-- Upcoming -->
    <div class="dot"></div>
  </div>
</div>
```

**Sizes:** `progress-dots--small`, `progress-dots--base`, `progress-dots--large`

## Charts

Charts use Highcharts/Chartkick. **Critical: disable animations.**

### Line Chart
```html
<div id="chart-line" class="w--full"></div>
<script>
document.addEventListener("chartkick:load", function() {
  Chartkick["LineChart"]("chart-line", [
    ["2024-06-09", 975],
    ["2024-06-10", 840],
    ["2024-06-11", 1200]
  ], {
    library: {
      chart: { animation: false },
      plotOptions: {
        series: {
          lineWidth: 4,
          enableMouseTracking: false
        }
      }
    }
  });
});
</script>
```

### Bar Chart
```html
<div id="chart-bar" class="w--full"></div>
<script>
document.addEventListener("chartkick:load", function() {
  Chartkick["BarChart"]("chart-bar", [
    ["Jan", 5883],
    ["Feb", 5260],
    ["Mar", 4912]
  ], {
    library: {
      chart: { animation: false, type: "column" },
      plotOptions: { series: { enableMouseTracking: false } }
    }
  });
});
</script>
```

### Multi-Series Line Chart
```javascript
[
  { name: "This Year", data: [...] },
  { name: "Last Year", data: [...] }
]
```

Second series uses pattern fill:
```javascript
color: {
  pattern: {
    image: "https://trmnl.com/images/grayscale/gray-5.png",
    width: 12,
    height: 12
  }
}
```

### Chart Settings

| Setting | Value | Purpose |
|---------|-------|---------|
| `animation` | `false` | Required for screenshot rendering |
| `enableMouseTracking` | `false` | E-ink has no interaction |
| `lineWidth` | `4` | Visible on 1-bit displays |
| `fontSize` | `"16px"` | Readable on small screens |

### Grayscale Patterns
- `https://trmnl.com/images/grayscale/gray-2.png`
- `https://trmnl.com/images/grayscale/gray-3.png`
- `https://trmnl.com/images/grayscale/gray-5.png`
- `https://trmnl.com/images/grayscale/gray-7.png`

## Utility Classes

### Flexbox
- `flex` - Display flex
- `flex-row` - Row direction
- `flex-col` - Column direction
- `items-center` - Align items center
- `justify-center` - Justify center
- `justify-between` - Space between

### Gap
- `gap--small`
- `gap--medium`
- `gap--large`
- `gap--space-between`

### Spacing
- `p--small`, `p--medium`, `p--large` (padding)
- `m--small`, `m--medium`, `m--large` (margin)

### Sizing
- `w--full`, `w--half`
- `h--full`, `h--half`

### Text
- `text--center`
- `text--left`
- `text--right`

### Responsive Prefixes
- `sm:` - Small breakpoint
- `md:` - Medium breakpoint
- `lg:` - Large breakpoint
- `portrait:` - Portrait orientation

## Liquid Templating

TRMNL uses Liquid syntax for dynamic data.

### Variables
```html
<span class="value">{{ metrics.total }}</span>
<span class="label">{{ metrics.label }}</span>
```

### Loops
```html
{% for item in items %}
<div class="item">
  <div class="content">
    <span class="title title--small">{{ item.title }}</span>
    <span class="description">{{ item.description }}</span>
  </div>
</div>
{% endfor %}
```

### Loop with Limit
```html
{% for item in items limit:5 %}
  ...
{% endfor %}
```

### Loop Index
```html
{% for item in items %}
  <span class="index">{{ forloop.index }}</span>
{% endfor %}
```

### Conditionals
```html
{% if show_chart %}
  <!-- Chart markup -->
{% endif %}

{% if value > 100 %}
  <span class="label">High</span>
{% else %}
  <span class="label">Normal</span>
{% endif %}
```

## Private API

For custom data sources:

**Endpoint:** `GET /api/display`

**Headers:**
- `ID`: Device MAC address (format: `XX:XX:XX:XX`)
- `Access-Token`: Your API key

**Response:**
```json
{
  "image_url": "https://s3.amazonaws.com/...",
  "filename": "2024-01-15-plugin-T10:30:00",
  "update_firmware": false
}
```

## Plugin Merge Strategy

Access data from other plugins without displaying them:

1. Install and hide a plugin (Weather, Stocks, etc.)
2. Create a Private Plugin with "Plugin Merge" strategy
3. Reference data via `{{ plugin_keyname_setting_id.field }}`

## Example Layouts

### Metric Dashboard
```html
<div class="layout layout--col layout--center gap--large">
  <div class="columns">
    <div class="column">
      <span class="value value--xxxlarge value--tnums">{{ primary }}</span>
      <span class="label">{{ primary_label }}</span>
    </div>
    <div class="column">
      <span class="value value--xlarge value--tnums">{{ secondary }}</span>
      <span class="label">{{ secondary_label }}</span>
    </div>
  </div>
  <div class="progress-bar progress-bar--large">
    <div class="content">
      <span class="label">Progress</span>
      <span class="value value--xxsmall">{{ progress }}%</span>
    </div>
    <div class="track">
      <div class="fill" style="width: {{ progress }}%"></div>
    </div>
  </div>
</div>
```

### List/Feed
```html
<div class="layout layout--col layout--top gap--small">
  {% for item in items limit:5 %}
  <div class="item">
    <div class="meta">
      <span class="index">{{ forloop.index }}</span>
    </div>
    <div class="content">
      <span class="title title--small">{{ item.title }}</span>
      <span class="description" data-clamp="1">{{ item.description }}</span>
      <div class="flex gap--small">
        <span class="label label--small label--underline">{{ item.source }}</span>
        <span class="label label--small">{{ item.time }}</span>
      </div>
    </div>
  </div>
  {% endfor %}
</div>
```

### Data Table
```html
<div class="layout layout--col stretch-y">
  <table class="table table--small" data-table-limit="true">
    <thead>
      <tr>
        <th><span class="title">Name</span></th>
        <th><span class="title">Value</span></th>
        <th><span class="title">Change</span></th>
      </tr>
    </thead>
    <tbody>
      {% for row in data %}
      <tr>
        <td><span class="label">{{ row.name }}</span></td>
        <td><span class="value value--small value--tnums">{{ row.value }}</span></td>
        <td><span class="label">{{ row.change }}</span></td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>
```

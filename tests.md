# CustomRangeSlider Test Cases

This document contains 5 test cases demonstrating the CustomRangeSlider component's capabilities. Each test case includes complete JSON configurations for all component properties.

---

## Test Case 1: Website Traffic Analysis with Logarithmic Scale

**Description**: Web analytics showing page views with extreme value differences (viral content vs. niche pages). Uses logarithmic scale to visualize data spanning 6 orders of magnitude.

**Use Case**: Analyzing website content performance where popular pages get millions of views while niche pages get only dozens. Linear scale would make small values invisible.

```json
{
  "min": 0,
  "max": 10000,
  "defaultStart": 100,
  "defaultEnd": 5000,
  "step": 50,
  "label": "Daily Page Views Range",
  "formatterFunction": "v => v >= 1000000 ? `${(v/1000000).toFixed(1)}M` : v >= 1000 ? `${(v/1000).toFixed(1)}K` : v.toString()",
  "primaryColor": "#10b981",
  "primaryLightColor": "#34d399",
  "secondaryColor": "#d1d5db",
  "backgroundColor": "#f9fafb",
  "textColor": "#111827",
  "tooltip": "#111827",
  "histogramScale": "logarithmic",
  "showNegativeValues": false,
  "distributionData": [
    { "bucket_index": 0, "bucket_min": 0, "bucket_max": 100, "count": 12500 },
    { "bucket_index": 1, "bucket_min": 100, "bucket_max": 500, "count": 8200 },
    { "bucket_index": 2, "bucket_min": 500, "bucket_max": 1000, "count": 3400 },
    { "bucket_index": 3, "bucket_min": 1000, "bucket_max": 2000, "count": 1850 },
    { "bucket_index": 4, "bucket_min": 2000, "bucket_max": 3000, "count": 920 },
    { "bucket_index": 5, "bucket_min": 3000, "bucket_max": 4000, "count": 450 },
    { "bucket_index": 6, "bucket_min": 4000, "bucket_max": 5000, "count": 280 },
    { "bucket_index": 7, "bucket_min": 5000, "bucket_max": 6000, "count": 125 },
    { "bucket_index": 8, "bucket_min": 6000, "bucket_max": 7500, "count": 45 },
    { "bucket_index": 9, "bucket_min": 7500, "bucket_max": 10000, "count": 18 }
  ]
}
```

**Note**: Try switching `histogramScale` between `"linear"`, `"logarithmic"`, and `"sqrt"` to see how the visualization changes. With linear scale, the high-count buckets dominate and low-count buckets become invisible. With logarithmic scale, all data is visible and comparable.

---

## Test Case 2: Unix Timestamp to Human-Readable Date Range

**Description**: Server log analysis with Unix timestamps converted to readable dates with dynamic formatting based on time scale.

**Use Case**: Analyzing server events across different time periods where raw timestamps need intelligent conversion (shows seconds for recent events, minutes/hours for older ones).

```json
{
  "min": 1704067200,
  "max": 1704153600,
  "defaultStart": 1704088800,
  "defaultEnd": 1704132000,
  "step": 3600,
  "label": "Event Time Range (Jan 2024)",
  "formatterFunction": "v => { const d = new Date(v * 1000); const now = new Date(1704110400 * 1000); const diff = Math.abs(now - d) / 1000; if (diff < 3600) return d.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', second: '2-digit' }); if (diff < 86400) return d.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' }) + ' (' + Math.floor(diff/3600) + 'h ago)'; return d.toLocaleDateString('en-US', { month: 'short', day: 'numeric' }) + ' ' + d.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' }); }",
  "primaryColor": "#3b82f6",
  "primaryLightColor": "#60a5fa",
  "secondaryColor": "#cbd5e1",
  "backgroundColor": "#f8fafc",
  "textColor": "#0f172a",
  "tooltip": "#0f172a",
  "histogramScale": "linear",
  "showNegativeValues": false,
  "distributionData": [
    { "bucket_index": 0, "bucket_min": 1704067200, "bucket_max": 1704074400, "count": 145 },
    { "bucket_index": 1, "bucket_min": 1704074400, "bucket_max": 1704081600, "count": 320 },
    { "bucket_index": 2, "bucket_min": 1704081600, "bucket_max": 1704088800, "count": 580 },
    { "bucket_index": 3, "bucket_min": 1704088800, "bucket_max": 1704096000, "count": 1250 },
    { "bucket_index": 4, "bucket_min": 1704096000, "bucket_max": 1704103200, "count": 1890 },
    { "bucket_index": 5, "bucket_min": 1704103200, "bucket_max": 1704110400, "count": 2150 },
    { "bucket_index": 6, "bucket_min": 1704110400, "bucket_max": 1704117600, "count": 1980 },
    { "bucket_index": 7, "bucket_min": 1704117600, "bucket_max": 1704124800, "count": 1420 },
    { "bucket_index": 8, "bucket_min": 1704124800, "bucket_max": 1704132000, "count": 890 },
    { "bucket_index": 9, "bucket_min": 1704132000, "bucket_max": 1704139200, "count": 520 },
    { "bucket_index": 10, "bucket_min": 1704139200, "bucket_max": 1704146400, "count": 280 },
    { "bucket_index": 11, "bucket_min": 1704146400, "bucket_max": 1704153600, "count": 175 }
  ]
}
```

---

## Test Case 3: Monthly Profit/Loss Analysis (Zero-Crossing Range)

**Description**: Financial analysis showing monthly profit/loss across product lines. Demonstrates negative values, zero-crossing, and context-aware formatting with color indicators.

**Use Case**: Filtering underperforming products (losses) vs. profitable ones. Tests component's ability to handle negative numbers and format them with appropriate symbols and context.

```json
{
  "min": -50000,
  "max": 100000,
  "defaultStart": -20000,
  "defaultEnd": 50000,
  "step": 5000,
  "label": "Monthly Profit/Loss Range",
  "formatterFunction": "v => { const abs = Math.abs(v); const formatted = abs >= 1000 ? `$${(abs/1000).toFixed(0)}K` : `$${abs}`; return v < 0 ? `-${formatted}` : v === 0 ? '$0' : `+${formatted}`; }",
  "primaryColor": "#ef4444",
  "primaryLightColor": "#f87171",
  "secondaryColor": "#e5e7eb",
  "backgroundColor": "#fef2f2",
  "textColor": "#7f1d1d",
  "tooltip": "#7f1d1d",
  "histogramScale": "linear",
  "showNegativeValues": true,
  "distributionData": [
    { "bucket_index": 0, "bucket_min": -50000, "bucket_max": -40000, "count": 8 },
    { "bucket_index": 1, "bucket_min": -40000, "bucket_max": -30000, "count": 15 },
    { "bucket_index": 2, "bucket_min": -30000, "bucket_max": -20000, "count": 28 },
    { "bucket_index": 3, "bucket_min": -20000, "bucket_max": -10000, "count": 45 },
    { "bucket_index": 4, "bucket_min": -10000, "bucket_max": 0, "count": 62 },
    { "bucket_index": 5, "bucket_min": 0, "bucket_max": 10000, "count": 85 },
    { "bucket_index": 6, "bucket_min": 10000, "bucket_max": 20000, "count": 120 },
    { "bucket_index": 7, "bucket_min": 20000, "bucket_max": 30000, "count": 95 },
    { "bucket_index": 8, "bucket_min": 30000, "bucket_max": 40000, "count": 78 },
    { "bucket_index": 9, "bucket_min": 40000, "bucket_max": 50000, "count": 58 },
    { "bucket_index": 10, "bucket_min": 50000, "bucket_max": 60000, "count": 42 },
    { "bucket_index": 11, "bucket_min": 60000, "bucket_max": 70000, "count": 28 },
    { "bucket_index": 12, "bucket_min": 70000, "bucket_max": 80000, "count": 18 },
    { "bucket_index": 13, "bucket_min": 80000, "bucket_max": 90000, "count": 10 },
    { "bucket_index": 14, "bucket_min": 90000, "bucket_max": 100000, "count": 5 }
  ]
}
```

**Note**:
- **`showNegativeValues: true`** raises the histogram baseline to show negative values below the x-axis and positive values above it, with a subtle zero line indicator
- The formatter intelligently handles negative values with `-` prefix, positive values with `+` prefix, and zero as `$0`
- Values are converted to K format for readability (e.g., `-$50K`, `+$100K`)
- Negative value bars have rounded corners at the bottom, positive bars at the top

---

## Test Case 4: File Size Filter

**Description**: File size filtering with MB formatting and bimodal distribution (small files and large files).

**Use Case**: Cloud storage or file management system filtering.

```json
{
  "min": 0,
  "max": 500,
  "defaultStart": 0,
  "defaultEnd": 100,
  "step": 5,
  "label": "File Size",
  "formatterFunction": "v => `${v} MB`",
  "primaryColor": "#8b5cf6",
  "primaryLightColor": "#a78bfa",
  "secondaryColor": "#d4d4d8",
  "backgroundColor": "#faf5ff",
  "textColor": "#4c1d95",
  "tooltip": "#4c1d95",
  "histogramScale": "sqrt",
  "showNegativeValues": false,
  "distributionData": [
    { "bucket_index": 0, "bucket_min": 0, "bucket_max": 25, "count": 1850 },
    { "bucket_index": 1, "bucket_min": 25, "bucket_max": 50, "count": 1200 },
    { "bucket_index": 2, "bucket_min": 50, "bucket_max": 75, "count": 680 },
    { "bucket_index": 3, "bucket_min": 75, "bucket_max": 100, "count": 420 },
    { "bucket_index": 4, "bucket_min": 100, "bucket_max": 125, "count": 280 },
    { "bucket_index": 5, "bucket_min": 125, "bucket_max": 150, "count": 180 },
    { "bucket_index": 6, "bucket_min": 150, "bucket_max": 200, "count": 120 },
    { "bucket_index": 7, "bucket_min": 200, "bucket_max": 250, "count": 95 },
    { "bucket_index": 8, "bucket_min": 250, "bucket_max": 300, "count": 150 },
    { "bucket_index": 9, "bucket_min": 300, "bucket_max": 350, "count": 380 },
    { "bucket_index": 10, "bucket_min": 350, "bucket_max": 400, "count": 520 },
    { "bucket_index": 11, "bucket_min": 400, "bucket_max": 450, "count": 280 },
    { "bucket_index": 12, "bucket_min": 450, "bucket_max": 500, "count": 145 }
  ]
}
```

---

## Test Case 5: Maximum Values Stress Test (Edge Case)

**Description**: Edge case where all histogram bars are at maximum height to test rendering and scaling.

**Use Case**: Testing component behavior with extremely high, uniform distribution values.

```json
{
  "min": 0,
  "max": 100,
  "defaultStart": 30,
  "defaultEnd": 70,
  "step": 1,
  "label": "Uniform Maximum Distribution",
  "formatterFunction": "v => `${v}%`",
  "primaryColor": "#f59e0b",
  "primaryLightColor": "#fbbf24",
  "secondaryColor": "#d6d3d1",
  "backgroundColor": "#fffbeb",
  "textColor": "#78350f",
  "tooltip": "#78350f",
  "histogramScale": "linear",
  "showNegativeValues": false,
  "distributionData": [
    { "bucket_index": 0, "bucket_min": 0, "bucket_max": 10, "count": 999999 },
    { "bucket_index": 1, "bucket_min": 10, "bucket_max": 20, "count": 999999 },
    { "bucket_index": 2, "bucket_min": 20, "bucket_max": 30, "count": 999999 },
    { "bucket_index": 3, "bucket_min": 30, "bucket_max": 40, "count": 999999 },
    { "bucket_index": 4, "bucket_min": 40, "bucket_max": 50, "count": 999999 },
    { "bucket_index": 5, "bucket_min": 50, "bucket_max": 60, "count": 999999 },
    { "bucket_index": 6, "bucket_min": 60, "bucket_max": 70, "count": 999999 },
    { "bucket_index": 7, "bucket_min": 70, "bucket_max": 80, "count": 999999 },
    { "bucket_index": 8, "bucket_min": 80, "bucket_max": 90, "count": 999999 },
    { "bucket_index": 9, "bucket_min": 90, "bucket_max": 100, "count": 999999 }
  ]
}
```

---

## How to Use These Test Cases

1. **In Retool**: Copy the entire JSON object for a test case
2. **Configure Component**: Paste each property value into the corresponding field in the CustomRangeSlider component inspector
3. **Test Interactions**:
   - Drag the range slider handles
   - Click on histogram bars to select ranges
   - Observe the formatted values in the display
   - Monitor the `selectedRange` output and `rangeChanged` event

## Key Features Demonstrated

- **Test Case 1**: Logarithmic histogram scale for extreme value ranges (12,500 to 18 page views) + intelligent number formatting (K/M suffixes)
- **Test Case 2**: Complex formatter with conditional logic converting Unix timestamps to context-aware date/time formats
- **Test Case 3**: **Zero-crossing range** (negative to positive values) with contextual formatting (+/- prefixes) for financial profit/loss data
- **Test Case 4**: Square root histogram scale for bimodal distribution (two peaks) + file size use case
- **Test Case 5**: Edge case testing with maximum uniform values across all bars (linear scale)

## Expected Behavior

- Histogram bars should render according to the selected `histogramScale`:
  - **linear**: Bars proportional to raw count values
  - **logarithmic**: Bars use log10 scale, making small values visible alongside large ones
  - **sqrt**: Bars use square root scale, a middle ground between linear and logarithmic
- Component correctly handles **negative values** and zero-crossing ranges (min < 0, max > 0)
- **`showNegativeValues`** option (only available when min or max is negative):
  - When **enabled**: Histogram shows a zero baseline with negative values extending downward and positive values upward
  - When **disabled**: Standard histogram with all bars extending upward from the bottom
  - A subtle horizontal line marks the zero position when enabled
- Selected range should highlight the appropriate bars in the primary color
- Unselected bars should display in the secondary color (at 30% opacity)
- Formatted values should appear correctly in the display and tooltips
- Formatter functions can add context-aware prefixes/suffixes (e.g., +/- for profit/loss, K/M for large numbers)
- Clicking histogram bars should update the slider range
- Dragging across histogram bars should select a multi-bucket range
- Tooltips should always remain visible (smart positioning at edges and tall bars)
- The component should remain responsive at all sizes

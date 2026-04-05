# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single self-contained HTML travel itinerary in Traditional Chinese for a 5-day Tokyo + Mt. Fuji trip. No build step — open `東京五天四夜旅遊計畫.html` directly in any browser.

## File

`東京五天四夜旅遊計畫.html` — the only file to edit (~1,360 lines of HTML/CSS/JS).

## Architecture

### CSS Variables
Defined at the top of `<style>`:
- `--red` `--navy` `--gold` `--sakura` `--sakura-dark` `--light-bg` — full theme color set

### Tab Navigation
- Buttons: `.tab-btn[data-tab="overview|day1|day2|day3|day4|day5"]`
- JS function `switchTab(tab)` drives all show/hide logic
- **Overview mode**: shows `#overview-panel` + `#overview-extras`, hides all `.day-card`
- **Day mode**: hides `#overview-panel` + `#overview-extras`, shows only `.day-card[data-day="dayN"]`

### Panel Structure
| Element | Visible when |
|---------|-------------|
| `#overview-panel` | Overview tab — contains 5 `.summary-card[data-goto="dayN"]` (clicking jumps to that day) |
| `#overview-extras` | Overview tab — budget estimates + packing checklist |
| `.day-card[data-day="day1"…"day5"]` | Respective day tab (all `display:none` by default) |
| `#itinerary-title` | Any day tab |

### Day Card Structure
```
.day-card[data-day]
  .day-header
    .day-num
    .day-info  (h2, .day-date, .day-tags > .tag)
  .day-body
    .transport-card          ← Day 1 only (airport transport options)
    .car-banner              ← Day 2 only (rental car route info)
    .timeline
      .tl-item
        .tl-left  (.tl-time + .tl-line)
        .tl-content  (.tl-title > .tl-icon + text, .tl-desc, .tl-tips > .tip-chip)
    .tips-box                ← Day 2 only (driving notes)
```

### Tip Chip Variants
- `.tip-chip` — blue, general info
- `.tip-chip.warn` — yellow, warning
- `.tip-chip.green` — green, positive/free

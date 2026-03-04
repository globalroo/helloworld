# Technical Debt & Future Improvements

Outstanding items from the multi-agent ideation session (Claude, Gemini, Codex) that were not implemented in the initial build.

## Visual Richness

- **Circuit SVG silhouettes**: Lightweight track layout diagrams per race, lazy-loaded in the expanded panel. Requires sourcing or creating SVG assets keyed by slug.
- **High-contrast theme**: Add a third theme option beyond dark/light for users who need maximum contrast.
- **IntersectionObserver for card entrance**: Currently using CSS animation-delay stagger. IO-based approach would avoid animating off-screen cards on load.
- **Active round pulse animation**: Subtle pulsing glow on the "next race" card in the list to draw attention.

## Data & Content

- **Weather integration**: Use Open-Meteo API (free, no key) to show forecast for races within 7 days, and historical climate averages for races further out. Lat/long data is already in the JSON.
- **Mini-map previews**: Use lat/long to embed static map tiles (Mapbox/Stadia free tier) or "Open in Maps" deep links in the expanded panel.
- **Wikipedia links**: Generate Wikipedia circuit links alongside the existing F1.com links.
- **Lap record data**: Add `lapRecord` field to JSON and display in circuit facts.
- **Race direction**: Add clockwise/anti-clockwise to circuit metadata.
- **Travel context**: Show distance from previous round and days between races (Codex idea).
- **Night race / high-altitude chips**: Contextual badges for races with notable characteristics (Singapore night race, Mexico City altitude).

## UX & Interaction

- **Full-season ICS export**: Single button to download all 24 races as one ICS file (currently only per-race export).
- **Expand All / Collapse All toggle**: Button to expand or collapse every card at once.
- **Continent/region filter**: Add filter buttons for Europe, Americas, Asia-Pacific, Middle East (derivable from a static lookup).
- **Month filter**: Filter races by month.
- **Sticky header on mobile**: Minimize the header to a compact bar when scrolling down.
- **Bottom-sheet details on mobile**: Swipe-up sheet for session details instead of inline expand on small screens.
- **Compact timeline view**: Alternative view mode showing races on a horizontal or vertical timeline.
- **Persist expanded card state**: Save which cards are open in localStorage so they survive page refresh.
- **URL hash for expanded cards**: Encode expanded rounds in the URL for deep-linking (currently only filter/search are in URL params).

## Accessibility

- **Roving tabindex / arrow-key navigation**: For power users, arrow keys to move between cards without tabbing through each one.
- **Additional skip links**: "Skip to next race", "Skip to filters" in addition to the existing "Skip to race calendar".
- **Focus management on expand**: Move focus into the expanded panel content when a card is opened.
- **UTC time toggle**: Add a third time display mode (UTC) alongside local and track time.

## Architecture

- **ES module split**: Break the monolithic `<script>` into separate modules (calendar.js, countdown.js, ics.js, theme.js, prefs.js). No bundler needed — `<script type="module">` works natively.
- **HTML `<template>` for cards**: Replace innerHTML string building with `<template>` cloning for better DOM safety and performance (Gemini suggestion).
- **Progressive enhancement**: Render a static HTML race list in the document, then enhance with JS. Currently the page is blank without JS beyond the noscript message.
- **Lazy-load flag images**: Flags already have `loading="lazy"` but could benefit from explicit dimension placeholders to prevent CLS.
- **Telemetry hooks**: Optional lightweight analytics for filter usage, ICS downloads, and theme preference (Codex suggestion).
- **i18n / multilingual support**: The `localeKey` field exists but is unused. Design a translation layer using it for future language support.

## Testing

- **Screen reader testing**: Manual testing with VoiceOver, NVDA, and JAWS to verify the full keyboard + SR flow.
- **ICS import testing**: Verify generated .ics files import correctly into Apple Calendar, Google Calendar, and Outlook.
- **Offline/PWA testing**: Verify service worker behavior with query-param URLs, cache invalidation on schedule changes, and installability across browsers.
- **Cross-browser flag rendering**: Verify flagcdn.com images load correctly; add fallback for failed loads.

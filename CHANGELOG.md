# Changelog

## [0.1.0.0] — 2026-05-16

### Added
- Full site scaffold: login gate, hero, adventure card grid, calendar, overlay modal, footer
- Password-gated entry with `localStorage` persistence (`rt_auth`)
- Adventure card grid with 5 cards: Grand Canyon, Bloodroot Ultra 50K, UTMB CCC, San Juans, Switzerland
- Interactive adventure calendar with month navigation and event pills
- Overlay modal with adventure details and CTA links (aria-accessible)
- Scroll-reveal animations via IntersectionObserver
- Complete design system in `assets/css/main.css` with CSS custom properties
- ADVENTURES array with 2026 trips for calendar (Bloodroot, Grand Canyon, Loon Camp, Mt. Washington, Chamonix, Italy, Dolomites)
- Logo-only top nav (no dropdown)
- Full archive section above calendar

### Fixed
- Nav dropdown z-index and positioning issues
- Calendar event pill colors
- Overlay aria-hidden attribute on initial load
- Grand Canyon card stats, link, and hero image
- UTMB CCC card title, description, hero image, and story link

### Infrastructure
- gstack skill routing added to CLAUDE.md
- `.claude/settings.json` with gstack pre-tool hook

---
name: iphone-olympian-layout
description: Organize a connected iPhone home screen with Unjiggle using the user's 12 Olympian emoji+English folder taxonomy, including checks for newly added apps, preserved Dock order, and recoverable backups before writes.
---

# iPhone Olympian Layout

Use this skill when the user asks to inspect, validate, restore, or rewrite their iPhone home screen layout with Unjiggle and the established Greek Olympian folder system.

The user's current intent is:

- Keep the Home Screen to one page when feasible.
- Do not change the Dock apps or their order.
- Preserve existing widgets on the first Home Screen page.
- Use Unjiggle for iPhone layout reads/writes.
- Before every layout write, create a recoverable verified backup.
- After every write, perform a read-only verification of page count, app count, folder names, and Dock bundle-id order.

## Folder Taxonomy

Use these exact folder names and their classification logic unless the user explicitly changes the theme:

| Folder | Classification Logic |
|---|---|
| `⚡ Zeus` | System authority, Apple/account management, settings, passwords, app installation/testing, Apple support, account web clips. |
| `👑 Hera` | Finance, banking, payment, wallet, tax, government services, public funds, civic service apps. |
| `🔱 Poseidon` | Maps, navigation, transit, ride-hailing, rail/metro, travel booking, hotels, compass. |
| `🌾 Demeter` | Shopping, local life, food, daily consumer supply, basic health/fitness maintenance. |
| `🦉 Athena` | Work, AI, knowledge production, notes, mail, calendar, documents, project/task management, CAD, productivity tools. |
| `☀️ Apollo` | Music, video, reading, podcasts/audio, media libraries, content consumption, creative/media playback. |
| `🌙 Artemis` | Camera, photos, weather, measuring/sensing, Find My, outdoor awareness, car/road context, alerts. |
| `⚔️ Ares` | Competition, job hunting, exams, civil-service prep, interview/quiz/drill apps, goal-combat workflows. |
| `💘 Aphrodite` | Social expression, relationship/contact surfaces, social content communities, short-video/social feeds, events/tickets. |
| `🔥 Hephaestus` | Utilities, hardware companion apps, maintenance, clocks/timers, watch, contacts, voice memos, practical small tools. |
| `🪽 Hermes` | Communication, networking, proxy/VPN/routing tools, browsers, carrier apps, SMS filtering, lightweight information streams. |
| `🏛️ Hestia` | Home, smart home, appliances, pets/home devices, residence services, household energy/utilities. |

## Decision Rules for New Apps

When the user has added new apps and asks for a check:

1. Read the current layout and list any apps not covered by the existing classification script or taxonomy.
2. Compare the user's current placement against the taxonomy above.
3. Preserve sensible user placement unless it conflicts with the folder's main job.
4. Move only the apps whose primary use clearly fits a different Olympian domain.
5. Treat web clips as classifiable items, not disposable extras. Preserve them unless the user asks to remove them.
6. Treat widgets as top-level widgets and preserve them; do not place widget bundle identifiers inside folders.

Fast boundary checks:

- "Creates work output" goes to `🦉 Athena`.
- Money, tax, official services go to `👑 Hera`.
- Network, proxy, browser, carrier, SMS tools go to `🪽 Hermes`.
- Home, appliance, household utility, pets, power service go to `🏛️ Hestia`.
- Transport, routes, trips, hotels go to `🔱 Poseidon`.
- Passive media or reading goes to `☀️ Apollo`.
- Social/community posting and relationship surfaces go to `💘 Aphrodite`.
- Shopping, dining, local consumption, marketplace apps go to `🌾 Demeter`.
- Job/exam/prep competition tools go to `⚔️ Ares`.
- Apple/system control goes to `⚡ Zeus`; small Apple utilities go to `🔥 Hephaestus` unless they are clearly work, media, or system-control tools.

## Unjiggle Workflow

If editing the device layout:

- Use the Python environment where `unjiggle` is installed; install it only if necessary and permitted.
- Use read-only scans first to inspect the current layout and identify new apps.
- Build a deterministic layout plan that assigns every non-Dock app or web clip exactly once.
- Exclude Dock bundle IDs from all folders so Dock order is preserved.
- Preserve first-page widgets by copying raw widget items into the target page.
- For iOS 26 folder raw objects, use `{"displayName": name, "iconLists": pages, "listType": "folder"}`; `listType: "folder"` is required.
- Use 9 icons per internal folder page unless there is a strong reason to do otherwise.
- Run a static coverage check before writing: no duplicates, no missing visible non-Dock apps, no extra nonexistent bundle IDs.
- Call Unjiggle's verified backup before `write_layout`.
- After write, read the layout again and verify:
  - page count is still 1 when that was requested,
  - total app count matches the pre-write layout,
  - Dock bundle-id sequence equals the backup's Dock bundle-id sequence,
  - folder names match the planned Olympian list.

## Reporting

When finished, tell the user:

- what was changed or moved,
- the final page/app count,
- whether Dock order was verified unchanged,
- the exact backup path.

Keep the explanation concise, but mention any judgment calls for newly classified apps.

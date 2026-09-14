---
name: iphone-olympian-layout
description: Organize or audit a connected iPhone Home Screen with Unjiggle using the user's 12 Olympian folder taxonomy.
---

# iPhone Olympian Layout

Use this skill when the user asks to inspect, validate, restore, or rewrite their iPhone Home Screen using the established Olympian-themed folders.

Core invariants:

- Preserve the Dock apps and their order.
- Preserve existing first-page widgets unless the user asks otherwise.
- Keep the Home Screen to one page when feasible.
- Create a recoverable backup before any Unjiggle write.
- After any write, verify page count, app count, folder names, and Dock bundle-id order.

Read only what the task needs:

- For classification questions or newly installed apps, read [references/taxonomy.md](references/taxonomy.md).
- For device reads/writes, backups, or restore work, read [references/unjiggle-workflow.md](references/unjiggle-workflow.md).

When the user only asks where one app belongs, answer from the taxonomy without touching the device. When the user asks to reorganize the phone, inspect the current layout first, make the smallest taxonomy-consistent changes, and report any judgment calls.

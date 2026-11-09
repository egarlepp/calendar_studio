# Security Policy

## Scope

SE Calendar Studio is a static, client-side page. It has no backend, stores data only in the visiting browser's `localStorage`, and loads Tailwind CSS and Google Fonts from public CDNs.

Relevant issues include:

- Script injection through roster, activity, or domain fields, or through crafted `localStorage` content.
- Malformed or injectable `.ics` output (for example, property or parameter injection through names or subjects).
- Anything that causes generated data to leave the browser.

## Reporting a vulnerability

Please do not open a public issue for security problems. Use GitHub's private reporting instead: **Security → Report a vulnerability** on this repository.

Include steps to reproduce, the browser and version, and the impact you observed. You can expect an acknowledgement within 7 days.

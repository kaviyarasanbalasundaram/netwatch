# 🛰 NetWatch – Simple Network Monitor

A lightweight, single-file web dashboard that displays network connection logs and flags simple suspicious activity. No install, no dependencies, no backend – just open `index.html`.

> All data is **synthetic sample data**. Nothing connects to or scans any real network.

## Features
- Connection log: time, device/host name, source IP, destination, port, protocol, status
- Summary cards and an alerts panel
- Search and filter (flagged only / failed only)
- Live feed simulation and one-click data regeneration
- Adjustable detection thresholds

## Detections
| Rule | Description |
|------|-------------|
| Repeated failed connections | One IP with many failed/blocked attempts (e.g. SSH brute force) |
| Too many connection attempts | One IP with an unusually high connection count |
| Port scan | One IP touching many distinct ports |
| Repeated connections | Same source → destination:port seen many times |
| Unknown IP | Source/destination outside the allow-list |
| Unusual / risky ports | Ports outside the common set (22, 53, 80, 123, 443, 993); 23, 445, 3389, 4444, 6667, 31337 marked risky |

## Run it
Open `index.html` in any browser, or visit the live demo (see below).

## Live demo (GitHub Pages)
Repo **Settings → Pages → Deploy from branch → `main` / root**. Your site will be at `(https://kaviyarasanbalasundaram.github.io/netwatch/)`.

## Use your own logs
Replace `generate()` in `index.html` with a parser that fills the `events` array with records shaped like:
```js
{ t: 1700000000000, src: "203.0.113.45", dst: "192.168.1.30", port: 22, proto: "TCP", status: "FAILED" }
```
Only analyze networks you own or are authorized to monitor.

## How it works
`analyze()` groups events by source IP and by source→destination:port, applies the threshold rules, and returns alerts plus per-row flags that `render()` displays.

## License
MIT

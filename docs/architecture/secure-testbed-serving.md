# Secure Testbed Serving

Camera and microphone access must be treated as secure-context-only from the first web repos. Desktop `localhost` is special, but plain `http://<tailscale-ip>:<port>` on a phone should be expected to fail for `navigator.mediaDevices.getUserMedia()`.

## Required Posture

Standard package testbeds and assembly demos need an HTTPS path before live camera validation is considered ready. Plain HTTP is acceptable only for local non-camera scenes and must visibly report that camera features are disabled when the page is not a secure context.

Camera testbed pages should check:

- `window.isSecureContext`
- `navigator.mediaDevices`
- `navigator.permissions` where supported

Unsupported or failed states should render through normal `aero-*` UI components and include copyable context such as origin, browser family when detectable, scene name, and version label.

## Tailscale And Local HTTPS

Preferred same-day phone path:

- Use `tailscale cert` for a MagicDNS host.
- Serve the repo-local testbed over HTTPS.
- Print the HTTPS phone URL, local URL, and QR code.

Fallback path:

- Use a local development CA such as `mkcert`.
- Document per-device trust setup for phones and remote PCs.

Desktop fallback:

- Use `https://localhost:<port>` for secure local debugging.
- Use `http://localhost:<port>` only where browser secure-context exceptions apply.

Last-resort insecure-origin browser flags may be documented for diagnostics, but must not become the default validation path.

## `testbed:serve` Expectations

Browser-visible standard package repos should expose a root `npm run testbed:serve` command when they own scenes, camera/CV checks, renderer output, or Web Components.

Expected behavior:

- Serve `.testbed/demo/` and `.testbed/scenes/` as appropriate for the repo.
- Use public package imports through `.testbed/node_modules/@aerobeat/web-<domain>`.
- Accept explicit host, port, certificate, and key inputs.
- Default to `127.0.0.1`; require an explicit Tailscale host or IP for remote exposure.
- Fail loudly if HTTPS is requested but certificate/key files are missing.
- Never silently fall back from HTTPS to HTTP.
- Display package name, version, git commit, dirty marker, build timestamp, served origin, scene name, browser user agent, viewport, DPR, selected camera constraints, and active debug-data state.
- Add cache-busting tokens to scene links and make the loaded token visible.


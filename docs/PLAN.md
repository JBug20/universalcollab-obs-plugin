# Plugin plan

The plugin is written in C++ against libobs and the OBS frontend API, with Qt for its panels. The recommended starting point is the official `obsproject/obs-plugintemplate`, which already has CMake and GitHub Actions builds for Windows, macOS and Linux.

## Milestones

| # | What | Needs a relay? |
|---|---|---|
| P0 | An empty "UniversalCollab" panel that loads in OBS on Windows and Linux | No |
| P1 | Layout tools: right-click move-to-corner, a 2×2 four-person split, snapping presets (works offline) | No |
| P2 | Join a relay: nickname/address/password, collab requests, approved friend feeds as sources | Yes |
| P3 | Twitch and YouTube accounts: sign-in (PKCE with a local callback), broadcast setup/metadata | No |
| P4 | Chat and moderation panel | No |

## Reference code (desktop app repo)

- The relay protocol and portal API: `universalcollab-relay/src/`
- Platform flows: `universalcollab-app/DesktopSource/platforms/service.cjs` and `studio.cjs`
- The token vault idea: `DesktopSource/platforms/vault.cjs`. The plugin will use the OS keychain directly (Windows Credential Manager, or libsecret on Linux).

## Rules

- Use only the existing Twitch/YouTube app registrations. Never bake secrets, tokens or stream keys into a release.
- Never pass sign-in tokens to browser sources or browser panels.
- Don't use the OBS name or logo as this plugin's branding.

## Open decision (before P2)

Where should the shared collab video be composed? Either the relay keeps composing it (as it does today), or the host's OBS composes it from friend feeds pulled from the relay. The second option makes text, image and browser sources work natively.

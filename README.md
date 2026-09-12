<div align="center">

# Cairn

**A Microsoft Rewards automation tool, rewritten from nothing in Go.**

One binary. No Electron, no Node, no browser driver, no telemetry you did not agree to.

[![License](https://img.shields.io/badge/License-AGPL--3.0-4968f2)](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/blob/main/LICENSE)
[![Source](https://img.shields.io/badge/Source%20%26%20issues-GitLab-fc6d26?logo=gitlab&logoColor=white)](https://gitlab.com/light_lgt/microsoft-rewards-bot)
[![Discord](https://img.shields.io/badge/Discord-join-5865F2?logo=discord&logoColor=white)](https://discord.gg/yPm6SHeSNF)

**This page is a mirror. The code, the issues and the releases all live on [GitLab](https://gitlab.com/light_lgt/microsoft-rewards-bot).**

</div>

> ### ⏳ There is no release yet — the links below will not work until there is.
> The engine works and has earned points on a real account. But the bar this project set for
> itself — **fourteen consecutive clean days, unattended** — has not been met, so nothing has been
> published. This page is here so that the day it is, you have one click and not a treasure hunt.
> Follow the project on [GitLab](https://gitlab.com/light_lgt/microsoft-rewards-bot) to know when.

---

## Download

Every link points straight at the file. No repository to browse, no version number to look up —
these always resolve to the **newest release**.

| | Download | Also available |
|---|---|---|
| 🪟 **Windows** (Intel/AMD) | **[cairn_windows_amd64.zip](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/cairn_windows_amd64.zip)** | [ARM64](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/cairn_windows_arm64.zip) |
| 🐧 **Linux** (Intel/AMD) | **[cairn_linux_amd64.tar.gz](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/cairn_linux_amd64.tar.gz)** | [ARM64](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/cairn_linux_arm64.tar.gz) |
| 🍎 **macOS** (Apple Silicon) | **[cairn_darwin_arm64.tar.gz](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/cairn_darwin_arm64.tar.gz)** | [Intel](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/cairn_darwin_amd64.tar.gz) |
| 🐳 **Docker** | `docker pull registry.gitlab.com/light_lgt/microsoft-rewards-bot/cairn:latest` | [compose file](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/blob/main/docker-compose.yml) |

Unpack it and run it. There is nothing to install.

```sh
cairn setup            # an account, a real sign-in, and the telemetry question
cairn                  # the dashboard, as an application window
```

> **Windows and macOS are community beta.** They are built and cross-compiled from the same commit
> as Linux, which is the reference platform, but nobody has yet run a real account journey on
> either. If you do, an issue saying what happened is worth more than any amount of testing here.

---

## ⚠️ Check what you downloaded

**This matters more than usual.** The project this replaced was taken down for distributing opaque
executables, and a mirror on another host is exactly the place someone would try to slip you a
different file. Two minutes:

```sh
# 1. The files match the published list
sha256sum -c SHA256SUMS

# 2. The list itself was signed by the release pipeline, and by nothing else
cosign verify-blob SHA256SUMS \
  --signature SHA256SUMS.sig \
  --certificate SHA256SUMS.pem \
  --certificate-identity-regexp '^https://gitlab.com/light_lgt/microsoft-rewards-bot/' \
  --certificate-oidc-issuer https://gitlab.com
```

[SHA256SUMS](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/SHA256SUMS) ·
[.sig](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/SHA256SUMS.sig) ·
[.pem](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/SHA256SUMS.pem) ·
[SBOM](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases/permalink/latest/downloads/cairn.spdx.json)

Signing is keyless: there is no private key for anyone to lose or leak, and the identity that signed
is the release pipeline itself. Cairn also tells you — run `cairn version` and an unstamped binary
says so.

**Anything that did not come from a link on this page or from the GitLab releases page is not ours.**
No legacy executable, no older version, and nothing sent to you directly will ever be supported.

---

## What it is

A tool that works through your daily Microsoft Rewards searches and activities by driving a real
browser, slowly, the way a person would.

**The one decision everything follows from: two accounts running this software must not look alike.**
Search terms, delays, session times, task order, quiet hours, how fast a new account ramps up — all
of it is derived from a per-installation seed. A shared constant would make every user of this tool
recognisable *as a group*, which is far worse than any one account behaving imperfectly. A test
fails the build if a fixed timer appears anywhere a browser can see.

What follows from that, so nothing is a surprise:

- It drives a real browser over the DevTools Protocol. No headless mode, no API shortcut.
- It is slow on purpose, and it never runs two accounts at once.
- **It never solves a CAPTCHA.** It records the signal and stops.
- **It never redeems points.** Spending real value is permanently out of scope.
- **Your data stays on your machine.** The dashboard listens on loopback only and refuses any
  request that did not arrive over loopback.
- **Telemetry is off** until you answer the first-run notice, and off entirely if you say no.

### Honestly, what is not proven

| | |
|---|---|
| **The fourteen-day gate** | One account earning its points unattended for fourteen consecutive clean days. Not met. |
| **Windows and macOS** | They cross-compile. No real account journey has been run on either. |
| **Markets other than France** | Everything observed was observed on one French account. |
| **Safety from suspension** | Automating Microsoft Rewards may breach Microsoft's terms. That is your decision to make. |

---

## Everything else is on GitLab

This page exists to hand you a file. Nothing else here is canonical.

| | |
|---|---|
| **Source code** | [gitlab.com/light_lgt/microsoft-rewards-bot](https://gitlab.com/light_lgt/microsoft-rewards-bot) |
| **Report a bug** | [Issues](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/issues) |
| **All releases** | [Releases](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/releases) |
| **Documentation** | [docs/](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/tree/main/docs) |
| **Project status** | [STATUS.md](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/blob/main/STATUS.md) |
| **Contributing** | [CONTRIBUTING.md](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/blob/main/CONTRIBUTING.md) |
| **Security** | [SECURITY.md](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/blob/main/SECURITY.md) |
| **Privacy** | [PRIVACY.md](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/blob/main/PRIVACY.md) |

Issues and merge requests opened here are not read. Open them on GitLab, where the code is.

## Licence

[AGPL-3.0](https://gitlab.com/light_lgt/microsoft-rewards-bot/-/blob/main/LICENSE). Anyone running a
service based on Cairn has to publish their changes.

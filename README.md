# Clickjacking, Strokejacking and Keylogger Proof of Concept

![Security](https://img.shields.io/badge/Security-Clickjacking%20%26%20Strokejacking-critical?style=flat-square)
![PoC](https://img.shields.io/badge/Type-Proof%20of%20Concept-orange?style=flat-square)
![Audience](https://img.shields.io/badge/Audience-Security%20Research-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

![Clickjacking and keylogger-style strokejacking demonstration](https://i.imgur.com/xsaZgZc.png)

## Overview

This repository contains a practical proof of concept demonstrating **clickjacking**, **strokejacking**, and **keylogger-style** credential capture through user interface redressing.

Although commonly described as a keylogger, the behaviour demonstrated here relies on user interface deception rather than browser compromise or malware.

## Why This Matters

Applications that allow framing can be abused through UI redressing attacks without exploiting browser vulnerabilities or bypassing the same-origin policy.

If framing is permitted, an attacker can:

- Perform clickjacking by redirecting user clicks to unintended actions
- Capture keystrokes using deceptive overlays (strokejacking)
- Harvest credentials in a manner that appears indistinguishable from a keylogger
- Influence cursor movement and user interaction
- Abuse user trust in legitimate application interfaces

## Threat Model

An attacker hosts a malicious HTML page and embeds a target application using an iframe. Deceptive overlays are positioned above the framed application to mislead users into entering credentials or other sensitive information.

The captured keystrokes are logged by the attacker-controlled page, enabling credential harvesting that appears identical to keylogger behaviour from the victim’s perspective.

## Usage

1. Open the HTML proof of concept file locally in a browser.
2. Replace the iframe source URL with the target application.
3. Observe the framed application on the left and the keystroke log on the right.
4. Enter text into the deceptive prompt and observe real-time keystroke capture.

No web server or special tooling is required.

## Mitigation

Applications should explicitly prevent framing by implementing the following HTTP response headers:

- Content-Security-Policy: frame-ancestors 'none';
- X-Frame-Options: DENY

These controls effectively mitigate clickjacking, strokejacking, and keylogger-style UI redressing attacks.

## License

MIT License.

## Disclaimer

This proof of concept is provided for defensive security testing and educational purposes only.

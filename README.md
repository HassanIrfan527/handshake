# Handshake

A self-hosted SIP/WebRTC calling app, built from scratch to actually understand how real-time voice calling works — not just wire an API together.

## What is Handshake?

Handshake is a softphone-style calling app: browser-to-browser voice calling over WebRTC, backed by a self-hosted SIP server instead of a third-party Voice API. You register as a SIP endpoint, the signaling and call setup happen over SIP/WebSocket, and the actual audio flows peer-to-peer over WebRTC.

## Why I'm building this

I previously built a telephony project on top of Telnyx's Voice API. It stalled and I never fully understood large parts of the code, especially the frontend, which was mostly AI-generated (vibe-coded) without me actually learning what it was doing.

Rather than abandon the idea, I'm rebuilding it as my own project, for a few reasons:

- **Understand it, not just ship it.** Using a Voice API abstracts away SIP registration, RTP, and ICE/STUN/TURN negotiation — the actual mechanics of a phone call. Running my own SIP backend forces me to deal with that layer directly instead of trusting a black box.
- **It fits where I'm headed.** I'm moving toward Linux/sysadmin/DevOps work. Standing up and running my own SIP server (Asterisk/FreeSWITCH) on a VPS is real infrastructure experience, not just app-layer code.
- **Zero cost.** Self-hosting removes the need for a paid Voice API entirely — I'm the phone company.

## Concepts and technologies

**Backend**

- **Laravel** — core app: users, call history, auth, SIP account provisioning
- **Livewire / Alpine.js** — for the UI, at least for v1, so I'm not learning a new framework (React) at the same time as SIP/WebRTC

**Real-time / calling layer**

- **WebRTC** — peer-to-peer audio between browsers
- **WebSockets** — signaling channel between client and SIP server (SIP over WS)
- **SIP** — call setup/teardown, registration, protocol-level understanding (this is the core learning goal of the project)
- **Asterisk or FreeSWITCH** — self-hosted SIP backend, no third-party Voice API

**Infrastructure**

- Self-hosted on a personal VPS
- Tailscale for private networking between services

## Future plans

- [ ] Get a basic two-browser-tab call working end to end (SIP registration + WebRTC audio)
- [ ] Move the SIP backend onto a proper VPS instead of local dev
- [ ] Add call history, contacts, basic account management in Laravel
- [ ] Once the SIP/WebRTC fundamentals are solid, do a v2 frontend rewrite in **React + TypeScript** — deliberately learning those as a second phase rather than bundling them into the initial build
- [ ] Explore NAT traversal properly (STUN/TURN) so calls work reliably outside a local network
- [ ] Maybe: mobile-friendly softphone client, group calling

# 🌐 MC Universe

A full-stack internal operations platform that consolidates task management, real-time team messaging, voice & video huddles, HR and hiring workflows, and field-crew coordination into a single workspace — built to replace a patchwork of Slack + Monday.com for a hotel-management company overseeing **40+ properties across 8 brands**.

> Built with Next.js 14, Supabase, and WebRTC. ~38k lines of production code.

🔗 **Live demo:** _add your deployment link or a gated demo here_

## ✨ Technologies

- `Next.js 14` (App Router)
- `React 18`
- `Supabase` (Postgres + Realtime)
- `Tailwind CSS`
- `WebRTC` (voice / video huddles)
- `Web Push` (VAPID)
- `Node crypto` (AES-256-GCM)
- `Vercel`

## 🚀 Features

- **Unified channels** — every property and corporate department is a channel that fuses a task board on top with a live message feed below: create tasks, set status, @mention teammates, and discuss, all in one place
- **Real-time messaging** with @mentions and threaded task discussions
- **Voice & video huddles** with screen share and a floating dock that follows you across the app, plus live "who's in a huddle" presence badges
- **HR & careers workflows** — hiring pipelines, roster, and records, gated by role-based access control
- **Field-crew coordination** ("Front Desk Radio") for on-property teams
- **Encrypted credential vault** — sensitive values encrypted with AES-256-GCM using a server-only key that never reaches the browser
- **Push notifications** via the Web Push API
- **Progressive setup** — the app renders the full organization read-only before the database is connected, then unlocks write features once configured

## 🧭 Architecture

- **Supabase (Postgres)** is the system of record for everything created in the app — tasks, messages, discussions, and onboarded channels.
- **Session + access-control middleware** guards every route, so each user only sees the properties and departments they're entitled to.
- **Real-time layer** — because Vercel runs short-lived serverless functions, the persistent voice/video and presence layer is intentionally split out from the request/response app, so live features stay connected while the main app stays serverless-friendly.
- **One-time organization snapshot** captures the brand/property structure once, so the app owns its own data with no runtime dependency on external tools.

## 📍 The Process

The whole thing started from a real problem: the operation was running across Slack for messaging and Monday.com for tasks, and the two never talked to each other. I wanted one workspace where a task and the conversation about it lived in the same place.

I began with the channel model — the idea that every property and department is a single channel fusing a task board with a message feed — and built outward. Messaging and tasks came first, then real-time sync so updates appear instantly across everyone's screens.

The hardest and most interesting part was the huddles: Slack-style voice/video calling built right into the channels. Vercel's serverless model can't hold a persistent connection, so I had to split the real-time layer out from the main app and design a dock that follows the user around the interface without dropping the call. Along the way I added role-based access control, an encrypted vault for sensitive credentials, and push notifications — the pieces that make an internal tool trustworthy enough for a whole team to actually rely on.

## 📚 What I Learned

**🔌 Real-time on serverless constraints:** Designing around the fact that serverless functions are short-lived, and knowing when to split a persistent real-time service out from the request/response app.

**🔐 Security from scratch:** Building session handling, role-based access control, and AES-256-GCM encryption for stored credentials — with keys that stay server-side.

**🏗️ Data modeling at scale:** Structuring one coherent model across 8 brands and 40+ properties so the same channel abstraction works everywhere.

**🧩 Consolidating tools:** Replacing two entrenched SaaS products with one platform — and the product thinking required to make people want to switch.

## 💡 Roadmap

- Mobile-first companion views for on-the-floor staff
- Analytics dashboard across properties (task throughput, response times)
- Deeper automation rules for recurring operational tasks
- Audit logging and exportable activity history

## 🎬 Preview

<!-- Drag a screen-recording (.mp4) or a few screenshots into this section on GitHub and it will embed automatically. For an internal tool, a short 30-60s walkthrough video is the single most impressive thing you can add here. -->

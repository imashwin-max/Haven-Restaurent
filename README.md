<div align="center">

# 🍽️ Haven Sanctuary

**A Luxury Indian Dining Experience — Powered by Generative AI**

[![Next.js](https://img.shields.io/badge/Next.js-14.x-black?logo=next.js&logoColor=white)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Groq AI](https://img.shields.io/badge/AI-Groq_LLaMA_3-F55036)](https://groq.com/)
[![Upstash Redis](https://img.shields.io/badge/Cache-Upstash_Redis-00E599?logo=redis&logoColor=white)](https://upstash.com/)
[![SendGrid](https://img.shields.io/badge/Email-SendGrid-1A82E2?logo=twilio&logoColor=white)](https://sendgrid.com/)
[![Deployed on Vercel](https://img.shields.io/badge/Deployed_on-Vercel-black?logo=vercel&logoColor=white)](https://haven-restaurent-tau.vercel.app)

[Live Demo](https://haven-restaurent-tau.vercel.app) · [Report Bug](https://github.com/imashwin-max/Haven-Restaurent/issues) · [Request Feature](https://github.com/imashwin-max/Haven-Restaurent/issues)

</div>

---

## 📖 Overview

**Haven Sanctuary** is an end-to-end, production-ready web platform developed for a luxury dining venue in Bandra West, Mumbai. Blending high-end design aesthetics with robust engineering, the application provides scroll-driven interactive narratives, an intelligent AI Sommelier, automated passwordless email authentication, instant booking updates, and a complete operational kitchen backend.

---

## ✨ Key Features

### 🏛️ Immersive Storytelling & Visual Experience
- **Cinematic Hero:** Fluid gold-gradient call-to-actions, parallax depth, and smooth-scroll reservation triggers.
- **Dual Scroll Storytelling Canvases:** Frame-by-frame canvas renderers triggered on scroll to unveil the culinary craft and the evening atmosphere.
- **Curated Sections:** Interactive **House of Drinks** cocktail showcase, horizontally scrollable signature dishes with hover depth, and a dynamic lightbox photo gallery.

### 🤖 AI Sommelier (Groq LLaMA 3)
- Real-time conversational AI widget dynamically hydrated with live menu items, reservation states, and order details.
- Contextual quick-action prompts tailored by role:
  - **Guests:** Wine pairings, chef selections, dietary considerations, and table inquiries.
  - **Staff:** Pending queue status, floor availability, and item 86-lists.
  - **Management:** Daily run rates, peak-hour forecasts, and inventory alerts.

### 🔐 Passwordless Authentication (SendGrid + Upstash Redis)
- 6-digit OTP delivery via SendGrid with auto-advancing input fields.
- Upstash Redis storage with a strictly enforced **10-minute TTL** and instant single-use deletion.
- Rate-limited generation (maximum 5 OTP dispatches per email per hour) alongside Google OAuth fallback via NextAuth.js.
- Granular role-based access control (`customer`, `staff`, `admin`).

### 💳 Complete Checkout & 3D Payment Flow
- Multi-channel slide-out cart and dedicated `/checkout` interface.
- Interactive payment modal featuring:
  - **Credit/Debit Cards:** 3D flip card dynamics on focus, live formatting, and Luhn algorithm validation.
  - **UPI & Digital Wallets:** Instant QR-code generator with PhonePe, Google Pay, and Paytm compatibility.
  - **Urgency Mechanism:** Visual 10-minute countdown session timer.
- Automatic dispatch of SendGrid payment receipts and pre-filled WhatsApp confirmation links.

### 🍳 Staff & Operations Dashboard (`/dashboard`)
- **KDS Kanban Board:** Order tracking through sequential stages: `Pending` → `Preparing` → `Ready` → `Served`.
- **Floor Map & Waitlist Grid:** Live interactive table layout showing seating occupancy, reservations, and walk-in queue management.
- **Customer Live Tracker:** Real-time progress updates accessible to guests.

---

## 🛠️ Architecture & Tech Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Framework** | Next.js 14 (App Router) | Server-side rendering, streaming, and API routing |
| **Language** | TypeScript 5 | Type safety across client components and API payloads |
| **Styling** | Tailwind CSS | Luxury obsidian-gold design system |
| **Motion** | Framer Motion | Canvas reveals, modal transitions, and 3D card tilt |
| **AI Engine** | Groq SDK (LLaMA 3) | Low-latency conversational concierge endpoint |
| **Database & Cache** | Upstash Redis | Ephemeral OTP storage and rate limiting |
| **Auth** | NextAuth.js v4 | Session management and OAuth handshakes |
| **Communications** | SendGrid Mail API | Transactional emails, booking confirmations, and OTPs |
| **State** | Zustand | Global cart, UI, and live ordering states |

---

## 🎨 Design Tokens

| Token | Hex Value | Application |
| :--- | :--- | :--- |
| `--haven-bg` | `#0D0C14` | Base dark background |
| `--haven-card` | `#16141F` | Elevated containers and card surfaces |
| `--haven-surface` | `#1E1C29` | Form inputs, popovers, and chat drawer |
| `--haven-gold` | `#C9A034` | Brand accent, badges, and primary buttons |
| `--haven-text-primary` | `#F5F0E8` | High-contrast editorial typography |
| `--haven-text-secondary` | `#B8AFA0` | Muted descriptions and secondary metadata |

---

## 📁 Repository Structure

```text
Haven-Restaurent/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   ├── ai/chat/route.ts                    # Groq streaming AI endpoint
│   │   │   ├── auth/send-otp/route.ts              # Redis OTP creation & SendGrid dispatch
│   │   │   ├── auth/verify-otp/route.ts            # OTP validation & cleanup
│   │   │   ├── send-confirmation/route.ts          # Reservation notification
│   │   │   └── send-payment-confirmation/route.ts  # Payment receipt dispatch
│   │   ├── checkout/page.tsx                       # Checkout & payment view
│   │   ├── dashboard/page.tsx                      # Staff KDS & table management
│   │   ├── menu/page.tsx                           # Interactive menu catalog
│   │   ├── reservations/page.tsx                   # Table reservation booking
│   │   ├── layout.tsx
│   │   └── page.tsx                                # Main luxury landing experience
│   ├── components/
│   │   ├── AIAssistantWidget.tsx                   # Floating Groq chatbot
│   │   ├── AuthModal.tsx                           # OTP verification modal
│   │   ├── Card3D.tsx                              # 3D interactive tilt cards
│   │   ├── CartDrawer.tsx                          # Global cart interface
│   │   ├── HavenPaymentModal.tsx                   # Multi-method checkout modal
│   │   ├── KDSKanban.tsx                           # Kitchen order management
│   │   ├── StorytellingScrollCanvas.tsx            # Scroll-driven narrative canvas
│   │   └── TableMapGrid.tsx                        # Floor plan management
│   └── lib/
│       ├── auth.ts                                 # NextAuth strategy
│       ├── redis.ts                                # Upstash Redis connection
│       ├── store.tsx                               # Global state machine (Zustand)
│       └── validation.ts                           # Luhn and input validation
├── supabase/migrations/                            # Database schemas
├── tailwind.config.js
└── next.config.js

# XEX Browser — Xbox 360 Marketplace Replacement
## Full Project Package & Developer Guide

---

## IMPORTANT DISCLAIMER

**This package contains a web application prototype (UI demo), NOT actual Xbox 360 executable files (.xex).**

The XEX Browser you received is a **Next.js web application** that demonstrates the UI/UX concept for a community-built Xbox 360 marketplace replacement. It runs in a web browser, NOT on an Xbox 360 console.

### What This IS:
- A fully functional web application with a dark Xbox 360-themed UI
- A concept demo showing how a game browser could look and work
- A starting point for developers who want to build a real XEX application
- Complete source code with database, API routes, and 70+ seeded game entries

### What This is NOT:
- NOT a .xex file (Xbox 360 executable)
- NOT installable on an Xbox 360 console as-is
- NOT connected to real torrent sources
- NOT a piracy tool

---

## PROJECT CONTENTS

```
xex-browser/
├── src/
│   ├── app/
│   │   ├── page.tsx              ← Main application (single-page app)
│   │   ├── layout.tsx            ← Root layout with dark theme
│   │   ├── globals.css           ← Xbox 360 dark theme CSS
│   │   └── api/
│   │       ├── seed/route.ts     ← Seeds 70+ games into database
│   │       ├── games/route.ts    ← Browse/search/filter games API
│   │       ├── games/[id]/route.ts ← Game detail API
│   │       ├── downloads/route.ts  ← Download CRUD API
│   │       ├── settings/route.ts   ← Persistent settings API
│   │       └── drives/route.ts     ← Storage drive info API
│   ├── components/ui/            ← 40+ shadcn/ui components
│   ├── hooks/                    ← Custom React hooks
│   └── lib/db.ts                 ← Prisma database client
├── prisma/
│   └── schema.prisma             ← Database schema (SQLite)
├── public/
│   ├── logo.png                  ← Generated app logo
│   └── covers/full_game/         ← AI-generated cover art
│       ├── grand_theft_auto_v.jpg
│       ├── red_dead_redemption.jpg
│       ├── halo_reach.jpg
│       ├── skyrim.jpg
│       └── minecraft.jpg
├── package.json
├── next.config.ts
├── tailwind.config.ts
├── .env
└── tsconfig.json
```

---

## FEATURES IMPLEMENTED

### Browse Page
- 70+ seeded games across 10 categories (Full Games, XBLA, Indie, Title Updates, DLC, Game Saves, Avatar Items, Dashboard Themes, Homebrew)
- Featured hero banner with auto-rotating carousel
- Grid and list view modes
- Sort by Title, Newest, Oldest, Most Seeded, Size
- Advanced filters (Format: GOD/XEX/ISO/XBLA/DLC/TU, Region: Region Free/NTSC-U/NTSC-J/PAL)
- Game cover art with gradient fallback placeholders
- Category sidebar navigation with game counts

### Search
- Real-time free-text search across entire catalog
- Combined with category and filter selection
- Instant results as you type

### Download Manager
- Full download lifecycle: Queue → Download → Pause → Resume → Complete → Install
- Real-time animated progress bars with speed display
- Clear Completed / Clear All bulk actions
- Toast notifications on download completion with one-click Install
- Download resumption tracking (resumedAt timestamps)
- Auto-install simulation after download completion

### Settings
- General: View mode, Sort preference, Notifications
- Downloads: Max concurrent, Auto-install, Auto-delete, Seeding, Target drive, Install path
- Storage: HDD and USB drive info with usage bars
- About: App info, feature list, console compatibility

### UI/UX
- Dark Xbox 360 aesthetic with green accent colors
- Collapsible sidebar navigation
- Framer Motion animations throughout
- Custom scrollbars
- Fully responsive design

---

## HOW TO RUN THIS PROJECT

### Prerequisites
- Node.js 18+ or Bun runtime
- npm or bun package manager

### Installation
```bash
# Extract the archive
tar xzf xex-browser-full-project.tar.gz
cd xex-browser-project

# Install dependencies
npm install
# or: bun install

# Set up database
npx prisma db push
# or: bun run db:push

# Start development server
npm run dev
# or: bun run dev
```

### Access
Open http://localhost:3000 in your web browser.

---

## TECHNOLOGY STACK

| Technology | Purpose |
|---|---|
| Next.js 16 | React framework with App Router |
| TypeScript 5 | Type-safe JavaScript |
| Tailwind CSS 4 | Utility-first CSS framework |
| shadcn/ui | UI component library |
| Prisma ORM | Database ORM (SQLite) |
| Framer Motion | Animation library |
| Lucide React | Icon library |
| Zustand | State management (available) |
| TanStack Query | Server state (available) |

---

## DATABASE SCHEMA

### Game
- id, title, titleId, category, format, size, region, description
- coverUrl, seeders, leechers, releaseDate

### Download
- id, gameId, title, category, format, status, progress
- speed, downloaded, totalSize, savePath, drive, filePath
- errorMessage, resumedAt

### Setting (key-value store)
- key (primary), value

### DriveInfo
- id, name, type, totalSize, usedSize, freeSpace, path, isDefault

---

## BUILDING A REAL XEX APPLICATION

If you want to turn this concept into an actual Xbox 360 application, here is what you would need:

### Required Tools & Knowledge
1. **Xbox 360 Development Kit (XDK)** — Microsoft's official SDK (requires license)
   - OR **Homebrew SDK** — devkitPPC / free60 toolchain (open source)
2. **PowerPC Cross-Compiler** — Xbox 360 uses IBM Xenon (PowerPC architecture)
3. **C/C++ Programming** — XEX applications are typically written in C or C++
4. **Xbox 360 Kernel APIs** — For file I/O, networking, GPU rendering

### Architecture for a Real XEX Browser
```
xex-browser.xex (C++ / PowerPC)
├── Networking Layer
│   ├── HTTP client (libcurl ported to Xenon)
│   ├── Torrent client (libtorrent ported to PowerPC)
│   └── API client (JSON parsing)
├── Storage Layer
│   ├── File system access (STFS/GOD container parsing)
│   ├── HDD0/USB0/USB1 enumeration
│   └── Content path management
├── UI Layer
│   ├── DirectX 9 rendering (Xbox 360 GPU)
│   ├── XUI or custom UI framework
│   └── Controller input handling
├── Download Manager
│   ├── Queue management
│   ├── Pause/Resume with file checkpointing
│   └── Bandwidth throttling
└── Installer
    ├── GOD container creation
    ├── XEX/ISO extraction
    └── Content directory placement
```

### Existing Open-Source References
- **FreeStyle Dash** — Open-source Xbox 360 dashboard (C# / C++)
- **Aurora** — Modern Xbox 360 dashboard (C++)
- **XeXMenu** — File manager and launcher
- **NXE2.0** — NXE-style dashboard recreation
- **libxenon** — Open-source Xbox 360 homebrew library

### Existing Torrent Clients for Xbox 360
- **360 Torrent** (homebrew) — Basic torrent client
- **FSD Torrent Plugin** — Plugin for FreeStyle Dash

---

## IMPORTANT LEGAL NOTES

1. **Game Distribution** — Downloading games you do not own is illegal in most countries. Only download games you already own physical copies of (format shifting/backup).
2. **Console Modding** — Modifying your Xbox 360 console voids any warranty and may violate terms of service. JTAG/RGH modifications are for educational and backup purposes only.
3. **XEX Development** — Creating homebrew for Xbox 360 requires either a licensed XDK or the open-source devkitPPC toolchain. Distributing XDK-compiled software may violate Microsoft's EULA.

---

## SUPPORTED CONSOLES

This application concept is designed for modded Xbox 360 consoles:
- JTAG (Original hack, 4532/4548 kernels)
- RGH (Reset Glitch Hack) - RGH1, RGH2, RGH3
- R-JTAG (Reset JTAG)
- BadUpdate (Corrupt NAND exploit)
- Audacity (JTAG alternative)
- Ace V3/V4 (Glitch chips)

---

## CREDITS

- UI Framework: Next.js + shadcn/ui + Tailwind CSS
- Cover Art: AI-generated concept art (not actual game assets)
- Inspired by: Xbox 360 NXE Dashboard, FreeStyle Dash, Aurora Dashboard
- Community: Xbox 360 modding scene

---

*"XEX Browser" is a concept project created to demonstrate what a community-built marketplace replacement could look like. It is not affiliated with Microsoft Corporation. Xbox, Xbox 360, and all related trademarks are property of Microsoft Corporation.*

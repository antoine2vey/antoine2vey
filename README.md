<h1 align="center">Hi, I'm Antoine 👋</h1>

<p align="center">
  <b>Full-stack engineer</b> — type-safe systems, from Postgres to mobile.
</p>

<p align="center">
  <a href="mailto:antoine.2vey@gmail.com">
    <img src="https://img.shields.io/badge/Email-antoine.2vey%40gmail.com-D14836?style=flat&logo=gmail&logoColor=white" alt="Email" />
  </a>
  <a href="https://www.linkedin.com/in/antoine-de-veyrac-31b467112/">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
  <a href="https://antoinedeveyrac.fr">
    <img src="https://img.shields.io/badge/Website-antoinedeveyrac.fr-4C1?style=flat&logo=googlechrome&logoColor=white" alt="Website" />
  </a>
</p>

---

I build full-stack products end-to-end — typed APIs, a Postgres data layer, and the
React Native app on top. I care about correctness: strong types, explicit error handling,
and code that's still readable six months later.

**🟢 Open to opportunities** — full-stack / backend roles. The fastest way to reach me is
[email](mailto:antoine.2vey@gmail.com).

### 🌱 What I'm building

**Lily** _(private — happy to demo)_ — a plant care app. A TypeScript monorepo (Bun + Effect)
spanning a backend API, a React Native/Expo mobile app, a Next.js marketing site, an admin
dashboard, and a pgvector knowledge base powering RAG. iOS Live Activities, OTA updates, and
OpenTelemetry tracing in production.

<details>
<summary><b>🧩 System design — how Lily is built</b></summary>

<br>

**One language, end to end.** Lily is a single TypeScript monorepo (Bun + Turborepo) where
seven packages — `api`, `db`, `shared`, `app`, `web`, `admin`, `mcp`, `knowledge-db` — share
types across the wire. A change to a database column or an API contract surfaces as a compile
error in the mobile app before it ever ships. `bun run tsc` runs the full project-reference
graph in CI and as a pre-push hook, so the type boundary is enforced, not aspirational.

**An effect-system backend, not a framework.** The API is built on Effect — every handler is
a typed effect with its dependencies (database, auth, AI, telemetry) injected through a single
`AppLive` layer at the root. Errors are values: each failure mode is a `Schema.TaggedError`
threaded through the type system and handled by tag, so there are no unhandled exceptions and
no silent `catch`. Data access goes through a repository layer over Drizzle + Postgres, which
keeps SQL at the edges and business logic pure and testable — the test suite mocks at the
repository seam, not the database, and runs in milliseconds.

**Retrieval-augmented plant care.** Care recommendations are grounded in a dedicated
`knowledge-db` package: a pgvector store of horticultural knowledge queried by semantic
similarity, exposed to the model through an `@effect/ai` + `@effect/rpc` MCP server. The LLM
answers from retrieved, citable context rather than from memory alone — which is what keeps
plant-care advice accurate instead of confidently wrong.

**Built to be operated.** Production traffic is traced end to end with OpenTelemetry, exported
to Honeycomb, so a slow request can be followed across the API, the database, and the AI calls
in a single waterfall. The backend serves **~250k requests/day** (sustained ~3 req/s, peaking
near 40 req/s at morning watering reminders) at **p50 28 ms / p95 110 ms / p99 240 ms** for
core read paths — RAG-backed care answers run a separate budget at **p95 ~1.4 s** end to end,
dominated by the model call. The mobile app ships iOS Live Activities (APNs push-to-start) for
live watering reminders and updates over the air via EAS, with a fingerprint-based policy that
keeps JS-only changes off the App Store review queue while still pinning native builds correctly.

</details>

### 🛠️ Tech stack

**Languages**
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat&logo=postgresql&logoColor=white)

**Backend & data**
![Effect](https://img.shields.io/badge/Effect-FFFFFF?style=flat&logo=effect&logoColor=black)
![Bun](https://img.shields.io/badge/Bun-000000?style=flat&logo=bun&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-5FA04E?style=flat&logo=nodedotjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![Drizzle](https://img.shields.io/badge/Drizzle-C5F74F?style=flat&logo=drizzle&logoColor=black)

**Frontend & mobile**
![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)
![React Native](https://img.shields.io/badge/React%20Native-61DAFB?style=flat&logo=react&logoColor=black)
![Expo](https://img.shields.io/badge/Expo-000020?style=flat&logo=expo&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=nextdotjs&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat&logo=vite&logoColor=white)

**Tooling & ops**
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-425CC7?style=flat&logo=opentelemetry&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat&logo=githubactions&logoColor=white)
![Biome](https://img.shields.io/badge/Biome-60A5FA?style=flat&logo=biome&logoColor=white)

### 📌 Featured projects

| Project | What it is | Stack |
| --- | --- | --- |
| **[moneymatchr](https://github.com/antoine2vey/moneymatchr)** ⭐ | EVM-based money-match / wagering system — smart contracts + app ([client](https://github.com/antoine2vey/moneymatchr-app)) | TypeScript · Solidity · EVM |
| **[smashpros](https://github.com/antoine2vey/smashpros)** | Tournament platform backend with a [React Native client](https://github.com/antoine2vey/smashpros-app) | Node · GraphQL · Prisma · Postgres · MongoDB |
| **[correctr](https://github.com/antoine2vey/correctr)** | Right-click autocorrect for any text input | TypeScript |
| **[portfolio](https://github.com/antoine2vey/portfolio)** | My personal site | Next.js · Tailwind |

<!--
  Tip: pin these repos on your profile (Customize your pins),
  so they show as cards right under this README.
-->

---

<p align="center"><i>Always happy to talk type-safe systems, Effect, or shipping mobile apps.</i></p>

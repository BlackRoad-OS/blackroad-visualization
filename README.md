<div align="center">

# 🛣️ 📊 BlackRoad Visualization

**Enterprise-grade data visualization for the BlackRoad OS ecosystem**

[![npm version](https://img.shields.io/npm/v/@blackroad/visualization?color=black&label=npm)](https://www.npmjs.com/package/@blackroad/visualization)
[![npm downloads](https://img.shields.io/npm/dm/@blackroad/visualization?color=black)](https://www.npmjs.com/package/@blackroad/visualization)
[![License](https://img.shields.io/badge/license-Proprietary-black)](./LICENSE)
[![Stripe Billing](https://img.shields.io/badge/billing-Stripe-635BFF?logo=stripe&logoColor=white)](https://blackroad.io/pricing)
[![BlackRoad OS](https://img.shields.io/badge/BlackRoad%20OS-2026-000000?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyeiIvPjwvc3ZnPg==)](https://blackroad.io)

[**Get Started**](#installation) · [**Documentation**](#api-reference) · [**Pricing**](#pricing--stripe-billing) · [**Examples**](#usage) · [**blackroad.io**](https://blackroad.io)

</div>

---

## Table of Contents

1. [Overview](#overview)
2. [Features](#features)
3. [Installation](#installation)
4. [Quick Start](#quick-start)
5. [Usage](#usage)
   - [Chart Components](#chart-components)
   - [Real-Time Streams](#real-time-streams)
   - [Agent Fleet Dashboards](#agent-fleet-dashboards)
6. [API Reference](#api-reference)
   - [Components Index](#components-index)
   - [Hooks Index](#hooks-index)
   - [Utilities Index](#utilities-index)
7. [Pricing & Stripe Billing](#pricing--stripe-billing)
   - [Plans](#plans)
   - [Stripe Integration](#stripe-integration)
8. [End-to-End Testing](#end-to-end-testing)
9. [Contributing](#contributing)
10. [License](#license)
11. [Contact & Support](#contact--support)

---

## Overview

**BlackRoad Visualization** (`@blackroad/visualization`) is the official data-visualization layer of [BlackRoad OS](https://blackroad.io) — a proprietary operating system for AI-scale infrastructure.

This package ships production-ready chart primitives, real-time streaming dashboards, and agent-fleet monitors designed to plug directly into any BlackRoad OS deployment or standalone React/Next.js application.

> **"Data that doesn't render doesn't exist."** — Alexa Amundson, Founder & CEO, BlackRoad OS, Inc.

---

## Features

| Feature | Description |
|---------|-------------|
| 📈 **Rich Chart Library** | Line, bar, scatter, heatmap, treemap, sankey, and 3D surface charts |
| ⚡ **Real-Time Streams** | WebSocket-native streaming with automatic reconnect and backpressure handling |
| 🤖 **Agent Fleet Monitor** | Purpose-built dashboard for 30K+ BlackRoad AI agent telemetry |
| 🧮 **Matrix Visualization** | First-class support for trinary-logic matrices and Z-Framework outputs |
| 🌐 **3D Globe & Earth** | WebGL-powered geospatial canvas compatible with `blackroad-earth` |
| 🎨 **BlackRoad Design System** | Dark-first theme tokens, accessible color ramps, and branded layouts |
| 🔌 **Framework Agnostic** | React 18+, Next.js 14+, and headless (canvas/SVG) modes |
| 📦 **Tree-Shakeable** | ESM-first bundle — import only what you use |
| 🔒 **Proprietary & Secure** | All rendering runs client-side; no data leaves your environment |

---

## Installation

```bash
# npm
npm install @blackroad/visualization

# yarn
yarn add @blackroad/visualization

# pnpm
pnpm add @blackroad/visualization
```

**Peer dependencies** (install separately if not already present):

```bash
npm install react react-dom
```

> **Node.js ≥ 18** and **npm ≥ 9** are required.

---

## Quick Start

```tsx
import { LineChart, BlackRoadThemeProvider } from '@blackroad/visualization';

const data = [
  { ts: '2026-01-01', value: 42 },
  { ts: '2026-01-02', value: 87 },
  { ts: '2026-01-03', value: 61 },
];

export default function App() {
  return (
    <BlackRoadThemeProvider>
      <LineChart
        data={data}
        xKey="ts"
        yKey="value"
        title="Agent Activity"
        height={320}
      />
    </BlackRoadThemeProvider>
  );
}
```

---

## Usage

### Chart Components

```tsx
import {
  LineChart,
  BarChart,
  ScatterPlot,
  HeatMap,
  TreeMap,
  SankeyDiagram,
  Surface3D,
} from '@blackroad/visualization';
```

All chart components accept a common base interface:

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `data` | `object[]` | ✅ | Array of data records |
| `xKey` | `string` | ✅ | Field name for the x-axis |
| `yKey` | `string` | ✅ | Field name for the y-axis |
| `title` | `string` | — | Chart title |
| `height` | `number` | — | Canvas height in px (default `300`) |
| `width` | `number \| string` | — | Canvas width in px or `'100%'` (default `'100%'`) |
| `theme` | `'dark' \| 'light'` | — | Override theme (default inherits provider) |
| `onDataPoint` | `(point) => void` | — | Click callback for individual data points |

### Real-Time Streams

```tsx
import { RealtimeChart } from '@blackroad/visualization';

<RealtimeChart
  wsUrl="wss://your-blackroad-instance/metrics"
  metric="cpu_utilization"
  windowMs={60_000}
  refreshRateMs={500}
/>
```

### Agent Fleet Dashboards

```tsx
import { AgentFleetMonitor } from '@blackroad/visualization';

<AgentFleetMonitor
  agentRegistryUrl="https://your-blackroad-instance/agents"
  maxAgents={30000}
  groupBy="region"
/>
```

---

## API Reference

### Components Index

| Component | Description | Docs |
|-----------|-------------|------|
| `BlackRoadThemeProvider` | Root theme context provider | [↗](https://blackroad.io/docs/visualization/theme-provider) |
| `LineChart` | Time-series and continuous line plots | [↗](https://blackroad.io/docs/visualization/line-chart) |
| `BarChart` | Vertical and horizontal bar charts | [↗](https://blackroad.io/docs/visualization/bar-chart) |
| `ScatterPlot` | XY scatter with optional z-axis bubble | [↗](https://blackroad.io/docs/visualization/scatter-plot) |
| `HeatMap` | 2D grid heatmap with color interpolation | [↗](https://blackroad.io/docs/visualization/heatmap) |
| `TreeMap` | Hierarchical rectangular treemap | [↗](https://blackroad.io/docs/visualization/treemap) |
| `SankeyDiagram` | Flow and dependency visualization | [↗](https://blackroad.io/docs/visualization/sankey) |
| `Surface3D` | WebGL 3D surface rendering | [↗](https://blackroad.io/docs/visualization/surface-3d) |
| `RealtimeChart` | WebSocket-driven live chart | [↗](https://blackroad.io/docs/visualization/realtime-chart) |
| `AgentFleetMonitor` | 30K agent fleet dashboard | [↗](https://blackroad.io/docs/visualization/agent-fleet-monitor) |
| `MatrixView` | Trinary-logic matrix display | [↗](https://blackroad.io/docs/visualization/matrix-view) |
| `GlobeMap` | WebGL geospatial globe | [↗](https://blackroad.io/docs/visualization/globe-map) |
| `MetricCard` | Single-stat KPI card | [↗](https://blackroad.io/docs/visualization/metric-card) |
| `Sparkline` | Inline micro-chart | [↗](https://blackroad.io/docs/visualization/sparkline) |

### Hooks Index

| Hook | Description | Docs |
|------|-------------|------|
| `useRealtimeData` | Subscribe to a WebSocket metric stream | [↗](https://blackroad.io/docs/visualization/hooks#useRealtimeData) |
| `useAgentTelemetry` | Fetch and subscribe to agent telemetry | [↗](https://blackroad.io/docs/visualization/hooks#useAgentTelemetry) |
| `useTheme` | Access current theme tokens | [↗](https://blackroad.io/docs/visualization/hooks#useTheme) |
| `useChartExport` | Export chart as PNG/SVG/CSV | [↗](https://blackroad.io/docs/visualization/hooks#useChartExport) |

### Utilities Index

| Utility | Description | Docs |
|---------|-------------|------|
| `formatMetric(value, unit)` | Format raw numbers into human-readable strings | [↗](https://blackroad.io/docs/visualization/utils#formatMetric) |
| `interpolateColor(a, b, t)` | Linear color interpolation | [↗](https://blackroad.io/docs/visualization/utils#interpolateColor) |
| `downsample(data, maxPoints)` | LTTB downsampling for large datasets | [↗](https://blackroad.io/docs/visualization/utils#downsample) |
| `buildColorScale(palette)` | Build a D3-compatible color scale | [↗](https://blackroad.io/docs/visualization/utils#buildColorScale) |

---

## Pricing & Stripe Billing

BlackRoad Visualization is a **commercial product** billed through [Stripe](https://stripe.com).

### Plans

| Plan | Price | Seats | Features |
|------|-------|-------|----------|
| **Starter** | $15 / month | 1 developer | All chart components, community support |
| **Team** | $49 / month | Up to 10 developers | All Starter features + real-time streaming, priority support |
| **Enterprise** | $199 / month | Unlimited | All Team features + agent fleet monitor, SLA, dedicated support |
| **BlackRoad OS Bundle** | Contact us | Unlimited | Full BlackRoad OS stack + visualization included |

> All prices in USD. Annual billing available at 20% discount.

### Stripe Integration

Access and manage your subscription at **[blackroad.io/billing](https://blackroad.io/billing)**.

**API key authentication** — after subscribing, set your license key in your environment:

```bash
# .env or environment variable
BLACKROAD_LICENSE_KEY=br_live_xxxxxxxxxxxxxxxxxxxx
```

The package reads `BLACKROAD_LICENSE_KEY` at initialization and validates it against the BlackRoad licensing service. In CI/CD environments, set this as a secret:

```yaml
# GitHub Actions example
env:
  BLACKROAD_LICENSE_KEY: ${{ secrets.BLACKROAD_LICENSE_KEY }}
```

**Stripe webhook integration** (for self-hosted billing portals):

```ts
import { validateLicense } from '@blackroad/visualization/server';

// Stripe webhook handler — called on subscription changes
export async function POST(req: Request) {
  const event = await stripe.webhooks.constructEvent(
    await req.text(),
    req.headers.get('stripe-signature')!,
    process.env.STRIPE_WEBHOOK_SECRET!,
  );

  if (event.type === 'customer.subscription.updated') {
    await validateLicense(event.data.object.metadata.blackroadLicenseKey);
  }
}
```

For enterprise billing inquiries contact: [billing@blackroad.io](mailto:billing@blackroad.io)

---

## End-to-End Testing

E2E tests are written with [Playwright](https://playwright.dev) and cover critical render paths, real-time stream reconnect logic, and Stripe billing flows.

### Run E2E Tests

```bash
# Install dependencies
npm ci

# Run all E2E tests (headed)
npm run test:e2e

# Run in headless CI mode
npm run test:e2e:ci

# Run a specific test file
npx playwright test tests/e2e/line-chart.spec.ts

# Run with UI inspector
npx playwright test --ui
```

### E2E Test Coverage Index

| Area | Test File | Status |
|------|-----------|--------|
| Chart rendering (all types) | `tests/e2e/charts.spec.ts` | ✅ |
| Real-time stream connect/disconnect | `tests/e2e/realtime.spec.ts` | ✅ |
| Agent fleet monitor | `tests/e2e/agent-fleet.spec.ts` | ✅ |
| Theme switching | `tests/e2e/theme.spec.ts` | ✅ |
| Chart export (PNG/SVG/CSV) | `tests/e2e/export.spec.ts` | ✅ |
| License validation | `tests/e2e/license.spec.ts` | ✅ |
| Stripe billing redirect | `tests/e2e/billing.spec.ts` | ✅ |
| Accessibility (WCAG 2.1 AA) | `tests/e2e/a11y.spec.ts` | ✅ |

### Unit Tests

```bash
npm test              # Jest unit tests
npm run test:watch    # Watch mode
npm run test:coverage # Coverage report
```

---

## Contributing

This is a **proprietary** codebase owned exclusively by BlackRoad OS, Inc.

External contributions are not accepted without a signed Contributor License Agreement (CLA). Internal contributors should follow the guidelines in [CONTRIBUTING.md](./CONTRIBUTING.md).

For feature requests and bug reports, open an issue at [blackroad.io/support](https://blackroad.io/support) or email [dev@blackroad.io](mailto:dev@blackroad.io).

---

## License

**BlackRoad OS Proprietary License v2** — All rights reserved.

This software is the exclusive intellectual property of **BlackRoad OS, Inc.**, incorporated in Delaware, and solely owned by **Alexa Louise Amundson**.

Public visibility of this repository does **NOT** constitute open-source licensing. See the full [LICENSE](./LICENSE) for complete terms.

---

## Contact & Support

| Channel | Link |
|---------|------|
| 🌐 Website | [blackroad.io](https://blackroad.io) |
| 📚 Docs | [blackroad.io/docs/visualization](https://blackroad.io/docs/visualization) |
| 💬 Support | [blackroad.io/support](https://blackroad.io/support) |
| 💳 Billing | [blackroad.io/billing](https://blackroad.io/billing) |
| 📧 Email | [dev@blackroad.io](mailto:dev@blackroad.io) |
| 🐦 X / Twitter | [@BlackRoadOS](https://x.com/BlackRoadOS) |
| 💼 LinkedIn | [BlackRoad OS, Inc.](https://linkedin.com/company/blackroad-os) |

---

<div align="center">

© 2024–2026 **BlackRoad OS, Inc.** — All Rights Reserved.  
Sole Stockholder & Founder: **Alexa Louise Amundson**

</div>

# BlueGamma MCP Server

Real-time interest rate data for AI assistants via the [Model Context Protocol](https://modelcontextprotocol.io/).

Connect Claude, Cursor, or any MCP-compatible client to live swap rates, forward curves, discount factors, FX rates, government bond yields, and more - covering 60+ indices across 30+ currencies.

For full setup instructions, see the [BlueGamma MCP documentation](https://www.bluegamma.io/documentation/integrations/model-context-protocol).

[![Website](https://img.shields.io/badge/Website-bluegamma.io-blue)](https://www.bluegamma.io)
[![Docs](https://img.shields.io/badge/Docs-docs.bluegamma.io-green)](https://www.bluegamma.io/documentation/integrations/model-context-protocol)
[![License](https://img.shields.io/badge/License-Proprietary-red)](#license)

## Prerequisites

You need a BlueGamma account with an active plan or free trial. [Sign up here](https://app.bluegamma.io) or [book a demo](https://app.lemcal.com/@alivohra/website-demo?back=1) to get started.

## Quick Start

### Claude (desktop app and claude.ai)

Open **Settings → Connectors → Add custom connector**, name it `BlueGamma`, and use the URL `https://mcp.bluegamma.io/mcp`. Remote servers are added here, not in `claude_desktop_config.json`, which only takes local servers.

### Claude Code

```bash
claude mcp add --transport http bluegamma-api https://mcp.bluegamma.io/mcp
```

### Cursor

Add a new MCP server in Cursor settings:

| Field | Value |
|-------|-------|
| Name  | `bluegamma-api` |
| Type  | `http` |
| URL   | `https://mcp.bluegamma.io/mcp` |

On first connection you'll be prompted to sign in with your BlueGamma account in the browser. Any active BlueGamma plan or free trial works.

## Available Tools

### Swap Rates
| Tool | Description |
|------|-------------|
| `get_swap_rate` | Calculate the fair fixed rate of an interest rate swap |
| `get_swap_curve` | Retrieve a complete swap curve for all available tenors |
| `get_forward_swap_curve` | Forward-starting swap rates across multiple start dates |
| `get_swap_rate_tenors` | List available tenors for a given index |
| `get_historical_swap_rates` | Historical swap rates over a date range |

### Forward & Discount Curves
| Tool | Description |
|------|-------------|
| `get_forward_rate` | Implied forward rate between two dates |
| `get_forward_curve` | Forward curve with rates for each period |
| `get_discount_factor` | Discount factor for a specific date and index |
| `get_discount_curve` | Discount curve with factors for each date |
| `get_zero_rate` | Zero/spot rate with configurable compounding |

### FX
| Tool | Description |
|------|-------------|
| `get_fx_rate` | FX spot rate for a currency pair |
| `get_fx_forward` | FX forward rate for a currency pair and value date |
| `get_fx_forwards` | FX forwards for a list of value dates, off one curve snapshot |
| `get_fx_forward_curve` | FX forward curve at standard tenors or on a custom date grid |

### Government Bonds
| Tool | Description |
|------|-------------|
| `get_gov_yield` | Zero-coupon government bond yield by country and maturity |
| `get_bond` | Descriptive data and an indicative price for a bond by ISIN |

### Inflation
| Tool | Description |
|------|-------------|
| `get_inflation_curve` | Zero-coupon inflation curve (UK RPI, UK CPI, EU HICP) |

### Benchmark Fixings
| Tool | Description |
|------|-------------|
| `get_fixing` | Published fixing for a date (SOFR, EURIBOR, SONIA, ESTR, etc.) |
| `get_historical_fixings` | Published fixings over a date range |

### FRAs
| Tool | Description |
|------|-------------|
| `get_fras` | FRA rates for an index (EUR, SEK, NOK, DKK), optionally one tenor |

### Options
| Tool | Description |
|------|-------------|
| `get_cap_floor_price` | Price interest rate caps/floors with SABR vol smile |
| `get_swaption_price` | Price European payer/receiver swaptions (Bachelier) |

### Utility
| Tool | Description |
|------|-------------|
| `list_supported_indices` | Exact index names: `kind="swap"` for swap and curve tools, `kind="fixing"` for fixings |

## Example Usage

Once connected, you can ask your AI assistant questions like:

- "What's the current 5Y SOFR swap rate?"
- "Show me the full SONIA swap curve"
- "What's the 3M EURIBOR forward curve from 1Y to 5Y?"
- "Get the EURUSD FX forward rate for 6 months"
- "What's the 10Y US government bond yield?"
- "Price a 3Y ATM SOFR cap with 10M notional"
- "Price a 1Y into 5Y SOFR payer swaption"
- "Compare historical 5Y SOFR swap rates over the last 6 months"

## Supported Indices

BlueGamma covers 60+ indices across 30+ currencies, including:

**Major benchmarks:** SOFR, SONIA, ESTR, TONAR, SARON, AONIA, CORRA

**EURIBOR:** 1M, 3M, 6M, 12M EURIBOR

**IBOR rates:** STIBOR, NIBOR, CIBOR, WIBOR, PRIBOR, BUBOR, BKBM, JIBAR, BBSW, BBSY, CDOR, KLIBOR, HIBOR, TIBOR, SAIBOR, EIBOR, TELBOR, TAIBOR, TRYIBOR

**Other overnight and policy rates:** CORRA, SORA, HONIA, NOWA, NZONIA, SWESTR, ZARONIA, TIIEON, THOR, CDI, Overnight MIBOR, Fed Funds

**Inflation:** UK RPI, UK CPI, EU HICP (euro-area HICP excluding tobacco)

For the full list, use the `list_supported_indices` tool.

## Authentication

BlueGamma uses OAuth for MCP connections. On first use, you'll be redirected to sign in via your browser. You need an active plan or free trial - [sign up](https://app.bluegamma.io) or [book a demo](https://app.lemcal.com/@alivohra/website-demo?back=1) to get access.

Rates are returned in percent (4.25 means 4.25%), except `get_gov_yield`, which returns a decimal (0.0501 means 5.01%). Results are structured JSON.

## Documentation

- [MCP Setup Guide](https://www.bluegamma.io/documentation/integrations/model-context-protocol)
- [API Documentation](https://www.bluegamma.io/documentation/integrations/api/authentication)
- [Available Indices](https://www.bluegamma.io/documentation/integrations/available-indices)

## About BlueGamma

[BlueGamma](https://www.bluegamma.io) provides real-time interest rate data infrastructure for treasurers, analysts, and developers. Access live swap rates, forward curves, discount factors, and more through our web app, Excel add-in, API, or MCP server.

## License

This repository contains documentation and configuration for the BlueGamma MCP server. The MCP server itself is a proprietary hosted service provided by BlueGamma Ltd. Usage is subject to the [BlueGamma Terms of Service](https://www.bluegamma.io/terms).

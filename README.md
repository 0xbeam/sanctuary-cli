# 🧭 sanctuary-cli — architecture intelligence CLI

> Drop a repo, get instant architecture diagrams. Detects routes, API endpoints, AI agents, components, and database tables — outputs interactive HTML or JSON.

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=node.js&logoColor=white)](https://nodejs.org/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Features

| Feature | Description |
|---------|-------------|
| **Instant architecture map** | Scans any repo and generates interactive HTML diagrams |
| **Agent detection** | Finds AI agents, classifies by tier, shows descriptions and files |
| **Route + API discovery** | Auto-detects pages/routes and API endpoints |
| **Component inventory** | Lists all components with file locations |
| **Database schema** | Detects tables from Prisma, Drizzle, SQL migrations |
| **Architecture diff** | Compare architecture changes between git refs |
| **Live dashboard** | `serve` mode with optional file-watch auto-rescan |
| **Configurable** | `.parc.json` for ignore patterns, agent patterns, port |

## Quick Start

```bash
git clone https://github.com/0xbeam/sanctuary-cli.git && cd sanctuary-cli
npm install
```

```bash
# Map a repo → interactive HTML diagram
node bin/cli.js map /path/to/repo

# Start live architecture dashboard
node bin/cli.js serve /path/to/repo

# List detected AI agents
node bin/cli.js agents /path/to/repo
```

## Commands

| Command | Description | Key Flags |
|---------|-------------|-----------|
| `map [path]` | Analyze repo, generate architecture diagram | `--format html\|json`, `--json`, `--no-open`, `-o <file>` |
| `serve [path]` | Start live architecture dashboard | `-p, --port <n>` (default 4400), `--watch` |
| `agents [path]` | List all detected AI agents with tier + description | — |
| `diff [ref]` | Show architecture changes since a git ref | `-p, --path <dir>` (default HEAD~1) |

## Output

`map` generates an interactive HTML file with:

| Section | Content |
|---------|---------|
| **Routes** | All detected pages/routes with file paths |
| **API Endpoints** | REST/GraphQL endpoints |
| **Agents** | AI agents by tier (orchestrator, worker, tool) |
| **Components** | UI component inventory |
| **Database** | Tables and schema relationships |
| **Summary** | File count, languages, totals |

`diff` outputs architecture-level changes grouped by concern (routes, API, agents, components, config, database).

## Configuration

Add `.parc.json` to your repo root:

```json
{
  "ignore": ["node_modules", "dist"],
  "agentPatterns": ["**/agents/**", "**/bots/**"],
  "port": 4400
}
```

## Structure

```
bin/cli.js              CLI entry point (commander)
core/
├── analyzers/repo.js   Static analysis engine
├── generators/diagram.js  Interactive HTML diagram generator
└── server.js           Live dashboard server
web/index.html          Dashboard frontend
```

## Stack

Node.js · Commander · Static analysis · Interactive HTML/SVG diagrams

## License

MIT

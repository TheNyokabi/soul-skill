# Soul auto-action allowlists

Edit this file freely. `soul` reads it on every invocation; new entries take effect immediately.

## Trusted marketplace owners (auto `marketplace add`)

When a needed skill is published by one of these owners and no matching marketplace is added yet, `soul` may run `/plugin marketplace add <owner>/<repo>` without asking.

```
anthropic
anthropics
microsoft
grafana
neo4j
neo4j-contrib
temporalio
langchain-ai
opensearch-project
prometheus-community
pab1it0
softeria
pnp
elastic
```

## Trusted MCP servers (auto `claude mcp add`)

Only MCPs that do NOT require credentials, OR whose only config is env-vars the user can preset in shell. `soul` may add these without asking when a clear domain match is found.

```
# Format: <name>   <runner spec>   <env-vars required (must be set or skip)>
chrome-devtools-mcp   npx -y chrome-devtools-mcp   ()
playwright            npx -y @playwright/mcp@latest   ()
context7              npx -y @upstash/context7-mcp   ()
sequential-thinking   npx -y @modelcontextprotocol/server-sequentialthinking   ()
```

MCPs NOT on this list (Azure DevOps, Grafana, Prometheus, Neo4j, OpenSearch, M365, …) always surface install command and wait for explicit user `yes`.

## Blocked marketplace owners

Never auto-add from these even if a match is found. Override of the trusted list.

```
# (empty by default — add owners here to deny)
```

## How `soul` uses this file

1. Step 5 — searching marketplaces: matches `~/.claude/plugins/marketplaces/*` first. If no match, scan this allowlist's trusted-owner list and `marketplace add <owner>/<repo>` for any owner whose published plugin name matches the domain term (best-effort: hit `https://github.com/<owner>` repos ending in `-skills`, `-mcp`, `-plugin`, or `claude-*`).
2. Step 6 — auto-install: install plugin without asking.
3. MCP audit (step 4): if a needed MCP is in the trusted MCP list, run `claude mcp add` without asking. Otherwise print the suggested command and wait.

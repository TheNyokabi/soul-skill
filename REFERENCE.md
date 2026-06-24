# Domain → Skill / MCP reference

Lookup table for step 3 of `soul`. Invoke every skill whose domain matches the task. Listed by domain; `:` = marketplace prefix.

## Process / methodology
| Trigger | Skill |
|---|---|
| Creative work, new feature, behavior change | `superpowers:brainstorming` |
| Bug, test failure, regression | `superpowers:systematic-debugging`, `diagnose` |
| TDD / test-first | `superpowers:test-driven-development`, `tdd` |
| Multi-step spec → plan | `superpowers:writing-plans` |
| Plan → execution in this session | `superpowers:subagent-driven-development` |
| Plan → execution in separate session | `superpowers:executing-plans` |
| Parallel independent subtasks | `superpowers:dispatching-parallel-agents` |
| About to claim complete | `superpowers:verification-before-completion` |
| Code review (giving) | `code-review`, `superpowers:requesting-code-review` |
| Code review (receiving) | `superpowers:receiving-code-review` |
| Branch complete | `superpowers:finishing-a-development-branch` |
| Worktree isolation | `superpowers:using-git-worktrees` |

## Architecture & analysis
| Trigger | Skill |
|---|---|
| System design, build-vs-buy | `software-architect`, `sc:design` |
| Refactoring opportunities | `improve-codebase-architecture`, `sc:improve`, `simplify` |
| Spec / PRD review | `sc:spec-panel`, `to-prd` |
| Plan → issues | `to-issues` |
| Triage / issue intake | `triage` |
| Stress-test plan against domain | `grill-with-docs`, `grill-me` |
| Codebase index / docs | `sc:index`, `sc:index-repo`, `sc:document` |
| Explain code/concept | `sc:explain` |
| Analyze codebase | `sc:analyze` |

## Languages / runtimes
| Trigger | Skill |
|---|---|
| Python type-checking | `pyright-lsp` (if installed) |
| TypeScript / JavaScript | `typescript-lsp` |
| Go | `gopls-lsp` |
| C/C++ | `clangd-lsp` |
| Rust | `rust-analyzer-lsp` |
| Ruby | `ruby-lsp` |
| Java | `jdtls-lsp` |
| C# | `csharp-lsp` |
| Swift | `swift-lsp` |
| Kotlin | `kotlin-lsp` |
| PHP | `php-lsp` |

## AI / agents / LLM
| Trigger | Skill |
|---|---|
| Anthropic SDK / Claude API code | `claude-api` |
| LangChain / LangGraph | `langchain-skills:langchain-fundamentals`, `langchain-skills:langgraph-fundamentals` |
| LangChain RAG | `langchain-skills:langchain-rag` |
| LangGraph human-in-the-loop | `langchain-skills:langgraph-human-in-the-loop` |
| Deep Agents | `langchain-skills:deep-agents-core` + `-memory` + `-orchestration` |
| Pydantic AI | `pydantic-ai` |
| Atomic Agents framework | `atomic-agents` |
| Claude Agent SDK | `agent-sdk-dev` |
| Multi-source research | `deep-research` |

## Workflow / orchestration
| Trigger | Skill |
|---|---|
| Temporal workflows | `temporal:temporal-developer` |
| Recurring task | `loop`, `schedule` |
| Background subagents | `superpowers:dispatching-parallel-agents` |

## Frontend / UI
| Trigger | Skill |
|---|---|
| React / Vite / general FE | `frontend-design` |
| E2E browser testing | `playwright` (if installed), `chrome-devtools-mcp` |
| Launch / verify app | `run`, `verify` |

## Data / storage
| Trigger | Skill / MCP |
|---|---|
| PostgreSQL | `cloud-sql-postgresql`, `neon`, `supabase`, `prisma` |
| MySQL | `cloud-sql-mysql`, `planetscale` |
| ClickHouse | `clickhouse`, `clickhouse-best-practices` |
| MongoDB | `mongodb` |
| Redis | `redis-development` |
| BigQuery | `bigquery-data-analytics` |
| Vector: Pinecone / Qdrant / Zilliz | `pinecone`, `qdrant-skills`, `zilliz` |
| DuckDB | `duckdb-skills` |
| Neo4j | MCP: `mcp-neo4j-cypher` |
| OpenSearch | MCP: `opensearch-mcp-server-py` |

## Cloud / infra
| Trigger | Skill |
|---|---|
| AWS | `aws-core`, `aws-serverless`, `deploy-on-aws` |
| Azure | `azure`, `microsoft-docs` |
| GCP data | `data-agent-kit-starter-pack`, `dataproc`, `spanner` |
| Terraform | `terraform` |
| Cloudflare | `cloudflare` |
| Vercel / Netlify / Railway | `vercel`, `netlify-skills`, `railway` |

## DevOps / CI / VCS
| Trigger | Skill |
|---|---|
| GitHub PRs | `github`, `pr-review-toolkit`, `review` |
| GitLab | `gitlab` |
| Commit workflow | `commit-commands` |
| CI: Buildkite / TeamCity | `buildkite`, `teamcity-cli` |
| Azure DevOps | MCP: `@azure-devops/mcp` |
| SharePoint / M365 | MCP: `@softeria/ms-365-mcp-server` |

## Observability
| Trigger | Skill / MCP |
|---|---|
| Datadog | `datadog` |
| Sentry | `sentry`, `sentry-cli` |
| Logfire / Pydantic obs | `logfire` |
| OTel-first | `dash0` |
| LLM tracing & evals | `langfuse-observability`, `langfuse` |
| Prometheus | MCP: `pab1it0/prometheus-mcp-server` |
| Grafana | MCP: `mcp-grafana` |

## Security
| Trigger | Skill |
|---|---|
| Security review of changes | `security-review`, `security-guidance` |
| SAST / secrets | `semgrep`, `sonarqube`, `aikido` |
| API security audit | `42crunch-api-security-testing` |
| Supply-chain | `sonatype-guide`, `ai-plugins` (Endor) |
| DAST | `nightvision` |
| Auth (OAuth/OIDC) | `auth0`, `workos`, `duende-skills` |

## Documentation & writing
| Trigger | Skill |
|---|---|
| Generate docs | `sc:document`, `sc:index`, `mintlify` |
| Init CLAUDE.md | `init`, `claude-md-management` |
| Microsoft docs lookup | `microsoft-docs` |
| Library docs lookup | `context7` |

## Meta / skill management
| Trigger | Skill |
|---|---|
| Create / edit a skill | `write-a-skill`, `superpowers:writing-skills`, `skill-creator` |
| Configure settings.json | `update-config` |
| Reduce permission prompts | `fewer-permission-prompts` |
| Customize keybindings | `keybindings-help` |
| Caveman / token-saving mode | `caveman` |
| Generate session report | `session-report` |

---

## Marketplace search snippet (step 5)

Drop in the domain keywords:
```bash
python3 - <<'EOF'
import json, glob
TERMS = ["YOUR_DOMAIN_TERM_HERE"]
for path in glob.glob("/Users/jamesnyokabi/.claude/plugins/marketplaces/*/.claude-plugin/marketplace.json"):
    m = json.load(open(path))
    for p in m.get("plugins", []):
        text = (p["name"] + " " + p.get("description","")).lower()
        if any(t in text for t in TERMS):
            print(f"{m['name']}\t{p['name']}")
EOF
```

## Auto-install snippet (step 6)
After confirming a marketplace match exists:
```
/plugin install <plugin-name>@<marketplace-name>
```
Then re-scan the available-skills list and invoke the newly available skill via `Skill`.

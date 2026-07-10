# Supermetrics API — Bruno Collection

A ready-to-run [Bruno](https://www.usebruno.com/) collection for exploring the
Supermetrics APIs — **Management**, **Data Transfer Service (DTS)**,
**Discovery**, and **Data Query**. Every request ships with sample values and a
short description; fill in your credentials and run.

> All values in this collection are **samples/placeholders**. Replace IDs
> (accounts, transfers, workspaces, etc.) with ones from your own team — the
> `List …` requests in each folder are the easiest way to find them.

## Prerequisites

- The [Bruno desktop app](https://www.usebruno.com/downloads), **or** the Bruno
  CLI (`npm install -g @usebruno/cli`) to run requests from the terminal.
- A Supermetrics **API key** and your **Team ID**.

## Setup

1. Copy the example environment file and fill in your values:

   ```bash
   cp .env-example .env
   ```

2. Set the variables in `.env`:

   | Variable                 | Purpose                                                                    |
   |--------------------------|----------------------------------------------------------------------------|
   | `API_KEY`                | Bearer token for most requests, and the `api_key` for Data Query requests  |
   | `API_KEY_TEAM_MGMT`      | A key with team-management scope, used by Mgmt Teams/Workspaces requests    |
   | `TEAM_ID`                | Injected into `/teams/{team_id}/…` paths and query params                   |
   | `DS_USER`                | A data source login/username (optional; one Transformations request)       |
   | `BQ_SERVICE_ACCOUNT_KEY` | BigQuery service-account JSON (single-line string) for "Create destination - BQ" |

   `.env` is git-ignored, so your keys are never committed. **Never hard-code
   credentials into `.bru` files.**

3. Open the folder in the Bruno app, or run from the CLI:

   ```bash
   bru run --env .env "Query - Data API"     # run one folder
   bru run --env .env                          # run everything
   ```

## Authentication

- Most requests inherit a **Bearer token** (`API_KEY`) defined once in
  `collection.bru`.
- **Mgmt - Teams** and **Mgmt - Workspaces** override this to use
  `API_KEY_TEAM_MGMT` (a team-management-scoped key).
- **Data Query** requests use **no bearer**; they pass the key as an `api_key`
  query parameter instead.
- A few endpoints (**Mgmt - API Keys**, **Discovery / Search data sources for
  team**) require an **OAuth access token** rather than an API key — see the
  "Please note" in those requests.

## What's inside

| Folder | What it covers |
|--------|----------------|
| `Auth - Data Source Login Links` | Create/manage single-use OAuth login links |
| `Auth - Data Source Logins` | Inspect connected logins and their accounts |
| `Auth - Team Lists` | Centralised team lists (account-id lists) |
| `Discovery - Data Sources` | Data source catalogue, search, categories, tags |
| `Mgmt - API Keys` | API key management (OAuth-authenticated) |
| `Mgmt - Connector Builder` | Custom connector CRUD, secrets, logos, logs, schema |
| `Mgmt - Saved Queries` | List and retrieve saved queries |
| `Mgmt - Team Settings` | Team-level settings |
| `Mgmt - Teams` | Team details, users, roles, licenses, invites |
| `Mgmt - Workspaces` | Sub-workspaces, users, invites, license pools |
| `DWH - Destinations` | Warehouse destination config + connection test |
| `DWH - Transfers` | Transfer CRUD, validation, state, options |
| `DWH - Backfills` | Historical backfills |
| `DWH - Transfer Runs` | Transfer run history/status |
| `DWH - Table Groups` | Export/import table-group configs |
| `Query - Custom Fields` | Custom field CRUD + metadata |
| `Query - Data API` | Direct data queries, accounts, fields, batch, history |
| `Query - Data Blending` | Cross-source blend CRUD + querying |
| `Query - Transformations` | Field-level `transform` filters (Liquid syntax) |

## Tips

- **Find IDs fast:** run the `List …` request in a folder, copy an ID from the
  response, and paste it into the path/param of the related `Get`/`Update`
  request.
- **Data Query accounts:** use `Query - Data API / Get accounts` to find account
  IDs your key can access, then use them in the `Get data …` requests.
- Each request has a short description and, where relevant, a **"Please note"**
  with anything worth knowing before you run it.

## API base URLs

| API | Base URL |
|-----|----------|
| Management | `https://api.supermetrics.com/enterprise/v2` and `https://api.supermetrics.com/v1` |
| Data Transfer Service | `https://dts-api.supermetrics.com/v1` |
| Discovery | `https://api.supermetrics.com/datasource` |
| Data Query | `https://api.supermetrics.com/enterprise/v2/query` |

For full endpoint documentation see the
[Supermetrics API docs](https://docs.supermetrics.com/).

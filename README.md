# British Virgin Islands Company Registry MCP

Connect your AI assistant to about a million of British Virgin Islands (BVI) business companies and limited partnerships through [The Company Atlas](https://thecompanyatlas.com) and the Model Context Protocol.

Use it to confirm that an offshore entity named in a contract, filing or shareholder register exists, and when it was incorporated.

- Search by company name, BVI company number, incorporation date and address (usually the registered agent's office)
- Every record has a name and company number; about two thirds have an incorporation date and about 3% an address
- Entity type, status, directors and shareholders are not included

The MCP connection is provided by The Company Atlas. This repository does not run a separate server.

## Connect

```text
https://thecompanyatlas.com/mcp/bvi
```

Add this URL as a custom MCP connector in Claude, Cursor, or another MCP-compatible client. Sign in with Google when prompted.

- Transport: Streamable HTTP
- Auth: Google OAuth
- Docs: [thecompanyatlas.com/tools/bvi-company-registry](https://thecompanyatlas.com/tools/bvi-company-registry)

## Tools

### `BVI_search_companies`

Search BVI companies. Filters are combined with AND logic; include at least one.

| Parameter | Type | Description |
|---|---|---|
| `q` | string, optional | Company name substring, 3–120 characters |
| `address` | string, optional | Address substring, e.g. a registered agent such as `Trident Chambers` |
| `incorporatedFrom` / `incorporatedTo` | date, optional | Incorporation date range, `YYYY-MM-DD` |
| `page` / `limit` | integer, optional | Pagination, `limit` up to 50 (default 20) |

Returns `{ data, total, page, limit }`. `id` is `VG` + the BVI company number.

### `BVI_get_company`

One company by BVI company number (e.g. `1678725`, with or without the `VG` prefix), with former names where recorded.

| Parameter | Type | Description |
|---|---|---|
| `companyNumber` | string | BVI company number |

## Example prompts

- *"BVI companies with Holdings in the name incorporated in 2017."*
- *"Companies registered at Trident Chambers."*
- *"Look up BVI company number 1678725."*

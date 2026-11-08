# Better Stack MCP server

Review uptime coverage and create an approved status monitor. Read provider data first, then explicitly approve the selected change with operator write opt-in and a unique per-call approval key.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `BETTER_STACK_API_TOKEN`



Credential help: https://betterstack.com/docs/uptime/api/list-all-existing-monitors/

## Supported scope

- Global API tokens may require team_name. Monitor creation may enable provider notifications according to account policy.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call list_monitors '{}'
```

## Use with an MCP client

Launch `node /absolute/path/better-stack-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| list_monitors | Read | List monitors. |
| get_monitor | Read | Get monitor. |
| create_status_monitor | Explicit approval required | Create status monitor. |

## Concrete workflow

Review uptime coverage and create an approved status monitor. Read provider data first, then explicitly approve the selected change with operator write opt-in and a unique per-call approval key.

1. list_monitors
2. get_monitor
3. create_status_monitor

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=better-stack&integration=better-stack-mcp&utm_source=github&utm_campaign=github-better-stack-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/better-stack/).

## Provenance and maintenance

- https://betterstack.com/docs/uptime/api/list-all-existing-monitors/
- https://betterstack.com/docs/uptime/api/get-a-single-monitor/
- https://betterstack.com/docs/uptime/api/create-a-new-monitor/

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.

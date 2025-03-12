# Sentry MCP Server

A Model Context Protocol (MCP) server for interacting with Sentry. This MCP server provides tools to interact with the Sentry API, allowing AI assistants to retrieve and analyze error data, manage projects, and monitor application performance.

<a href="https://glama.ai/mcp/servers/sfel2251tz">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/sfel2251tz/badge" alt="Sentry Server MCP server" />
</a>

## Requirements

- Node.js (v14 or higher)
- npm or yarn
- Sentry account with API access
- Sentry authentication token with appropriate permissions

## Setup

1. Install dependencies:
   ```
   npm install
   ```

## Using this within an IDE 

This MCP has been verified to work against Codeium Windsurf.

Cursor is currently having issues with its MCP implementation; and this tool is not yet fully functional.

## Using with Claude

To use this MCP server with Claude, add the following configuration to your Claude settings:

```json
{
    "mcpServers": {
        "sentry": {
            "command": "npx",
            "args": ["ts-node", "/Users/<your-user-directory>/mcp-sentry-ts/index.ts"],
            "env": {
                "SENTRY_AUTH": "<YOUR_AUTH_TOKEN>"
            }
        }
    }
}
```

* Update with your directory path in the `args` field.
* Replace `<YOUR_AUTH_TOKEN>` with your Sentry authentication token.

## Available Tools

### list_projects

Lists all accessible Sentry projects for a given organization.

**Parameters:**
- `organization_slug` (string, required): The slug of the organization to list projects from
- `view` (string, optional): View type, either "summary" or "detailed" (default: "detailed")
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

### resolve_short_id

Retrieves details about an issue using its short ID.

**Parameters:**
- `organization_slug` (string, required): The slug of the organization the issue belongs to
- `short_id` (string, required): The short ID of the issue to resolve (e.g., PROJECT-123)
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

### get_sentry_event

Retrieves and analyzes a specific Sentry event from an issue.

**Parameters:**
- `issue_id_or_url` (string, required): Either a full Sentry issue URL or just the numeric issue ID
- `event_id` (string, required): The specific event ID to retrieve
- `view` (string, optional): View type, either "summary" or "detailed" (default: "detailed")
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

### list_error_events_in_project

Lists error events from a specific Sentry project.

**Parameters:**
- `organization_slug` (string, required): The slug of the organization the project belongs to
- `project_slug` (string, required): The slug of the project to list events from
- `view` (string, optional): View type, either "summary" or "detailed" (default: "detailed")
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

### create_project

Creates a new project in Sentry and retrieves its client keys.

**Parameters:**
- `organization_slug` (string, required): The slug of the organization to create the project in
- `team_slug` (string, required): The slug of the team to assign the project to
- `name` (string, required): The name of the new project
- `platform` (string, optional): The platform for the new project
- `view` (string, optional): View type, either "summary" or "detailed" (default: "detailed")
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

### list_project_issues

Lists issues from a specific Sentry project.

**Parameters:**
- `organization_slug` (string, required): The slug of the organization the project belongs to
- `project_slug` (string, required): The slug of the project to list issues from
- `view` (string, optional): View type, either "summary" or "detailed" (default: "detailed")
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

### list_issue_events

Lists events for a specific Sentry issue.

**Parameters:**
- `organization_slug` (string, required): The slug of the organization the issue belongs to
- `issue_id` (string, required): The ID of the issue to list events from
- `view` (string, optional): View type, either "summary" or "detailed" (default: "detailed")
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

### get_sentry_issue

Retrieves and analyzes a Sentry issue.

**Parameters:**
- `issue_id_or_url` (string, required): Either a full Sentry issue URL or just the numeric issue ID
- `view` (string, optional): View type, either "summary" or "detailed" (default: "detailed")
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

### list_organization_replays

Lists replays from a specific Sentry organization.

**Parameters:**
- `organization_slug` (string, required): The slug of the organization to list replays from
- `project_ids` (string[], optional): List of project IDs to filter replays by
- `environment` (string, optional): Environment to filter replays by
- `stats_period` (string, optional): Time period for stats (e.g., "24h", "7d")
- `start` (string, optional): Start date for filtering replays
- `end` (string, optional): End date for filtering replays
- `sort` (string, optional): Field to sort replays by
- `query` (string, optional): Search query to filter replays
- `per_page` (number, optional): Number of replays per page
- `cursor` (string, optional): Cursor for pagination
- `view` (string, optional): View type, either "summary" or "detailed" (default: "detailed")
- `format` (string, optional): Output format, either "plain" or "markdown" (default: "markdown")

## Running the Server

```
npx ts-node index.ts
```

## Authentication

This tool requires a Sentry authentication token with appropriate permissions to access the Sentry API. You can generate a token in your Sentry account settings under "API Keys".

## Error Handling

The server includes comprehensive error handling for:
- Missing authentication token
- API request failures
- Invalid parameters
- Network errors

All errors are logged to the console for debugging.
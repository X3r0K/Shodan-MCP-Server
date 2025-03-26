# shodan-mcp-server

This is a Model Context Protocol (MCP) server that provides access to the Shodan API. It allows you to programmatically query Shodan for information about devices, vulnerabilities, and more.

## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage with Node.js](#usage-with-nodejs)
- [API Documentation](#api-documentation)
  - [get_ip_info](#get_ip_info)
  - [dns_lookup](#dns_lookup)
  - [get_vulnerabilities](#get_vulnerabilities)
  - [cve_info](#cve_info)
  - [search](#search)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## Introduction

The `shodan-mcp-server` provides a simple way to integrate Shodan intelligence into your applications using the Model Context Protocol (MCP). It exposes several tools that allow you to query Shodan for various types of information.

## Features

Host Information: Get detailed information about an IP address
Search: Query Shodan's database using their search syntax
DNS Lookup: Resolve domain names
CVE Information: Get details about specific CVE vulnerabilities

## Installation

1.  Clone the repository:

    ```bash
    git clone https://github.com/X3r0K/Shodan-MCP-Server.git
    cd shodan-mcp-server
    ```

2.  Install the dependencies:

    ```bash
    npm install
    ```

3.  Build the project:

    ```bash
    npm run build
    ```

## Configuration

1.  Obtain a Shodan API key from [Shodan](https://account.shodan.io/).
2.  Configure the MCP server in your MCP settings file (e.g., `~/.config/mcp/settings.json`):

    ```json
    {
      "mcpServers": {
        "shodan": {
          "command": "node",
          "args": ["/path/to/shodan-mcp-server/build/index.js"],
          "env": {
            "SHODAN_API_KEY": "<your_shodan_api_key>"
          },
          "disabled": false,
          "autoApprove": []
        }
      }
    }
    ```

    Replace `<your_shodan_api_key>` with your actual Shodan API key and `/path/to/shodan-mcp-server` with the actual path to the shodan-mcp-server directory.

## Usage with Node.js

You can use the MCP server with Node.js using the `@modelcontextprotocol/sdk` package.

1.  Install the MCP SDK:

    ```bash
    npm install @modelcontextprotocol/sdk
    ```

2.  Use the `use_mcp_tool` function to call the tools:

    ```javascript
    import { use_mcp_tool } from '@modelcontextprotocol/sdk';

    async function getIpInfo(ip) {
      const result = await use_mcp_tool('shodan', 'get_ip_info', { ip });
      console.log(result);
    }

    getIpInfo('8.8.8.8');
    ```

## API Documentation

### get\_ip\_info

Get information about a specific IP address.

**Input:**

```json
{
  "ip": "string" // The IP address to query
}
```

**Output:**

A JSON object containing information about the IP address.

### dns\_lookup

Perform DNS lookups for a given domain.

**Input:**

```json
{
  "hostname": "string" // The hostname to resolve
}
```

**Output:**

A JSON object containing the resolved IP address.

### get\_vulnerabilities

Track vulnerabilities associated with a specific IP address.

**Input:**

```json
{
  "ip": "string" // The IP address to query for vulnerabilities
}
```

**Output:**

A JSON object containing a list of vulnerabilities associated with the IP address.

### cve\_info

Retrieve information about a specific CVE ID.

**Input:**

```json
{
  "cve": "string" // The CVE ID to query
}
```

**Output:**

A JSON object containing information about the CVE ID.

### search

Search Shodan for devices matching a query.

**Input:**

```json
{
  "query": "string" // The search query
}
```

**Output:**

A JSON object containing a list of devices matching the query.

## Project Structure

```
shodan-mcp-server/
├── .gitignore
├── package.json
├── README.md
├── tsconfig.json
└── src/
    ├── index.ts
    └── index.mts
```

## License

MIT

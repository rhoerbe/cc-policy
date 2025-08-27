# MCP Server Setup and Tools Guide
# =============================

## Context 7
**Usage**: lookup documentation. Use carefully, because it retrieves large amounts of data.
**Setup**: claude mcp add context7 -- npx -y @upstash/context7-mcp@latest

## Browser MCP
**Usage**: Automate browser interactions, web scraping, and testing.
  - User needs to manually "connect" a browser tab to the MCP server:
  - Open the website you want Claude to interact with in your browser.
  - Click the Browser MCP extension icon in your browser's toolbar.
  - Click the "Connect" button. The icon should change to indicate that the tab is now connected.
**Setup**: claude mcp add --scope user browsermcp npx @browsermcp/mcp@latest  # available to all projects of the user

## Template
**Usage**: 
**Setup**: 

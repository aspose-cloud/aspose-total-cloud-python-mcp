# Aspose Cloud MCP Servers

Give an AI assistant (Claude Desktop, Claude Code, VS Code, Cursor, Cline, Windsurf, or any other
[MCP](https://modelcontextprotocol.io) client) the ability to work with documents through
[Aspose Cloud](https://products.aspose.cloud/): convert, read, edit, merge and split Word, Excel,
PowerPoint, PDF and e-mail files, and manage the files in Aspose cloud storage.

This repository is the **index**. Each product has its own server in its own repository; you install
only the ones you need.

> **Why one server per product, not one big server?** An assistant picks the right tool more reliably
> from a few dozen focused tools than from hundreds in one list. Every server also bundles the four
> shared file tools (upload, download, list, delete), so a single server is enough for a complete
> upload → process → download workflow.

## The servers

| Product | Repository | Command | What it does |
|---|---|---|---|
| **Aspose.Words Cloud** | [aspose-words-cloud-python-mcp](https://github.com/aspose-cloud/aspose-words-cloud-python-mcp) | `aspose-words-mcp` | Convert, compare, replace text, read comments, bookmarks, properties and statistics of Word documents |
| **Aspose.Cells Cloud** | [aspose-cells-cloud-python-mcp](https://github.com/aspose-cloud/aspose-cells-cloud-python-mcp) | `aspose-cells-mcp` | Read and edit workbooks: cells, ranges, charts, pivot tables, formatting, protection, conversion, merge and split |
| **Aspose.Slides Cloud** | [aspose-slides-cloud-python-mcp](https://github.com/aspose-cloud/aspose-slides-cloud-python-mcp) | `aspose-slides-mcp` | Create, convert, split presentations; read slides, text and images; replace text |
| **Aspose.PDF Cloud** | [aspose-pdf-cloud-python-mcp](https://github.com/aspose-cloud/aspose-pdf-cloud-python-mcp) | `aspose-pdf-mcp` | Merge PDFs, convert PDF to Word, read document properties |
| **Aspose.Email Cloud** | [aspose-email-cloud-python-mcp](https://github.com/aspose-cloud/aspose-email-cloud-python-mcp) | `aspose-email-mcp` | Convert and read e-mail, contacts and calendars; work with a mailbox (folders, messages, threads) |
| *Shared file tools* | [aspose-storage-cloud-python-mcp](https://github.com/aspose-cloud/aspose-storage-cloud-python-mcp) | – | A library, not a server: the upload / download / list / delete tools every server above bundles |

Every tool that a server offers has been run against a document whose contents are known, and its
output checked. Tools that could not be proven are not offered. The product READMEs list their tools.

## Install

You need Python 3.11 or later and an [Aspose Cloud](https://dashboard.aspose.cloud/) account
(a free evaluation tier is available). Create an application on the dashboard's *Applications* page
to get a **Client ID** and a **Client Secret**.

```bash
python -m venv .venv
# Windows:  .venv\Scripts\activate
# macOS / Linux:  source .venv/bin/activate

pip install \
  git+https://github.com/aspose-cloud/aspose-storage-cloud-python-mcp.git@v1.0.5 \
  git+https://github.com/aspose-cloud/aspose-words-cloud-python-mcp.git@v2.0.1 \
  git+https://github.com/aspose-cloud/aspose-cells-cloud-python-mcp.git@v2.2.0 \
  git+https://github.com/aspose-cloud/aspose-slides-cloud-python-mcp.git@v1.0.3 \
  git+https://github.com/aspose-cloud/aspose-pdf-cloud-python-mcp.git@v1.1.4 \
  git+https://github.com/aspose-cloud/aspose-email-cloud-python-mcp.git@v1.4.0
```

Install the first line plus only the products you want. The first package is the shared file-tool
library every server depends on; it is not on PyPI, so it is installed from GitHub in the same command.

Each command installs one released version of that server (the `@vX.Y.Z` after the repository name), not
whatever is on the repository's default branch. To upgrade, change the version to a newer release of that
repository (see its *Releases* page) and run the command again with `--upgrade`.

This puts one command per product into the virtual environment: `aspose-words-mcp`,
`aspose-cells-mcp`, `aspose-slides-mcp`, `aspose-pdf-mcp`, `aspose-email-mcp`.

## Add them to your MCP client

Credentials are never passed as a tool argument. Each server reads `ASPOSE_CLIENT_ID` and
`ASPOSE_CLIENT_SECRET` from its environment when it starts. Set `ASPOSE_FILES_PATH` to the folder on
your computer that the servers may read local files from and write results to (each server refuses
paths outside it).

### Claude Desktop

Edit `claude_desktop_config.json` (Windows: `%APPDATA%\Claude\`, macOS:
`~/Library/Application Support/Claude/`), then fully quit and restart Claude Desktop.
On macOS / Linux replace `C:\\path\\to\\.venv\\Scripts\\NAME.exe` with `/path/to/.venv/bin/NAME`.

```json
{
  "mcpServers": {
    "aspose-words": {
      "command": "C:\\path\\to\\.venv\\Scripts\\aspose-words-mcp.exe",
      "env": {
        "ASPOSE_CLIENT_ID": "your-client-id",
        "ASPOSE_CLIENT_SECRET": "your-client-secret",
        "ASPOSE_FILES_PATH": "C:\\Users\\you\\Documents\\aspose-files"
      }
    },
    "aspose-cells": {
      "command": "C:\\path\\to\\.venv\\Scripts\\aspose-cells-mcp.exe",
      "env": {
        "ASPOSE_CLIENT_ID": "your-client-id",
        "ASPOSE_CLIENT_SECRET": "your-client-secret",
        "ASPOSE_FILES_PATH": "C:\\Users\\you\\Documents\\aspose-files"
      }
    },
    "aspose-pdf": {
      "command": "C:\\path\\to\\.venv\\Scripts\\aspose-pdf-mcp.exe",
      "env": {
        "ASPOSE_CLIENT_ID": "your-client-id",
        "ASPOSE_CLIENT_SECRET": "your-client-secret",
        "ASPOSE_FILES_PATH": "C:\\Users\\you\\Documents\\aspose-files"
      }
    },
    "aspose-email": {
      "command": "C:\\path\\to\\.venv\\Scripts\\aspose-email-mcp.exe",
      "env": {
        "ASPOSE_CLIENT_ID": "your-client-id",
        "ASPOSE_CLIENT_SECRET": "your-client-secret",
        "ASPOSE_FILES_PATH": "C:\\Users\\you\\Documents\\aspose-files"
      }
    },
    "aspose-slides": {
      "command": "C:\\path\\to\\.venv\\Scripts\\aspose-slides-mcp.exe",
      "env": {
        "ASPOSE_CLIENT_ID": "your-client-id",
        "ASPOSE_CLIENT_SECRET": "your-client-secret",
        "ASPOSE_FILES_PATH": "C:\\Users\\you\\Documents\\aspose-files"
      }
    }
  }
}
```

Add only the entries for the servers you installed.

### VS Code, Cursor, Cline, Windsurf

The same entries, with a `"type": "stdio"` line, under a `"servers"` key (VS Code: `.vscode/mcp.json`)
or `"mcpServers"` (Cursor: `~/.cursor/mcp.json`):

```json
{
  "servers": {
    "aspose-pdf": {
      "type": "stdio",
      "command": "/path/to/.venv/bin/aspose-pdf-mcp",
      "env": {
        "ASPOSE_CLIENT_ID": "your-client-id",
        "ASPOSE_CLIENT_SECRET": "your-client-secret",
        "ASPOSE_FILES_PATH": "/home/you/aspose-files"
      }
    }
  }
}
```

### Try it

Put a file in your `ASPOSE_FILES_PATH` folder and ask, for example:

- *"Upload `report.pdf`, tell me its title and author, then convert it to Word and download it."*
- *"Merge `4pages.pdf` and `5pages.pdf` and tell me how many pages the result has."*
- *"In `sales.xlsx`, read the first five rows of the Sales sheet and add a chart title."*

## About this project

These servers are generated and kept current by an automated pipeline from Aspose Cloud's published
API specifications. Each release is checked against the live API before it is published, and rolled
back automatically if a post-release check fails. Please report problems in the repository of the
product concerned.

## License

MIT for the code in these repositories. It does **not** cover, and grants no rights to, the Aspose
Cloud products or APIs themselves, which remain governed by
[Aspose's own product and usage terms](https://purchase.aspose.cloud/policies). A valid Aspose Cloud
account is required to call the API.

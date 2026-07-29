---
name: topgit
description: "Trigger: search bookmarks, find projects, look up tools, search links, browse TOPGit, search saved URLs. Search and browse TOPGit bookmarks using natural language via the public API."
license: Apache-2.0
metadata:
  author: topgit
  version: "1.0"
  url: "https://topgit.us"
---

## What is TOPGit?

TOPGit is a bookmark manager for developers. It collects and organizes useful GitHub and GitLab repositories shared by the community.

## API

Base URL: `https://topgit.us/api`

All endpoints are read-only. No authentication required.

### Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/search?q=<query>&tag=<tag>&limit=<n>&offset=<n>` | Search bookmarks by keywords and/or tag |
| GET | `/all?limit=<n>&offset=<n>` | List all bookmarks (paginated, max 500 per page) |
| GET | `/tags` | List all tags with bookmark counts |
| GET | `/stats` | Cache status and bookmark count |

### Search Parameters

- `q` — Natural language or keyword query. Matches against title, description, URL, and tags.
- `tag` — Filter by tag name (without `#`). Example: `ai`, `cybersecurity`
- `limit` — Max results to return (default: 10, max: 50)
- `offset` — Pagination offset

### Response Format

```json
{
  "query": "docker",
  "tag": null,
  "count": 5,
  "total": 32,
  "results": [
    {
      "id": 585,
      "url": "https://github.com/...",
      "title": "Project Name",
      "description": "Short description...",
      "tag_names": ["docker", "devops"],
      "date_added": "2025-08-11T12:21:25.235781Z"
    }
  ]
}
```

## Usage for AI Agents

When a user asks to search for projects, tools, or repositories:

1. Extract keywords from the natural language request
2. Call the API: `curl -s "https://topgit.us/api/search?q=<keywords>&limit=10"`
3. Present results with title, URL, description, and tags
4. Offer to search more or browse by tag

### Examples

```bash
# Search for Docker tools
curl -s "https://topgit.us/api/search?q=docker+containers&limit=5"

# Search by tag
curl -s "https://topgit.us/api/search?tag=cybersecurity&limit=10"

# List all tags
curl -s "https://topgit.us/api/tags"

# Get all bookmarks
curl -s "https://topgit.us/api/all?limit=100"
```

## Hard Rules

- Always use `https://topgit.us/api` as the base URL
- Present results with: title, URL, description, and tags
- Default to 10 results; fetch more if the user asks
- Use the user's language for presentation
- If no results, suggest trying different keywords or browsing by tag

## Links

- Web: https://topgit.us
- API: https://topgit.us/api
- Telegram: https://t.me/TOPGitUS

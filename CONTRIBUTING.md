# Contributing to Obul APIs

Thank you for your interest in contributing! This guide walks you through adding new API skills to the Obul marketplace.

## What You Can Contribute

- **New skills** - Add documentation for APIs that work with the Obul proxy
- **Improvements** - Fix typos, clarify docs, improve examples
- **Bug fixes** - Correct pricing, endpoints, or other inaccuracies

## Quick Start

Adding a new skill involves 3 steps:

1. Create `skills/obul-<name>/SKILL.md`
2. Add entry to `apis.json`
3. Update category table in `README.md`

---

## Step 1: Create the SKILL.md File

### Directory Structure

```
skills/
└── obul-<service-name>/
    └── SKILL.md
```

### SKILL.md Template

```markdown
---
name: obul-<service-name>
description: Brief 1-2 sentence description of what this API does
homepage: https://example.com
metadata:
  obul-skill:
    emoji: "🔧"
    requires:
      env: ["OBUL_API_KEY"]
    primaryEnv: "OBUL_API_KEY"
registries: {}
---

# ServiceName

Overview paragraph describing the service and its capabilities through the Obul proxy.

## Authentication

All requests route through the Obul proxy and require an API key header:

```json
{
  "headers": {
    "Content-Type": "application/json",
    "x-obul-api-key": "{{OBUL_API_KEY}}"
  }
}
```

**Base URL:** `https://proxy.obul.ai/proxy/https/<upstream-host>/api`

## Common Operations

### Operation Name

Brief description of what this operation does.

**Pricing:** $0.01

```json
{
  "method": "POST",
  "url": "https://proxy.obul.ai/proxy/https/<upstream-host>/api/endpoint",
  "headers": {
    "Content-Type": "application/json",
    "x-obul-api-key": "{{OBUL_API_KEY}}"
  },
  "body": {
    "param": "value"
  }
}
```

**Response:** Description of the response fields

### Another Operation

...

### Health Check (Free)

Verify service availability before spending credits.

**Pricing:** $0.00

```json
{
  "method": "GET",
  "url": "https://proxy.obul.ai/proxy/https/<upstream-host>/api/health",
  "headers": {
    "x-obul-api-key": "{{OBUL_API_KEY}}"
  }
}
```

## Endpoint Pricing Reference

| Endpoint | Price | Purpose |
|----------|-------|---------|
| `GET /api/health` | $0.00 | Service status check |
| `POST /api/endpoint` | $0.01 | Operation description |

## When to Use

- Use case 1: When you need to...
- Use case 2: For...

## Best Practices

1. **Tip one:** Explanation
2. **Tip two:** Explanation

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `ERROR_CODE` | What caused it | How to fix it |
```

---

## Required Conventions

### 1. Naming

- **Skill name**: Must start with `obul-` prefix (e.g., `obul-chronos`, `obul-sybil`)
- **Directory name**: Matches skill name (`obul-<service>/`)
- **YAML frontmatter `name`**: Must match directory name

### 2. YAML Frontmatter

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Skill identifier (kebab-case, starts with `obul-`) |
| `description` | Yes | 1-2 sentence summary |
| `homepage` | Yes | Service homepage URL |
| `metadata.obul-skill.emoji` | Yes | Visual identifier (emoji) |
| `metadata.obul-skill.requires.env` | Yes | Must include `OBUL_API_KEY` |
| `metadata.obul-skill.primaryEnv` | Yes | Must be `OBUL_API_KEY` |
| `registries` | Yes | Must include `registries: {}` |

### 3. Title Format

- Use `# ServiceName` — not `# ServiceName Operations`
- Match the service name in the homepage (e.g., `# Chronos`, not `# Chronos Time`)

### 4. Authentication Section

Every skill MUST have an Authentication section with:
- Standard JSON headers showing `x-obul-api-key` and `Content-Type`
- The **Base URL** for the service

### 5. Pricing Format

Always use **dollar amounts**, never credits:

| Tier | Price | Use Case |
|------|-------|----------|
| Free | $0.00 | Health checks, status endpoints |
| Polling | $0.0001 | Async status polling |
| Simple | $0.001–$0.01 | Basic queries, retrieval |
| Complex | $0.01–$0.05 | AI-powered operations |
| Heavy | $0.05+ | Long-running tasks |

### 6. Required Sections

Every SKILL.md must include:
1. **Authentication** — Base URL + headers (REQUIRED)
2. **Common Operations** — At least 2-3 operations with pricing
3. **Endpoint Pricing Reference** — Table of all endpoints
4. **When to Use** — Use cases
5. **Best Practices** — Tips
6. **Error Handling** — Error codes + solutions

### 7. Request Examples

- Use full Obul proxy URLs: `https://proxy.obul.ai/proxy/https/<host>/api/...`
- Include `x-obul-api-key` in headers
- Show realistic example values (not placeholders)

---

## Step 2: Update apis.json

Add your API to the `apis` array in alphabetical order within its category:

```json
{
  "name": "service-name",
  "category": "infrastructure",
  "skill": "obul-service-name",
  "description": "Brief description",
  "homepage": "https://example.com"
}
```

### Category Options

- `infrastructure`
- `web-scraping`
- `web-search`
- `social-media`
- `blockchain-defi`
- `image-audio-video`
- `security-risk`
- `lead-enrichment`
- `weather-data`

---

## Step 3: Update README.md

Add your API to the category table:

```markdown
| **Category** | APIs |
|-------------|------|
| **CategoryName** | ExistingAPI, NewAPI |
```

---

## Review Checklist

Before submitting a PR, verify:

- [ ] SKILL.md follows the template structure
- [ ] Name starts with `obul-` prefix
- [ ] Frontmatter includes `metadata.obul-skill` with emoji and OBUL_API_KEY
- [ ] Frontmatter includes `registries: {}`
- [ ] Title is `# ServiceName` (not `# ServiceName Operations`)
- [ ] **Authentication section exists** with Base URL and headers
- [ ] All operations have pricing in dollar format ($0.00)
- [ ] Request examples use full proxy URLs
- [ ] Endpoint Pricing Reference table is complete
- [ ] Entry added to `apis.json` in correct category
- [ ] Entry added to `README.md` category table
- [ ] No placeholder text or TODO comments

---

## Reference

For a detailed guide on writing skills, see:
[How to Write Obul Skills](https://github.com/dpbmaverick98/Agent_Army_Skills/blob/main/Agent_Army_Skills_Obul/how-to-write-obul-skills.md)

For examples, browse existing skills in `skills/`.

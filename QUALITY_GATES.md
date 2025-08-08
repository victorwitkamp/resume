# Quality Gates

This repository includes automated quality gates to ensure professional and reliable content.

## Implemented Quality Checks

### 1. **Markdownlint** - Markdown Formatting Standards
- **Tool**: `markdownlint-cli`
- **Configuration**: `.markdownlint.json`
- **Purpose**: Ensures consistent Markdown formatting across all source files
- **Runs on**: All `src/*.md` files

#### Key Rules Enforced:
- **ATX-style headers** (`#` instead of underlined headers)
- **Consistent indentation** (2 spaces for lists)
- **Line length limits** (120 characters with exceptions for tables)
- **Allowed HTML elements** (only `<br>`, `<img>`, `<a>` for resume formatting)
- **Sibling-only duplicate headers** (allows repeated section names in different contexts)

### 2. **Lychee** - Link Validation
- **Tool**: `lychee`
- **Configuration**: `.lycheerc.toml`
- **Purpose**: Validates all external links to prevent broken URLs in published resume
- **Runs on**: All `src/*.md` files

#### Link Checking Features:
- **HTTP status validation** (accepts 200-308 status codes)
- **Concurrent requests** (up to 10 simultaneous checks for speed)
- **Retry logic** (3 retries for temporary failures)
- **Timeout protection** (20-second timeout per request)
- **Smart exclusions** (skips localhost, private IPs, mailto links, relative file paths)
- **Caching** (1-hour cache to avoid repeated requests)

## Quality Gate Behavior

### Non-Blocking Mode
Currently configured with `continue-on-error: true` to:
- ✅ **Report issues** without stopping the build
- ✅ **Allow content updates** even with minor quality issues
- ✅ **Provide feedback** for continuous improvement

### Making Quality Gates Blocking
To enforce strict quality standards, remove `continue-on-error: true` from the workflow steps. This will:
- 🛑 **Stop the build** if links are broken
- 🛑 **Prevent deployment** if Markdown formatting is inconsistent
- 🛑 **Require fixes** before content can be published

## Configuration Files

### `.markdownlint.json`
```json
{
  "default": true,
  "MD013": { "line_length": 120 },
  "MD033": { "allowed_elements": ["br", "img", "a"] },
  "MD041": false
}
```

### `.lycheerc.toml`
```toml
max_concurrency = 10
timeout = 20
max_retries = 3
accept = [200, 201, 204, 206, 300, 301, 302, 303, 304, 307, 308]
```

## Local Testing

### Test Markdown Formatting
```bash
npx markdownlint src/*.md --config .markdownlint.json
```

### Test Link Validity
```bash
# Install lychee (one-time setup)
cargo install lychee

# Check links
lychee src/*.md --config .lycheerc.toml
```

## Benefits

1. **Professional Appearance**: Consistent formatting ensures resume looks polished
2. **Reliability**: Working links maintain credibility and user experience
3. **Automated Quality**: Catches issues before they reach production
4. **Version Control**: Quality standards are enforced across all changes
5. **Maintainability**: Clear configuration makes standards easy to understand and modify

## Troubleshooting

### Common Markdownlint Issues
- **MD013**: Line too long → Break long lines or update config
- **MD033**: Disallowed HTML → Use only `<br>`, `<img>`, `<a>` tags
- **MD024**: Duplicate header → Use unique headers or enable `siblings_only`

### Common Link Issues
- **404 Not Found**: Update or remove broken links
- **Timeout**: Check if external sites are temporarily down
- **Certificate errors**: Update lychee config if needed for specific domains

The quality gates help maintain a professional, reliable resume while providing clear feedback for improvements.

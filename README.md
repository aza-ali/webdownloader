# Web Downloader CLI

[![npm version](https://img.shields.io/npm/v/web-downloader-cli?style=flat-square&logo=npm&logoColor=white)](https://www.npmjs.com/package/web-downloader-cli)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)
[![Node](https://img.shields.io/badge/node-%3E%3D14-43853d?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org)

A terminal tool for archiving complete web pages (HTML, CSS, JavaScript, images, fonts) for offline viewing or markdown export.

`wget` grabs the file. `curl` fetches the bytes. `web-downloader` captures the **whole page**: rewrites links to local paths, follows the asset graph, and ships you a working offline copy or a clean markdown export.

## Features

- Downloads HTML, CSS, JavaScript, images, and other assets
- Rewrites links to local references so pages work offline
- Optional conversion to Markdown
- Configurable depth for following links
- `robots.txt` modes: obey, warn, or ignore
- Follows redirects automatically
- Respects `crawl-delay` directives
- Programmatic API for use as a Node.js module

## Install

```bash
npm install -g web-downloader-cli
```

## Usage

```bash
web-downloader https://example.com
```

### Options

```
  -h, --help              Show help message
  -o, --output <dir>      Output directory (default: ./downloaded-site)
  --no-assets             Skip CSS, JS, images, and other assets
  -f, --follow-links      Follow and download linked pages
  -d, --depth <n>         Maximum link-follow depth (default: 1)
  -m, --markdown          Convert HTML to Markdown
  -r, --robots <mode>     How to handle robots.txt (default: ignore)
                          ignore - skip robots.txt entirely
                          obey   - respect rules, skip blocked URLs
                          warn   - warn but proceed
```

### Examples

```bash
# Single page with all assets
web-downloader https://example.com

# Convert to Markdown
web-downloader -m https://example.com/article

# Follow linked pages, depth 2, custom output
web-downloader -f -d 2 -o ./my-site https://example.com

# Multiple pages in one run
web-downloader https://example.com/page1 https://example.com/page2

# HTML only, skip assets
web-downloader --no-assets https://example.com

# Respect robots.txt
web-downloader -r obey -f https://example.com
```

## Programmatic API

```javascript
const WebDownloader = require('web-downloader-cli');

const downloader = new WebDownloader({
  outputDir: './my-downloads',
  includeAssets: true,
  followLinks: true,
  maxDepth: 2,
  markdown: false,
  robotsTxt: 'obey'
});

downloader.download('https://example.com');
```

## When to use what

| You want to... | Reach for |
|---|---|
| Download a single file | `curl` or `wget` |
| Mirror a static site | `wget --mirror` |
| Save one page to read offline (with images, working CSS) | **`web-downloader`** |
| Save a page as Markdown for LLM ingestion | **`web-downloader -m`** |
| Crawl a JS-heavy site | A real browser tool (Playwright, Puppeteer) |

## License

MIT

## Contributing

PRs welcome. Open an issue first for anything substantial.

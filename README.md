# Web Downloader CLI

A powerful terminal tool for downloading complete web pages with all their assets for offline viewing.

## Features

- Downloads HTML, CSS, JavaScript, images, and other assets
- Converts links to local references for offline viewing
- Supports multiple output formats
- Optional conversion to markdown
- Customizable depth for following links
- robots.txt compliance checking (obey, warn, or ignore)
- Follows redirects automatically
- Respects crawl-delay directives

## Installation

```bash
npm install -g web-downloader-cli
```

## Usage

### Basic Usage

```bash
# Download a single page with all assets
web-downloader https://example.com
```

### Options

```
  -h, --help              Show help message
  -o, --output <dir>      Output directory (default: ./downloaded-site)
  --no-assets             Don't download CSS, JS, images, etc.
  -f, --follow-links      Follow and download linked pages
  -d, --depth <n>         Maximum depth for following links (default: 1)
  -m, --markdown          Convert HTML to Markdown
  -r, --robots <mode>     How to handle robots.txt (default: ignore)
                          ignore - Completely ignore robots.txt
                          obey   - Respect robots.txt rules (skip blocked URLs)
                          warn   - Show warnings but download anyway
```

### Examples

```bash
# Download a single page with all assets
web-downloader https://example.com

# Download and convert to markdown
web-downloader -m https://example.com/article

# Download a site with linked pages (max depth 2)
web-downloader -f -d 2 -o ./my-site https://example.com

# Download multiple pages
web-downloader https://example.com/page1 https://example.com/page2

# Download page without assets
web-downloader --no-assets https://example.com

# Respect robots.txt restrictions
web-downloader -r obey -f https://example.com

# Show warnings for robots.txt violations but continue
web-downloader -r warn -f https://example.com
```

## Use as a Module

You can also use this tool programmatically in your Node.js projects:

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

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Issues

If you encounter any problems, please file an issue on GitHub.

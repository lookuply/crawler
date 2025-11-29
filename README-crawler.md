# Lookuply Crawler

**Privacy-first web crawler supporting 24 EU languages**

Part of the [Lookuply](https://github.com/lookuply) open-source search engine project.

---

## Overview

The Lookuply Crawler is a distributed web crawler built with Python and Scrapy that respects robots.txt, implements polite crawling practices, and supports all 24 official EU languages from day one.

### Key Features

- **24 EU Languages Support**: Bulgarian, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, German, Greek, Hungarian, Irish, Italian, Latvian, Lithuanian, Maltese, Polish, Portuguese, Romanian, Slovak, Slovenian, Spanish, Swedish
- **Privacy-First**: No user tracking, open-source, transparent crawling
- **Distributed Architecture**: Redis-based URL queue for horizontal scaling
- **Respectful Crawling**: robots.txt compliance, configurable delays, user-agent identification
- **Language Detection**: Automatic content language detection using fastText
- **Metadata Extraction**: Title, description, links, publication date

---

## Architecture

```
┌─────────────┐
│   Scrapy    │
│   Crawler   │
└──────┬──────┘
       │
       ├─→ Redis Queue (URLs)
       │
       ├─→ Language Detection
       │
       └─→ Storage (crawled content)
```

---

## Technology Stack

- **Python 3.11+**
- **Scrapy**: Web crawling framework
- **Redis**: URL queue and deduplication
- **fastText**: Language detection
- **BeautifulSoup**: HTML parsing
- **Docker**: Containerization

---

## Getting Started

### Prerequisites

```bash
- Python 3.11+
- Redis server
- Docker (optional)
```

### Installation

```bash
# Clone repository
git clone https://github.com/lookuply/crawler.git
cd crawler

# Install dependencies
pip install -r requirements.txt

# Configure crawler
cp config.example.yml config.yml
# Edit config.yml with your settings
```

### Running Locally

```bash
# Start Redis
docker run -d -p 6379:6379 redis:7

# Run crawler
python -m scrapy crawl web_crawler
```

### Running with Docker

```bash
# Build image
docker build -t lookuply/crawler .

# Run container
docker run -d \
  -e REDIS_HOST=redis \
  -e CRAWL_LANGUAGES=en,de,fr \
  lookuply/crawler
```

---

## Configuration

Key configuration options in `config.yml`:

```yaml
languages:
  - en  # English
  - de  # German
  - fr  # French
  # ... all 24 EU languages

politeness:
  download_delay: 1.0  # seconds
  concurrent_requests: 16
  respect_robots_txt: true

storage:
  output_format: jsonl
  compression: gzip
```

---

## Development

### Project Structure

```
crawler/
├── scrapy.cfg           # Scrapy config
├── crawler/
│   ├── spiders/         # Spider implementations
│   ├── pipelines.py     # Data processing pipelines
│   ├── items.py         # Data models
│   └── settings.py      # Crawler settings
├── tests/               # Unit tests
└── docker/              # Docker configuration
```

### Running Tests

```bash
pytest tests/
```

### Code Style

```bash
# Format code
black crawler/

# Lint
flake8 crawler/
```

---

## Contributing

We welcome contributions! Please see our [Contributing Guidelines](https://github.com/lookuply/.github/blob/main/CONTRIBUTING.md).

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## License

This project is licensed under the **GNU General Public License v3.0** - see the [LICENSE](LICENSE) file for details.

---

## Related Projects

- [lookuply/indexer](https://github.com/lookuply/indexer) - Content indexing
- [lookuply/search-api](https://github.com/lookuply/search-api) - Search API
- [lookuply/frontend](https://github.com/lookuply/frontend) - Web interface
- [lookuply/docs](https://github.com/lookuply/docs) - Documentation

---

## Links

- **Website**: [lookuply.info](https://lookuply.info)
- **Documentation**: [docs.lookuply.info](https://docs.lookuply.info)
- **API**: [api.lookuply.info](https://api.lookuply.info)

---

**Built with privacy in mind. Supporting all 24 EU languages from day one.**

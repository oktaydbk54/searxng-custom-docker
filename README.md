```markdown
# SearXNG Custom Docker Setup

A customized SearXNG deployment using Docker Compose, with Redis for caching and configurable settings for enhanced privacy and functionality.

![SearXNG](https://github.com/searxng/searxng/raw/master/docs/searxng.png)

## Features

- Self-hosted, privacy-respecting meta-search engine.
- Redis-based caching for improved performance.
- Customizable settings via `settings.yml` and `limiter.toml`.
- Easy deployment with Docker Compose.

## Prerequisites

- Docker installed ([Install Guide](https://docs.docker.com/engine/install/))
- Docker Compose installed ([Install Guide](https://docs.docker.com/compose/install/))
- Basic terminal/command-line knowledge.

## Quick Start

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/oktaydbk54/searxng-custom-docker
   cd searxng-custom-docker
   ```

2. **Configure Environment Variables (Optional)**:
   Create a `.env` file to override default settings (e.g., instance name, domain):
   ```env
   INSTANCE_NAME=my-searxng
   SERVICE_FQDN_SEARXNG_8080=https://search.example.com
   SERVICE_PASSWORD_SEARXNGSECRET=your-strong-secret
   ```

3. **Start the Services**:
   ```bash
   docker-compose up -d
   ```

4. **Access SearXNG**:
   Open your browser at [http://localhost:8080](http://localhost:8080) (or your configured domain).

## Configuration

### Key Files
- **`docker-compose.yml`**: Defines the SearXNG and Redis services.
- **`settings.yml`**: Configures search formats, image proxy, and UI settings.
- **`limiter.toml`**: Enables bot detection via `link_token` to mitigate abuse.

### Customization
1. **Instance Settings**:
   - Modify `.env` or environment variables in `docker-compose.yml` to set:
     - `INSTANCE_NAME`: Name of your instance.
     - `BASE_URL`: Public URL for your SearXNG instance.
     - `SEARXNG_SECRET`: Secret key for security (change this in production!).

2. **Search Preferences**:
   Edit `settings.yml` to:
   - Enable/disable search formats (HTML, CSV, JSON, RSS).
   - Toggle the image proxy (`server.image_proxy`).

3. **Rate Limiting**:
   Adjust `limiter.toml` to fine-tune bot detection and rate limiting.

## Maintenance

### Update Containers
```bash
docker-compose pull
docker-compose up -d
```

### View Logs
```bash
docker-compose logs searxng  # SearXNG logs
docker-compose logs redis    # Redis logs
```

### Data Persistence
- Redis data is stored in a Docker volume (`redis-data`) and persists across restarts.
- To reset Redis data:
  ```bash
  docker-compose down -v
  docker-compose up -d
  ```

## Troubleshooting

- **Port Conflicts**: Ensure port `8080` is free or modify `ports` in `docker-compose.yml`.
- **Health Checks**: If services fail to start, check health status with `docker-compose ps`.
- **Configuration Errors**: Validate YAML/TOML syntax if changes are made to config files.

## Contributing

Contributions are welcome! Fork the repository and submit a pull request.  
GitHub: [oktaydbk54/searxng-custom-docker](https://github.com/oktaydbk54/searxng-custom-docker)

---

**Disclaimer**: SearXNG is a metasearch engine that aggregates results from other platforms. Use it responsibly and comply with applicable laws and terms of service of search providers.

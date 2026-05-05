# PHP Docker Images (Alpine)

A collection of optimized PHP Docker images based on Alpine Linux, including FPM, CLI, and ZTS variants for PHP versions 8.2, 8.3, 8.4, and 8.5.

Images are available on Docker Hub: [kalidyasin/php](https://hub.docker.com/r/kalidyasin/php)

## Features

- **Lightweight**: Based on Alpine Linux.
- **Pre-configured Extensions**: Includes commonly used extensions:
    - `gd` (with FreeType, JPEG, and WebP support)
    - `pdo`, `pdo_mysql`, `pdo_pgsql`
    - `zip`, `mbstring`, `exif`, `pcntl`, `bcmath`, `calendar`
    - `redis` (via PECL)
- **Composer**: Latest version included in all variants.
- **Variants**: `fpm`, `cli`, and `zts`.

## Supported Versions & Tags

Images follow the naming convention: `kalidyasin/php:<version>-<variant>-alpine`

| PHP Version | Alpine | Variants | Docker Hub Tag Examples |
| :--- | :--- | :--- | :--- |
| 8.5 | Yes | fpm, cli, zts | `8.5-fpm-alpine`, `8.5-cli-alpine` |
| 8.4 | Yes | fpm, cli, zts | `8.4-fpm-alpine`, `8.4-cli-alpine` |
| 8.3 | Yes | fpm, cli, zts | `8.3-fpm-alpine`, `8.3-cli-alpine` |
| 8.2 | Yes | fpm, cli, zts | `8.2-fpm-alpine`, `8.2-cli-alpine` |

---

## Usage Instructions

### 1. Docker

#### Pull an Image
```bash
docker pull kalidyasin/php:8.5-fpm-alpine
```

#### Run a Container
```bash
docker run -it --rm -v $(pwd):/var/www/html kalidyasin/php:8.5-fpm-alpine
```

### 2. Docker Compose

Create a `docker-compose.yml` file:
```yaml
services:
  app:
    image: kalidyasin/php:8.5-fpm-alpine
    volumes:
      - .:/var/www/html
    ports:
      - "9000:9000"
```

Run with:
```bash
docker compose up -d
```

### 3. Podman

#### Run a Container
```bash
podman run -it --rm -v $(pwd):/var/www/html:Z kalidyasin/php:8.5-fpm-alpine
```
*Note: The `:Z` flag is often needed on systems with SELinux (like Fedora/RHEL) to handle volume permissions.*

### 4. Podman Compose

Using the same `docker-compose.yml` as above:
```bash
podman-compose up -d
```

---

## Building from Source

If you want to build the images locally or customize them:

### Build using Docker
```bash
docker build -t my-php-app:8.5-fpm ./8.5/alpine/fpm
```

### Build using Podman
```bash
podman build -t my-php-app:8.5-fpm ./8.5/alpine/fpm
```

---

## Directory Structure
The repository is organized by version and OS:
```text
.
├── 8.2/
│   └── alpine/
│       ├── cli/
│       ├── fpm/
│       └── zts/
├── 8.3/ ...
├── 8.4/ ...
└── 8.5/ ...
```

## License
MIT License. See [LICENSE](LICENSE) for details.

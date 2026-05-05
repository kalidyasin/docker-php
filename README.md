# PHP Docker Images (Alpine)

A collection of optimized PHP Docker images based on Alpine Linux, including FPM, CLI, and ZTS variants for PHP versions 8.2, 8.3, 8.4, and 8.5.

## Features

- **Lightweight**: Based on Alpine Linux.
- **Pre-configured Extensions**: Includes commonly used extensions:
    - `gd` (with FreeType, JPEG, and WebP support)
    - `pdo`, `pdo_mysql`, `pdo_pgsql`
    - `zip`, `mbstring`, `exif`, `pcntl`, `bcmath`, `calendar`
    - `redis` (via PECL)
- **Composer**: Latest version included in all variants.
- **Variants**: `fpm`, `cli`, and `zts`.

## Supported Versions

| PHP Version | Alpine | Variants |
| :--- | :--- | :--- |
| 8.5 | Yes | fpm, cli, zts |
| 8.4 | Yes | fpm, cli, zts |
| 8.3 | Yes | fpm, cli, zts |
| 8.2 | Yes | fpm, cli, zts |

---

## Usage Instructions

### 1. Docker

#### Build an Image
To build a specific version and variant:
```bash
docker build -t my-php-app:8.5-fpm ./8.5/alpine/fpm
```

#### Run a Container
```bash
docker run -it --rm -v $(pwd):/var/www/html my-php-app:8.5-fpm
```

### 2. Docker Compose

Create a `docker-compose.yml` file:
```yaml
services:
  app:
    build:
      context: ./8.5/alpine/fpm
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

Podman is a daemonless container engine and is a drop-in replacement for Docker.

#### Build an Image
```bash
podman build -t my-php-app:8.5-fpm ./8.5/alpine/fpm
```

#### Run a Container
```bash
podman run -it --rm -v $(pwd):/var/www/html:Z my-php-app:8.5-fpm
```
*Note: The `:Z` flag is often needed on systems with SELinux (like Fedora/RHEL) to handle volume permissions.*

### 4. Podman Compose

Podman Compose is a tool for running unchanged Docker Compose files with Podman.

#### Install (if not present)
```bash
pip install podman-compose
```

#### Run with Podman Compose
Using the same `docker-compose.yml` as above:
```bash
podman-compose up -d
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

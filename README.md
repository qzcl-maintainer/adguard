# AdGuard Docker Compose Setup

This repository provides a Docker Compose configuration for spinning up an AdGuard container with DNS & DHCP services. AdGuard acts as an effective blocklist manager for ads, trackers, and other unwanted web elements.

## Project Details

- **Author**: QZCL Maintainer [maintainer@qzconsultancy.com](mailto:maintainer@qzconsultancy.com)
- **Git Repository**: [AdGuard Docker Setup](https://github.com/qzcl-maintainer/adguard)
- **Created On**: 14-Oct-2024

## Purpose

The goal of this project is to set up and run an AdGuard instance using Docker. This configuration enables AdGuard to provide DNS, DHCP (optional), and other related services such as DNS-over-QUIC and DNSCrypt.

## Docker Services

This project uses Docker Compose to manage the AdGuard container. The configuration file defines the following:

### Service: `app` (AdGuard)

- **Container Name**: `adguard`
- **Hostname**: `adguard`
- **Image**: `adguard/adguardhome`
- **Ports**:
  - `80:80`: HTTP Web Interface
  - `443:443`: HTTPS Web Interface
  - `3000:3000`: Management Interface
  - `53:53` (TCP/UDP): DNS (Domain Name System)
  - `853:853` (TCP/UDP): DNS-over-TLS
  - `784:784/udp`: DNS-over-QUIC
  - `8853:8853/udp`: Alternate DNS-over-QUIC
  - `5443:5443` (TCP/UDP): DNSCrypt
- **Volumes**:
  - `./work:/opt/adguardhome/work`: Stores AdGuard’s runtime data.
  - `./conf:/opt/adguardhome/conf`: Stores AdGuard’s configuration files.
- **Restart Policy**: The container will automatically restart unless stopped (`unless-stopped`).
- **Network**: Connects to the custom network `adguard-net`.

### Networks

- **adguard-net**: 
  - Uses the `host` driver by default for direct access to the host's network stack.
  - Optionally, you can use the `bridge` driver for a more isolated network setup.

## Setup Instructions

### Prerequisites

- Ensure Docker and Docker Compose are installed on your machine.
- For help with Docker Compose installation, refer to the [official documentation](https://docs.docker.com/reference/compose-file/version-and-name/).

### How to Run

1. Clone the repository:
    ```bash
    git clone https://github.com/qzcl-maintainer/adguard
    cd adguard
    ```

2. Verify the configuration:
    ```bash
    docker compose config
    ```

3. Start the AdGuard service in detached mode:
    ```bash
    docker compose up --detach
    ```

### DHCP Services (Optional)

To enable DHCP services, uncomment the following ports in the `docker-compose.yml` file:

```yaml
# - "67:67/udp"  # DHCP Port
# - "68:68"      # DHCP Port
# - "68:68/udp"  # DHCP Ports
```
```

### Stop the Service

To stop the AdGuard container:
```
docker compose down
```

This `README.md` provides a clear overview of the Docker Compose setup for the AdGuard container. It includes project details, a description of services and networks, instructions for running the container, and optional DHCP setup.


### References:
1. [Docker Compose File Reference](https://docs.docker.com/reference/compose-file/version-and-name/)
2. [AdGuard Docker Hub Page](https://hub.docker.com/r/adguard/adguardhome)


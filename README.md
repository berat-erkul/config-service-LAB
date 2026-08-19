# Config Service

![Java](https://img.shields.io/badge/Java-11-orange)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-2.3.4-brightgreen)

Centralized configuration server for the Ticketing microservices system. Built with Spring Cloud Config Server, it serves environment-specific configuration to the other services from a Git repository, with optional HashiCorp Vault integration for secrets.

## Context

This service is part of a larger microservices-based ticketing application. It is the first service the other services depend on at startup, since they fetch their configuration from here. See the main system repository: [TicketinApp](https://github.com/berat-erkul/TicketinApp).

## Tech Stack

- Java 11
- Spring Boot 2.3.4.RELEASE
- Spring Cloud (Hoxton.SR9)
- Spring Cloud Config Server
- Spring Cloud Vault Config (for secrets, currently disabled by default)
- Maven

## Running the Service

### With Maven

```bash
mvn spring-boot:run
```

### With Docker

```bash
docker build -t config-service .
docker run -p 8888:8888 config-service
```

The service starts on port **8888**.

## Configuration

The Config Server reads its own configuration from `bootstrap.yml` and expects the following environment variables to be set:

| Variable | Description |
| --- | --- |
| `CONFIG_GIT_URI` | Git repository URI where the actual service configuration files are stored |
| `CONFIG_GIT_DEFAULT_LABEL` | Default branch/label to use in the config Git repository |
| `CONFIG_GIT_USERNAME` | Username for accessing the config Git repository |
| `CONFIG_GIT_PASSWORD` | Password/token for accessing the config Git repository |
| `VAULT_ROLE_ID` | AppRole role ID for HashiCorp Vault authentication (only used if Vault is enabled) |
| `VAULT_SECRET_ID` | AppRole secret ID for HashiCorp Vault authentication (only used if Vault is enabled) |

Vault integration (`spring.cloud.vault.enabled`) is disabled by default and can be turned on when secret management via Vault is needed.

## Related Services

- [config-service-LAB](https://github.com/berat-erkul/config-service-LAB) — this service
- [discovery-service-LAB](https://github.com/berat-erkul/discovery-service-LAB) — service discovery (Eureka)
- [gateway-service-LAB](https://github.com/berat-erkul/gateway-service-LAB) — API gateway
- [user-service-LAB](https://github.com/berat-erkul/user-service-LAB) — user management service
- [task-service-LAB](https://github.com/berat-erkul/task-service-LAB) — task management service
- [project-service-LAB](https://github.com/berat-erkul/project-service-LAB) — project management service
- [web-ui-service-LAB](https://github.com/berat-erkul/web-ui-service-LAB) — web frontend
- [mobile-ticketing-app-LAB](https://github.com/berat-erkul/mobile-ticketing-app-LAB) — mobile client

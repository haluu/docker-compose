# Authentik Identity Provider

This directory contains the Docker Compose configuration for Authentik, an open-source Identity Provider (IdP) that provides authentication and authorization services. Authentik supports SSO, LDAP, SAML, OAuth2, and OIDC protocols, making it a comprehensive solution for managing access to your applications.

## Features

- **Single Sign-On (SSO)**: Unified authentication across multiple applications
- **Multi-Protocol Support**: OAuth2, OIDC, SAML, LDAP providers
- **User Management**: Self-service portal for password resets and profile management
- **Multi-Factor Authentication**: Support for TOTP, WebAuthn, and more
- **Forward Auth**: Seamless integration with Traefik for application protection
- **Customizable Flows**: Flexible authentication and authorization workflows
- **Admin Interface**: Web-based administration dashboard

## File Structure

```
authentik/
├── .env.example          # Environment variables template
├── docker-compose.yml    # Multi-container service definition
└── README.md            # This file
```

## Architecture

The setup includes four containers:
- **authentik-proxy**: Main Authentik server (web interface and API)
- **worker**: Background worker for tasks and email sending
- **postgresql**: Database for storing user data and configurations
- **redis**: Cache and message broker for Authentik services

## Quick Start

1. Copy `.env.example` to `.env` and configure:
   ```bash
   VOLUME_PATH=/path/to/authentik/data
   HOSTNAME=auth.yourdomain.com
   DOMAIN=yourdomain.com
   PROJECT_NAME=authentik
   AUTHENTIK_SECRET_KEY=<generate-a-secure-key>
   PG_PASS=<secure-database-password>
   ```

2. Generate a secure secret key:
   ```bash
   openssl rand -base64 32
   ```

3. Create required networks (if not already created):
   ```bash
   docker network create internal
   docker network create proxy
   ```

4. Start Authentik: `docker-compose up -d`

5. Access Authentik at `https://auth.yourdomain.com`

6. Initial setup: Create admin user via web interface

## Configuration

### Environment Variables

- **`VOLUME_PATH`**: Base path for persistent data (PostgreSQL, Redis, media files)
- **`HOSTNAME`**: Domain name for Authentik web interface
- **`DOMAIN`**: Base domain for outpost routing
- **`PROJECT_NAME`**: Container prefix (used for Traefik routing)
- **`AUTHENTIK_SECRET_KEY`**: Secret key for encryption (generate a strong random value)
- **`PG_USER`/`PG_DB`/`PG_PASS`**: PostgreSQL database credentials
- **`TAG`**: Docker image tag (default: `latest`)

### Traefik Integration

The configuration includes:
- **Main Router**: Routes `auth.yourdomain.com` to Authentik web interface
- **Outpost Router**: Handles authentication requests from protected applications
- **Forward Auth Middleware**: Enables authentication for other services

### Security Notes

- Change default PostgreSQL password in production
- Generate a strong random `AUTHENTIK_SECRET_KEY`
- Keep the secret key secure and backed up
- Use strong passwords for the admin account

### Data Persistence

The following volumes are created under `${VOLUME_PATH}`:
- `psql/`: PostgreSQL database files
- `redis/`: Redis persistence data
- `media/`: Uploaded media files (logos, icons)
- `custom-templates/`: Custom email and page templates

## Usage with Other Services

To protect a service with Authentik authentication, add the middleware label to your service:
```yaml
- traefik.http.routers.myapp.middlewares=authentik@docker
```

Configure the application as a provider in Authentik's admin interface.

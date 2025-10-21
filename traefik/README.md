# Traefik Reverse Proxy

This directory contains the Traefik configuration for the Docker Compose collection. Traefik serves as a modern reverse proxy and load balancer that automatically handles SSL certificates, routing, and secure connections for all services in the stack.

## Features

- **Automatic HTTPS**: Let's Encrypt integration for automatic SSL certificate generation and renewal
- **Dynamic Configuration**: Automatic service discovery and routing based on Docker labels
- **Dashboard**: Web-based dashboard for monitoring and configuration
- **Middleware Support**: Built-in security headers, rate limiting, and authentication
- **Production Ready**: Secure defaults and best practices configured

## File Structure

```
traefik/
├── .env.example              # Environment variables template
├── docker-compose.yml        # Traefik service definition
├── README.md                 # This file
├── traefik.yml               # Main Traefik configuration
└── configurations/
    └── dynamic.yml           # Dynamic configuration for middlewares and routes
```
## Configuration Files

- **`traefik.yml`**: Static configuration including entry points, certificate resolvers, and API settings
- **`configurations/dynamic.yml`**: Dynamic configuration for middlewares, services, and advanced routing rules
- **`docker-compose.yml`**: Traefik container definition with necessary volumes and networks

The Traefik instance automatically discovers other services in the Docker network and routes traffic based on their labels.
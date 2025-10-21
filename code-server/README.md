# Code-Server (VS Code in Browser)

This directory contains the Docker Compose configuration for code-server, which runs Visual Studio Code in your browser. Access a full-featured development environment from anywhere with just a web browser, complete with extensions, terminal, and all VS Code features.

## Features

- **Browser-based VS Code**: Full VS Code experience accessible via web browser
- **Remote Development**: Code from any device without local setup
- **Extension Support**: Install and use VS Code extensions
- **Integrated Terminal**: Access to shell and command-line tools
- **Traefik Integration**: Automatic HTTPS and authentication via OIDC
- **Persistent Storage**: Your projects and settings are preserved across container restarts

## File Structure

```
code-server/
├── .env.example          # Environment variables template
├── docker-compose.yml    # Code-server service definition
└── README.md            # This file
```

## Security

The configuration includes OIDC authentication middleware (`oidcAuth@file`) for secure access. Make sure this middleware is properly configured in your Traefik dynamic configuration.
# Hemmelig Secret Sharing

This directory contains the Docker Compose configuration for Hemmelig, a self-hosted secret sharing service. Share passwords, API keys, and sensitive information securely with time-limited, encrypted links that self-destruct after being read or after a specified time period.

## Features

- **Secure Secret Sharing**: Share sensitive information with encrypted, self-destructing links
- **Time-Limited Access**: Set expiration times for shared secrets
- **Read-Once Option**: Secrets that automatically delete after first viewing
- **File Upload Support**: Share files securely (up to 10MB by default)
- **User Management**: Create accounts to track and manage shared secrets
- **No Database Required**: Uses SQLite for simplicity
- **Burn After Reading**: Optional immediate deletion after viewing
- **OIDC Authentication**: Secure access via Authentik or other OIDC providers

## File Structure

```
hemmelig/
├── .env.example          # Environment variables template
├── docker-compose.yaml   # Hemmelig service definition
└── README.md            # This file
```

## Security

- **OIDC Authentication**: Protected with `oidcAuth@file` middleware
- **JWT Secret**: Used for token signing - must be kept secure
- **File Permissions**: Container runs as user 1000 - ensure volumes have correct ownership

## Notes

- Secrets are encrypted in the database
- Once a secret expires or is burned, it cannot be recovered
- File uploads are stored encrypted on disk
- The database is SQLite-based for simplicity and portability

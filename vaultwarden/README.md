# Vaultwarden Password Manager

This directory contains the Docker Compose configuration for Vaultwarden, a lightweight, self-hosted implementation of the Bitwarden password manager. Store and sync your passwords, notes, and two-factor authentication codes securely across all your devices with full compatibility with Bitwarden clients.

## Features

- **Bitwarden Compatible**: Works with all official Bitwarden apps (desktop, mobile, browser extensions)
- **Self-Hosted**: Full control over your sensitive password data
- **End-to-End Encryption**: All data encrypted on the client side
- **Multi-Platform**: Access from Windows, macOS, Linux, iOS, Android, and web browsers
- **Two-Factor Authentication**: Support for TOTP, U2F, and Duo
- **Password Generator**: Built-in secure password generation
- **Secure Notes**: Store sensitive information beyond just passwords
- **Organization Support**: Share passwords securely with teams
- **Web Vault**: Browser-based interface for managing passwords
- **WebSocket Support**: Real-time sync across devices
- **Admin Panel**: Web-based administration interface

## File Structure

```
vaultwarden/
├── .env                  # Environment variables configuration
├── docker-compose.yml    # Vaultwarden service definition
└── README.md            # This file
```

## Security Best Practices

- **Disable Signups**: Public registration is disabled by default
- **Admin Token**: Required to access the admin panel - keep it secure
- **HTTPS Only**: Always use HTTPS in production (configured via Traefik)
- **Strong Master Password**: Users should use a strong, unique master password
- **Backup Regularly**: Back up the `${VOLUME_PATH}` directory regularly

## Notes

- Vaultwarden is a lightweight alternative to the official Bitwarden server
- Fully compatible with all Bitwarden clients
- Much lower resource requirements than the official implementation
- Regular backups are essential - this contains all your passwords!

# Draw.io Diagramming Tool

This directory contains the Docker Compose configuration for Draw.io (also known as diagrams.net), a free and open-source diagramming application. Create flowcharts, process diagrams, network diagrams, UML diagrams, and more directly in your browser with this self-hosted instance.

## Features

- **Versatile Diagramming**: Create flowcharts, UML, network diagrams, wireframes, and more
- **Browser-Based**: No installation required, works in any modern web browser
- **Export Options**: Save diagrams in multiple formats (PNG, SVG, PDF, XML)
- **Collaboration Ready**: Share diagrams with your team
- **Offline Capable**: Works without internet connection once loaded
- **OIDC Authentication**: Secure access via Authentik or other OIDC providers
- **Auto-Updates**: Watchtower integration for automatic container updates

## File Structure

```
drawio/
├── .env.example          # Environment variables template
├── docker-compose.yaml   # Draw.io service definition
└── README.md            # This file
```

## Security

## Notes

- No persistent storage is configured as Draw.io is a client-side application
- Diagrams are saved locally in your browser or exported to files
- For diagram storage integration, consider connecting to cloud storage or Git repositories through the Draw.io interface

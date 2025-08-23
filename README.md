# Home Assistant Addon Repository

This repository contains custom Home Assistant addons that can be installed on Home Assistant OS.

## Available Addons

### Portainer Business Edition
- **Description**: Manage your Docker environment with ease using Portainer Business Edition
- **Features**: 
  - Web-based Docker management interface
  - Support for multiple architectures (aarch64, amd64, armv7)
  - SSL support
  - Ingress integration
- **Current Version**: 2.33.0

## Installation

1. In Home Assistant, go to **Settings** → **Add-ons** → **Add-on Store**
2. Click the three dots in the top right corner
3. Select **Repositories**
4. Add this repository URL: `https://github.com/ypj0202/hassio-addons`
5. Click **Add**
6. Find the addon you want to install and click **Install**

## Building and Publishing

This repository uses GitHub Actions to automatically build and publish Docker images to GitHub Container Registry (ghcr.io).

### Automatic Builds

Images are automatically built and published when:
- Code is pushed to the `main` or `master` branch
- Pull requests are created (builds but doesn't push)
- Manual workflow dispatch is triggered

### Manual Builds

You can manually trigger builds using the GitHub Actions interface:

1. Go to **Actions** tab in your repository
2. Select **Build and Upload Addon Images**
3. Click **Run workflow**
4. Choose options:
   - **Addon**: Leave empty to build all addons, or specify one (e.g., "portainer")
   - **Version**: Leave empty for latest, or specify a version (e.g., "2.34.0")

### Image Tags

Images are tagged with:
- `latest` - Latest version from the default branch
- `{version}` - Specific version number
- `{branch}-{sha}` - Branch-specific builds
- `{sha}` - Commit-specific builds

## Repository Structure

```
hassio-addons/
├── .github/
│   └── workflows/
│       └── build-addons-advanced.yml  # Build workflow
├── portainer/                          # Portainer addon
│   ├── config.json                     # Addon configuration
│   ├── Dockerfile                      # Docker image definition
│   ├── icon.png                        # Addon icon
│   └── logo.png                        # Addon logo
└── repository.json                     # Repository metadata
```

## Adding New Addons

To add a new addon:

1. Create a new directory for your addon
2. Include these required files:
   - `config.json` - Addon configuration (see schema below)
   - `Dockerfile` - Docker image definition
   - `icon.png` - 64x64 pixel icon
   - `logo.png` - 128x128 pixel logo

### Config.json Schema

```json
{
  "name": "Addon Name",
  "version": "1.0.0",
  "slug": "addon-slug",
  "description": "Addon description",
  "arch": ["aarch64", "amd64", "armv7"],
  "image": "ghcr.io/username/repository/addon-slug",
  "ingress": true,
  "ingress_port": 8080,
  "panel_admin": false,
  "panel_icon": "mdi:icon-name",
  "startup": "application",
  "boot": "auto",
  "options": {},
  "schema": {},
  "ports": {},
  "ports_description": {}
}
```

## Multi-Architecture Support

All addons are built for multiple architectures:
- **aarch64** - ARM 64-bit (Raspberry Pi 4, newer ARM devices)
- **amd64** - x86 64-bit (Intel/AMD desktop/server)
- **armv7** - ARM 32-bit (Raspberry Pi 3 and older)

## GitHub Container Registry

Images are published to: `ghcr.io/ypj0202/hassio-addons/{addon-name}`

To use these images in other projects:
```bash
docker pull ghcr.io/ypj0202/hassio-addons/portainer:latest
```

## Troubleshooting

### Build Failures
- Check that all required files exist in your addon directory
- Ensure `config.json` is valid JSON
- Verify Dockerfile syntax
- Check GitHub Actions logs for specific error messages

### Installation Issues
- Ensure your Home Assistant version supports the addon architecture
- Check that the repository URL is correct
- Verify the addon is compatible with your Home Assistant version

## Contributing

1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Test your addon locally
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For issues and questions:
- Create an issue in this repository
- Check the Home Assistant community forums
- Review the Home Assistant addon documentation

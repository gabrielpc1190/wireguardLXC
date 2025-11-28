# WireGuard LXC

> **Fork Notice:** This is a fork of [WireGuard UI](https://github.com/ngoduykhanh/wireguard-ui) by [Khanh Ngo](https://github.com/ngoduykhanh), specifically optimized for deployment in LXC containers with NO-NAT architecture.
> 
> See [CREDITS.md](CREDITS.md) for full attribution to the original project.
> 
> **Key Enhancements:**
> - Fixed session secret validation (prevents login loop bug)
> - Added automatic WireGuard interface restart functionality
> - Improved for LXC deployment without Docker

## Features

- Friendly web-based UI for WireGuard management
- User authentication and session management
- Manage client information (name, email, allocated IPs)
- Retrieve client config via QR code, file download, email, or Telegram
- Automatic configuration application (optional)
- Wake-on-LAN support
- Optimized for LXC containerization

## Quick Start

> ⚠️ **Default Credentials:** Username and password are both `admin`. **Change immediately** in production!

### Using Binary

Download from [Releases](#) and run directly:

```bash
./wireguard-ui
```

### Environment Variables

Key environment variables for this fork:

| Variable | Description | Default |
|----------|-------------|---------|
| `SESSION_SECRET` | Session encryption key (min 32 chars, **REQUIRED**) | Random |
| `WGUI_MANAGE_RESTART` | Auto-restart WireGuard on config changes | `false` |
| `BIND_ADDRESS` | Server bind address | `0.0.0.0:5000` |
| `WGUI_USERNAME` | Initial admin username | `admin` |
| `WGUI_PASSWORD` | Initial admin password | `admin` |

For complete environment variable documentation, see the [original project docs](https://github.com/ngoduykhanh/wireguard-ui#environment-variables).

## LXC Deployment

This fork is optimized for LXC containers with NO-NAT routing:

### Prerequisites (Proxmox Host)

Add to `/etc/pve/lxc/CTID.conf`:

```
lxc.cgroup2.devices.allow: c 10:200 rwm
lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
```

### Recommended Configuration

```bash
export SESSION_SECRET="your-32-character-or-longer-secret-here"
export WGUI_MANAGE_RESTART="true"
export WGUI_ENDPOINT_ADDRESS="your.domain.com:51820"
./wireguard-ui
```

## Build from Source

```bash
# Prepare assets
./prepare_assets.sh

# Build binary
go build -o wireguard-ui

# Or build with version info
go build -ldflags "-X main.appVersion=v1.0.0 -X main.gitCommit=$(git rev-parse --short HEAD)" -o wireguard-ui
```

## Key Differences from Upstream

See [docs/modifications_analysis.md](docs/modifications_analysis.md) for detailed technical changes.

**Summary:**
1. **Session Secret Validation** - Prevents login loop caused by improperly sized secrets
2. **Auto-Restart Feature** - `WGUI_MANAGE_RESTART` environment variable
3. **UX Improvements** - Autocomplete attributes for password managers
4. **LXC Optimization** - Tested and configured for LXC deployment

## License

MIT License - Same as the original project.

See [LICENSE](LICENSE) for the full license text.

## Credits

**Original Project:** [WireGuard UI](https://github.com/ngoduykhanh/wireguard-ui) by [Khanh Ngo](https://github.com/ngoduykhanh)

This fork maintains the original MIT license and gratefully acknowledges the excellent foundation provided by the upstream project.

## Support

For issues specific to this fork, please open an issue on [this repository](https://github.com/gabrielpc1190/wireguardLXC/issues).

For general WireGuard UI questions, refer to the [original project](https://github.com/ngoduykhanh/wireguard-ui).

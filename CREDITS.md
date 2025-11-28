# Credits

## Original Project

This project is a fork of [WireGuard UI](https://github.com/ngoduykhanh/wireguard-ui) by [Khanh Ngo](https://github.com/ngoduykhanh).

**Original Repository:** https://github.com/ngoduykhanh/wireguard-ui  
**License:** MIT License  
**Version Base:** v0.6.2

We are grateful for the excellent foundation provided by the original project.

## Modifications

This fork includes the following enhancements specifically for LXC deployment:

- **Fixed session secret validation** - Prevents login loop bug caused by invalid session secret length
- **Added automatic WireGuard interface restart** - `WGUI_MANAGE_RESTART` environment variable for seamless configuration application
- **Improved login UX** - Added autocomplete attributes for better password manager integration
- **Optimized for NO-NAT architecture** - Designed for transparent routing in LXC containers

For detailed technical analysis of modifications, see [docs/modifications_analysis.md](docs/modifications_analysis.md).

## License

This fork maintains the original MIT License. See [LICENSE](LICENSE) for details.

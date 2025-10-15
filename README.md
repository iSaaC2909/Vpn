
A simple, secure, and efficient VPN implementation written in C.  provides both client and server functionality with strong encryption and minimal overhead.

## Features

- Simple and lightweight implementation
- Strong encryption using Xoodoo-based cryptography
- Support for both IPv4 and IPv6
- Automatic MTU optimization
- Cross-platform support (Linux, macOS, BSD)
- Built-in firewall rules management
- Automatic gateway detection
- Support for custom interface names
- Configurable IP addresses and ports

## Requirements

- C compiler (GCC or Clang)
- Make
- Root/Administrator privileges (for TUN device creation)
- Linux: TUN module loaded
- macOS: utun support
- BSD: tun device support

## Building

```bash
make
```

## Usage

### Server Mode

```bash
sudo ./dsvpn server <key_file> <vpn_server_ip_or_name> <vpn_server_port> <tun_interface> <local_tun_ip> <remote_tun_ip> <external_ip>
```

### Client Mode

```bash
sudo ./dsvpn client <key_file> <vpn_server_ip_or_name> <vpn_server_port> <tun_interface> <local_tun_ip> <remote_tun_ip> <gateway_ip>
```

### Parameters

- `key_file`: Path to the encryption key file (32 bytes)
- `vpn_server_ip_or_name`: Server's IP address or hostname
- `vpn_server_port`: Server's port (default: 443)
- `tun_interface`: TUN interface name (use "auto" for automatic)
- `local_tun_ip`: Local TUN IP address (use "auto" for default)
- `remote_tun_ip`: Remote TUN IP address (use "auto" for default)
- `external_ip`: External IP (server mode only)
- `gateway_ip`: Gateway IP (client mode only)

### Example Setup

1. Generate a key file:
```bash
dd if=/dev/urandom of=vpn.key count=1 bs=32
```

2. Start the server:
```bash
sudo ./dsvpn server vpn.key 0.0.0.0 443 auto auto auto auto
```

3. Start the client:
```bash
sudo ./dsvpn client vpn.key server.example.com 443 auto auto auto auto
```

## Default Values

- Default MTU: 9000 (1500 on NetBSD)
- Default Client IP: 192.168.192.1
- Default Server IP: 192.168.192.254
- Default Port: 443

## Security

- Uses Xoodoo-based cryptography for encryption
- Implements secure key exchange
- Includes timestamp validation to prevent replay attacks
- Supports automatic firewall rules for additional security

## Platform-Specific Notes

### Linux
- Requires TUN module to be loaded
- Uses iptables for firewall rules
- Supports BBR congestion control

### macOS
- Uses utun interface
- Supports automatic interface detection

### BSD
- Uses tun interface
- Supports automatic interface detection
- Default MTU is 1500

## License

This project is open source software. See the LICENSE file for details.

# OpenVPN-client

This is a docker image of an OpenVPN client tied to a SOCKS proxy server.  It is
useful to isolate network changes (so the host is not affected by the modified
routing).

This supports directory style (where the certificates are not bundled together in one `.ovpn` file) and those that contains `update-resolv-conf`
In ./vpn-configs/ directory you can prepare configs for different openvpn proxies for batch start. Each configuration in a separate directory inside ./vpn-configs/.

## Usage
At the beginning you have to build local docker image. Simply run:
```bash
build_image
```

Then you can start openvpn socks proxy using `runproxy` in this repository:
```bash
runproxy /your/openvpn/directory proxy-port
```

`/your/openvpn/directory` should contain *one* OpenVPN `.ovpn` file. It can reference other certificate files or key files in the same directory.

Or batch start all proxies from ./vpn-configs/ directory:
```bash
runall
```

Then connect to SOCKS proxy through through `127.0.0.1:<proxy-port>`. For example:

```bash
curl --proxy socks5://127.0.0.1:1081 ipinfo.io
```

At the end you can stop all proxies (if you started them from 'runall' script):
```bash
stopall
```

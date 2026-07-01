# Networking Basics

## 02.1 — IP, interfaces and localhost

An IP address identifies a machine or network interface in a network.

Common examples:

- `127.0.0.1`
- `172.x.x.x`
- `192.168.x.x`
- `10.x.x.x`

`127.0.0.1` is the loopback address and refers to the local machine.

In simple terms:

```text
127.0.0.1 = localhost = this machine
```

A network interface is a way for the machine to communicate through the network.

Common interfaces:

| Interface | Meaning |
|---|---|
| `lo` | Loopback interface |
| `eth0` | Main network interface |
| `wlan0` | Wireless interface, on some systems |

### Useful commands

| Command | Purpose |
|---|---|
| `ip addr` | Shows network interfaces and IP addresses |
| `hostname -I` | Shows the machine IP address |
| `ping -c 4 127.0.0.1` | Tests local connectivity |
| `ping -c 4 google.com` | Tests external connectivity |

### Practice result

The loopback interface showed:

```text
127.0.0.1
```

The main network interface showed an IP similar to:

```text
172.28.62.52
```

A successful ping shows:

```text
4 packets transmitted, 4 received, 0% packet loss
```

This means the host responded correctly.

---

## 02.2 — DNS basics

DNS means Domain Name System.

DNS translates domain names into IP addresses.

Example:

```text
github.com -> 140.82.121.3
```

Without DNS, the system would not know which IP address belongs to a domain name.

### Useful DNS commands

| Command | Purpose |
|---|---|
| `resolvectl query github.com` | Resolves a domain name into an IP address |
| `ping -c 4 github.com` | Tests DNS resolution and network connectivity |
| `curl -I https://github.com` | Tests DNS, HTTPS connection and web response |

### Important idea

`resolvectl query` tests if DNS can resolve a domain.

Example:

```bash
resolvectl query github.com
```

Example result:

```text
github.com: 140.82.121.3
```

This means DNS resolved the domain successfully.

### Difference between DNS, ping and curl

| Command | What it tests |
|---|---|
| `resolvectl query github.com` | DNS resolution |
| `ping -c 4 github.com` | DNS + network connectivity |
| `curl -I https://github.com` | DNS + HTTPS connection + web response |

A response such as:

```text
HTTP/2 200
```

means the web service responded successfully.

### Important note

Sometimes `resolvectl` and `ping` may show different IP addresses for the same domain.

This can happen because large services like GitHub or Google use multiple servers, DNS caching and load balancing.

---

## 02.3 — Ports and services

An IP address identifies a machine.

A port identifies a specific service running on that machine.

Example:

```text
192.168.1.10:80   -> HTTP web service
192.168.1.10:443  -> HTTPS web service
192.168.1.10:22   -> SSH service
```

In simple terms:

```text
IP = machine
Port = service entry point
Service = application listening on that port
```

### Common ports

| Port | Service |
|---|---|
| `22` | SSH |
| `53` | DNS |
| `80` | HTTP |
| `443` | HTTPS |
| `3000` | Common frontend development port |
| `5000` | Common backend/API development port |
| `8000` | Common local test server port |
| `8080` | Common web application port |

### Useful commands

| Command | Purpose |
|---|---|
| `ss -tuln` | Shows listening TCP/UDP ports |
| `python3 -m http.server 8000` | Starts a simple local web server on port 8000 |
| `curl -I http://localhost:8000` | Tests if the local web server responds |
| `curl -I http://127.0.0.1:8000` | Tests the same service using the loopback IP |
| `ss -tuln \| grep 8000` | Checks if something is listening on port 8000 |

### Practice result

A local Python web server was started on port `8000`.

The command:

```bash
curl -I http://localhost:8000
```

returned:

```text
HTTP/1.0 200 OK
```

This means the local web service responded successfully.

The command:

```bash
ss -tuln | grep 8000
```

showed:

```text
tcp   LISTEN 0      5      0.0.0.0:8000      0.0.0.0:*
```

This means a TCP service was listening on port `8000`.

### Important idea

```text
localhost = 127.0.0.1 = this machine
```

```text
127.0.0.1 means local only.
0.0.0.0 means all available network interfaces.
```

After stopping the server with `CTRL + C`, this command failed:

```bash
curl -I http://localhost:8000
```

because there was no service listening on port `8000`.

In simple terms:

```text
Service running + port listening = curl responds.
Service stopped = curl cannot connect.
```

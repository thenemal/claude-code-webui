# claude-code-webui

Deployment config for [claude-code-webui](https://github.com/nicholasgasior/claude-code-webui) on the Proxmox LXC at `192.168.45.20`.

## What's here

| File | Purpose |
|------|---------|
| `claude-code-webui.service` | systemd unit — runs the backend on port 9090 |
| `caddy-snippet.conf` | Caddy reverse-proxy snippet to paste into the Caddy LXC's `Caddyfile` |

## Status

✅ Working. Service running on port 9090, proxied via Caddy at `home9.compagnie-lily.org`.

## Setup

### 1. Install the binary (already done)

```bash
npm install -g @anthropic-ai/claude-code-webui
# or via the package that ships it
```

Binary is at `/usr/bin/claude-code-webui` (v0.1.56).

### 2. Install the systemd service

```bash
cp claude-code-webui.service /etc/systemd/system/
systemctl daemon-reload
systemctl enable --now claude-code-webui
```

### 3. Caddy reverse proxy

On the Caddy LXC, paste the contents of `caddy-snippet.conf` into the `Caddyfile` and replace the password hash:

```bash
caddy hash-password --plaintext yourpassword
```

Then reload Caddy:

```bash
systemctl reload caddy
```

### 4. Verify

```bash
curl -I http://192.168.45.20:9090
```

## Notes

- The webui has no built-in authentication — basic_auth in Caddy is the only gate.
- Working directory in the service is `/root/botnificent-manager` so Claude Code launches with the right context.
- Claude binary path: `/root/.local/bin/claude`

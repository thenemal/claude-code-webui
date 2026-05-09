# claude-code-webui deployment

Config files to run [claude-code-webui](https://github.com/nicholasgasior/claude-code-webui) on this machine.

## Status

⚠️ **Not working yet.** Binary is installed (`/usr/bin/claude-code-webui` v0.1.56) but the systemd service has not been deployed or enabled.

## Files

- `claude-code-webui.service` — systemd unit, port 9090, `WorkingDirectory=/root/botnificent-manager`
- `caddy-snippet.conf` — reverse proxy snippet for Caddy LXC, `home9.compagnie-lily.org` → `192.168.45.20:9090` with basic_auth

## Next steps to fix

1. Copy service file to `/etc/systemd/system/` and enable it
2. Generate a real Caddy password hash and replace the placeholder in `caddy-snippet.conf`
3. Deploy the Caddy config on the Caddy LXC and reload
4. Confirm `curl http://192.168.45.20:9090` returns a response

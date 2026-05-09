# claude-code-webui deployment

Config files to run [claude-code-webui](https://github.com/nicholasgasior/claude-code-webui) on this machine.

## Status

✅ Working. Verified 2026-05-09.

## Files

- `claude-code-webui.service` — systemd unit, port 9090, `WorkingDirectory=/root/botnificent-manager`
- `caddy-snippet.conf` — reference snippet for the Caddy LXC config (actual live config on the Caddy LXC is more complete: health check, logging, security imports, real password hash)

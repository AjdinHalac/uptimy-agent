# uptimy-agent — Cross-Platform Monitoring Agent

## Overview

Uptimy Agent is a lightweight, cross-platform service watchdog and health monitor designed to keep your backend applications running smoothly. Supports Linux, macOS, and Windows.

---

## Installation

### Linux and macOS

Run the install script with your agent credentials:

```bash
curl -fsSL https://github.com/AjdinHalac/uptimy-agent/releases/latest/download/install.sh | sudo bash -s -- <agent_id> <secret>
```

Or use a specific version:

```bash
curl -fsSL https://github.com/AjdinHalac/uptimy-agent/releases/download/${AGENT_VERSION}/install.sh | sudo bash -s -- <agent_id> <secret>
```

- **Linux:** Installs as a systemd service  
- **macOS:** Installs as a launchd agent  
- **Requires root privileges (sudo) to install and run as a service**

---

### Windows

1. Download the latest Windows installer script `install.ps1` from the [Releases](https://github.com/AjdinHalac/uptimy-agent/releases) page.
2. Open PowerShell as Administrator.
3. Run:

```powershell
.\install.ps1 -AgentID "your-agent-id" -AgentSecret "your-agent-secret"
```

- Downloads the correct `.exe` binary for your architecture  
- Registers a Windows Service  
- Starts the agent automatically  

---

## Running inside Docker

To run Uptimy Agent inside your Docker containers:

```dockerfile
FROM ubuntu:22.04

# Install dependencies and Uptimy Agent binary
COPY uptimy-agent-linux-amd64 /usr/local/bin/uptimy-agent
COPY config.json /etc/uptimy-agent/config.json

ENTRYPOINT ["/usr/local/bin/uptimy-agent"]
```

- Make sure your `config.json` with agent credentials is baked into the image or mounted as a volume.
- You can run the agent as a sidecar container if preferred.

---

## Integrating with CI/CD and GitHub Actions

You can automate Uptimy Agent deployment by including the install command in your workflows:

```yaml
jobs:
  deploy-agent:
    runs-on: ubuntu-latest
    steps:
      - name: Install Uptimy Agent
        run: |
          curl -fsSL https://github.com/AjdinHalac/uptimy-agent/releases/latest/download/install.sh | sudo bash -s -- <agent_id> <secret>
```

- Store your `AGENT_ID` and `AGENT_SECRET` securely in GitHub Secrets
- Trigger the workflow on deploy or environment setup

---

## Support and Troubleshooting

Logs for the agent are available at:

- **Linux:** `journalctl -u uptimy-agent`
- **macOS:** `/tmp/uptimy-agent.log` and `/tmp/uptimy-agent.err`
- **Windows:** Windows Event Viewer / service logs

For issues, open a GitHub issue on this repo.

---

## License

MIT License

# Rootline releases

Installers for the **Rootline edge agent**, the small program an operator runs in its management network to give Rootline read-only access to its own monitoring systems. Only binaries are published here; the source is private.

The agent does nothing on its own: it needs a one-time join token, which we issue for your agent.

## Download

The newest release is always at these links:

| File | For |
|---|---|
| [edge-agent-linux-amd64.deb](https://github.com/txhub-labs/rootline-releases/releases/latest/download/edge-agent-linux-amd64.deb) | Debian 12, Ubuntu 24.04 (x86-64) |
| [edge-agent-linux-arm64.deb](https://github.com/txhub-labs/rootline-releases/releases/latest/download/edge-agent-linux-arm64.deb) | Debian, Ubuntu (ARM64) |
| [edge-agent-linux-x86_64.rpm](https://github.com/txhub-labs/rootline-releases/releases/latest/download/edge-agent-linux-x86_64.rpm) | RHEL, Rocky 9 (x86-64) |
| [edge-agent-linux-aarch64.rpm](https://github.com/txhub-labs/rootline-releases/releases/latest/download/edge-agent-linux-aarch64.rpm) | RHEL, Rocky 9 (ARM64) |
| [edge-agent-image.oci.tar](https://github.com/txhub-labs/rootline-releases/releases/latest/download/edge-agent-image.oci.tar) | Container image (amd64 and arm64) |
| `zabbix-mcp-linux-*`, `observium-mcp-linux-*` | MCP servers for Zabbix and Observium |
| [SHA256SUMS](https://github.com/txhub-labs/rootline-releases/releases/latest/download/SHA256SUMS) | Checksums |

Earlier versions and pre-releases are under [Releases](https://github.com/txhub-labs/rootline-releases/releases).

## Install

```bash
curl -fLO https://github.com/txhub-labs/rootline-releases/releases/latest/download/edge-agent-linux-amd64.deb
curl -fLO https://github.com/txhub-labs/rootline-releases/releases/latest/download/SHA256SUMS
sha256sum --check --ignore-missing SHA256SUMS
sudo apt install ./edge-agent-linux-amd64.deb

sudo edge-agent enroll -platform-enroll https://<enrollment-host> -token '<join-token>'
sudoedit /etc/edge-agent/edge-agent.env      # EDGE_PLATFORM, EDGE_PLATFORM_ENROLL, EDGE_MCP
sudo systemctl enable --now edge-agent
journalctl -u edge-agent -f                  # "tunnel connected"
```

We send the hostnames and the join token separately. The full guide (requirements, firewall, several MCP servers, write approvals, containers) comes with your onboarding.

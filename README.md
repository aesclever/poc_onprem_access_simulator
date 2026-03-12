# poc_onprem_access_simulator
Similate RDP/SSH access to the proof of concept on-premise infrastructure.

**THIS IS A SIMULATOR**

→ Click Emmulate client RDP/SSH connections to [poc_onprem_infra_client](https://aesclever.github.io/poc_onprem_access_simulator/poc_rdp_ssh_sim.html)

→ Click onprem infrastructure server [poc_onprem_infra_server](https://aesclever.github.io/poc_onprem_infra/poc_generator.html)


## SSH Terminal
Click any Linux host in the sidebar (node-01, poc-vm-001, vault-server) to open an animated SSH session through the WireGuard tunnel. The terminal is fully interactive — type commands and press Enter:

```
help          → show all available commands
uname -a      → kernel info
uptime        → system uptime
ip addr       → network interfaces (shows wg0 tunnel)
wg show       → WireGuard peer status
vault status  → Vault seal/unseal state
vault kv get secret/vms/poc-vm-001  → VM metadata
df -h  |  free -h  |  ps aux  |  ls -la  |  whoami  |  id
systemctl status wg-quick@wg0
```
Arrow keys cycle through command history. `Ctrl+L` clears the screen.

## RDP Desktop
Click either Windows host (win-dev-01 or win-ops-01) to open a simulated Windows desktop connected via WireGuard. **Double-click any desktop icon** to open a draggable window — File Explorer, PowerShell, Vault CLI, Task Manager, Settings, or a browser pointing at the Vault UI.

## WireGuard Tunnel
The third tab shows the live tunnel state — interface config, all 5 peers with latency and active/inactive status, traffic stats, and encryption details. Hit **↻ Refresh** to simulate updated RTT readings.

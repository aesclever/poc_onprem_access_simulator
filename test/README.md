
Since the page is the scaffold generator **we built together in this conversation**, I already have the full spec. I'll build the smoke test tool directly from it — using the exact values defined in our `poc_generator.html`: `poc-vm-001`, `10.100.0.10`, `svc` user, `root` Vault token, `10.100.0.1` WireGuard gateway, Docker services on `localhost:8080/8200/8181`, and the KVM libvirt network.Here's the smoke test tool, wired directly to the specs from the scaffold generator. Here's what each section does:

## SSH Terminal
Click any target in the sidebar to open an animated session. All 6 targets from the scaffold are represented — the VM, the host, and all 3 Docker services. Interactive commands include everything needed to validate a running PoC:

```
# Service checks
vault status         vault kv list secret/
vault kv get secret/vms/poc-vm-001
opa check            keycloak info

# Network / tunnel
wg show              ip addr       ss -tlnp
ping 10.100.0.10     systemctl status wg-quick@wg0

# Jump straight to tests
test all             test wg       test vault
test opa             test ssh      test vm
```

## Smoke Tests (25 tests across 6 groups)
Click **▶ Run All** to execute the full suite. Tests are staggered with realistic delays and each expands to show the exact command and expected output. Groups covered:

| Group | Tests |
|---|---|
| **WireGuard** | Interface up, peer registered, tunnel ping, Vault key present |
| **SSH** | Host key, login as `svc`, Vault PKI TTL, wg0 active inside VM |
| **Vault** | Health, KV engine, AppRole, policies, VM secret |
| **OPA** | Health, ALLOW case, DENY case |
| **Keycloak** | Health, admin token |
| **VM** | libvirt list, DHCP lease, cloud-init done, tunnel port |

## WireGuard Tab
Shows the full `wg show`-style output for `wg0` including peer handshake times, transfer stats, and key lifecycle details — plus the exact commands to paste into your Ubuntu 24.04 terminal to validate each check manually.

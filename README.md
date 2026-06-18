# ACME Security Policies Collection

[![Ansible Collection](https://img.shields.io/badge/collection-acme.security__policies-blue)](https://github.com/Automation-Portal-ACME/acme-security-policies)

An Ansible collection maintained by the **ACME Corp InfoSec Team** for enforcing security compliance baselines across RHEL and CentOS hosts. This collection provides opinionated roles aligned with CIS benchmarks and ACME internal security standards.

## Requirements

- Ansible Core >= 2.15
- RHEL 8 / RHEL 9 or CentOS Stream 8/9 managed hosts
- Root or sudo access on target hosts

## Included Roles

### `acme.security_policies.cis_benchmark`

Applies CIS Level 1 and Level 2 hardening controls to RHEL hosts. Covers filesystem permissions, audit rules, SSH configuration, password policies, and kernel parameters.

**Variables:**

| Variable | Default | Description |
|----------|---------|-------------|
| `cis_level` | `1` | CIS benchmark level to apply (1 or 2) |
| `cis_skip_rules` | `[]` | List of rule IDs to skip |
| `cis_audit_only` | `false` | When true, reports non-compliance without making changes |

### `acme.security_policies.firewall_baseline`

Configures `firewalld` zones and rules according to ACME network security policy. Ensures only approved services and ports are open, drops all other inbound traffic, and enables logging for denied connections.

**Variables:**

| Variable | Default | Description |
|----------|---------|-------------|
| `firewall_zone` | `internal` | Default firewalld zone for managed interfaces |
| `firewall_allowed_services` | `[ssh]` | List of allowed service names |
| `firewall_allowed_ports` | `[]` | Additional ports to allow (e.g., `8443/tcp`) |
| `firewall_log_denied` | `all` | Logging level for denied traffic |

## Usage

```yaml
- hosts: all
  roles:
    - role: acme.security_policies.cis_benchmark
      cis_level: 2
      cis_audit_only: true

    - role: acme.security_policies.firewall_baseline
      firewall_allowed_services:
        - ssh
        - https
```

## License

Proprietary - ACME Corp Internal Use Only

## Author

ACME Corp Platform Engineering Team

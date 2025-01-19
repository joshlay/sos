# sos

This role installs [sosreport](https://github.com/sosreport/sos),
[xsos](https://github.com/ryran/xsos),
and configures _(optional)_ `extras.d` entries

## Variables

1. `sos_extras`: custom commands or files in `sos` reports.
Default: see [Example Playbook](#example-playbook)
2. `sos_xsos`: controls [xsos](https://github.com/ryran/xsos) installation.
Default: `true`
3. `sos_xsos_url`: `xsos` installation URL.
[Default](https://github.com/ryran/xsos/raw/master/xsos)

## Example Playbook

```yaml
---
- name: "'sos' role"
  hosts: all
  roles:
    - name: Configure 'sosreport' w/ extra files and checks
      role: sos
      sos_extras:
        amdgpu:
          - 'rocm-smi -a'
          - ':/sys/class/drm/card*/device/pp_features'
          - ':/sys/class/drm/card*/device/numa_node'
        systemd:
          - 'systemctl status'
          - 'systemd-analyze critical-chain'
        cri:
          - 'podman system info'
          - 'docker system info'
```

## License

MIT

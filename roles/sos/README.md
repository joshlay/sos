sos
=========

This role installs [sosreport](https://github.com/sosreport/sos)
and configures optional `extras.d` entries

Role Variables
--------------

1. `sos_extras`

Custom commands or files in `sos` reports.

Example Playbook
----------------

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
              - podman system info
              - docker system info

License
-------

MIT

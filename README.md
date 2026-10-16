# sysrq-on-shutdown

A systemd unit that enables the full [SysRq](https://docs.kernel.org/admin-guide/sysrq.html)
key set for the duration of the shutdown and reboot sequence.

## Why

The Linux kernel default for `/proc/sys/kernel/sysrq` restricts which SysRq
commands are available. Arch Linux ships `16`, which only allows `s`
(sync). That means the keys that matter most when a machine is hanging —
`b` (reboot), `o` (power off), `u`/`e`/`i` — are masked exactly when you need
them.

This unit writes `1` to `/proc/sys/kernel/sysrq`, ordered `Before=shutdown.target`,
so the full key set is available while services and storage are being brought
down.

## Install

From the AUR:

```console
$ git clone https://aur.archlinux.org/sysrq-on-shutdown.git
$ cd sysrq-on-shutdown
$ makepkg -si
```

The unit is **not** enabled automatically. Enable it with:

```console
$ sudo systemctl enable sysrq-on-shutdown.service
```

## Usage

```console
$ sudo systemctl enable sysrq-on-shutdown.service   # queue for shutdown/reboot
$ sudo systemctl start sysrq-on-shutdown.service    # also apply right now
$ cat /proc/sys/kernel/sysrq                        # inspect current value
```

See `man 8 sysrq-on-shutdown` for the full description.

## Files

| Path | Purpose |
| --- | --- |
| `/usr/lib/systemd/system/sysrq-on-shutdown.service` | the unit |
| `/usr/share/man/man8/sysrq-on-shutdown.8` | manual page |

## Notes

* A persistent alternative for the whole run time is `kernel.sysrq = 1` in
  `/etc/sysctl.d/`.
* Enabling the full SysRq set also lets a console user force a reboot or dump
  kernel state; scoping it to the shutdown path limits that window.

## License

CC0-1.0 — released into the public domain. See [LICENSE](LICENSE).

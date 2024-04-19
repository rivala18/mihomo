# mihomo
  Konfigurasi clash untuk linux
# Konfigurasi
- Unduh kernel [mihomo](https://github.com/MetaCubeX/mihomo/releases)
- Ubah nama file menjadi `mihomo` dan copy ke `/usr/local/bin`
  ```shell
  cp mihomo /usr/local/bin
  ```
- Unduh [config.yaml](https://github.com/rivala18/mihomo/blob/main/config.yaml) dan copy ke `/etc/mihomo`
  ```shell
  cp config.yaml /etc/mihomo
- Buat file konfigurasi systemd di `/etc/systemd/system/mihomo.service`
```ini
[Unit]
Description=mihomo Daemon, Another Clash Kernel.
After=network.target NetworkManager.service systemd-networkd.service iwd.service

[Service]
Type=simple
LimitNPROC=500
LimitNOFILE=1000000
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_RAW CAP_NET_BIND_SERVICE CAP_SYS_TIME CAP_SYS_PTRACE CAP_DAC_READ_SEARCH CAP_DAC_OVERRIDE
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_RAW CAP_NET_BIND_SERVICE CAP_SYS_TIME CAP_SYS_PTRACE CAP_DAC_READ_SEARCH CAP_DAC_OVERRIDE
Restart=always
ExecStartPre=/usr/bin/sleep 1s
ExecStart=/usr/local/bin/mihomo -d /etc/mihomo
ExecReload=/bin/kill -HUP $MAINPID

[Install]
WantedBy=multi-user.target
```
- Reload systemd command

```shell
systemctl daemon-reload
```

- Enable service Mihomo command

```shell
systemctl enable mihomo
```

- Mulai mihomo dengan command

```shell
systemctl start mihomo
```

# Command mihomo
- Reload Mihomo

```shell
systemctl reload mihomo
```

- Cek status Mihomo

```shell
systemctl status Mihomo
```

- Cek log Mihomo yang sedang berjalan

```shell
journalctl -u mihomo -o cat -e
```

Atau

```shell
journalctl -u mihomo -o cat -f
```


ystemd is a system and service manager for [[Linux]] operating systems. It is designed to be backward compatible with SysV init scripts and provides many features such as parallel startup of system services at boot time, on-demand activation of daemons, or dependency-based service control logic [access.redhat.com](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system_administrators_guide/chap-managing_services_with_systemd).

The main goal of systemd is to unify service configuration and behavior across Linux distributions [en.wikipedia.org](https://en.wikipedia.org/wiki/Systemd). It includes features like on-demand starting of daemons, mount and automount point maintenance, snapshot support, and process tracking using Linux control groups [linode.com](https://www.linode.com/docs/guides/what-is-systemd/).

```zsh
# To check the status of a service
systemctl status <service_name>

# To start a service
systemctl start <service_name>

# To stop a service
systemctl stop <service_name>

# To enable a service to start on boot
systemctl enable <service_name>

# To disable a service from starting on boot
systemctl disable <service_name>

```

### Configuring DoT ([[DNS]] over TLS) using Systemd

1. Edit the configuration file for the `systemd-resolved` service. This file is typically located at `/etc/systemd/resolved.conf` and contains settings for the DNS resolver service in systemd. 
 ```conf
 [Resolve]
 DNS=1.1.1.1 1.0.0.1 8.8.8.8
  36   │ FallbackDNS=1.1.1.1 8.8.8.10 8.8.8.8
  37   │ DNSSEC=yes
  38   │ DNSOverTLS=yes
 ```

3. You then used `systemctl`, a [[CLI|command-line]] utility that interacts with systemd and manages system services, to restart the `systemd-resolved` service. This is done with the command:
```zsh
# Restart the service to apply changes
sudo systemctl restart systemd-resolved.service

# Ensure that your changes persist after reboot
sudo systemctl enable systemd-resolved.service

# Check the resolve
systemd-resolve --status
```

# Nice to know Unraid commands

## Docker service

```bash
/etc/rc.d/rc.docker <command>
```

**Available commands:**
==start== ==stop== ==restart== ==status==

## Docker containers

```bash
docker <command> <containername>
```

**Available commands:**
==start== ==stop== ==restart== ==pasue== ==logs==

**Print all container names:**
```bash
docker ps --format ‘{{.Names}}’
```
**Print all container images:**
```bash
docker ps --format ‘{{.Image}}’
```

## Nginx

```bash
/etc/rc.d/rc.nginx <command>
```

**Available commands:**
==start== ==stop== ==restart== ==status==

## PHP

```bash
/etc/rc.d/rc.php-fpm <command>
```

**Available commands:**
==start== ==stop== ==restart== ==status==



## VM Service

==start== ==stop==

```bash
/etc/rc.d/rc.libvirt <command>
```

**List all domains:**
```bash
virsh list --all
```

### Domains

==start== ==shutdown== ==reboot== ==suspend==

```bash
virsh <command> <domain>
```

## Samba

==start== ==stop==

```bash
/etc/rd.d/rc.samba <command>
```

## Unraid

### Shutdown/Reboot

==reboot== ==poweroff== ==shutdown==

```bash
/sbin/<command>
```

!!! note "Note"
    `poweroff` will gracefully shut everything down, even spin down the hard drives,
    but will not actually turn off the power supply.But there is a race condition in the code
    which could cause the system to power off before the Flash is updated indicating 'clean shutdown'.
    This can't cause data loss, but will cause parity-check to automatically start upon next reboot.

### Run diagnostics

```bash
diagnostics
```

### Tail the syslog

```bash
tail -f /var/log/syslog
```

### Look at the parameters in the config file

```bash
nano /boot/syslinux.cfg-
```

### Create a backup image of your usb and store it on disk1

```bash
dd if=/dev/sda of=/mnt/disk1/unraid.img
```

### Copy files using midnight commander

```bash
mc
```

### Check power on hours for all drives

```bash
for drive in $(ls -la /dev | grep -Ev 'sda|sd[a-z][0-9]' | grep sd[a-z] | awk '{print $10}'); do hours=$(smartctl --all /dev/${drive} | grep Power_On_Hours | awk '{print $10}'); echo "Power on Hours for ${drive}: ${hours}"; echo ''; done
```

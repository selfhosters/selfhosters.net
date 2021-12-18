
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
==start== ==stop== ==restart== ==pause== ==logs==

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

```bash
/etc/rc.d/rc.libvirt <command>
```

**Available commands:**
==start== ==stop==

**List all domains:**

```bash
virsh list --all
```

### Domains

```bash
virsh <command> <domain>
```

**Available commands:**
==start== ==shutdown== ==reboot== ==suspend==

## Samba

```bash
/etc/rd.d/rc.samba <command>
```

**Available commands:**
==start== ==stop==

## Unraid

### Shutdown/Reboot

```bash
/sbin/<command>
```

**Available commands:**
==reboot== ==poweroff== ==shutdown==

!!! note "Note"
    `poweroff` If you get an unclean shutdown when issuing this command you need to adjust your timeout settings,
    see [https://forums.unraid.net/topic/69868-dealing-with-unclean-shutdowns](https://forums.unraid.net/topic/69868-dealing-with-unclean-shutdowns)

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

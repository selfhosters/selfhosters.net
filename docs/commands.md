
# Nice to know Unraid commands

## Docker service

&nbsp;&nbsp;&nbsp;&nbsp;==start== ==stop== ==restart== ==status==

&nbsp;&nbsp;&nbsp;&nbsp;`/etc/rc.d/rc.docker <command>`

## Docker containers

&nbsp;&nbsp;&nbsp;&nbsp;==start== ==stop== ==restart== ==pause== ==logs==

&nbsp;&nbsp;&nbsp;&nbsp;`docker <command> <containername>`

&nbsp;&nbsp;&nbsp;&nbsp;**Print all container names:** `docker ps --format ‘{{.Names}}’`
&nbsp;&nbsp;&nbsp;&nbsp;**Print all container images:** `docker ps --format ‘{{.Image}}’`

## Nginx

&nbsp;&nbsp;&nbsp;&nbsp;==start== ==stop== ==restart== ==status==

&nbsp;&nbsp;&nbsp;&nbsp;`/etc/rc.d/rc.nginx <command>`

## PHP

&nbsp;&nbsp;&nbsp;&nbsp;==start== ==stop== ==restart== ==status==

&nbsp;&nbsp;&nbsp;&nbsp; `/etc/rc.d/rc.php-fpm <command>`

## VM Service

&nbsp;&nbsp;&nbsp;&nbsp;==start== ==stop==

&nbsp;&nbsp;&nbsp;&nbsp;`/etc/rc.d/rc.libvirt <command>`

&nbsp;&nbsp;&nbsp;&nbsp;**List all domains:** `virsh list --all`

### &nbsp;&nbsp;&nbsp;&nbsp;Domains

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;==start== ==shutdown== ==reboot== ==suspend==

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`virsh <command> <domain>`

## Samba

&nbsp;&nbsp;&nbsp;&nbsp;==start== ==stop==

&nbsp;&nbsp;&nbsp;&nbsp;`/etc/rd.d/rc.samba <command>`

## Unraid

### Shutdown/Reboot

&nbsp;&nbsp;&nbsp;&nbsp;==reboot== ==poweroff== ==shutdown==

&nbsp;&nbsp;&nbsp;&nbsp;`/sbin/<command>`

!!! note "Note"
    `poweroff` will gracefully shut everything down, even spin down the hard drives,
    but will not actually turn off the power supply.But there is a race condition in the code
    which could cause the system to power off before the Flash is updated indicating 'clean shutdown'.
    This can't cause data loss, but will cause parity-check to automatically start upon next reboot.

### Run diagnostics

`diagnostics`

### Tail the syslog

`tail -f /var/log/syslog`

### Look at the parameters in the config file

`nano /boot/syslinux.cfg-`

### Create a backup image of your usb and store it on disk1

`dd if=/dev/sda of=/mnt/disk1/unraid.img`

### Copy files using midnight commander

`mc`

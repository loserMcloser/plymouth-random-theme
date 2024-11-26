# Description

This is a script and SystemD service file to choose a new plymouth theme on every shutdown/reboot.
The script will randomly choose a theme from `/usr/share/plymouth/themes/` and load it into your initramfs for the next boot.
You can exclude themes from being randomly chosen by including them in `/etc/plymouth/random-theme.exclude`, one per line. (See the sample `random-theme.exclude` included in this repo.)

There is currently only one command-line option: `--backup` will create a backup of your current initramfs in `/boot`.
The default is to not create a backup, since space on `/boot` might be limited.
If you want a backup created every time when using the SystemD service,
copy `plymouth-random-theme-service-backup.conf` from this repo to the location `/etc/systemd/system/plymouth-random-theme.d/backup.conf` and then run `systemctl daemon-reload` (as root).

A record of theme switches is logged to `/var/log/plymouth-random-theme.log` in case your last boot used a theme you don't care for and want to add it to `random-theme.exclude`.

# WARNINGS

+ This script is **for Arch Linux ONLY**.
+ **USE AT YOUR OWN RISK**. This script unpacks and repacks the initramfs required for boot. Make sure you have a bootable rescue USB (and know how to use it) in case something gets messed up and you need to rebuild your initramfs using `mkinitcpio`.
+ You need to have already run `mkinitcpio` at least once with `plymouth` in the `HOOKS` array in `/etc/mkinitcpio.conf`.
+ The SystemD service file won't work if `/boot` is not mounted before shutdown/reboot. (Having `/boot` set to automount via SystemD also won't work.)

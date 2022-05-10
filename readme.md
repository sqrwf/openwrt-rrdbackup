# OpenWrt RRDBackup


## Rationale

By default, with OpenWrt the collectd RRD database is kept in temporary (RAM) storage. This is a simple init script that backs up the database on router shutdown and restores it on router startup (with optional periodic backups in between). This way, the RRD database persists across (planned) reboots.

## Compatibility

This is a very basic script using very fundamental OpenWrt mechanisms that haven't changed in eons. Tested with OpenWrt 19.07, 21.02, 22.03 and snapshots as of May 2022.

## Installation

* upload `/etc/init.d/rrdbackup` and make it executable (`chmod +x`)

* enable the script: `/etc/init.d/rrdbackup enable`

* optional: make an entry in crontab to backup in regular intervals (e.g. `0 */6 * * * /etc/init.d/rrdbackup backup` for a backup every 6 hours)
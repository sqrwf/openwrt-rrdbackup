# OpenWrt RRDBackup

## Note/update

This script has been integrated, along with some improvements, into [`luci-app-statistics` starting with OpenWrt 23.05.2](https://github.com/openwrt/luci/pull/6646), making that the the preferred and easiest way to have your RRD database persist across reboots.

However, this script is neither outdated nor obsolete. It is still useful if you want to adjust backup parameters, don't have LuCI and/or its Statistics app installed, or prefer to keep the backup functionality standalone.

## Rationale

By default, with OpenWrt the collectd RRD database is kept in temporary (RAM) storage. This simple init script backups the database on router shutdown and restores it on router startup (with optional periodic backups in between). This way, the RRD database persists across (planned) reboots.

## Prerequisites

None that aren't covered with a basic OpenWrt install. The script doesn't really make sense if you're not running _collectd_, though. :wink:

## Compatibility

Tested with OpenWrt 19.07, 21.02, 22.03, and 23.05. This is a very basic script using very fundamental OpenWrt mechanisms that haven't changed in eons and aren't expected to change anytime soon.

## Installation

* upload `/etc/init.d/rrdbackup` and make it executable (`chmod +x /etc/init.d/rrdbackup`)

* optional: adjust the variables for backup path and filename at the top of the script if you're unhappy with the defaults

* enable the script: `/etc/init.d/rrdbackup enable`

* optional: make an entry in crontab to backup in regular intervals (e.g.  
  `0 */6 * * * /etc/init.d/rrdbackup backup`  
  for a backup every 6 hours)

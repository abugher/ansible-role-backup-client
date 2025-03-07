# Usage

To add a backup client:

- Add host to backup-client group.
- Set backup_client_users in host_vars.
- Set backup_paths in host_vars.
- Set backup_minute in host_vars.
- Set backup_hour in host_vars.
- Deploy backup-server role.
- Deploy backup-client role.
- Deploy nagios role, if monitored.
- Be aware that backups will not succeed if backup users' SSH keys are
  encrypted.

# Notes

## snapshots and timestamps

`rsync` must have the `-t` option, causing timestamps to be updated.
Otherwise, `rsync` always thinks the files have changed.  In addition to
burdening the network and slowing the transfer, this causes `btrfs`
"copy on write" model to kick in, duplicating storage allocation that
would otherwise be shared with existing snapshots, so that ongoing
snapshots each consume storage similar in size to the contents of the
filesystem.  The result is that, if `-t` is not given to `rsync` during
backup, backup storage consumption rises by 100% of actual backed up
data size, every day.

The `-c` option, for checksum matching, is almost as good.  It takes
about 50 times longer than checking timestamps, but should result in no
extra space used.  It takes about 1/10 as long as a full transfer.
(Numeric comparisons reflect my processing and networking resources.)

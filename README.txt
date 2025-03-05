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

## checksum matching

In the backup script, `rsync` should get `-c` for checksum matching.
Otherwise, many files get synced every time.  The extra syncs may be due
to timestamp mismatch, possibly caused by filesystem differences, but
that is unconfirmed.  

Resulting from the extra sync, each snapshot seems to contain a full
copy of each updated file, judging from snapshot sizes.  With `-c` in
place for backup jobs, when nothing is actually changed, snapshots have
zero size.  

Backups are also running faster, at 9 minutes vs 161 minutes for the
same directory.

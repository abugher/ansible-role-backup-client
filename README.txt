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

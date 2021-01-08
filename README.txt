To add a backup client:

- Add host to backup_client group.
- Set backup_client_users in host_vars.
- Set backup_paths in host_vars.
- Deploy backup_server role.
- Deploy backup_client role.
- Deploy nagios role, if monitored.
- Be aware that backups will not succeed if backup users' SSH keys are
  encrypted.

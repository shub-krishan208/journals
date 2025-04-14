# 2025-24-14: Jounal Log SPAM

## Issue:

I installed chatgpt-desktop using snap and had problems in sign in so removed it. but the remaining background processes stayed for some reason (even the directory for the application was not there , but these processes were still going on.)

## Symptoms:
- syslog and journal log files /var/log/ became unbelievably large 39GB and 4GB
- '2025-04-14T17:32:04.824206+05:30 workpool env[5261]: [5261:0414/173204.824198:ERROR:address_tracker_linux.cc(447)] Failed to recv from netlink socket: Permission denied (13) ' repeated in syslog

## Cause:
chatgpt-desktop corrupted installation using snap

## Fix:
- looking at the PID of the process, '5261' *number after the env[5261]*
- 'ps -p 5261 -0 comm,args' to get teh name of teh process spamming the error log
- 'ps aux | grep chatgpt' looking at the system processes running with that name
- killing the process in system settings (GUI)
- 'sudo truncate -s 0 /var/log/syslog' truncate the syslog file

## Future Prevention:
Make sure to enable logrotation at '/etc/logrotate.d/rsyslog' and set up the limits accordingly in '/etc/systemd/journald.conf'

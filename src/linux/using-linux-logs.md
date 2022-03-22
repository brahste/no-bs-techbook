# Using Linux Logs

> Links:
> 
> - [What are Linux Logs](https://stackify.com/linux-logs/#:~:text=Linux%20logs%20will%20display%20with,view%20everything%20under%20the%20syslog.)

Linux logs provide a timeline of events. When issues arise when using the Linux operating system, and application, or when conducting general troubleshooting, analyzing the log files is the first place to start to pinpoint the isse.

Linux specific log files are found in the _/var/log_ directory. The _syslog_ is one of the most important logs because it's where everything required for authentication is logged (confirm).

**TODO: Expand on what syslog is**

To view a specific log file you can use

```bash
$ dmesg                    # Prints the kernel ring buffer
$ cat /var/log/syslog      # Prints everything to stdout
$ less /var/log/syslog     # Scrollable stdout, use Shft+G to go to end
$ tail /var/log/syslog     # Shows most recent 10 logs
$ tail -f /var/log/syslog  # Follows/watches most recent 10 logs
$ tail -f -n 25 /var/log/syslog  # Follows most recent 25 logs
```

## Types of Linux Logs

- Application logs

- Event logs

- Service logs

- System logs

## Must Monitor Logs

1. _/var/log/syslog_ (Ubuntu and Debian) or _/var/log/messages_ (Redhat and CentOS): General and system-related logs.

2. _/var/log/auth.log_ or _/var/log/secure_: Authenication related logs such as successful and failed logins.

3. _/var/log/boot.log_: Messages logged during system startup.

4. _/var/log/maillog_: Mail-related logs from email, postfix, or smtpd.

5. _/var/log/kern_: Kernel-related logs and warnings. Especially valuable for monitoring custom kernels.

6. _/var/log/dmesg_: Device driver and hardware-related messages. Use `dmesg` to view the contents of this file.

7. _/var/log/faillog_: Logs related to failed loging attempts. Useful for diagnosing hacks and brute-force attacks.

8. _/var/log/cron_: Crond-related logs.































# Auto suspend when idle
Like [1] I'd like my servers to suspend, but not if
* a user is connected to the system using sshfs
* a user has been connected within the last 30 minutes (it's likely that he will come back, soon)
* a screen session is active (for example when reencoding videos in background)
* the system is active for less than 30 minutes

This document contains instructions for how I set it up on my systems running Ubuntu 16.04.

**Required tools**
* etherwake
* ethtool


Create `/etc/udev/rules/50-wol.rules`
```bash
ACTION=="add", SUBSYSTEM=="net", KERNEL=="eth*", RUN+="/usr/bin/ethtool -s %k wol g"
```

Create `/usr/local/sbin/system-login`
```bash
#!/bin/bash

# Check if process is alive using pgrep -P $pid
ppid="$(ps -p $$ -o ppid= | tr -d ' ')"

activepath="/var/run/system-login/active"
inactivepath="/var/run/system-login/inactive"

case "$PAM_TYPE" in
    'open_session')
        test -d "$activepath" || mkdir -p "$activepath"
        echo "$PAM_USER" > "$activepath/$ppid"
    ;;

    'close_session')
        test -d "$inactivepath" || mkdir -p "$inactivepath"
        test -e "$activepath/$ppid" && mv "$activepath/$ppid" "$inactivepath/$ppid"
    ;;
esac
```

Append to `/etc/pam.d/common-session`
```bash
optional   pam_exec.so          quiet /usr/local/sbin/system-login
```

Create `/lib/systemd/system-sleep/last-resume`
```bash
#!/bin/sh

case $1 in
  post)
    touch "/var/run/last-resume"
    ;;
esac
```

Create `/usr/local/sbin/should-suspend`
```bash
#!/bin/bash

result=0
timeout=30
NOW=`date +%s`

# Check system uptime
test -e /var/run/last-resume || touch /var/run/last-resume
if find /var/run/ -maxdepth 1 -type f -name last-resume -cmin -$timeout | grep -q .; then
    let age=(NOW-$(stat -c %Z /var/run/last-resume))/60
    echo "uptime to short ($age min)"
    result=1
fi

# Check for active screen sessions
if pgrep -l '^screen$'; then
    result=1
fi

# Check for active user
if [ -d "/var/run/system-login/active" ]; then
    for n in $(find /var/run/system-login/active -type f -printf "%f\n"); do
        if pgrep -P "$n" > /dev/null; then
            result=1
            filename="/var/run/system-login/active/$n"
            let age=(NOW-$(stat -c %Z "$filename"))/60
            echo "active login: $n (`cat "$filename"`, $age min)"
        else
            rm "/var/run/system-login/active/$n"
        fi
    done
fi

# Check for logouts that where at least $timeout minutes ago
if [ -d "/var/run/system-login/inactive" ]; then
    for n in $(find /var/run/system-login/inactive -cmin -$timeout -type f -printf "%f\n"); do
        result=1
        filename="/var/run/system-login/inactive/$n"
        let age=(NOW-$(stat -c %Z "$filename"))/60
        echo "inactive login: $n (`cat "$filename"`, $age min)"
    done
fi

exit $result
```

Create `/etc/cron.d/suspend-on-idle`
```bash
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
*/5 * * * * root /usr/local/sbin/should-suspend > /dev/null && systemctl hibernate
```


## Resources
1. http://rolandtapken.de/blog/2013-07/use-autofs-wake-fileserver-demand
2. http://rolandtapken.de/blog/2013-07/suspend-nas-when-idle
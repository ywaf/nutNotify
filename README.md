# nutNotify
Script to send notifications to various services about NUT (network UPS tools) events. Supported services:
- mail
- Telegram
- Pushbullet
- Pushover
- SMS

## Install commands

```
git clone https://github.com/ywaf/nutNotify.git
cd nutNotify
cp nutNotify.conf.txt /usr/local/etc/nutNotify.conf
# add your keys, etc.. >
nano /usr/local/etc/nutNotify.conf
cp nutNotifyFct.sh nutNotifyBoot.sh nutNotify.sh nutShutdown.sh /usr/local/bin
cp systemd-notify /lib/systemd/system/nut-notify-boot.service
systemctl daemon-reload
systemctl enable nut-notify-boot.service
mkdir /var/log/nutNotify
chown nut:nut /var/log/nutNotify
cp nutNotify.logrotate /etc/logrotate.d
chmod +x /usr/local/bin/nutNotify.sh
```

## NUT Configuration
Place these into /etc/nut/upsmon.conf

```
NOTIFYCMD /usr/local/bin/nutNotify.sh
NOTIFYMSG ONLINE "ONLINE %s"
NOTIFYMSG ONBATT "ONBATT %s"
NOTIFYMSG LOWBATT "LOWBATT %s"
NOTIFYMSG FSD "FSD %s"
NOTIFYMSG COMMBAD "COMMBAD %s"
NOTIFYMSG COMMOK "COMMOK %s"
NOTIFYMSG SHUTDOWN "SHUTDOWN %s"
NOTIFYMSG REPLBATT "REPLBATT %s"
NOTIFYMSG NOCOMM "NOCOMM %s"

NOTIFYFLAG ONLINE SYSLOG+EXEC
NOTIFYFLAG ONBATT SYSLOG+EXEC
NOTIFYFLAG LOWBATT SYSLOG+WALL+EXEC
NOTIFYFLAG FSD SYSLOG+WALL+EXEC
NOTIFYFLAG COMMBAD SYSLOG+EXEC
NOTIFYFLAG COMMOK SYSLOG+EXEC
NOTIFYFLAG SHUTDOWN SYSLOG+WALL+EXEC
NOTIFYFLAG REPLBATT SYSLOG+EXEC
NOTIFYFLAG NOCOMM SYSLOG+EXEC
```



## Original Repo Links (not really related to this fork)
Here an article (in french) in my website about [the notification of Nut by Telegram Pushbullet or Pushover](https://www.monlinux.net/2023/02/nut-notifications-push-telegram-pushbullet-pushover-pour-ups/)

You can see a howto to [setup your nut configuration to monitore your UPS from scratch (in french)](https://www.monlinux.net/2018/03/nut-ups-notifications-mails-et-arret/)

# Commands Practiced

## Service Management

systemctl status ssh

systemctl start ssh

systemctl stop ssh

systemctl restart ssh

systemctl enable ssh

systemctl disable ssh

---

## Journal Logs

journalctl

journalctl -n 20

journalctl -f

journalctl -u ssh

---

## Log Files

cd /var/log

tail auth.log

tail -f auth.log

---

## Log Searching

grep "root" /etc/passwd

grep -i "root" file

grep -n "Failed" auth.log

grep -c "Failed password" auth.log

grep -r "Failed password" /var/log

ps -ef | grep ssh

---

## Hashing

md5sum file

sha256sum file

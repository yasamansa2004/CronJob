# CronJob

for user in $(cut -f1 -d: /etc/passwd); do
    echo "User: $user"
    sudo crontab -u $user -l 2>/dev/null
done


_______________________________________________________________________________________

awk -F: '{print $1}' /etc/passwd | while read user; do
  crontab -u $user -l 2>/dev/null | while read line; do
    [[ "$line" =~ ^#.*$ ]] && continue
    echo "User: $user, Job: $line"
  done
done
cat /etc/crontab /etc/cron.d/* 2>/dev/null | grep -v '^#'

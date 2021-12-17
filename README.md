# Fail2ban rule :
Fail2Ban rule for blocking the log4shell exploitation on NGINX service


# in /etc/fail2ban/jail.conf

```
[log4j]
enabled = true
filter = log4j
action   = iptables-multiport[name="log4j", port="http,https"]
port = http, https
logpath = /var/log/nginx/access.log
findtime = 1
bantime = -1
maxretry = 1

```

# in /etc/fail2ban/filter.d/log4j.conf
```
#Filtre REGEX de recherche d'exploitation de la vuln log4Shell (log4j)

# [log4j-jndi]
# maxretry = 1
# enabled = true
# port = 80,443
# logpath = /var/log/nginx/access.log

[Definition]
failregex   = (?i)^<HOST> .* ".*\$.*(7B|\{).*(lower:)?.*j.*n.*d.*i.*:.*".*?$
```


# Restart fail2ban services
```
sudo service fail2ban restart
```


**My IPtables configuration file example:**
```
    *filter
    # SSH
    -A INPUT -p tcp --dport 22 -j ACCEPT

    # PPTP
    -A INPUT -p 47 -j ACCEPT
    -A INPUT -p tcp –dport 1723 -j ACCEPT

    # ALLOW ESTABLISHED CONNECTION FROM INSIDE
    -A INPUT -m conntrack –ctstate ESTABLISHED,RELATED -j ACCEPT

    # FTP
    -A INPUT -p tcp –dport 20 -j ACCEPT
    -A INPUT -p tcp –dport 21 -j ACCEPT
    -A INPUT -m state –state NEW -m tcp -p tcp –dport 1024:65535 -j ACCEPT

    # HTTP
    -A INPUT -p tcp –dport 80 -j ACCEPT

    # mySQL
    -A INPUT -p tcp –dport 3306 -j ACCEPT

    # GENERAL RULES
    -P INPUT DROP
    -P FORWARD ACCEPT
    -P OUTPUT ACCEPT

    COMMIT

    *nat
    # NAT FOR PPTP CLIENTS
    -A POSTROUTING -s 192.168.10.0/24 -d 0.0.0.0/0 -o ens3 -j MASQUERADE

    COMMIT
```

***filter** and ***nat** are chains beginnings.

**COMMIT** closes a chain section.
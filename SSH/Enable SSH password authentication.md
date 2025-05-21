enable ssh password authentication
```bash
grep -r PasswordAuthentication /etc/ssh -l | xargs -n 1 sed -i 's/#\s*PasswordAuthentication\s.*$/PasswordAuthentication yes/; s/^PasswordAuthentication\s*no$/PasswordAuthentication yes/'
```




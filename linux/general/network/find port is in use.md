```bash
sudo netstat -tulpn | grep :8080
```

- `-t`: Shows TCP connections.
- `-u`: Shows UDP connections.
- `-l`: Shows only listening sockets.
- `-p`: Shows the PID and program name.
- `-n`: Shows numerical addresses instead of resolving hostnames.
- `grep :8080`: Filters the output to show only lines containing the specified port.
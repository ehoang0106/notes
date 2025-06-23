create a second tunnel like normal:

```js
cloudflared tunnel create [your-tunnel-name]
```

create a config for a tunnel:


```js
sudo nano ~/.cloudflared/your-second-tunnel-config.yml
```

config example:

```js
tunnel: my-second-tunnel
credentials-file: /home/pi/.cloudflared/my-second-tunnel.json

ingress:
  - hostname: something.yourdomain.com
    service: http://localhost:1234
  - service: http_status:404

```

create a service:

```js
sudo nano /etc/systemd/system/cloudflared-second.service
```

example content:

```js
[Unit]
Description=Cloudflare Tunnel Second Instance
After=network.target

[Service]
TimeoutStartSec=0
Type=simple
ExecStart=/usr/local/bin/cloudflared --config /home/pi/.cloudflared/config-second.yml tunnel run my-second-tunnel
Restart=always
User=pi

[Install]
WantedBy=multi-user.target

```


enable service:

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable cloudflared-second
sudo systemctl start cloudflared-second
```
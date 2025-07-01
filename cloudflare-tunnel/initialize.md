install cloudflare

```bash
sudo mkdir -p --mode=0755 /usr/share/keyrings

curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg | sudo tee /usr/share/keyrings/cloudflare-main.gpg >/dev/null

echo "deb [signed-by=/usr/share/keyrings/cloudflare-main.gpg] https://pkg.cloudflare.com/cloudflared any main" | sudo tee /etc/apt/sources.list.d/cloudflared.list

sudo apt-get update && sudo apt-get install cloudflared
```

login to cloudflare tunnel

```bash
cloudflared tunnel login
```

create tunnel:

```bash
cloudflared tunnel create [NAME_OF_YOUR_TUNNEL]
```

config file:

```bash
sudo nano ~/.cloudflared/config.yml
```

```sh
tunnel: [TUNNEL_ID]
credentials-file: [PATH_OF_THE_CERT_ABOVE]

ingress:
	- hostname: [your-subdomain].[your-domain] #pi4.khoah.com
	  service: ssh://localhost:22
	- service: http_status:404
```

create tunnel dns

```bash
cloudflared tunnel route dns [TUNNEL_ID] [HOSTNAME]
```

use this for create service: [[multiple tunnel]]
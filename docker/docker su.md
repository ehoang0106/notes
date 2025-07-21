add docker to su

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```

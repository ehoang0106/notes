```bash
#!/bin/bash

sudo yum install -y ecs-init

sudo echo ECS_CLUSTER="NAME_YOUR_CLUSTER" | sudo tee /etc/ecs/ecs.config

sudo systemctl start docker

sudo systemctl enable --now --no-block ecs.service
```

This command will install ecs agent and install docker then run docker and enable ecs.service
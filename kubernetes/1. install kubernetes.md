
`x86` download:

```bash
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

`arm` download:

```bash
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl.sha256"
```

after download, install k8s:

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

test if installed successfully:

```bash
kubectl version --client
```


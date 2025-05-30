
Generate SSH Keypair on your Local PC:

```bash
ssh-keygen -t rsa -b 4096
```



ssh to the server then set the permission of the `/.ssh` folder 

```bash
chmod 700 ~/.ssh
```

Copy your public key (e.g: `id_rsa.pub`) to the server you want to ssh (manually way):

In your local machine, get the public key and copy it:
```bash
cat ~/.ssh/id_rsa.pub
```

Then go to the server:

```bash
echo "PASTE_YOUR_PUBLIC_KEY_HERE" >> ~/.ssh/authorized_keys
```

Change the permission for the key:

```bash
chmod 600 ~/.ssh/authorized_keys
```

Done!

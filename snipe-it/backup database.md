Run `snipeit:backup` inside the container `snipe-it-app-1`:

```bash
docker exec -it snipe-it-app-1 bash -c 'php artisan snipeit:backup'
```

Copy the folder `/var/www/html/storage/app/backups/` to the host:

```bash
 sudo docker cp snipe-it-app-1:/var/www/html/storage/app/backups/ /mnt/snipe-it/
```

Zip the folder `backups`: 

```bash
sudo zip -r backups.zip /mnt/snipe-it/backups/
```

Upload to `s3`: 

```bash
aws s3 cp backups.zip s3://as-snipeit-backup/
```


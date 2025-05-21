create folder:
```
sudo mkdir -p /mnt/qnap
```
~
create a credentials file `~/.smbcredentials`
```
username=<your-username>
password=<your-password>

```
then mount:
make sure to adjust the path of the qnap: `//11.0.0.53/Software` 

```
sudo mount -t cifs //11.0.0.53/Software /mnt/qnap -o credentials=/home/khoa/Desktop/qnap/.smbcredentials,vers=3.0,uid=$(id -u),gid=$(id -g),file_mode=0777,dir_mode=0777
```

```
CREATE TABLE IF NOT EXISTS orbwatcher (id INT AUTO_INCREMENT PRIMARY KEY, currency_id VARCHAR(255), currency_name VARCHAR(255), price_value VARCHAR(255), exchange_price_value VARCHAR(255), date DATETIME, created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP)
```
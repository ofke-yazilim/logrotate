# logrotate
If you want to split log files daily then you could use logrotate module for linux environments. I will tell how to make it.

- Firstly, we install **logrotate** module for system.
```yum update && yum install logrotate```
- Logrotate configirations are in **/etc/logrotate.conf**
- Logrotate web server configirations are in **/etc/logrotate.d**
> Note : I use nginx web server so i will make the configirations for nginx.
- Open the **/etc/logrotate.d/nginx** file with editor and then add the following commands in.
```html
 /var/log/nginx/access.log {
    create 0640 nginx root
    daily
    rotate 10
    missingok
    dateext
    dateformat -%d-%m-%Y
    olddir /var/log/access
    notifempty
    compress
    delaycompress
}
```
> The above commands provides that access log data will be wrote to daily files in **/var/log/access**, If you have not **/var/log/access** folder then you should create it with : ``mkdir /var/log/access``
- Lastly you have to add a cron job and it should work daily. It is command:
```html
logrotate -f /etc/logrotate.d/nginx
```

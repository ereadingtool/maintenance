# Maintenance Page

I've found that the easiest way to tell a user that the site is undergoing maintenance is 
to show them the maintenance page that lives in a separate repository `ereadingtool/maintenance`. To do this, hop onto the `node_frontend` container with `docker exec -it node_frontend /bin/bash`. Make a directory `/var/www/maintenance/html` and place the following files in it:
```
.
|-- dist
|   `-- elm.compiled.js
|-- img
|   `-- engineering_black.svg
|-- index.html
`-- main.js
```
Then create a configuration file at `/etc/nginx/sites-available/maintenance` by `cp`ing `/etc/nginx/sites-available/<SITE>.<TLD>`. Change line 8 of this file to `root /var/www/maintenance/html;`. Head over to `/etc/nginx/site-enabled` and create the symbolic link to `/etc/nginx/sites-available` 
```
ln -s /etc/nginx/sites-available/maintenance /etc/nginx/sites-enabled/
```
being sure to delete the other enabled symbolic link. Reload the page with
```
service nginx reload
```
There should now be a maintenance page.

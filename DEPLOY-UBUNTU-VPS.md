# Run the site on an Ubuntu VPS

Two ways: **quick test** (Python) or **proper setup** (Nginx).

---

## Option 1: Quick test with Python (no install)

On the VPS, after you’ve copied your project folder:

```bash
cd /path/to/the\ beautiful\ ART.
python3 -m http.server 8000
```

- Site: **http://YOUR_VPS_IP:8000**
- Stop: `Ctrl+C`
- Not ideal for “always on” or production.

---

## Option 2: Nginx (recommended for always-on)

### 1. Copy the site to the VPS

From your **local machine** (replace with your VPS IP and path):

```bash
cd "/home/hessi/Desktop/Developement/the beautiful ART."
scp -r index.html styles.css script.js assets .nojekyll user@YOUR_VPS_IP:/tmp/blue-note-site/
```

Or use **rsync**:

```bash
rsync -avz --exclude '*.txt' --exclude '*.md' \
  "./" user@YOUR_VPS_IP:/tmp/blue-note-site/
```

(Excluding `.txt`/`.md` keeps README/instructions off the server; include them if you want.)

### 2. On the VPS: install Nginx

```bash
sudo apt update
sudo apt install nginx -y
```

### 3. Put the site where Nginx will serve it

```bash
sudo mkdir -p /var/www/blue-note
sudo cp -r /tmp/blue-note-site/* /var/www/blue-note/
sudo chown -R www-data:www-data /var/www/blue-note
```

### 4. Add a site config

```bash
sudo nano /etc/nginx/sites-available/blue-note
```

Paste this (replace `YOUR_DOMAIN_OR_IP` with your domain or VPS IP):

```nginx
server {
    listen 80;
    server_name YOUR_DOMAIN_OR_IP;
    root /var/www/blue-note;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~* \.(mp3|png|jpg|jpeg|gif|ico|css|js)$ {
        expires 7d;
        add_header Cache-Control "public";
    }
}
```

Save and exit (`Ctrl+X`, then `Y`, then `Enter`).

### 5. Enable the site and restart Nginx

```bash
sudo ln -s /etc/nginx/sites-available/blue-note /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 6. Open in browser

- **http://YOUR_VPS_IP** or **http://yourdomain.com**

---

## Firewall (if you can’t reach the site)

```bash
sudo ufw allow 80/tcp
sudo ufw allow 22/tcp
sudo ufw enable
```

---

## HTTPS with Let’s Encrypt (optional)

If you use a **domain** pointing to the VPS:

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourdomain.com
```

Then use **https://yourdomain.com**.

---

## Update the site later

From your machine:

```bash
rsync -avz --exclude '*.txt' --exclude '*.md' \
  "./" user@YOUR_VPS_IP:/tmp/blue-note-site/
```

On the VPS:

```bash
sudo cp -r /tmp/blue-note-site/* /var/www/blue-note/
```

No need to restart Nginx for static file updates.

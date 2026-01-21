# 09. Deploy ke VPS (Ubuntu + Nginx)

## 🖥️ Persiapan VPS

### Requirements

- Ubuntu 22.04 LTS
- Minimal 1GB RAM
- SSH access

### Install Dependencies

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Nginx
sudo apt install nginx -y

# Install PHP 8.2
sudo apt install software-properties-common -y
sudo add-apt-repository ppa:ondrej/php -y
sudo apt update
sudo apt install php8.2 php8.2-fpm php8.2-mysql php8.2-mbstring php8.2-xml php8.2-bcmath php8.2-curl php8.2-zip php8.2-gd -y

# Install MySQL
sudo apt install mysql-server -y
sudo mysql_secure_installation

# Install Composer
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install nodejs -y
```

## 📦 Upload Project

```bash
# Di VPS, buat folder
sudo mkdir -p /var/www/inventory
sudo chown -R $USER:$USER /var/www/inventory

# Clone atau upload project
cd /var/www
git clone https://github.com/username/inventory-filament.git inventory
# Atau upload via SFTP

cd inventory
composer install --optimize-autoloader --no-dev
```

## ⚙️ Configure Environment

```bash
cp .env.example .env
nano .env
```

```env
APP_NAME="Inventory System"
APP_ENV=production
APP_DEBUG=false
APP_URL=https://yourdomain.com

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=inventory_db
DB_USERNAME=inventory_user
DB_PASSWORD=your_secure_password
```

```bash
php artisan key:generate
```

## 🗄️ Setup Database

```bash
sudo mysql -u root -p

CREATE DATABASE inventory_db;
CREATE USER 'inventory_user'@'localhost' IDENTIFIED BY 'your_secure_password';
GRANT ALL PRIVILEGES ON inventory_db.* TO 'inventory_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

```bash
php artisan migrate --force
php artisan db:seed --force
```

## 🔧 Configure Nginx

```bash
sudo nano /etc/nginx/sites-available/inventory
```

```nginx
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;
    root /var/www/inventory/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;
    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

```bash
sudo ln -s /etc/nginx/sites-available/inventory /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

## 🔒 Set Permissions

```bash
sudo chown -R www-data:www-data /var/www/inventory
sudo chmod -R 755 /var/www/inventory
sudo chmod -R 775 /var/www/inventory/storage
sudo chmod -R 775 /var/www/inventory/bootstrap/cache

php artisan storage:link
```

## ⚡ Optimize

```bash
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan icons:cache
php artisan filament:cache-components
php artisan filament:assets
```

## 🔐 SSL dengan Let's Encrypt

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

## ✅ Test

Buka `https://yourdomain.com/admin` dan login!

---

## 🎓 Recap Tutorial Intermediate

Anda telah belajar:

- ✅ Multi-role (Admin/Staff)
- ✅ Policies & Authorization
- ✅ Complex relations
- ✅ Dashboard widgets & charts
- ✅ Custom actions
- ✅ Notifications system
- ✅ Deploy ke VPS dengan Nginx

## ➡️ Lanjut ke Level Pro

Siap naik level? Lanjut ke: [Tutorial Pro](../03-pro/README.md)

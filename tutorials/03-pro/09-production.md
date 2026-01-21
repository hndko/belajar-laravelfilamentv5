# 09. Production Deployment

## 🚀 Full Production Setup

### Server Requirements

- Ubuntu 22.04 LTS
- 2GB+ RAM
- Nginx
- PHP 8.2
- MySQL 8.0
- Redis (untuk queue & cache)
- SSL Certificate

## 📦 Docker Setup (Alternative)

### docker-compose.yml

```yaml
version: "3.8"

services:
  app:
    build: .
    volumes:
      - .:/var/www/html
    depends_on:
      - mysql
      - redis

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - .:/var/www/html
      - ./docker/nginx.conf:/etc/nginx/conf.d/default.conf

  mysql:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: booking_saas
    volumes:
      - mysql_data:/var/lib/mysql

  redis:
    image: redis:alpine

volumes:
  mysql_data:
```

## 🔄 CI/CD dengan GitHub Actions

Buat `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      mysql:
        image: mysql:8.0
        env:
          MYSQL_ROOT_PASSWORD: secret
          MYSQL_DATABASE: testing
        ports:
          - 3306:3306

    steps:
      - uses: actions/checkout@v4

      - name: Setup PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: "8.2"
          extensions: mbstring, mysql, xml, bcmath

      - name: Install Dependencies
        run: composer install --no-progress --prefer-dist

      - name: Run Tests
        env:
          DB_CONNECTION: mysql
          DB_HOST: 127.0.0.1
          DB_DATABASE: testing
          DB_USERNAME: root
          DB_PASSWORD: secret
        run: php artisan test

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'

    steps:
      - name: Deploy to Server
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.SERVER_HOST }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SERVER_KEY }}
          script: |
            cd /var/www/booking-saas
            git pull origin main
            composer install --no-dev --optimize-autoloader
            php artisan migrate --force
            php artisan config:cache
            php artisan route:cache
            php artisan view:cache
            php artisan filament:cache-components
            php artisan icons:cache
            php artisan queue:restart
```

## 🔧 Production .env

```env
APP_NAME="Booking SaaS"
APP_ENV=production
APP_KEY=base64:...
APP_DEBUG=false
APP_URL=https://yourdomain.com

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=booking_saas
DB_USERNAME=booking_user
DB_PASSWORD=secure_password

CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis

REDIS_HOST=127.0.0.1

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailgun.org
```

## 📋 Production Checklist

### Security

- [ ] APP_DEBUG=false
- [ ] Secure APP_KEY
- [ ] HTTPS enabled
- [ ] Firewall configured
- [ ] Database credentials secure

### Performance

- [ ] OPcache enabled
- [ ] Redis for cache/queue
- [ ] Database indexes
- [ ] Filament assets cached

### Monitoring

- [ ] Error logging (Sentry/Bugsnag)
- [ ] Server monitoring
- [ ] Database backups
- [ ] SSL auto-renewal

## 🎉 Deployment Complete!

---

## 🎓 Master Level Achieved!

Selamat! Anda telah menyelesaikan tutorial Pro dan menguasai:

- ✅ Multi-Panel Architecture
- ✅ Multi-Tenant System
- ✅ Complex Relations
- ✅ Advanced Authorization
- ✅ Real-time Features
- ✅ Automated Testing
- ✅ Production Deployment dengan CI/CD

## 🚀 Next Steps

1. **Build your own SaaS** dengan pengetahuan ini
2. **Contribute** ke Filament ecosystem
3. **Share** knowledge dengan komunitas
4. **Freelance** atau bangun startup!

**Selamat! Anda siap untuk dunia kerja dan freelance! 🎊**

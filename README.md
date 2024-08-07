# APP

## Menyiapkan struktur deployment
```bash
$ docker create --name temp-dkb dhanuprys/kalender-bali:latest \
    && docker cp temp-dkb:/var/www/html/.env.example ./.env \
    && docker cp temp-dkb:/var/www/html/storage . \
    && docker cp temp-dkb:/var/www/html/docker-compose.prod.yaml ./docker-compose.yaml \
    && docker rm temp-dkb
```

## Mengatur file environment (.env)
Anda dapat membuka konfigurasi environment menggunakan text editor atau menggunakan nano (jika melalui CLI)
```bash
$ nano .env
```
### Mengatur port publish aplikasi
Port publish adalah port yang akan di ekspos oleh container yang nantinya akan diakses oleh pengguna
```
APP_PORT=<angka>
```

### Mengatur database
```
DB_USERNAME -> Username database
DB_PASSWORD -> Password database
DB_DATABASE -> Nama database
```

## Memulai aplikasi
```bash
$ docker compose up -d
```

## Konfigurasi KEY
```bash
$ docker compose exec -ti webapp php artisan key:generate
```

## Melakukan migrasi
```bash
$ docker compose exec -ti webapp php artisan migrate
```

## Membuat akun admin
```bash
$ docker compose exec -ti webapp php artisan make:filament-user
```

## Membuat daftar libur (api-harilibur.vercel.app)
```bash
$ docker compose exec -ti webapp php artisan app:fetch-holidays
```

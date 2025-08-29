# GENIEACS INSTALL MULTITAB

# GENIEACS INSTALL MBPS20

## Cara Penggunaan

```bash
apt install git curl -y
```

```bash
git clone https://github.com/MBPS20/ACS.git
```

```bash
cd ACS
```

```bash
chmod +x install-v22-04.sh
```

Ubuntu 20.04/22.04

```bash
bash install-v22-04.sh
```

ARMBIAN

```bash
bash install-armbian.sh
```

```bash
reboot
```

## Kalau sudah ada GenieACS

```bash
cp -r genieacs /usr/lib/node_modules/
```

```bash
mongorestore --db genieacs --drop db
```

```bash
reboot
```

## Instalasi Menggunakan Docker (Direkomendasikan)

### Persyaratan

* Docker Engine 20.10.0 atau lebih baru
* Docker Compose 2.0.0 atau lebih baru
* Minimal 2GB RAM (4GB direkomendasikan)
* Minimal 10GB ruang disk

### Langkah-langkah Instalasi

1. **Clone Repository**

   ```bash
   git clone https://github.com/MBPS20/ACS.git
   cd ACS
   ```

2. **Persiapan Direktori**

   ```bash
   mkdir -p db ext logs config
   chmod -R 777 db ext logs
   ```

3. **Konfigurasi Awal**

   * Salin file konfigurasi contoh:

     ```bash
     cp config/genieacs.json.example config/genieacs.json
     ```
   * Edit file konfigurasi sesuai kebutuhan:

     ```bash
     nano config/genieacs.json
     ```

4. **Jalankan dengan Docker Compose**

   ```bash
   # Bangun dan jalankan container
   docker-compose up -d --build

   # Pantau log
   docker-compose logs -f
   ```

5. **Akses GenieACS**

   * Web UI: [http://localhost:3000](http://localhost:3000)

     * Username: `admin`
     * Password: `admin` (segera ganti setelah login pertama)
   * API: [http://localhost:7557](http://localhost:7557)
   * CWMP (TR-069): `http://your-server-ip:7547`

### Perintah Penting

```bash
# Menjalankan perintah di dalam container
docker-compose exec genieacs <command>

# Melihat log
docker-compose logs -f

# Menghentikan semua layanan
docker-compose down

# Backup database
./backup-db.sh

# Restart layanan
docker-compose restart
```

### Variabel Lingkungan

Anda dapat menyesuaikan konfigurasi melalui environment variables di file `.env`:

```env
# Kredensial MongoDB
MONGO_INITDB_ROOT_USERNAME=genieacs
MONGO_INITDB_ROOT_PASSWORD=genieacs
MONGO_INITDB_DATABASE=genieacs

# Konfigurasi GenieACS
GENIEACS_UI_JWT_SECRET=your-secure-secret
GENIEACS_UI_INITIAL_USER=admin
GENIEACS_UI_INITIAL_PASSWORD=admin

# Opsional: Sesuaikan dengan kebutuhan
# NODE_ENV=production
# GENIEACS_EXT_DIR=/opt/genieacs/ext
```

### Menggunakan Docker Desktop

#### Cara 1: Menggunakan Docker Dashboard (GUI)

1. Buka Docker Desktop
2. Klik tombol "Build" di sidebar kiri
3. Pilih direktori proyek GenieACS
4. Beri nama image (contoh: `genieacs:latest`)
5. Klik "Build"

#### Cara 2: Menggunakan Terminal Docker Desktop

1. Buka terminal di Docker Desktop (atau terminal biasa)
2. Arahkan ke direktori proyek:

   ```bash
   cd /path/ke/ACS
   ```
3. Build image:

   ```bash
   docker build -t genieacs:latest .
   ```

#### Cara 3: Menggunakan Docker Compose (Direkomendasikan)

1. Buka terminal di direktori proyek
2. Jalankan perintah berikut untuk membangun dan menjalankan:

   ```bash
   # Build dan jalankan semua service
   docker-compose up -d --build

   # Atau untuk service tertentu (contoh: hanya genieacs)
   docker-compose up -d --build genieacs
   ```

#### Memeriksa Image yang Telah Dibangun

```bash
# Melihat daftar image
docker images

# Melihat container yang sedang berjalan
docker ps

# Melihat log container
docker logs <container_id>
```

#### Menjalankan Container dari Image yang Telah Dibangun

```bash
# Menjalankan container
docker run -d --name genieacs -p 3000:3000 -p 7547:7547 -p 7557:7557 -p 7567:7567 genieacs:latest

# Atau gunakan docker-compose
docker-compose up -d
```

#### Troubleshooting

* Jika build gagal, periksa log build:

  ```bash
  docker-compose logs --tail=100 -f
  ```
* Jika port sudah digunakan, hentikan service yang menggunakan port tersebut atau ubah port di `docker-compose.yml`
* Pastikan Docker Desktop sudah berjalan dengan baik (ikon Docker di system tray berwarna putih)

## Lisensi

2025 MBPS20 ACS MULTITAB








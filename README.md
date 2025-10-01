# SOFTWARE REQUIREMENTS SPECIFICATION (SRS)
# SISTEM IKAN SHOP

**Versi:** 1.0  
**Tanggal:** 1 Oktober 2025  
**Status:** Draft

---

## DAFTAR REVISI

| Versi | Tanggal | Deskripsi | Penulis |
|-------|---------|-----------|---------|
| 1.0 | 01/10/2025 | Dokumen awal SRS | Ultraman |

---

## 1. PENDAHULUAN

### 1.1 Tujuan Dokumen
Dokumen Software Requirements Specification (SRS) ini bertujuan untuk mendeskripsikan secara komprehensif dan rinci seluruh kebutuhan fungsional dan non-fungsional dari sistem **Ikan Shop**. Dokumen ini ditujukan untuk:

- **FORR A TEAM**: Sebagai panduan teknis dalam implementasi sistem
- **Stakeholder & Investor**: Untuk memahami ruang lingkup dan kemampuan sistem
- **Quality Assurance**: Sebagai acuan pengujian dan validasi sistem
- **User (Nelayan & Pembeli)**: Untuk memahami fitur dan manfaat yang akan diperoleh

### 1.2 Lingkup Sistem

**Nama Sistem:** Ikan Shop  
**Kategori:** B2B Marketplace Platform

**Deskripsi:**  
Ikan Shop adalah platform marketplace berbasis website yang menghubungkan nelayan tradisional Indonesia dengan pembeli dalam skala besar (distributor, importir, restoran, dan event organizer) secara langsung. Sistem ini mengeliminasi perantara tradisional dan memberikan transparansi dalam proses transaksi hasil tangkapan laut.

**Fitur Utama:**
- Marketplace ikan dengan sistem booking pre-arrival
- Live chat real-time antara penjual dan pembeli
- Informasi cuaca maritim dan jadwal ibadah
- Tips keselamatan laut untuk nelayan
- Dashboard manajemen transaksi dan inventori

**Batasan Sistem:**
- Sistem tidak menangani proses logistik dan pengiriman fisik
- Sistem tidak memproses pembayaran secara langsung (terintegrasi dengan payment gateway pihak ketiga)
- Fokus pada pasar B2B, bukan B2C retail

### 1.3 Definisi, Akronim, dan Singkatan

| Term | Definisi |
|------|----------|
| **SRS** | Software Requirements Specification |
| **UI** | User Interface - Antarmuka pengguna |
| **UX** | User Experience - Pengalaman pengguna |
| **API** | Application Programming Interface |
| **B2B** | Business to Business |
| **CRUD** | Create, Read, Update, Delete |
| **JWT** | JSON Web Token |
| **SSL/TLS** | Secure Sockets Layer / Transport Layer Security |
| **HTTPS** | Hypertext Transfer Protocol Secure |
| **REST** | Representational State Transfer |
| **RBAC** | Role-Based Access Control |
| **XSS** | Cross-Site Scripting |
| **SQL** | Structured Query Language |
| **OTP** | One-Time Password |

### 1.4 Referensi
- IEEE Std 830-1998: IEEE Recommended Practice for Software Requirements Specifications
- Standar Keamanan Data: ISO/IEC 27001
- Web Content Accessibility Guidelines (WCAG) 2.1

### 1.5 Overview Dokumen
Dokumen ini terdiri dari tiga bagian utama:
1. **Pendahuluan** - Konteks dan tujuan dokumen
2. **Deskripsi Umum** - Gambaran sistem secara keseluruhan
3. **Kebutuhan Spesifik** - Detail fungsional dan non-fungsional

---

## 2. DESKRIPSI UMUM

### 2.1 Perspektif Produk

Ikan Shop merupakan sistem standalone yang dikembangkan untuk mendigitalisasi rantai distribusi perikanan tradisional di Indonesia. Sistem ini bukan merupakan bagian dari sistem yang lebih besar, namun dirancang dengan arsitektur yang dapat diintegrasikan dengan sistem eksternal seperti:

- Payment Gateway (Midtrans, Xendit, dll)
- Weather API (OpenWeatherMap, BMKG)
- Prayer Time API (Aladhan API)
- SMS/Email Notification Service
- Cloud Storage (untuk media files)

**Arsitektur Sistem:**
```
┌─────────────┐         ┌──────────────┐         ┌─────────────┐
│   Browser   │ ◄─────► │  Web Server  │ ◄─────► │  Database   │
│  (Client)   │  HTTPS  │  (Backend)   │         │  (MySQL/    │
└─────────────┘         └──────────────┘         │  PostgreSQL)│
                               │                  └─────────────┘
                               │
                        ┌──────▼──────┐
                        │ External    │
                        │ Services    │
                        │ (API)       │
                        └─────────────┘
```

### 2.2 Fungsi Produk

Sistem Ikan Shop menyediakan solusi end-to-end untuk transaksi ikan dalam skala besar dengan fungsi-fungsi berikut:

1. **Manajemen Akun & Autentikasi**
   - Registrasi multi-role (Nelayan, Distributor, Admin)
   - Login dengan verifikasi dua faktor (2FA)
   - Manajemen profil dan kredensial

2. **Marketplace Ikan**
   - Katalog produk dengan filter advance
   - Sistem booking pre-arrival
   - Real-time inventory update
   - Sistem rating dan review

3. **Komunikasi**
   - Live chat real-time dengan notifikasi
   - Push notification untuk update penting
   - Email notification untuk transaksi

4. **Informasi Pendukung**
   - Prakiraan cuaca maritim berdasarkan lokasi
   - Jadwal shalat untuk nelayan muslim
   - Artikel dan tips keselamatan laut

5. **Manajemen Transaksi**
   - Dashboard penjualan (untuk nelayan)
   - Dashboard pembelian (untuk distributor)
   - Riwayat transaksi lengkap
   - Laporan keuangan

### 2.3 Karakteristik Pengguna

| Role | Karakteristik | Keahlian Teknis | Kebutuhan Utama |
|------|---------------|-----------------|-----------------|
| **Nelayan** | Usia 25-55 tahun, pendidikan menengah, familiar dengan smartphone dasar | Pemula - Menengah | Interface sederhana, tutorial jelas, dukungan Bahasa Indonesia |
| **Distributor/Importir** | Usia 30-50 tahun, berpengalaman dalam bisnis perikanan | Menengah | Efisiensi pemesanan, data akurat, komunikasi cepat |
| **Admin** | Staff IT atau manajemen sistem | Mahir | Dashboard lengkap, kontrol penuh sistem, reporting |
| **Super Admin** | Pengelola sistem keseluruhan | Expert | Konfigurasi sistem, user management, sistem monitoring |

### 2.4 Batasan Sistem

1. **Batasan Teknis:**
   - Sistem memerlukan koneksi internet stabil
   - Kompatibel dengan browser modern (Chrome, Firefox, Safari, Edge versi 2 tahun terakhir)
   - Ukuran file upload maksimal 10 MB per file

2. **Batasan Operasional:**
   - Sistem tidak menangani logistik fisik pengiriman
   - Pembayaran melalui gateway pihak ketiga
   - Verifikasi identitas nelayan dilakukan manual oleh admin

3. **Batasan Regulasi:**
   - Harus mematuhi UU ITE No. 19 Tahun 2016
   - Perlindungan data sesuai PP No. 71 Tahun 2019
   - Standar keamanan transaksi elektronik

### 2.5 Asumsi dan Ketergantungan

**Asumsi:**
- Pengguna memiliki akses internet minimal 3G
- Nelayan memiliki smartphone atau akses ke komputer
- Data cuaca dari API eksternal tersedia dan akurat
- Payment gateway berfungsi normal

**Ketergantungan:**
- Ketersediaan API cuaca dari penyedia eksternal
- Stabilitas layanan hosting dan server
- Keandalan payment gateway partner
- Dukungan dari komunitas nelayan dan distributor

---

## 3. KEBUTUHAN SPESIFIK

### 3.1 Kebutuhan Fungsional

#### 3.1.1 Modul Autentikasi dan Manajemen Akun

**FR-01: Registrasi Pengguna**

| ID | FR-01 |
|----|-------|
| Nama | Registrasi Akun Baru |
| Prioritas | Tinggi |
| Deskripsi | Sistem harus memungkinkan pengguna baru (nelayan atau distributor) untuk mendaftar dengan mengisi formulir registrasi |
| Input | Nama lengkap, email, nomor telepon, password, role (nelayan/distributor), alamat, foto KTP |
| Proses | 1. Validasi format data input<br>2. Cek duplikasi email/nomor telepon<br>3. Hash password dengan bcrypt<br>4. Kirim OTP verifikasi ke email/SMS<br>5. Simpan data setelah verifikasi berhasil |
| Output | Akun pengguna terdaftar, email konfirmasi terkirim |
| Validasi | - Email harus valid dan unik<br>- Password minimal 8 karakter, kombinasi huruf dan angka<br>- Nomor telepon format Indonesia (+62)<br>- Foto KTP wajib untuk verifikasi |

**FR-02: Login Pengguna**

| ID | FR-02 |
|----|-------|
| Nama | Login ke Sistem |
| Prioritas | Tinggi |
| Deskripsi | Pengguna yang telah terdaftar dapat login menggunakan email dan password |
| Input | Email/nomor telepon, password |
| Proses | 1. Validasi kredensial<br>2. Generate JWT token jika valid<br>3. Update last login timestamp<br>4. Redirect ke dashboard sesuai role |
| Output | Session token (JWT), redirect ke dashboard |
| Validasi | - Maksimal 5 percobaan login gagal dalam 15 menit<br>- Account lockout otomatis jika melebihi batas |

**FR-03: Lupa Password**

| ID | FR-03 |
|----|-------|
| Nama | Reset Password |
| Prioritas | Sedang |
| Deskripsi | Pengguna dapat mereset password jika lupa |
| Input | Email terdaftar |
| Proses | 1. Validasi email<br>2. Generate token reset (expire 1 jam)<br>3. Kirim link reset via email<br>4. User input password baru<br>5. Update password di database |
| Output | Password berhasil direset, notifikasi email terkirim |

**FR-04: Manajemen Profil**

| ID | FR-04 |
|----|-------|
| Nama | Edit Profil Pengguna |
| Prioritas | Sedang |
| Deskripsi | Pengguna dapat mengupdate informasi profil mereka |
| Input | Nama, foto profil, alamat, nomor telepon, deskripsi bisnis |
| Proses | 1. Load data profil existing<br>2. User edit data<br>3. Validasi perubahan<br>4. Update database<br>5. Log perubahan |
| Output | Data profil terupdate, notifikasi sukses |

#### 3.1.2 Modul Manajemen Produk Ikan

**FR-05: Tambah Produk Ikan (Nelayan)**

| ID | FR-05 |
|----|-------|
| Nama | Menambahkan Listing Ikan |
| Prioritas | Tinggi |
| Deskripsi | Nelayan dapat menambahkan ikan hasil tangkapan ke marketplace |
| Input | - Jenis ikan (dropdown)<br>- Berat (kg)<br>- Harga per kg<br>- Foto ikan (max 5 foto)<br>- Lokasi tangkapan<br>- Estimasi waktu tiba<br>- Status (tersedia/booking)<br>- Deskripsi kondisi ikan |
| Proses | 1. Upload foto ke cloud storage<br>2. Validasi semua field<br>3. Generate product ID<br>4. Simpan ke database<br>5. Publish ke marketplace<br>6. Notifikasi ke distributor yang subscribed |
| Output | Produk muncul di marketplace, notifikasi terkirim |
| Validasi | - Minimal 1 foto wajib<br>- Harga harus positif<br>- Estimasi waktu tiba realistis (max 7 hari) |

**FR-06: Edit/Update Produk**

| ID | FR-06 |
|----|-------|
| Nama | Update Informasi Produk |
| Prioritas | Sedang |
| Deskripsi | Nelayan dapat mengupdate detail produk yang sudah dipublish |
| Input | Product ID, field yang diupdate |
| Proses | 1. Verifikasi ownership<br>2. Load data existing<br>3. Update field yang diubah<br>4. Log perubahan<br>5. Notifikasi ke pembeli yang telah booking (jika ada perubahan signifikan) |
| Output | Data produk terupdate |

**FR-07: Hapus Produk**

| ID | FR-07 |
|----|-------|
| Nama | Menghapus Listing Ikan |
| Prioritas | Sedang |
| Deskripsi | Nelayan dapat menghapus produk (soft delete) |
| Input | Product ID |
| Proses | 1. Cek apakah ada booking aktif<br>2. Jika ada booking, tolak penghapusan<br>3. Jika tidak ada, soft delete (set status = inactive)<br>4. Log aktivitas |
| Output | Produk tidak muncul di marketplace |

#### 3.1.3 Modul Marketplace dan Pencarian

**FR-08: Browsing Marketplace**

| ID | FR-08 |
|----|-------|
| Nama | Melihat Katalog Ikan |
| Prioritas | Tinggi |
| Deskripsi | Distributor dapat melihat semua ikan yang tersedia di marketplace |
| Input | Optional: filter dan sorting |
| Proses | 1. Load produk aktif dari database<br>2. Apply filter jika ada<br>3. Sorting sesuai preferensi<br>4. Pagination (20 item per page)<br>5. Display dengan infinite scroll |
| Output | List produk ikan dengan thumbnail, harga, lokasi |

**FR-09: Filter dan Pencarian Advance**

| ID | FR-09 |
|----|-------|
| Nama | Filter Produk Ikan |
| Prioritas | Tinggi |
| Deskripsi | Distributor dapat memfilter ikan berdasarkan kriteria tertentu |
| Input Filter | - Jenis ikan (multi-select)<br>- Range harga<br>- Lokasi tangkapan<br>- Berat minimum<br>- Waktu tiba (hari ini, minggu ini, dll)<br>- Rating nelayan |
| Proses | 1. Apply filter ke query database<br>2. Real-time update hasil<br>3. Simpan preferensi filter (optional) |
| Output | Hasil pencarian sesuai filter |

**FR-10: Detail Produk**

| ID | FR-10 |
|----|-------|
| Nama | Melihat Detail Ikan |
| Prioritas | Tinggi |
| Deskripsi | Menampilkan informasi lengkap tentang satu produk ikan |
| Output Display | - Galeri foto<br>- Spesifikasi lengkap<br>- Informasi nelayan (rating, lokasi)<br>- Review dari pembeli sebelumnya<br>- Tombol booking/chat<br>- Estimasi waktu tiba<br>- Lokasi di map |

#### 3.1.4 Modul Booking dan Transaksi

**FR-11: Booking Ikan**

| ID | FR-11 |
|----|-------|
| Nama | Pre-order Ikan |
| Prioritas | Tinggi |
| Deskripsi | Distributor dapat melakukan booking ikan sebelum kapal tiba |
| Input | - Product ID<br>- Jumlah (kg)<br>- Metode pembayaran<br>- Alamat pengiriman<br>- Catatan khusus |
| Proses | 1. Validasi ketersediaan stok<br>2. Kalkulasi total harga<br>3. Reserve stok<br>4. Generate booking ID<br>5. Kirim konfirmasi ke nelayan<br>6. Redirect ke payment gateway<br>7. Update status booking setelah payment |
| Output | Booking berhasil, invoice terkirim via email |
| Status Booking | - Pending Payment<br>- Confirmed<br>- In Transit<br>- Delivered<br>- Cancelled |

**FR-12: Konfirmasi Booking (Nelayan)**

| ID | FR-12 |
|----|-------|
| Nama | Nelayan Konfirmasi Pesanan |
| Prioritas | Tinggi |
| Deskripsi | Nelayan dapat menerima atau menolak booking |
| Input | Booking ID, status (accept/reject), alasan jika reject |
| Proses | 1. Update status booking<br>2. Jika accept: lock stok<br>3. Jika reject: refund otomatis, release stok<br>4. Notifikasi ke distributor |
| Output | Status booking terupdate |

**FR-13: Tracking Status Pesanan**

| ID | FR-13 |
|----|-------|
| Nama | Pelacakan Pesanan Real-time |
| Prioritas | Sedang |
| Deskripsi | Distributor dapat melacak status pesanan mereka |
| Output Display | - Timeline status<br>- Estimasi waktu tiba<br>- Lokasi kapal (jika available)<br>- Kontak nelayan<br>- Chat history |

**FR-14: Selesaikan Transaksi**

| ID | FR-14 |
|----|-------|
| Nama | Finalisasi Transaksi |
| Prioritas | Tinggi |
| Deskripsi | Distributor mengkonfirmasi penerimaan ikan |
| Input | Booking ID, rating (1-5 stars), review (optional), bukti penerimaan (foto) |
| Proses | 1. Update status = Completed<br>2. Release payment ke nelayan<br>3. Simpan rating & review<br>4. Update seller rating<br>5. Generate invoice final |
| Output | Transaksi selesai, dana ditransfer |

#### 3.1.5 Modul Live Chat

**FR-15: Inisiasi Chat**

| ID | FR-15 |
|----|-------|
| Nama | Memulai Percakapan |
| Prioritas | Tinggi |
| Deskripsi | Distributor dapat memulai chat dengan nelayan melalui halaman produk |
| Input | Product ID atau User ID |
| Proses | 1. Create/resume chat room<br>2. Load chat history jika ada<br>3. Enable real-time messaging via WebSocket<br>4. Display online status |
| Output | Chat window terbuka |

**FR-16: Kirim Pesan Real-time**

| ID | FR-16 |
|----|-------|
| Nama | Mengirim Pesan |
| Prioritas | Tinggi |
| Deskripsi | User dapat mengirim pesan teks dan file |
| Input | - Teks message<br>- Attachment (image, dokumen - max 5MB) |
| Proses | 1. Validasi input<br>2. Upload attachment ke storage<br>3. Broadcast via WebSocket<br>4. Simpan ke database<br>5. Push notification jika recipient offline |
| Output | Pesan terkirim dengan status (sent/delivered/read) |
| Fitur | - Typing indicator<br>- Read receipt<br>- Timestamp<br>- File sharing |

**FR-17: Notifikasi Chat**

| ID | FR-17 |
|----|-------|
| Nama | Notifikasi Pesan Baru |
| Prioritas | Sedang |
| Deskripsi | User mendapat notifikasi untuk pesan baru |
| Trigger | Pesan baru diterima saat user offline atau di halaman lain |
| Output | - Browser push notification<br>- Badge counter di icon chat<br>- Email notification (jika > 1 jam tidak dibaca) |

#### 3.1.6 Modul Informasi Cuaca dan Jadwal Shalat

**FR-18: Prakiraan Cuaca Maritim**

| ID | FR-18 |
|----|-------|
| Nama | Menampilkan Cuaca Laut |
| Prioritas | Sedang |
| Deskripsi | Menampilkan prakiraan cuaca untuk area penangkapan ikan |
| Input | Lokasi user (auto-detect atau manual) |
| Proses | 1. Get user location<br>2. Call Weather API<br>3. Parse data cuaca<br>4. Display dalam format user-friendly<br>5. Cache data (1 jam) |
| Output Display | - Suhu<br>- Kondisi cuaca<br>- Kecepatan angin<br>- Tinggi gelombang<br>- Visibilitas<br>- Peringatan cuaca ekstrem<br>- Forecast 3-7 hari |
| Refresh | Update setiap 1 jam atau manual refresh |

**FR-19: Jadwal Shalat**

| ID | FR-19 |
|----|-------|
| Nama | Menampilkan Waktu Shalat |
| Prioritas | Rendah |
| Deskripsi | Menampilkan jadwal shalat 5 waktu berdasarkan lokasi |
| Input | Lokasi user |
| Proses | 1. Get coordinates<br>2. Call Prayer Time API<br>3. Calculate prayer times<br>4. Display with countdown |
| Output | Waktu shalat: Subuh, Dzuhur, Ashar, Maghrib, Isya |
| Fitur Tambahan | - Countdown ke waktu shalat berikutnya<br>- Notifikasi adzan (optional) |

#### 3.1.7 Modul Tips Keselamatan Laut

**FR-20: Kelola Artikel Tips (Admin)**

| ID | FR-20 |
|----|-------|
| Nama | Manajemen Konten Tips |
| Prioritas | Rendah |
| Deskripsi | Admin dapat menambah, edit, dan hapus artikel tips keselamatan |
| Input | Judul, konten (rich text), kategori, gambar, tags |
| Proses | CRUD operation standar dengan versioning |
| Output | Artikel published |

**FR-21: Tampilkan Tips untuk Nelayan**

| ID | FR-21 |
|----|-------|
| Nama | Akses Artikel Tips |
| Prioritas | Rendah |
| Deskripsi | Nelayan dapat membaca artikel tips keselamatan laut |
| Output Display | - List artikel dengan thumbnail<br>- Kategori: cuaca, peralatan, navigasi, pertolongan pertama<br>- Search dan filter<br>- Bookmark artikel favorit |

#### 3.1.8 Modul Dashboard

**FR-22: Dashboard Nelayan**

| ID | FR-22 |
|----|-------|
| Nama | Dashboard Penjual |
| Prioritas | Tinggi |
| Deskripsi | Nelayan dapat melihat ringkasan aktivitas penjualan |
| Output Display | - Total produk aktif<br>- Total booking pending<br>- Revenue minggu ini/bulan ini<br>- Grafik penjualan<br>- Recent orders<br>- Rating & reviews<br>- Notifikasi penting |

**FR-23: Dashboard Distributor**

| ID | FR-23 |
|----|-------|
| Nama | Dashboard Pembeli |
| Prioritas | Tinggi |
| Deskripsi | Distributor dapat melihat ringkasan aktivitas pembelian |
| Output Display | - Booking aktif<br>- Riwayat transaksi<br>- Pengeluaran total<br>- Favorite sellers<br>- Rekomendasi produk<br>- Wishlist |

**FR-24: Dashboard Admin**

| ID | FR-24 |
|----|-------|
| Nama | Admin Control Panel |
| Prioritas | Tinggi |
| Deskripsi | Admin dapat mengelola seluruh sistem |
| Output Display | - Statistik sistem (total users, transactions, revenue)<br>- User management<br>- Content moderation<br>- Transaction monitoring<br>- System logs<br>- Analytics & reports |

#### 3.1.9 Modul Rating dan Review

**FR-25: Berikan Rating**

| ID | FR-25 |
|----|-------|
| Nama | Rating Transaksi |
| Prioritas | Sedang |
| Deskripsi | Distributor dapat memberikan rating setelah transaksi selesai |
| Input | - Rating (1-5 stars)<br>- Review text (optional)<br>- Foto produk yang diterima (optional) |
| Proses | 1. Validasi transaksi completed<br>2. Simpan rating<br>3. Update average rating nelayan<br>4. Publish review |
| Output | Review muncul di profil nelayan dan halaman produk |

**FR-26: Tampilkan Review**

| ID | FR-26 |
|----|-------|
| Nama | Lihat Review & Rating |
| Prioritas | Sedang |
| Deskripsi | Menampilkan review dari pembeli sebelumnya |
| Output | - Average rating (stars)<br>- Total review<br>- Filter by rating<br>- Sort by date/helpfulness<br>- Response from seller (optional) |

---

### 3.2 Kebutuhan Non-Fungsional

#### 3.2.1 Keamanan (Security)

**NFR-01: Autentikasi dan Otorisasi**
- Implementasi JWT (JSON Web Token) untuk session management
- Token expiry: 24 jam untuk access token, 30 hari untuk refresh token
- Password hashing menggunakan bcrypt dengan cost factor minimum 12
- Implementasi Role-Based Access Control (RBAC)
- Rate limiting untuk login attempts: maksimal 5 percobaan dalam 15 menit
- Account lockout otomatis setelah 5 kali gagal login

**NFR-02: Enkripsi Data**
- Seluruh komunikasi menggunakan HTTPS (TLS 1.3)
- Enkripsi data sensitif at rest menggunakan AES-256
- Secure cookie dengan flag HttpOnly dan Secure

**NFR-03: Validasi Input**
- Sanitasi semua input untuk mencegah XSS (Cross-Site Scripting)
- Prepared statements untuk mencegah SQL Injection
- CSRF token untuk semua form submissions
- Validasi file upload (type, size, content)

**NFR-04: Privacy & Data Protection**
- Compliance dengan UU ITE dan PP 71/2019 tentang SPSE
- Data personal hashing untuk PII (Personally Identifiable Information)
- Implementasi right to be forgotten (hapus akun & data)
- Data retention policy: log maksimal 90 hari

**NFR-05: Audit Trail**
- Logging semua aktivitas critical (login, transaction, admin actions)
- Immutable audit log
- Log format: timestamp, user ID, action, IP address, result

#### 3.2.2 Performa (Performance)

**NFR-06: Response Time**
- Halaman utama harus load dalam ≤ 2 detik (3G connection)
- API response time ≤ 500ms untuk 95% requests
- Search query ≤ 1 detik
- Image loading: progressive/lazy loading

**NFR-07: Throughput**
- Sistem harus dapat menangani minimal 1000 concurrent users
- Database query optimization untuk handle 10,000+ produk
- API rate limiting: 1000 requests per hour per user

**NFR-08: Database Performance**
- Indexing pada field yang sering di-query (user_id, product_id, created_at)
- Query caching untuk data yang jarang berubah
- Database connection pooling

**NFR-09: Caching Strategy**
- Redis untuk session dan frequently accessed data
- CDN untuk static assets (images, CSS, JS)
- Browser caching dengan proper cache headers

#### 3.2.3 Skalabilitas (Scalability)

**NFR-10: Horizontal Scaling**
- Stateless backend untuk memudahkan load balancing
- Microservices architecture untuk services yang resource-intensive (chat, notification)

**NFR-11: Database Scaling**
- Database replication (master-slave) untuk read-heavy operations
- Sharding strategy untuk partisi data berdasarkan region

**NFR-12: Cloud Infrastructure**
- Deployable pada cloud platform (AWS, GCP, Azure)
- Auto-scaling berdasarkan CPU/memory usage
- Load balancer untuk distribusi traffic

#### 3.2.4 Ketersediaan (Availability)

**NFR-13: Uptime**
- Target uptime: 99.5% (maksimal downtime 3.65 jam per bulan)
- Scheduled maintenance window: Minggu pagi 01:00-05:00 WIB

**NFR-14: Backup & Recovery**
- Daily automated backup database (retention 30 hari)
- Point-in-time recovery capability
- Disaster recovery plan dengan RTO (Recovery Time Objective) ≤ 4 jam

**NFR-15: High Availability**
- Database failover otomatis
- Health check endpoint untuk monitoring
- Graceful degradation saat ada service failure

#### 3.2.5 Kegunaan (Usability)

**NFR-16: User Interface**
- Desain responsif untuk desktop, tablet, dan mobile (320px - 1920px)
- Konsistensi UI menggunakan design system
- Maximum 3 klik untuk reach any feature
- Clear visual hierarchy dan typography
- Color contrast ratio minimum 4.5:1 (WCAG AA standard)

**NFR-17: User Experience**
- Onboarding tutorial untuk first-time users
- Contextual help dan tooltips
- Error messages yang jelas dan actionable
- Loading indicators untuk proses yang memakan waktu
- Empty state yang informatif

**NFR-18: Accessibility**
- Keyboard navigation support
- Screen reader compatibility
- Alt text untuk semua images
- ARIA labels untuk interactive elements
- Focus indicators yang jelas

**NFR-19: Multi-language Support (Future)**
- Framework i18n ready
- Prioritas: Bahasa Indonesia dan Inggris
- RTL (Right-to-Left) support untuk ekspansi pasar

**NFR-20: Browser Compatibility**
- Support browser modern (last 2 versions):
  - Google Chrome 90+
  - Mozilla Firefox 88+
  - Safari 14+
  - Microsoft Edge 90+
- Graceful degradation untuk browser lama

#### 3.2.6 Maintainability

**NFR-21: Code Quality**
- Modular dan reusable code
- Code documentation (inline comments dan external docs)
- Naming convention yang konsisten
- Code review mandatory sebelum merge

**NFR-22: Version Control**
- Git-based version control
- Branching strategy: GitFlow (main, develop, feature/*, hotfix/*)
- Semantic versioning (MAJOR.MINOR.PATCH)

**NFR-23: Testing**
- Unit test coverage minimum 70%
- Integration test untuk critical flows
- End-to-end testing untuk user journeys
- Automated testing dalam CI/CD pipeline

**NFR-24: Documentation**
- API documentation menggunakan OpenAPI/Swagger
- User manual untuk setiap role
- Technical documentation untuk developer
- Deployment guide

**NFR-25: Monitoring & Logging**
- Application performance monitoring (APM)
- Error tracking dan alerting (Sentry/Rollbar)
- Real-time dashboard untuk system health
- Automated alerts untuk critical issues

#### 3.2.7 Portability

**NFR-26: Platform Independence**
- Cross-platform deployment (Linux, Windows Server)
- Containerization menggunakan Docker
- Orchestration-ready (Kubernetes)

**NFR-27: Database Agnostic**
- ORM-based database access
- Support multiple database engines (MySQL, PostgreSQL)

#### 3.2.8 Compliance & Legal

**NFR-28: Regulatory Compliance**
- Compliance dengan UU ITE No. 19/2016
- GDPR-ready untuk ekspansi internasional
- PCI DSS compliance untuk payment data

**NFR-29: Terms of Service**
- Jelas dan mudah dipahami
- Explicit consent untuk data collection
- Privacy policy yang transparan

---

## 4. INTERFACE REQUIREMENTS

### 4.1 User Interface

#### 4.1.1 Skema Warna
- **Primary Color**: Ocean Blue (#0066CC)
- **Secondary Color**: Turquoise (#00B4D8)
- **Accent**: Coral (#FF6B6B)
- **Neutral**: Gray scale (#F8F9FA to #212529)
- **Success**: Green (#28A745)
- **Warning**: Orange (#FFA500)
- **Error**: Red (#DC3545)

#### 4.1.2 Typography
- **Heading Font**: Poppins (Bold, SemiBold)
- **Body Font**: Inter (Regular, Medium)
- **Size Scale**: 12px, 14px, 16px, 18px, 24px, 32px, 48px

#### 4.1.3 Komponen UI Utama
- Navigation bar (sticky)
- Sidebar untuk dashboard
- Card components untuk product listing
- Modal dialogs untuk confirmations
- Toast notifications untuk feedback
- Dropdown menus
- Form inputs dengan validation states
- Buttons (primary, secondary, ghost, danger)
- Data tables dengan pagination
- Charts dan graphs untuk analytics

#### 4.1.4 Layout Responsif

**Desktop (≥ 1024px)**
- Sidebar navigation permanent visible
- Grid layout untuk product listing (4 columns)
- Chat window sebagai floating panel

**Tablet (768px - 1023px)**
- Collapsible sidebar
- Grid layout 2-3 columns
- Bottom navigation bar

**Mobile (< 768px)**
- Hamburger menu
- Single column layout
- Full-screen chat
- Bottom tab navigation

### 4.2 Hardware Interface

**NFR-30: Minimum Device Requirements**

**Server Side:**
- CPU: 4 cores minimum
- RAM: 8 GB minimum
- Storage: 100 GB SSD
- Network: 100 Mbps

**Client Side:**
- CPU: Dual-core processor
- RAM: 2 GB minimum
- Display: 320px width minimum
- Network: 3G connection (minimum 1 Mbps)

### 4.3 Software Interface

#### 4.3.1 External APIs

**API Cuaca:**
- Provider: OpenWeatherMap API / BMKG API
- Endpoint: `/weather/marine`
- Update frequency: 1 jam
- Data: Temperature, wind speed, wave height, visibility

**API Jadwal Shalat:**
- Provider: Aladhan API
- Endpoint: `/timings`
- Update: Daily
- Data: 5 prayer times with coordinates

**Payment Gateway:**
- Provider: Midtrans / Xendit
- Integration: REST API
- Supported methods: Transfer bank, e-wallet, QRIS
- Webhook untuk payment notification

**SMS Gateway:**
- Provider: Twilio / Vonage
- Purpose: OTP verification, booking notification

**Email Service:**
- Provider: SendGrid / AWS SES
- Purpose: Transactional emails (confirmation, invoice, notification)

**Cloud Storage:**
- Provider: AWS S3 / Google Cloud Storage
- Purpose: Image dan file storage
- CDN integration untuk fast delivery

#### 4.3.2 Internal Interfaces

**Frontend-Backend Communication:**
- Protocol: HTTPS REST API
- Data Format: JSON
- Authentication: JWT Bearer Token
- Base URL: `https://api.ikanshop.com/v1`

**Real-time Communication:**
- Protocol: WebSocket (WSS)
- Library: Socket.io
- Purpose: Live chat, real-time notifications

**Database Connection:**
- Primary: MySQL 8.0+ / PostgreSQL 13+
- ORM: Sequelize / Prisma
- Connection Pool: Maximum 50 connections

---

## 5. OTHER NON-FUNCTIONAL REQUIREMENTS

### 5.1 Data Requirements

**DR-01: Database Schema**

**Table: users**
```sql
- id (UUID, Primary Key)
- email (VARCHAR, Unique)
- phone (VARCHAR, Unique)
- password_hash (VARCHAR)
- full_name (VARCHAR)
- role (ENUM: nelayan, distributor, admin)
- address (TEXT)
- ktp_photo_url (VARCHAR)
- profile_photo_url (VARCHAR)
- is_verified (BOOLEAN)
- rating_average (DECIMAL)
- total_reviews (INT)
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)
- last_login (TIMESTAMP)
```

**Table: products**
```sql
- id (UUID, Primary Key)
- seller_id (UUID, Foreign Key -> users.id)
- fish_type (VARCHAR)
- weight_kg (DECIMAL)
- price_per_kg (DECIMAL)
- total_stock (DECIMAL)
- available_stock (DECIMAL)
- location (VARCHAR)
- latitude (DECIMAL)
- longitude (DECIMAL)
- estimated_arrival (TIMESTAMP)
- status (ENUM: available, booked, sold, cancelled)
- description (TEXT)
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)
```

**Table: product_images**
```sql
- id (UUID, Primary Key)
- product_id (UUID, Foreign Key)
- image_url (VARCHAR)
- is_primary (BOOLEAN)
- order_index (INT)
```

**Table: bookings**
```sql
- id (UUID, Primary Key)
- product_id (UUID, Foreign Key)
- buyer_id (UUID, Foreign Key)
- seller_id (UUID, Foreign Key)
- quantity_kg (DECIMAL)
- total_price (DECIMAL)
- status (ENUM: pending_payment, confirmed, in_transit, delivered, completed, cancelled)
- payment_method (VARCHAR)
- payment_status (ENUM: pending, paid, refunded)
- delivery_address (TEXT)
- notes (TEXT)
- booking_date (TIMESTAMP)
- payment_date (TIMESTAMP)
- delivery_date (TIMESTAMP)
- completed_date (TIMESTAMP)
```

**Table: reviews**
```sql
- id (UUID, Primary Key)
- booking_id (UUID, Foreign Key)
- reviewer_id (UUID, Foreign Key)
- seller_id (UUID, Foreign Key)
- rating (INT, 1-5)
- review_text (TEXT)
- photos (JSON)
- created_at (TIMESTAMP)
```

**Table: chat_rooms**
```sql
- id (UUID, Primary Key)
- user1_id (UUID, Foreign Key)
- user2_id (UUID, Foreign Key)
- last_message (TEXT)
- last_message_at (TIMESTAMP)
- created_at (TIMESTAMP)
```

**Table: chat_messages**
```sql
- id (UUID, Primary Key)
- room_id (UUID, Foreign Key)
- sender_id (UUID, Foreign Key)
- message_type (ENUM: text, image, file)
- content (TEXT)
- attachment_url (VARCHAR)
- is_read (BOOLEAN)
- created_at (TIMESTAMP)
```

**DR-02: Data Retention**
- User data: Retained until account deletion
- Transaction data: Minimum 5 tahun (compliance)
- Chat history: 1 tahun
- System logs: 90 hari
- Backup retention: 30 hari

**DR-03: Data Privacy**
- Personal data encryption at rest
- Anonymization untuk analytics
- Right to data portability (export dalam JSON)
- Right to erasure (soft delete dengan grace period 30 hari)

### 5.2 Security Requirements

**SR-01: Authentication Security**
- Multi-factor authentication (2FA) optional untuk admin
- OAuth 2.0 untuk social login (future feature)
- Session timeout: 24 jam inactivity
- Password complexity: minimum 8 karakter, kombinasi huruf besar, kecil, angka

**SR-02: Authorization Security**
- Principle of least privilege
- Resource-level permission checking
- API endpoint protection dengan middleware

**SR-03: Network Security**
- Firewall rules untuk restrict unauthorized access
- DDoS protection via CDN (Cloudflare)
- Rate limiting untuk API abuse prevention

**SR-04: Application Security**
- Regular security audits (quarterly)
- Dependency vulnerability scanning (automated)
- Penetration testing sebelum production release

**SR-05: Incident Response**
- Security incident response plan documented
- Notification kepada affected users dalam 72 jam
- Post-mortem analysis untuk setiap security breach

### 5.3 Environmental Requirements

**ENV-01: Development Environment**
- OS: Ubuntu 22.04 LTS / macOS / Windows 10+
- Node.js: v18 LTS atau v20 LTS
- Database: MySQL 8.0 atau PostgreSQL 13+
- Git version: 2.30+

**ENV-02: Staging Environment**
- Mirroring production environment
- Isolated database
- Mock external services untuk testing

**ENV-03: Production Environment**
- Cloud hosting (AWS/GCP/Azure)
- Load balancer untuk traffic distribution
- Auto-scaling groups
- Separate database server
- Redis cache server
- CDN untuk static assets

---

## 6. ANALYSIS MODELS

### 6.1 Use Case Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    IKAN SHOP SYSTEM                     │
└─────────────────────────────────────────────────────────┘

              [Nelayan]                    [Distributor]
                 │                              │
                 │                              │
         ┌───────┼──────────┐          ┌────────┼─────────┐
         │       │          │          │        │         │
         ▼       ▼          ▼          ▼        ▼         ▼
    [Register] [Add    [Manage      [Browse  [Book   [Chat with
               Product] Bookings]   Products] Ikan]   Seller]
                 │          │          │        │         │
                 │          │          │        │         │
                 └──────────┼──────────┴────────┼─────────┘
                            │                   │
                            ▼                   ▼
                    [View Dashboard]    [Rate & Review]
                            │
                            │
                      [Admin]
                            │
                    ┌───────┼───────┐
                    │       │       │
                    ▼       ▼       ▼
            [Manage    [View      [Manage
             Users]    Analytics]  Content]
```

### 6.2 Data Flow Diagram (Level 0 - Context Diagram)

```
                    ┌──────────────┐
                    │   NELAYAN    │
                    └──────┬───────┘
                           │
                  Produk Ikan, Info
                           │
                           ▼
┌─────────────┐    ┌──────────────┐    ┌──────────────┐
│  Weather    │───►│              │◄───│  Distributor │
│    API      │    │  IKAN SHOP   │    │              │
└─────────────┘    │   SYSTEM     │    └──────────────┘
                   │              │
┌─────────────┐    │              │    ┌──────────────┐
│  Payment    │◄──►│              │◄───│    Admin     │
│  Gateway    │    └──────────────┘    └──────────────┘
└─────────────┘           │
                          │
                          ▼
                   ┌──────────────┐
                   │   Database   │
                   └──────────────┘
```

### 6.3 Entity Relationship Diagram (ERD)

```
┌─────────────┐         ┌──────────────┐         ┌─────────────┐
│    USERS    │         │   PRODUCTS   │         │  BOOKINGS   │
├─────────────┤         ├──────────────┤         ├─────────────┤
│ id (PK)     │────┐    │ id (PK)      │────┐    │ id (PK)     │
│ email       │    │    │ seller_id(FK)│    │    │ product_id  │
│ phone       │    └───►│ fish_type    │    └───►│   (FK)      │
│ full_name   │    ┌────│ weight_kg    │    ┌────│ buyer_id(FK)│
│ role        │    │    │ price_per_kg │    │    │ seller_id   │
│ rating      │    │    │ status       │    │    │   (FK)      │
└─────────────┘    │    └──────────────┘    │    │ quantity_kg │
       │           │            │            │    │ total_price │
       │           │            │            │    │ status      │
       │           │            ▼            │    └─────────────┘
       │           │    ┌──────────────┐    │            │
       │           │    │PRODUCT_IMAGES│    │            │
       │           │    ├──────────────┤    │            ▼
       │           │    │ id (PK)      │    │    ┌─────────────┐
       │           │    │ product_id   │    │    │   REVIEWS   │
       │           │    │   (FK)       │    │    ├─────────────┤
       │           │    │ image_url    │    │    │ id (PK)     │
       │           │    └──────────────┘    │    │ booking_id  │
       │           │                        │    │   (FK)      │
       │           └────────────────────────┘    │ reviewer_id │
       │                                         │   (FK)      │
       └────────────────────────────────────────►│ seller_id   │
                                                 │   (FK)      │
                                                 │ rating      │
                                                 │ review_text │
                                                 └─────────────┘
```

### 6.4 State Diagram - Booking Flow

```
    [Initiated]
         │
         │ Payment Made
         ▼
  [Pending Payment]
         │
         ├──► [Cancelled] (Payment Timeout)
         │
         │ Payment Confirmed
         ▼
    [Confirmed]
         │
         │ Seller Accepts
         ▼
    [In Transit]
         │
         │ Arrived at Port
         ▼
    [Delivered]
         │
         │ Buyer Confirms Receipt
         ▼
    [Completed]
         │
         │ Review Given
         ▼
     [Reviewed]
```

---

## 7. APPENDICES

### 7.1 Glossary

| Term | Definisi |
|------|----------|
| **Booking Pre-Arrival** | Sistem pemesanan ikan sebelum kapal nelayan tiba di pelabuhan |
| **Distributor** | Pembeli dalam skala besar (perusahaan, importir, restoran) |
| **JWT** | Token autentikasi berbasis JSON untuk session management |
| **Marketplace** | Platform digital tempat jual-beli |
| **Nelayan Tradisional** | Nelayan skala kecil-menengah dengan metode tangkapan konvensional |
| **ORM** | Object-Relational Mapping - Library untuk database operations |
| **Payment Gateway** | Layanan pihak ketiga untuk memproses pembayaran |
| **Soft Delete** | Menandai data sebagai deleted tanpa menghapus fisik dari database |
| **WebSocket** | Protokol komunikasi real-time bidirectional |

### 7.2 Assumptions

1. Nelayan memiliki akses ke smartphone atau dapat dibantu oleh anggota keluarga
2. Wilayah operasional awal: pesisir Jawa dan Sumatera
3. Distributor memiliki kendaraan/logistik sendiri untuk pengambilan ikan
4. Internet connectivity tersedia di area pelabuhan
5. Nelayan dapat mengupdate status tangkapan via mobile
6. Payment gateway partner memiliki uptime >99%

### 7.3 Dependencies

**External Services:**
- Cuaca API availability
- Payment gateway uptime
- SMS/Email service reliability
- Cloud hosting stability

**Internal:**
- Database performance
- Server capacity
- Network bandwidth

### 7.4 Future Enhancements (Out of Scope v1.0)

1. **Mobile Application** (iOS & Android native apps)
2. **GPS Tracking Integration** untuk tracking kapal real-time
3. **AI Price Prediction** berdasarkan historical data
4. **Blockchain** untuk supply chain transparency
5. **Multi-currency Support** untuk ekspansi internasional
6. **Auction System** untuk ikan premium
7. **Cold Chain Integration** untuk monitoring suhu selama transit
8. **API Marketplace** untuk third-party integration
9. **Loyalty Program** untuk repeat buyers
10. **Insurance Integration** untuk transaksi besar

### 7.5 Risks & Mitigation

| Risk | Probability | Impact | Mitigation Strategy |
|------|-------------|--------|---------------------|
| Adopsi rendah dari nelayan tradisional | Medium | High | - Training & onboarding program<br>- User interface yang sangat simple<br>- Customer support via WhatsApp |
| Keterbatasan internet di area pesisir | High | Medium | - Offline mode untuk basic features<br>- SMS fallback untuk notifikasi<br>- Progressive Web App |
| Ketidakpastian hasil tangkapan | High | Medium | - Clear terms & conditions<br>- Flexible cancellation policy<br>- Insurance option untuk buyer |
| Kompetitor dengan modal besar | Medium | High | - Focus pada niche market<br>- Build strong community<br>- Partnership dengan koperasi nelayan |
| Regulasi pemerintah yang berubah | Low | High | - Regular compliance check<br>- Legal consultation<br>- Flexible system architecture |
| Security breach | Low | High | - Regular security audit<br>- Bug bounty program<br>- Cyber insurance |

### 7.6 Success Metrics (KPI)

**User Acquisition:**
- Target: 500 nelayan terdaftar dalam 6 bulan pertama
- Target: 200 distributor aktif dalam 6 bulan pertama

**Engagement:**
- Daily Active Users (DAU): 30% dari total users
- Average session duration: > 5 menit
- Booking conversion rate: > 15%

**Transaction:**
- GMV (Gross Merchandise Value): Rp 500 juta dalam 6 bulan pertama
- Average transaction value: Rp 5 juta
- Repeat purchase rate: > 40%

**Satisfaction:**
- Net Promoter Score (NPS): > 50
- Average rating: > 4.0/5.0
- Customer support response time: < 2 jam

---

## 8. APPROVAL

Dokumen ini harus disetujui oleh stakeholder berikut sebelum development dimulai:

| Role | Nama | Signature | Tanggal |
|------|------|-----------|---------|
| **Product Owner** | FOUR A TEAM | _______________ | __________ |
| **Technical Lead** | KAPTEN AMMAR | _______________ | __________ |
| **UI/UX Designer** | FOUR A TEAM | _______________ | __________ |
| **QA Lead** | _______________ | _______________ | __________ |
| **Business Stakeholder** | _______________ | _______________ | __________ |

---

**Catatan Revisi:**
- Dokumen ini adalah living document dan akan diupdate sesuai kebutuhan development
- Setiap perubahan major (>20% dari requirements) memerlukan approval ulang
- Minor changes dapat didokumentasikan dalam changelog

---

**END OF DOCUMENT**

---

*Dokumen ini dibuat sesuai standar IEEE 830-1998 untuk Software Requirements Specification*

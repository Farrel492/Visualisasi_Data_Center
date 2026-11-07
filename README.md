# Simulasi Data Center dan IBM SAN

Visualisasi interaktif 3D sebuah data center besar dengan jaringan penyimpanan IBM SAN, lengkap dengan keamanan fisik dari gerbang sampai pintu rack. Dibuat sebagai alat belajar: semua berjalan di browser, satu file HTML, tanpa instalasi.

> Simulasi edukatif. Nama model perangkat hanyalah contoh dan bukan konfigurasi produksi.

**Demo:** https://farrel492.github.io/Visualisasi_Data_Center

## Fitur

### Ruang server
- 100 rack dalam 5 lorong (20 rack per lorong): Compute, Fabric SAN, Storage, Backup dan jaringan, serta Daya.
- Isi tiap rack terlihat per unit (U): server IBM Power, IBM Z, x86, switch Fibre Channel, SVC, FlashSystem, DS8000, tape, UPS, dan baterai.
- Pintu kaca di semua rack yang bisa dibuka dengan klik atau ketukan.
- Berjalan pelan di dalam lorong dengan tombol Maju/Mundur, atau tombol W/S dan panah di keyboard.

### SAN dan daya
- Topologi SAN 2D: host, dua fabric (A dan B), SVC, storage, dan tape, dengan jalur data yang beranimasi.
- Diagram daya: PLN, genset, ATS, UPS feed A dan B, busway, sampai rack.
- Skenario gangguan: listrik PLN putus, genset gagal, UPS rusak, fabric terganggu, pendingin mati. Suhu, jalur data, dan alarm ikut bereaksi.
- Alarm suara untuk kondisi darurat, bisa dimatikan.

### Keamanan fisik (visual saja, tanpa konfigurasi)
Gerbang, pos satpam, gerbang 2 (speed gate), lobi, ruang transit (mantrap), pintu server room (kartu dan sidik jari), sampai rack berkunci kartu.
- Seret kartu akses atau sidik jari ke pembaca untuk membuka pintu.
- Interlock antara pintu lobi dan ruang transit.
- Kartu yang ditolak, pintu ditahan atau dipaksa, tailgating, dan rack dibuka tanpa kartu memicu alarm.
- Tur jalan kaki otomatis "Masuk sebagai teknisi", lengkap dengan suara langkah.
- Log akses mencatat semua kejadian.
- Kunci kartu hanya dipasang di rack data sensitif (storage, SVC, dan switch fabric). Rack lain bisa dibuka bebas.

## Cara memakai

1. Buka `index.html` (atau tautan GitHub Pages) di browser.
2. Geser untuk memindahkan kamera. Klik kanan atau Ctrl+geser untuk memutar. Scroll untuk zoom. Di HP: satu jari geser, dua jari zoom dan putar.
3. Pilih lorong lewat tombol bawah, lalu tahan Maju/Mundur untuk berjalan.
4. Klik pintu kaca rack untuk membukanya, lalu klik unit untuk melihat perangkatnya.
5. Coba panel Kontrol untuk skenario gangguan dan skenario keamanan.

## Teknologi

- HTML, CSS, dan JavaScript dalam satu file.
- [Three.js](https://threejs.org) 0.160.0 (dimuat dari CDN) untuk tampilan 3D.
- Web Audio API untuk suara kipas, alarm, dan langkah.

## Cara kerja singkat (bahasa awam)

### Istilah penting
- **Rack:** lemari besi tempat server, switch, dan storage disusun bertumpuk. Ukurannya dihitung dalam "U" (satu unit tinggi).
- **Lorong dingin:** jalur sempit di antara dua baris rack. Udara dingin dari lantai ditiup ke depan rack, lalu udara panas keluar dari belakang.
- **SAN (Storage Area Network):** jaringan khusus yang menghubungkan server ke tempat penyimpanan data, lewat kabel serat optik (Fibre Channel).
- **Fabric A dan B:** dua jaringan SAN yang terpisah. Setiap server tersambung ke keduanya, jadi kalau satu putus, data tetap bisa lewat jalur lain.
- **SVC (SAN Volume Controller):** "pengatur lalu lintas" yang berdiri di depan storage, menggabungkan banyak storage jadi satu sumber.
- **UPS, genset, ATS:** UPS adalah baterai penahan sementara saat listrik padam, genset adalah pembangkit cadangan, dan ATS adalah saklar yang otomatis berpindah ke genset.
- **Feed A dan B:** dua jalur listrik terpisah ke setiap rack, supaya satu jalur mati tidak mematikan rack.
- **CRAC:** mesin pendingin ruangan. Kalau mati, suhu naik.

### Perjalanan masuk (keamanan berlapis)
Makin ke dalam, makin ketat. Setiap lapis punya fungsi sendiri:

| Zona | Tempat | Yang terjadi |
|---|---|---|
| 1 | Gerbang dan pos satpam | Satpam membukakan gerbang untuk pengunjung atau teknisi |
| 2 | Gerbang 2 (speed gate) | Hanya satu orang per kartu. Kartu tamu boleh sampai sini |
| 3 | Lobi | Pintu menuju ruang transit, hanya kartu teknisi yang diterima |
| 4 | Ruang transit (mantrap) | Dua pintu tidak boleh terbuka bersamaan (interlock). Pintu server perlu kartu **lalu** sidik jari |
| 5 | Ruang server | Rack storage, SVC, dan switch fabric punya pintu yang dikunci kartu |

### Kartu dan sidik jari
- **Kartu teknisi:** boleh melewati gerbang 2, pintu lobi, ruang transit, dan rack berkunci.
- **Kartu tamu:** hanya sampai gerbang 2. Ditempelkan di tempat lain, sistem menolaknya dan alarm berbunyi.
- **Kartu asing:** tidak diterima di mana pun.
- **Sidik jari:** untuk pintu server, sidik jari teknisi harus menyusul kartu dalam 20 detik. Sidik jari asing ditolak.
- **Interlock:** pintu lobi dan pintu ruang transit tidak bisa terbuka bersamaan. Yang satu harus menutup dulu.

### Skenario keamanan (panel Kontrol)
| Skenario | Yang kamu lihat |
|---|---|
| Kartu tidak dikenal | Pembaca merah, alarm "orang tak dikenal" |
| Kartu tamu di ruang transit | Ditolak, alarm berbunyi |
| Tailgating | Dua orang masuk dengan satu kartu, gerbang dikunci dan alarm bunyi |
| Pintu ditahan | Pintu terbuka lebih dari 9 detik memicu alarm |
| Pintu dipaksa | Pintu server terbuka tanpa kartu memicu alarm |
| Rack dibuka tanpa kartu | Alarm untuk rack storage tertentu |

Tombol **Pulihkan keamanan** menutup semua pintu dan mematikan alarm.

### Skenario gangguan listrik dan jaringan
Listrik PLN putus: UPS menahan, lalu genset menyala, lalu bila genset juga gagal baterai habis dan rack mati satu per satu. Gangguan fabric A atau B: host masih tersambung lewat fabric yang satunya (jalur tinggal 1 dari 2). Pendingin mati: suhu naik dan alarm berbunyi bila melewati 26°C dan 30°C.

### Mengendalikan kamera
- **Preset:** Semua, Atas, Bawah, Luar. Kamera berpindah dengan animasi halus.
- **Zona 1 sampai 5:** kamera terbang ke tiap lapis keamanan dan fokus ke pembaca kartunya.
- **Lorong 1 sampai 5:** masuk ke lorong, lalu tahan Maju/Mundur untuk berjalan pelan.
- **Masuk:** tur jalan kaki otomatis sebagai teknisi, langkah demi langkah. Tombol Hentikan atau Esc untuk berhenti.

### Cara membaca kodenya (untuk yang penasaran)
Semua ada di satu file HTML dan dibagi dalam bagian: tampilan dan gaya (CSS), data rack dan unit, model daya dan pendingin, model keamanan (pintu, pembaca, kartu), pembangun 3D (Three.js), lalu pengatur tampilan dan tombol. Kalau ingin mengubah sesuatu, cukup jelaskan hasil yang diinginkan, bukan bagian kodenya.

## Catatan

- Butuh koneksi internet saat pertama dibuka untuk memuat Three.js. Jika gagal dimuat, aplikasi memakai tampilan 2D.
- iOS di bawah 16.4 tidak mendukung importmap, sehingga memakai tampilan 2D.
- Dengan 100 rack, perangkat lama mungkin terasa berat. Sudah dioptimalkan untuk HP, tetapi belum dites di semua perangkat.

## Lisensi

Tentukan lisensi sesuai keinginanmu (misalnya MIT).

# Simulasi Data Center dan IBM SAN

Visualisasi interaktif 3D sebuah data center besar dengan jaringan penyimpanan IBM SAN, lengkap dengan keamanan fisik dari gerbang sampai pintu rack. Dibuat sebagai alat belajar: semua berjalan di browser, satu file HTML, tanpa instalasi.

> Simulasi edukatif. Nama model perangkat hanyalah contoh dan bukan konfigurasi produksi.

Demo: https://farrel492.github.io/Visualisasi_Data_Center

Fitur

Ruang server
- 100 rack dalam 5 lorong (20 rack per lorong): Compute, Fabric SAN, Storage, Backup dan jaringan, serta Daya.
- Isi tiap rack terlihat per unit (U): server IBM Power, IBM Z, x86, switch Fibre Channel, SVC, FlashSystem, DS8000, tape, UPS, dan baterai.
- Pintu kaca di semua rack yang bisa dibuka dengan klik atau ketukan.
- Berjalan pelan di dalam lorong dengan tombol Maju/Mundur, atau tombol W/S dan panah di keyboard.

SAN dan daya
- Topologi SAN 2D: host, dua fabric (A dan B), SVC, storage, dan tape, dengan jalur data yang beranimasi.
- Diagram daya: PLN, genset, ATS, UPS feed A dan B, busway, sampai rack.
- Skenario gangguan: listrik PLN putus, genset gagal, UPS rusak, fabric terganggu, pendingin mati. Suhu, jalur data, dan alarm ikut bereaksi.
- Alarm suara untuk kondisi darurat, bisa dimatikan.

Keamanan fisik (visual saja, tanpa konfigurasi)
Gerbang, pos satpam, gerbang 2 (speed gate), lobi, ruang transit (mantrap), pintu server room (kartu dan sidik jari), sampai rack berkunci kartu.
- Seret kartu akses atau sidik jari ke pembaca untuk membuka pintu.
- Interlock antara pintu lobi dan ruang transit.
- Kartu yang ditolak, pintu ditahan atau dipaksa, tailgating, dan rack dibuka tanpa kartu memicu alarm.
- Tur jalan kaki otomatis "Masuk sebagai teknisi", lengkap dengan suara langkah.
- Log akses mencatat semua kejadian.
- Kunci kartu hanya dipasang di rack data sensitif (storage, SVC, dan switch fabric). Rack lain bisa dibuka bebas.

Cara memakai

1. Buka `index.html` (atau tautan GitHub Pages) di browser.
2. Geser untuk memindahkan kamera. Klik kanan atau Ctrl+geser untuk memutar. Scroll untuk zoom. Di HP: satu jari geser, dua jari zoom dan putar.
3. Pilih lorong lewat tombol bawah, lalu tahan Maju/Mundur untuk berjalan.
4. Klik pintu kaca rack untuk membukanya, lalu klik unit untuk melihat perangkatnya.
5. Coba panel Kontrol untuk skenario gangguan dan skenario keamanan.

Teknologi

- HTML, CSS, dan JavaScript dalam satu file.
- [Three.js](https://threejs.org) 0.160.0 (dimuat dari CDN) untuk tampilan 3D.
- Web Audio API untuk suara kipas, alarm, dan langkah.

Catatan

- Butuh koneksi internet saat pertama dibuka untuk memuat Three.js. Jika gagal dimuat, aplikasi memakai tampilan 2D.
- iOS di bawah 16.4 tidak mendukung importmap, sehingga memakai tampilan 2D.
- Dengan 100 rack, perangkat lama mungkin terasa berat. Sudah dioptimalkan untuk HP, tetapi belum dites di semua perangkat.

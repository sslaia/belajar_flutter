# alasa_app

Belajar membuat aplikasi berbasis database di Flutter melalui aplikasi Alasa


## Pengantar

Setelah 10 kali pertemuan belajar bersama Flutter, kini saatnya menempuh metode lain untuk belajar pembuatan aplikasi. Daripada kita belajar satu per satu widget secara sembarang, kita mempelajarinya sambil lalu tergantung kebutuhan tahap pembentukan satu aplikasi konkrit. Saya harap dengan demikian peserta akan lebih termotivasi untuk belajar.

Proses pembuatan aplikasi ini ditujukan bagi pemula, yang ingin tahu bagaimana mengembangkan satu aplikasi tahap demi tahap, mulai dari nol sampai ke aplikasi siap jadi. Jadi melalui berbagai langkah yang ditempuh, peserta akan pelan-pelan belajar mulai dari dasar sampai bisa mengembangkan aplikasi sendiri dengan mencari berbagai informasi yang dibutuhkan di internet secara mandiri.

## Bagaimana mulai

Silakan menggandakan repositori [alasa_app](https://github.com/sslaia/alasa_app) ke komputer Anda. Repositori tsb. merekam berbagai langkah dalam proses pembuatan aplikasi. Untuk melihat berbagai langkah pembuatan aplikasi silakan mencek berbagai cabang (_branch_) yang ada.

Anda bisa melihat cabang yang ada dengan mengklik di icon **main** di depan nama aplikasi di repositori **alasa_app**. Untuk melihatnya secara lokal Anda harus menginstalasi dan menggunakan git.

## Persiapan

Untuk mulai dengan pengembangan aplikasi Alasa silakan menciptakan aplikasi baru dalam **Android Studio (AS)**, yang akan digunakan menjadi basis.

1. Buat aplikasi baru melalui **File** > **New** > **New Flutter project**
2. Beri nama **alasa_app** dan tekan tombol **Finish**. Tunggu sampai proses pembuatan templat aplikasi baru selesai. Otomatis berkas **main.dart** akan terbuka. Kalau tidak bukalah berkas tsb. yang terdapat di dalam folder lib.
3. Dalam berkas **main.dart** ubahlah judul aplikasi (baris 14) menjadi "Aplikasi Alasa".


## Sedikit bantuan navigasi (orientasi)

**Menampilkan struktur proyek**

Silakan mengamati struktur folder aplikasi baru ini, yang terpajang di kolom sebelah kiri (lihat gambar berikut).

![Folder aplikasi Alasa](./alasa_app/struktur_folder.png?raw=true)

Seandainya pajangan folder tsb tertutup, silakan membukanya dengan mengklik **Project** di pinggir kiri jendela **AS** (no. 1 dalam gambar di atas) dan pastikan modusnya "Project" dan bukan yang lain (no. 2).

**Berkas dan folder utama**

1. Semua berkas kode yang akan ditulis disimpan di dalam folder **lib** (no. 3). Salah satunya adalah berkas **main.dart** (no. 4).
2. Di folder utama ini ada juga satu berkas yang sangat penting bernama **pubspec.yaml** (no. 5). Di dalam berkas inilah nanti didaftarkan semua pustaka, gambar, huruf dlsb. yang dibutuhkan oleh aplikasi. **Catatan**: Hati-hati mengubah berkas **pubspec.yaml** karena cara penulisan di dalamnya sangat ketat mengikuti aturan tertentu!

**Tombol penting dan sering digunakan**

1. **Run** (no. 8). Tombol inilah yang ditekan untuk menjalankan aplikasi di emulator atau di smartphone.
2. **Terminal** (no. 10). Klik tombol tsb. untuk menampilkan jendela terminal. Sebagai programmer, dari waktu ke waktu akan ada kebutuhan untuk menulis perintah di dalam terminal.
3. **Emulator** (no. 7). Klik tombol tsb. untuk menghidupkan emulator (kemungkinan besar namanya Pixel 2 atau nama lain yang dipilih waktu proses setup). Setelah selesai dihidupkan, nama emulator tsb. akan muncul di sini.
4. **AVD Manager** (no. 9). Klik tombol tsb. untuk men-setup emulator smartphone Android. Tanpa men-setup satu emulator, kolom emulator di no. 7 tidak akan menampilkan emulator smartphone apa pun.


## Langkah-langkah

1. [Anatomi satu aplikasi](./alasa_anatomi.md)
2. [Mendesain database Alasa](./alasa_design_database.md)
3. [Merancang formulir, bagian pertama](./alasa_formulir1.md)
4. [Merancang formulir, bagian kedua](./alasa_formulir2.md)
5. [Membuat database](./alasa_membuat_database.md)





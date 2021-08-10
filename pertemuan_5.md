# Belajar Bersama Flutter

Pertemuan 5, 12 Aug 2021


## Merangkum kembali apa yang telah dipelajari minggu lalu

Pada pertemuan ke-4 minggu lalu kita telah memoles aplikasi [Kartu Nama](https://github.com/sslaia/kartu_nama) dengan menambah beberapa fitur: menambah foto sendiri, menambah icon, mengenal beberapa widget yang berkaitan (CircleAvatar, Icon, Row, Column), mengenal beberapa properti dari widget Text (mengubah besar serta gaya huruf, mengubah warna). Kita juga telah berkenalan bagaimana mengedit berkas pubspec.yaml dengan menambahkan informasi tentang PATH gambar.

Minggu ini kita membuat aplikasi [Kartu Nama](https://github.com/sslaia/kartu_nama) itu tampil profesional dan layak dipamerkan/dipajang kepada orang lain.


## Berkenalan dengan keseharian para programmer: *refactoring*

Bagi seorang programmer menulis satu aplikasi itu tidak pernah selesai sekali jadi. Umumnya setelah aplikasi selesai, muncul ide baru untuk membuat aplikasi tsb. lebih baik, entah memperbaiki desain atau malah menambah fitur baru. Karena itu satu aplikasi mengalami update terus menerus, ada versi 1.0, 2.0 dst.

Seluruh proses membongkar-pasang satu aplikasi untuk mengadopsi fitur baru dinamakan *refactoring*. Tidak jarang untuk mencapai tujuan itu, kerangka aplikasi harus diubah, berarti gonta-ganti widget sana sini.

Hal yang sama terjadi dengan aplikasi [Kartu Nama](https://github.com/sslaia/kartu_nama). Masih ingat penampilan pertama aplikasi, yang hanya menampilkan satu teks di tengah? ![Refactoring Kartu Nama](./kartu_nama/kartu_nama_refactoring.jpg?raw=true) Kemudian kita menghapus widget tertentu (widget **Center**), menambahkan yang lain (widget **Image**, **Text**, **Icon** dan **SizedBox**), bahkan menggunakan widget yang memiliki anak-anak (*children*) (widget **Row** dan **Column**) dlsb. Karena kita ingin memasang foto, icon, memasang berbagai elemen di layar, kita telah membongkar-pasang (*refactoring*) aplikasi tsb. Jadi secara Anda tidak sadari Anda telah menjalani hidup nyata sebagai programmer!


## Membuat aplikasi Kartu Nama tampil profesional

Bagaimana kita membuat aplikasi Kartu Nama tsb. tampil lebih profesional? Perubahan sedikit bisa mengakibatkan efek visual yang kuat.

Coba lihat mis. konsep pertama kartu nama dalam gambar di atas. Bagus, sederhana dan *to the point*. Tetapi bandingkan dengan gambar sebelah kanan. Hanya dengan memberi warna latarbelakang berbeda, kesan yang muncul terasa lebih intensif. Hal ini kemudian diperkuat lagi dengan membuat nama lebih besar serta menampilkan nomor telepon, alamat email serta alamat rumah dalam gaya sebuah kartu (menggunakan widget **Card**), yang memiliki efek bayangan.

Bagaimana kita mencapai hal tsb.? Silakan membuka kode [Kartu Nama pada Pertemuan 5](https://github.com/sslaia/kartu_nama/blob/pertemuan-5/lib/main.dart) Dan sambil mengamati perubahan dalam kode itu, kita mengimplementasikan berbagai perbaikan yang disebut di atas.


## Menggunakan Google Fonts (*kalau ada waktu*)

Google Fonts tersedia sebagai paket tambahan untuk Flutter di [https://pub.dev/packages/google_fonts](https://pub.dev/packages/google_fonts)

1. Tambahkan paket tsb. entah dengan mengedit langsung berkas pubspec.yaml seperti ditulis dalam cara menginstalasi di alamat tsb. di atas, atau menggunakan jalan pintas berikut di terminal Android Studio:
```
flutter pub add google_fonts 
```

2. Impor paket tsb. dengan menambahkan baris berikut di atas isi dari berkas main.dart
```
import 'package:google_fonts/google_fonts.dart';
```

3. Aplikasikan penggunakan google fonts di dalam kode. Perhatikan bagaimana penulisan parameter **style** dari widget **Text**, contoh baris tentang pekerjaan.
```
          Text(
            _pekerjaan,
            style: TextStyle(
              fontSize: 14.0,
              letterSpacing: 2.5,
              fontWeight: FontWeight.bold,
              color: Colors.white,
            ),
          ),
```

Nah menurut dokumentasi dari Google Fonts

```
          Text(
            _pekerjaan,
            style: GoogleFonts.lato(
              textStyle: TextStyle(fontSize: 14.0, letterSpacing: 2.5, fontWeight: FontWeight.bold, color: Colors.white),
            ),
          ),
```

Selesai! Dengan kode sederhana ini Anda tak perlu membeli huruf profesional yang harganya ratusan dollar. Google telah menyediakannya bebas untuk Anda dan Anda bisa menggunakannya secara komersil tanpa harus membayar apa-apa!


## Referensi

Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)

Bantuan selalu dapat di [stockoverflow.com](https://www.stockoverflow.com) dan di berbagai situs di Internet (perhatikan yang ada medium dalam alamatnya).

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)

